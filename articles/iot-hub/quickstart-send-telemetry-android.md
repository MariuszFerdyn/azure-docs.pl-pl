---
title: Wysyłanie danych telemetrycznych do usługi Azure IoT Hub — Szybki start (Android) | Microsoft Docs
description: W tym przewodniku Szybki start uruchomisz przykładową aplikację systemu Android wysyłającą symulowane dane telemetryczne do centrum IoT Hub oraz odczytującą dane telemetryczne z centrum IoT Hub na potrzeby przetwarzania w chmurze.
author: wesmc7777
manager: philmea
ms.service: iot-hub
services: iot-hub
ms.devlang: java
ms.topic: quickstart
ms.custom: mvc
ms.date: 11/05/2018
ms.author: wesmc
ms.openlocfilehash: d90595d3d557293bfbc6b06aca638eb1b7c08d30
ms.sourcegitcommit: efcd039e5e3de3149c9de7296c57566e0f88b106
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2018
ms.locfileid: "53164317"
---
# <a name="quickstart-send-iot-telemetry-from-an-android-device"></a>Szybki start: Przesyłanie danych telemetrycznych usługi IoT z urządzenia z systemem Android

[!INCLUDE [iot-hub-quickstarts-1-selector](../../includes/iot-hub-quickstarts-1-selector.md)]

IoT Hub to usługa platformy Azure, która umożliwia pozyskiwanie dużych ilości danych telemetrycznych z urządzeń IoT do chmury w celu magazynowania lub przetwarzania. W tym przewodniku Szybki start opisano sposób wysyłania danych telemetrycznych do centrum IoT Hub z aplikacji systemu Android uruchomionej na urządzeniu fizycznym lub symulowanym.

Do wysyłania danych telemetrycznych w tym przewodniku jest używana wstępnie napisana aplikacja dla systemu Android. Dane telemetryczne będzie można odczytać z centrum IoT Hub przy użyciu usługi Azure Cloud Shell. Przed uruchomieniem aplikacji należy utworzyć centrum IoT Hub i zarejestrować urządzenie w centrum.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

## <a name="prerequisites"></a>Wymagania wstępne

* Program Android Studio ze strony https://developer.android.com/studio/. Aby uzyskać więcej informacji na temat instalacji programu Android Studio, zobacz artykuł dotyczący [instalowania w systemie Android](https://developer.android.com/studio/install). 

* W przykładzie w tym artykule jest używany zestaw Android SDK 27. 

