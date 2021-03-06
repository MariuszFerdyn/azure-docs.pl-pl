---
title: Samouczek dotyczący wdrażania usługi Azure Machine Learning na urządzeniu — Azure IoT Edge | Microsoft Docs
description: W tym samouczku usługa Azure Machine Learning jest wdrażana jako moduł na urządzeniu brzegowym
author: kgremban
manager: philmea
ms.author: kgremban
ms.date: 11/15/2018
ms.topic: tutorial
ms.service: iot-edge
services: iot-edge
ms.custom: mvc, seodec18
ms.openlocfilehash: 464d16d4bbcbdbefd36ce1132630ad702d7a0c90
ms.sourcegitcommit: 58dc0d48ab4403eb64201ff231af3ddfa8412331
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2019
ms.locfileid: "55076977"
---
# <a name="tutorial-deploy-azure-machine-learning-as-an-iot-edge-module-preview"></a>Samouczek: Wdrażanie usługi Azure Machine Learning jako modułu usługi IoT Edge (wersja zapoznawcza)

Moduły usługi IoT Edge umożliwiają wdrożenie kodu implementującego logikę biznesową bezpośrednio na urządzeniach usługi IoT Edge. Ten samouczek zawiera opis sposobu wdrażania modułu usługi Azure Machine Learning, który przewiduje awarię urządzenia na podstawie symulowanych danych dotyczących temperatury maszyny. Więcej informacji na temat usługi Azure Machine Learning Service na platformie IoT Edge można znaleźć w [dokumentacji usługi Azure Machine Learning](../machine-learning/service/how-to-deploy-to-iot.md).

Moduł usługi Azure Machine Learning tworzony w tym samouczku odczytuje dane środowiska wygenerowane przez urządzenie i oznacza, czy komunikaty wskazują wystąpienie anomalii, czy nie.

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie modułu usługi Azure Machine Learning
> * Wypychanie kontenera modułów do usługi Azure Container Registry
> * Wdrażanie modułu usługi Azure Machine Learning na urządzeniu usługi IoT Edge
> * Wyświetlanie wygenerowanych danych

>[!NOTE]
>Moduły usługi Azure Machine Learning w usłudze Azure IoT Edge są dostępne w publicznej wersji zapoznawczej.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]


## <a name="prerequisites"></a>Wymagania wstępne

Urządzenie usługi Azure IoT Edge:

* Jako urządzenia brzegowego możesz użyć maszyny deweloperskiej albo maszyny wirtualnej, postępując zgodnie z instrukcjami w przewodniku Szybki start dla urządzeń z systemem [Linux](quickstart-linux.md) lub [Windows](quickstart.md).
* Moduł usługi Azure Machine Learning nie obsługuje procesorów ARM.

Zasoby w chmurze:

* Usługa [IoT Hub](../iot-hub/iot-hub-create-through-portal.md) w warstwie Bezpłatna lub Standardowa na platformie Azure.
* Obszar roboczy usługi Azure Machine Learning. Aby go utworzyć, postępuj zgodnie z instrukcjami w artykule [Przygotowywanie do wdrażania modeli w usłudze IoT Edge](../machine-learning/service/how-to-deploy-to-iot.md).


### <a name="disable-process-identification"></a>Wyłączanie identyfikacji procesu

>[!NOTE]
>
> Usługa Azure Machine Learning w wersji zapoznawczej nie obsługuje funkcji zabezpieczeń identyfikacji procesu włączonej domyślnie w usłudze IoT Edge.
> Poniżej przedstawiono kroki, które umożliwiają jej wyłączenie. Nie są one jednak odpowiednie do użycia w środowisku produkcyjnym. Wykonanie tych kroków jest niezbędne tylko w systemie Linux, ponieważ zostały już one wykonane podczas instalowania środowiska uruchomieniowego usługi Windows Edge.

W celu wyłączenia identyfikacji procesu na urządzeniu usługi IoT Edge należy podać adres IP i port dla elementów **workload_uri** i **management_uri** w sekcji **connect** konfiguracji demona usługi IoT Edge.

Najpierw uzyskaj adres IP. Wprowadź polecenie `ipconfig` w wierszu polecenia i skopiuj adres IP interfejsu **docker0**.

Edytuj plik konfiguracji demona usługi IoT Edge:

```cmd/sh
sudo nano /etc/iotedge/config.yaml
```

Zaktualizuj sekcję **zawartości** konfiguracji przy użyciu adresu IP. Na przykład:
```yaml
connect:
  management_uri: "http://172.17.0.1:15580"
  workload_uri: "http://172.17.0.1:15581"
```

Wprowadź te same adresy w sekcji **listen** konfiguracji. Na przykład:

```yaml
listen:
  management_uri: "http://172.17.0.1:15580"
  workload_uri: "http://172.17.0.1:15581"
```

