---
title: Przewodnik po interfejsie użytkownika usługi Azure IoT Central | Microsoft Docs
description: Jako konstruktor możesz zapoznać się z kluczowymi obszarami interfejsu użytkownika usługi Azure IoT Central używanego do utworzenia rozwiązania IoT.
author: dominicbetts
ms.author: dobett
ms.date: 01/24/2019
ms.topic: overview
ms.service: iot-central
services: iot-central
ms.custom: mvc
manager: philmea
ms.openlocfilehash: 80fe2fb2998ed129098a99f004da9c9e5e88e474
ms.sourcegitcommit: 359b0b75470ca110d27d641433c197398ec1db38
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/07/2019
ms.locfileid: "55815034"
---
# <a name="take-a-tour-of-the-azure-iot-central-ui-new-ui-design"></a>Przewodnik po interfejsie użytkownika usługi Azure IoT Central (nowy projekt interfejsu użytkownika)

W tym artykule przedstawiono wprowadzenie do interfejsu użytkownika usługi Microsoft Azure IoT Central. Interfejs użytkownika umożliwia tworzenie i używanie rozwiązania usługi Azure IoT Central oraz jego połączonych urządzeń, a także zarządzanie nimi.

_Konstruktor_ używa interfejsu użytkownika usługi Azure IoT Central, aby zdefiniować rozwiązanie usługi Azure IoT Central. Interfejs użytkownika umożliwia wykonywanie następujących zadań:

- Definiowanie typów urządzeń łączących się z rozwiązaniem
- Konfigurowanie reguł i akcji dla urządzeń
- Dostosowywanie interfejsu użytkownika dla _operatora_ używającego rozwiązania

_Operator_ używa interfejsu użytkownika usługi Azure IoT Central, aby zarządzać rozwiązaniem usługi Azure IoT Central. Interfejs użytkownika umożliwia wykonywanie następujących zadań:

- Monitorowanie urządzeń
- Konfigurowanie urządzeń
- Rozwiązywanie i korygowanie problemów z urządzeniami
- Aprowizacja nowych urządzeń.

[!INCLUDE [iot-central-experimental-note](../../includes/iot-central-experimental-note.md)]

## <a name="use-the-left-navigation-menu"></a>Używanie lewego menu nawigacji

Lewe menu nawigacji umożliwia uzyskiwanie dostępu do różnych obszarów aplikacji:

| Menu | Opis |
| ---- | ----------- |
| ![Lewe menu nawigacji](media/overview-iot-central-tour-experimental/navigationbar.png) | <ul><li>Przycisk **Strona główna** umożliwia wyświetlenie strony głównej aplikacji. Konstruktor może dostosować tę stronę główną dla operatorów.</li><li>Przycisk **Device Explorer** wyświetla listę symulowanych i rzeczywistych urządzeń skojarzonych z każdym szablonem urządzenia w aplikacji. Operator używa narzędzia **Device Explorer**, aby zarządzać połączonymi urządzeniami.</li><li>Przycisk **Zestawy urządzeń** umożliwia wyświetlenie i tworzenie zestawów urządzeń. Operator może tworzyć zestawy urządzeń w formie logicznych zbiorów urządzeń określonych w zapytaniu.</li><li>Przycisk **Analiza** umożliwia wyświetlenie analiz na podstawie danych telemetrycznych urządzeń i zestawów urządzeń. Operator może tworzyć widoki niestandardowe na podstawie danych urządzenia w celu uzyskania szczegółowych informacji z aplikacji.</li><li>Przycisk **Zadania** umożliwia zbiorcze zarządzanie urządzeniami przez tworzenie i uruchamianie zadań przeprowadzających aktualizacje w dużej skali.</li><li>Przycisk **Szablony urządzeń** powoduje wyświetlenie narzędzi używanych przez konstruktora do tworzenia szablonów urządzeń i zarządzania nimi.</li><li>Przycisk **Ciągły eksport danych** służy administratorom do konfigurowania ciągłego eksportowania do innych usług platformy Azure, takich jak magazyn czy kolejki.</li><li>Przycisk **Administracja** umożliwia wyświetlenie stron administracyjnych aplikacji, na których administrator może zarządzać użytkownikami, rolami i ustawieniami aplikacji.</li></ul> |