* [Przykładowa aplikacja dla systemu Android](https://github.com/Azure-Samples/azure-iot-samples-java/tree/master/iot-hub/Samples/device/AndroidSample) uruchamiana w tym przewodniku Szybki start jest częścią repozytorium azure-iot-samples-java w usłudze GitHub. Pobierz lub sklonuj repozytorium [azure-iot-samples-java](https://github.com/Azure-Samples/azure-iot-samples-java).



## <a name="create-an-iot-hub"></a>Tworzenie centrum IoT Hub

[!INCLUDE [iot-hub-include-create-hub](../../includes/iot-hub-include-create-hub.md)]

## <a name="register-a-device"></a>Rejestrowanie urządzenia

Zanim urządzenie będzie mogło nawiązać połączenie, należy je najpierw zarejestrować w centrum IoT. W tym przewodniku Szybki start opisano rejestrowanie urządzenia symulowanego przy użyciu usługi Azure Cloud Shell.

1. Uruchom następujące polecenia w usłudze Azure Cloud Shell, aby dodać rozszerzenie interfejsu wiersza polecenia usługi IoT Hub i utworzyć tożsamość urządzenia. 

   **YourIoTHubName**: zamień ten symbol zastępczy poniżej na wybraną nazwę centrum IoT Hub.

   **MyAndroidDevice**: MyAndroidDevice to nazwa nadana zarejestrowanemu urządzeniu. Użyj nazwy MyAndroidDevice w przedstawiony sposób. Jeśli wybierzesz inną nazwę dla swojego urządzenia, musisz również używać tej nazwy w tym artykule oraz zaktualizować nazwę urządzenia w przykładowych aplikacjach przed ich uruchomieniem.

    ```azurecli-interactive
    az extension add --name azure-cli-iot-ext
    az iot hub device-identity create --hub-name YourIoTHubName --device-id MyAndroidDevice
    ```

2. Uruchom następujące polecenia w usłudze Azure Cloud Shell, aby uzyskać _parametry połączenia urządzenia_ dla urządzenia, które właśnie zostało zarejestrowane:

    **YourIoTHubName**: zamień ten symbol zastępczy poniżej na wybraną nazwę centrum IoT Hub.

    ```azurecli-interactive
    az iot hub device-identity show-connection-string --hub-name YourIoTHubName --device-id MyAndroidDevice --output table
    ```

    Zanotuj parametry połączenia urządzenia, które wyglądają następująco:

   `HostName={YourIoTHubName}.azure-devices.net;DeviceId=MyAndroidDevice;SharedAccessKey={YourSharedAccessKey}`

    Tej wartości użyjesz w dalszej części tego przewodnika Szybki start do wysyłania danych telemetrycznych.

## <a name="send-telemetry"></a>Wysyłanie danych telemetrycznych

1. Otwórz przykładowy projekt GitHub dla systemu Android w programie Android Studio. Projekt znajduje się w następującym katalogu sklonowanej lub pobranej kopii repozytorium [azure-iot-sample-java](https://github.com/Azure-Samples/azure-iot-samples-java).

        \azure-iot-samples-java\iot-hub\Samples\device\AndroidSample

2. W programie Android Studio otwórz plik *gradle.properties* dla przykładowego projektu i zastąp symbol zastępczy **Device_Connection_String** zanotowanymi wcześniej parametrami połączenia.

    ```
    DeviceConnectionString=HostName={YourIoTHubName}.azure-devices.net;DeviceId=MyNodeDevice;SharedAccessKey={YourSharedAccessKey}
    ```

3. W programie Android Studio kliknij kolejno pozycje **File** > **Sync Project with Gradle Files** (Plik > Synchronizuj projekt z plikami Gradle). Sprawdź, czy kompilacja została zakończona.

4. Po zakończeniu kompilacji kliknij kolejno pozycje **Run** > **Run 'app'** (Uruchom > Uruchom „aplikację”). Skonfiguruj aplikację do uruchamiania na fizycznym urządzeniu z systemem Android lub w emulatorze systemu Android. Aby uzyskać więcej informacji na temat uruchamiania aplikacji systemu Android na urządzeniu fizycznym lub w emulatorze, zobacz [Run your app (Uruchamianie aplikacji)](https://developer.android.com/training/basics/firstapp/running-app).

5. Po załadowaniu aplikacji kliknij przycisk **Start**, aby rozpocząć wysyłanie danych telemetrycznych do centrum IoT Hub:

    ![Aplikacja](media/quickstart-send-telemetry-android/sample-screenshot.png)


## <a name="read-the-telemetry-from-your-hub"></a>Odczytywanie danych telemetrycznych z centrum

W tej sekcji, używając usługi Azure Cloud Shell z [rozszerzeniem IoT](https://docs.microsoft.com/cli/azure/ext/azure-cli-iot-ext/iot?view=azure-cli-latest), będziesz monitorować komunikaty urządzenia wysyłane przez urządzenie z systemem Android.

1. Używając usługi Azure Cloud Shell, uruchom następujące polecenie, aby nawiązać połączenie i odczytać komunikaty z centrum IoT:

   **YourIoTHubName**: zamień ten symbol zastępczy poniżej na wybraną nazwę centrum IoT Hub.

    ```azurecli-interactive
    az iot hub monitor-events --hub-name YourIoTHubName --output table
    ```
    Poniższy zrzut ekranu przedstawia dane wyjściowe w momencie odbierania przez centrum IoT Hub danych telemetrycznych wysyłanych przez urządzenie z systemem Android:

      ![Czytanie komunikatów urządzenia za pomocą interfejsu wiersza polecenia platformy Azure](media/quickstart-send-telemetry-android/read-data.png)


## <a name="clean-up-resources"></a>Oczyszczanie zasobów

[!INCLUDE [iot-hub-quickstarts-clean-up-resources](../../includes/iot-hub-quickstarts-clean-up-resources.md)]

## <a name="next-steps"></a>Następne kroki

W tym przewodniku Szybki start skonfigurowano centrum IoT Hub, zarejestrowano urządzenie, wysłano dane telemetryczne do centrum przy użyciu aplikacji z systemem Android oraz odczytano dane telemetryczne z centrum przy użyciu usługi Azure Cloud Shell.

Aby dowiedzieć się, jak kontrolować urządzenie symulowane z poziomu aplikacji zaplecza, przejdź do następnego przewodnika Szybki start.

> [!div class="nextstepaction"]
> [Szybki start: Sterowanie urządzeniem połączonym z centrum IoT Hub](quickstart-control-device-android.md)