Utwórz zmienną środowiskową IOTEDGE_HOST z adresem management_uri (aby ustawić ją trwale, dodaj ją do pliku `/etc/environment`). Na przykład:

```cmd/sh
export IOTEDGE_HOST="http://172.17.0.1:15580"
```


## <a name="create-the-azure-machine-learning-service-container"></a>Tworzenie kontenera usługi Azure Machine Learning Service
W tej sekcji pobierzesz pliki wytrenowanego modelu i przekonwertujesz je na kontener usługi Azure Machine Learning Service.

Aby utworzyć kontener platformy Docker przy użyciu modelu uczenia maszynowego, postępuj zgodnie z instrukcjami w artykule [Przygotowywanie do wdrażania modeli w usłudze IoT Edge](../machine-learning/service/how-to-deploy-to-iot.md).  Wszystkie wymagane składniki obrazu platformy Docker znajdują się w [repozytorium zestawu narzędzi SI dla usługi Azure IoT Edge](https://github.com/Azure/ai-toolkit-iot-edge/tree/master/IoT%20Edge%20anomaly%20detection%20tutorial).

### <a name="view-the-container-repository"></a>Wyświetlanie repozytorium kontenerów

Sprawdź, czy obraz kontenera został pomyślnie utworzony i zapisany w rejestrze kontenerów platformy Azure skojarzonym ze środowiskiem uczenia maszynowego.

1. W witrynie [Azure Portal](https://portal.azure.com) przejdź do obszaru **Wszystkie usługi**, a następnie wybierz pozycję **Rejestry kontenerów**.
2. Wybierz rejestr. Nazwa powinna zaczynać się od łańcucha **mlcr** i należy do grupy zasobów, lokalizacji i subskrypcji użytych do skonfigurowania funkcji zarządzania modułami.
3. Wybierz pozycję **Klucze dostępu**.
4. Skopiuj wartości w polach **Serwer logowania**, **Nazwa użytkownika** i **Hasło**.  Są one potrzebne do uzyskania dostępu do rejestru z urządzeń usługi Edge.
5. Wybierz pozycję **Repozytoria**.
6. Wybierz pozycję **machinelearningmodule**.
7. Masz teraz pełną ścieżkę do obrazu kontenera. Zanotuj tę ścieżkę w celu użycia w następnej sekcji. Powinna ona wyglądać następująco: **<nazwa_rejestru>.azurecr.io/machinelearningmodule:1**

## <a name="deploy-to-your-device"></a>Wdrażanie na urządzeniu

1. W witrynie [Azure Portal](https://portal.azure.com) przejdź do centrum IoT Hub.

1. Przejdź do pozycji **IoT Edge** i wybierz urządzenie usługi IoT Edge.

1. Wybierz opcję **Ustaw moduły**.

1. W sekcji **Ustawienia rejestru** dodaj poświadczenia skopiowane z rejestru kontenerów platformy Azure.

   ![Dodawanie poświadczeń rejestru do manifestu](./media/tutorial-deploy-machine-learning/registry-settings.png)

1. Jeśli moduł tempSensor został już wcześniej wdrożony na urządzeniu usługi IoT Edge, może on zostać automatycznie wypełniony. Jeśli nie znajduje się on jeszcze na liście modułów, dodaj go.

    1. Kliknij pozycję **Dodaj** i wybierz pozycję **Moduł usługi IoT Edge**.
    2. W polu **Nazwa** wprowadź wartość `tempSensor`.
    3. W polu **Identyfikator URI obrazu** wprowadź wartość `mcr.microsoft.com/azureiotedge-simulated-temperature-sensor:1.0`.
    4. Wybierz pozycję **Zapisz**.

1. Dodaj utworzony moduł uczenia maszynowego.

    1. Kliknij pozycję **Dodaj** i wybierz pozycję **Moduł usługi IoT Edge**.
    1. W polu **Nazwa** wprowadź wartość `machinelearningmodule`.
    1. W polu **Obraz** wprowadź adres obrazu, na przykład `<registry_name>.azurecr.io/machinelearningmodule:1`.
    1. Wybierz pozycję **Zapisz**.

1. W kroku **Dodawanie modułów** wybierz opcję **Dalej**.

1. W kroku **Określanie tras** skopiuj poniższe dane JSON do pola tekstowego. Pierwsza trasa służy do transportu komunikatów z czujnika temperatury do modułu uczenia maszynowego za pośrednictwem punktu końcowego „amlInput”, który jest używany przez wszystkie moduły usługi Azure Machine Learning. Druga trasa służy do transportu komunikatów z modułu uczenia maszynowego do centrum IoT Hub. W ramach tej trasy „amlOutput” to punkt końcowy używany przez wszystkie moduły usługi Azure Machine Learning do wyprowadzania danych, a element „$upstream” wskazuje centrum IoT Hub.

    ```json
    {
        "routes": {
            "sensorToMachineLearning":"FROM /messages/modules/tempSensor/outputs/temperatureOutput INTO BrokeredEndpoint(\"/modules/machinelearningmodule/inputs/amlInput\")",
            "machineLearningToIoTHub": "FROM /messages/modules/machinelearningmodule/outputs/amlOutput INTO $upstream"
        }
    }
    ```

1. Wybierz opcję **Dalej**.

1. W kroku **Przegląd wdrożenia** wybierz pozycję **Prześlij**.

1. Wróć do strony szczegółów urządzenia i wybierz opcję **Odśwież**.  Powinien zostać wyświetlony nowy moduł **machinelearningmodule** uruchomiony wraz z modułem **tempSensor** i modułami środowiska uruchomieniowego usługi IoT Edge.

## <a name="view-generated-data"></a>Wyświetlanie wygenerowanych danych

Wyświetlać możesz komunikaty generowane przez poszczególne moduły usługi IoT Edge oraz dostarczane do Twojego centrum IoT.

### <a name="view-data-on-your-iot-edge-device"></a>Wyświetlanie danych na urządzeniu usługi IoT Edge

Na urządzeniu usługi IoT Edge można wyświetlać komunikaty wysyłane z każdego pojedynczego modułu.

Jeśli te polecenia są wykonywane na urządzeniu z systemem Linux, może być konieczne użycie polecenia `sudo`, aby uzyskać podwyższony poziom uprawnień.

1. Wyświetl wszystkie moduły na urządzeniu usługi IoT Edge.

   ```cmd/sh
   iotedge list
   ```

2. Wyświetl komunikaty wysyłane z określonego urządzenia. Użyj nazwy modułu z danych wyjściowych poprzedniego polecenia.

   ```cmd/sh
   iotedge logs <module_name> -f
   ```

### <a name="view-data-arriving-at-your-iot-hub"></a>Wyświetlanie danych otrzymywanych przez centrum IoT

Komunikaty urządzenie-chmura odbierane przez centrum IoT można wyświetlić przy użyciu [rozszerzenia Azure IoT Hub Toolkit dla programu Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit) (dawniej rozszerzenia Azure IoT Toolkit).

Poniższe kroki pokazują, jak skonfigurować program Visual Studio Code w celu monitorowania komunikatów urządzenie-chmura w centrum IoT.

1. W programie Visual Studio Code wybierz pozycję **IoT Hub Devices** (Urządzenia centrum IoT Hub).

2. Wybierz pozycję **...** , a następnie wybierz pozycję **Set IoT Hub Connection String** (Ustaw parametry połączenia centrum IoT Hub) z menu.

   ![Określanie parametrów połączenia centrum IoT Hub](./media/tutorial-deploy-machine-learning/set-connection.png)

3. W polu tekstowym, które zostanie otwarte w górnej części strony wprowadź ciąg połączenia iothubowner dla używanego centrum IoT Hub. Urządzenie usługi IoT Edge powinno zostać wyświetlone na liście IoT Hub Devices (Urządzenia centrum IoT Hub).

4. Ponownie wybierz pozycję **...** , a następnie wybierz pozycję **Start monitoring D2C message** (Rozpocznij monitorowanie komunikatu D2C).

5. Obserwuj komunikaty przychodzące z modułu tempSensor co pięć sekund. Treść komunikatu zawiera właściwość o nazwie **anomaly**, którą moduł machinelearningmodule ustawia na wartość true lub false. Właściwość **AzureMLResponse** zawiera wartość „OK”, jeśli model został uruchomiony pomyślnie.

   ![Odpowiedź usługi Azure Machine Learning Service w treści komunikatu](./media/tutorial-deploy-machine-learning/ml-output.png)

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Jeśli zamierzasz przejść do kolejnego zalecanego artykułu, możesz zachować utworzone zasoby oraz konfiguracje i użyć ich ponownie. Możesz także nadal używać tego samego urządzenia usługi IoT Edge jako urządzenia testowego.

W przeciwnym razie możesz usunąć konfigurację lokalną i zasoby platformy Azure utworzone podczas pracy z tym artykułem, aby uniknąć naliczania opłat.

[!INCLUDE [iot-edge-clean-up-cloud-resources](../../includes/iot-edge-clean-up-cloud-resources.md)]

[!INCLUDE [iot-edge-clean-up-local-resources](../../includes/iot-edge-clean-up-local-resources.md)]


## <a name="next-steps"></a>Następne kroki

W tym samouczku wdrożono moduł usługi IoT Edge obsługiwany przez usługę Azure Machine Learning. Możesz teraz kontynuować pracę, korzystając ze wszystkich innych samouczków, aby dowiedzieć się o innych metodach, za pomocą których usługa Azure IoT Edge może ułatwiać przekształcanie danych w analizy biznesowe na urządzeniach brzegowych.

> [!div class="nextstepaction"]
> [Klasyfikowanie obrazów za pomocą usługi Custom Vision](tutorial-deploy-custom-vision.md)