## <a name="search-help-and-support"></a>Wyszukiwanie, pomoc i pomoc techniczna

Górne menu jest wyświetlane na każdej stronie:

![Pasek narzędzi](media/overview-iot-central-tour-experimental/toolbar.png)

- Aby wyszukać szablony urządzeń i urządzenia, wybierz ikonę **Wyszukiwanie**.
- Aby zmienić język interfejsu użytkownika, wybierz ikonę **Język**.
- Aby uzyskać pomoc i pomoc techniczną, wybierz pozycję rozwijaną **Pomoc**, aby uzyskać listę zasobów.
- Aby zmienić motyw interfejsu użytkownika lub wylogować się z aplikacji, wybierz ikonę **Konto**.

Możesz wybrać jasny lub ciemny motyw interfejsu użytkownika:

![Wybieranie motywu interfejsu użytkownika](media/overview-iot-central-tour-experimental/themes.png)

## <a name="home-page"></a>Strona główna

![Strona główna](media/overview-iot-central-tour-experimental/homepage.png)

Strona główna jest pierwszą stroną widoczną po zalogowaniu się do aplikacji usługi Azure IoT Central. Konstruktor może dostosować stronę główną dla innych użytkowników aplikacji przez dodanie kafelków. Więcej informacji można znaleźć w samouczku [Customize the Azure IoT Central operator's view (Dostosowywanie widoku operatora usługi Azure IoT Central)](tutorial-customize-operator-experimental.md?toc=/azure/iot-central-experimental/toc.json&bc=/azure/iot-central-experimental/breadcrumb/toc.json).

## <a name="device-explorer"></a>Device Explorer

![Strona Eksplorator](media/overview-iot-central-tour-experimental/explorer.png)

Na stronie eksploratora są wyświetlane _urządzenia_ w aplikacji usługi Azure IoT Central pogrupowane według _szablonu urządzeń_.

* Szablon urządzenia definiuje typ urządzenia, który może łączyć się z aplikacją. Aby dowiedzieć się więcej, zobacz [Define a new device type in your Azure IoT Central application (Definiowanie nowego typu urządzenia w aplikacji usługi Azure IoT Central)](tutorial-define-device-type-experimental.md?toc=/azure/iot-central-experimental/toc.json&bc=/azure/iot-central-experimental/breadcrumb/toc.json).
* Urządzenie reprezentuje rzeczywiste lub symulowane urządzenie w aplikacji. Aby dowiedzieć się więcej, zobacz [Add a new device to your Azure IoT Central application (Dodawanie nowego urządzenia do aplikacji usługi Azure IoT Central)](tutorial-add-device-experimental.md?toc=/azure/iot-central-experimental/toc.json&bc=/azure/iot-central-experimental/breadcrumb/toc.json).

## <a name="device-sets"></a>Zestawy urządzeń

![Strona Zestawy urządzeń](media/overview-iot-central-tour-experimental/devicesets.png)

Na stronie _Zestawy urządzeń_ są wyświetlane zestawy urządzeń utworzone przez konstruktora. Zestaw urządzeń to zbiór pokrewnych urządzeń. Konstruktor definiuje zapytanie, aby zidentyfikować urządzenia w zestawie urządzeń. Zestawy urządzeń są używane podczas dostosowywania analizy w aplikacji. Aby dowiedzieć się więcej, zobacz artykuł [Use device sets in your Azure IoT Central application (Używanie zestawów urządzeń w aplikacji usługi Azure IoT Central)](howto-use-device-sets-experimental.md?toc=/azure/iot-central-experimental/toc.json&bc=/azure/iot-central-experimental/breadcrumb/toc.json).

## <a name="analytics"></a>Analiza

![Strona Analiza](media/overview-iot-central-tour-experimental/analytics.png)

Strona analizy przedstawia wykresy, które ułatwiają zrozumienie zachowania urządzeń połączonych z aplikacją. Operator używa tej strony do monitorowania i badania problemów z połączonymi urządzeniami. Konstruktor może zdefiniować wykresy wyświetlane na tej stronie. Aby dowiedzieć się więcej, zobacz artykuł [Create custom analytics for your Azure IoT Central application (Tworzenie niestandardowej analizy dla aplikacji usługi Azure IoT Central)](howto-use-device-sets-experimental.md?toc=/azure/iot-central-experimental/toc.json&bc=/azure/iot-central-experimental/breadcrumb/toc.json).

## <a name="jobs"></a>Stanowiska

![Strona zadań](media/overview-iot-central-tour-experimental/jobs.png)

Strona zadań umożliwia wykonywanie zbiorczych operacji zarządzania urządzeniami na Twoich urządzeniach. Konstruktor używa tej strony do aktualizowania właściwości urządzeń, ustawień i poleceń. Aby dowiedzieć się więcej, zobacz artykuł [Uruchamianie zadania](howto-run-a-job-experimental.md?toc=/azure/iot-central-experimental/toc.json&bc=/azure/iot-central-experimental/breadcrumb/toc.json).

## <a name="device-templates"></a>Szablony urządzeń

![Strona Szablony urządzeń](media/overview-iot-central-tour-experimental/templates.png)

Na stronie szablonów urządzeń konstruktor tworzy szablony urządzeń w aplikacji i zarządza nimi. Aby dowiedzieć się więcej, zobacz samouczek [Define a new device type in your Azure IoT Central application (Definiowanie nowego typu urządzenia w aplikacji usługi Azure IoT Central)](tutorial-define-device-type-experimental.md?toc=/azure/iot-central-experimental/toc.json&bc=/azure/iot-central-experimental/breadcrumb/toc.json).

## <a name="continuous-data-export"></a>Ciągły eksport danych

![Strona Ciągły eksport danych](media/overview-iot-central-tour-experimental/export.png)

Na stronie ciągłego eksportu danych administrator definiuje sposób eksportowania danych, takich jak dane telemetryczne, z aplikacji. Inne usługi mogą zapisywać wyeksportowane dane lub poddawać je analizie. Aby dowiedzieć się więcej, zobacz artykuł [Eksportowanie danych do usługi Azure IoT Central](howto-export-data-experimental.md?toc=/azure/iot-central-experimental/toc.json&bc=/azure/iot-central-experimental/breadcrumb/toc.json).

## <a name="administration"></a>Administracja

![Strona Administracja](media/overview-iot-central-tour-experimental/administration.png)

Strona administracji zawiera linki do narzędzi używanych przez administratora, takich jak definiowanie użytkowników i ról w aplikacji. Aby dowiedzieć się więcej, zobacz artykuł [Administer your Azure IoT Central application (Administrowanie aplikacją usługi Azure IoT Central)](howto-administer-experimental.md?toc=/azure/iot-central-experimental/toc.json&bc=/azure/iot-central-experimental/breadcrumb/toc.json).

## <a name="next-steps"></a>Następne kroki

Po zapoznaniu się z omówieniem usługi Azure IoT Central i układem interfejsu użytkownika następnym sugerowanym krokiem jest wykonanie przewodnika Szybki start [Create an Azure IoT Central application (Tworzenie aplikacji usługi Azure IoT Central)](quick-deploy-iot-central-experimental.md?toc=/azure/iot-central-experimental/toc.json&bc=/azure/iot-central-experimental/breadcrumb/toc.json).