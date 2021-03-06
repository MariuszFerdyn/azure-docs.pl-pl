---
title: Jak dodać źródła zdarzeń Centrum IoT do usługi Azure Time Series Insights | Dokumentacja firmy Microsoft
description: W tym artykule opisano sposób dodawania źródła zdarzeń, który jest podłączony do usługi IoT hub dla środowiska usługi Time Series Insights.
ms.service: time-series-insights
services: time-series-insights
author: ashannon7
ms.author: anshan
manager: cshankar
ms.reviewer: v-mamcge, jasonh, kfile, anshan
ms.workload: big-data
ms.topic: conceptual
ms.date: 11/30/2018
ms.custom: seodec18
ms.openlocfilehash: 933d411f67655b49b4aef7bf413dfe5f87e4ff08
ms.sourcegitcommit: b767a6a118bca386ac6de93ea38f1cc457bb3e4e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2018
ms.locfileid: "53556734"
---
# <a name="add-an-iot-hub-event-source-to-your-time-series-insights-environment"></a>Dodawanie źródła zdarzeń Centrum IoT do środowiska usługi Time Series Insights

W tym artykule opisano sposób dodawania źródła zdarzeń, która odczytuje dane z usługi Azure IoT Hub dla środowiska usługi Azure Time Series Insights za pomocą witryny Azure portal.

> [!NOTE]
> Instrukcje w tym artykule mają zastosowanie Azure czas Series Insights w wersji ogólnodostępnej i środowisk czasu Series Insights w wersji zapoznawczej.

## <a name="prerequisites"></a>Wymagania wstępne

* Tworzenie [środowisko usługi Azure Time Series Insights](time-series-insights-update-create-environment.md).
* Tworzenie [usługi IoT hub przy użyciu witryny Azure portal](../iot-hub/iot-hub-create-through-portal.md).
* Usługa IoT hub musi mieć zdarzenia aktywne wiadomości wysyłanych.
* Utwórz grupę odbiorców dedykowanej w usłudze IoT hub dla środowiska usługi Time Series Insights, aby korzystać z. Każdego źródła zdarzeń usługi Time Series Insights musi mieć swój własny dedykowanej grupy klientów, które nie zostały udostępnione innych odbiorców. Jeśli wielu elementów odczytujących korzystanie ze zdarzeń z tej samej grupy konsumentów, wszystkich czytelników prawdopodobnie błędy. Aby uzyskać więcej informacji, zobacz [— przewodnik dewelopera usługi Azure IoT Hub](../iot-hub/iot-hub-devguide.md).

### <a name="add-a-consumer-group-to-your-iot-hub"></a>Dodaj grupę odbiorców do usługi IoT hub

Aplikacje używać grupy odbiorców do pobierania danych z usługi Azure IoT Hub. Podaj dedykowanej grupy klientów, jest używany tylko przez to środowisko usługi Time Series Insights niezawodnie odczytu danych z usługi IoT hub.

Aby dodać nową grupę odbiorców do Centrum IoT:

1. W witrynie Azure portal należy znaleźć i otworzyć Centrum IoT hub.

1. W menu w obszarze **ustawienia**, wybierz opcję **wbudowanych punktach końcowych**, a następnie wybierz pozycję **zdarzenia** punktu końcowego.

   ![Na stronie punkty końcowe w kompilacji wybierz przycisk zdarzenia][1]

1. W obszarze **grupy konsumentów**, wprowadź unikatową nazwę dla grupy odbiorców. Użyj tej samej nazwie w danym środowisku usługi Time Series Insights, tworząc nowe źródło zdarzeń.

1. Wybierz pozycję **Zapisz**.

## <a name="add-a-new-event-source"></a>Dodaj nowe źródło zdarzeń

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).

1. W menu po lewej stronie wybierz pozycję **Wszystkie zasoby**. Wybierz środowisko usługi Time Series Insights.

1. W obszarze **topologii środowiska**, wybierz opcję **źródła zdarzeń**, a następnie wybierz pozycję **Dodaj**.

   ![Wybierz źródła zdarzeń, a następnie wybierz przycisk Dodaj][2]

1. W **nowe źródło zdarzeń** okienku dla **nazwy źródła zdarzeń**, wprowadź nazwę, która jest unikatowa dla tego środowiska usługi Time Series Insights. Na przykład, wprowadź **strumienia zdarzeń**.

1. Aby uzyskać **źródła**, wybierz opcję **usługi IoT Hub**.

1. Wybierz wartość dla **opcji importowania**:

   * Jeśli masz już Centrum IoT hub w jednej z Twoich subskrypcji, wybierz opcję **korzystanie z usługi IoT Hub z dostępnych subskrypcji**. Ta opcja jest to najłatwiejsza metoda.
   * Jeśli usługi IoT hub jest zewnętrzne w stosunku do subskrypcji, lub jeśli chcesz wybrać opcje zaawansowane, wybierz **ustawienia Centrum IoT Hub zapewniają ręcznie**.

   ![Wybierz opcje w okienku źródło zdarzeń][3]

1. W poniższej tabeli opisano właściwości, które są wymagane dla **korzystanie z usługi IoT Hub z dostępnych subskrypcji** opcji:

   ![Nowe okienko źródłowej zdarzenia - właściwości, aby ustawić w usłudze IoT Hub w korzystanie z opcji subskrypcje dostępne][4]

   | Właściwość | Opis |
   | --- | --- |
   | Identyfikator subskrypcji | Wybierz subskrypcję, w której utworzono Centrum IoT hub.
   | Nazwa centrum IoT | Wybierz nazwę Centrum IoT hub.
   | Nazwa zasad Centrum IoT | Wybierz zasady dostępu współdzielonego. Zasady dostępu współdzielonego można znaleźć na karcie Ustawienia Centrum IoT. Wszystkie zasady dostępu współdzielonego ma nazwę uprawnienia, ustaw i klucze dostępu. Zasady dostępu współdzielonego dla źródła zdarzenia *musi* mają **połączenie z usługą** uprawnienia.
   | Klucz zasad Centrum IoT | Klucz jest wypełniana wstępnie.
   | Grupa konsumentów Centrum IoT | Grupa odbiorców odczytuje zdarzenia z usługi IoT hub. Firma Microsoft zdecydowanie zaleca się Użyj dedykowanej grupy klientów dla źródła zdarzenia.
   | Format serializacji zdarzeń | Obecnie JSON jest format serializacji jedyną dostępną. Komunikaty o zdarzeniach musi być w następującym formacie, lub żadne dane nie mogą być odczytywane. |
   | Nazwa właściwości sygnatury czasowej | Aby określić tę wartość, należy zrozumieć format wiadomości danych komunikatów, które są wysyłane do usługi IoT hub. Ta wartość jest **nazwa** właściwości określone zdarzenie w danych wiadomości, które chcesz użyć jako sygnatura czasowa zdarzenia. Wartość jest rozróżniana wielkość liter. Jeśli pole pozostanie puste, **czas umieścić w kolejce zdarzenia** w zdarzeniu źródłowego jest używana jako sygnatura czasowa zdarzenia. |

1. W poniższej tabeli opisano wymaganych właściwości dla **ustawienia Centrum IoT Hub zapewniają ręcznie**:

   | Właściwość | Opis |
   | --- | --- |
   | Identyfikator subskrypcji | Subskrypcja, w której utworzono Centrum IoT hub.
   | Grupa zasobów | Nazwa grupy zasobów, w której utworzono Centrum IoT hub.
   | Nazwa centrum IoT | Nazwa centrum IoT hub. Podczas tworzenia Centrum IoT hub, wprowadzono nazwę Centrum IoT.
   | Nazwa zasad Centrum IoT | Zasady dostępu współdzielonego. Na karcie Ustawienia Centrum IoT, można utworzyć zasady dostępu współdzielonego. Wszystkie zasady dostępu współdzielonego ma nazwę uprawnienia, ustaw i klucze dostępu. Zasady dostępu współdzielonego dla źródła zdarzenia *musi* mają **połączenie z usługą** uprawnienia.
   | Klucz zasad Centrum IoT | Klucz dostępu współdzielonego, który jest używany do uwierzytelniania dostępu do przestrzeni nazw usługi Azure Service Bus. Wprowadź tutaj klucz podstawowy lub pomocniczy.
   | Grupa konsumentów Centrum IoT | Grupa odbiorców odczytuje zdarzenia z usługi IoT hub. Firma Microsoft zdecydowanie zaleca się Użyj dedykowanej grupy klientów dla źródła zdarzenia.
   | Format serializacji zdarzeń | Obecnie JSON jest format serializacji jedyną dostępną. Komunikaty o zdarzeniach musi być w następującym formacie, lub żadne dane nie mogą być odczytywane. |
   | Nazwa właściwości sygnatury czasowej | Aby określić tę wartość, należy zrozumieć format wiadomości danych komunikatów, które są wysyłane do usługi IoT hub. Ta wartość jest **nazwa** właściwości określone zdarzenie w danych wiadomości, które chcesz użyć jako sygnatura czasowa zdarzenia. Wartość jest rozróżniana wielkość liter. Jeśli pole pozostanie puste, **czas umieścić w kolejce zdarzenia** w zdarzeniu źródłowego jest używana jako sygnatura czasowa zdarzenia. |

1. Dodanie dedykowane usługi Time Series Insights konsumenta grupy nazwy dodanego do usługi IoT hub.

1. Wybierz pozycję **Utwórz**.

   ![Przycisk Utwórz][5]

1. Po utworzeniu źródła zdarzeń usługi Time Series Insights automatycznie rozpoczyna się przesyłanie strumieniowe danych do danego środowiska.

## <a name="next-steps"></a>Kolejne kroki

* [Zdefiniuj zasady dostępu do danych](time-series-insights-data-access.md) do zabezpieczania danych.
* [Wysyłanie zdarzeń](time-series-insights-send-events.md) do źródła zdarzenia.
* Dostęp do środowiska w [Eksploratora usługi Time Series Insights](https://insights.timeseries.azure.com).

<!-- Images -->
[1]: media/time-series-insights-how-to-add-an-event-source-iothub/iothub_one.png
[2]: media/time-series-insights-how-to-add-an-event-source-iothub/iothub_two.png
[3]: media/time-series-insights-how-to-add-an-event-source-iothub/iothub_three.png
[4]: media/time-series-insights-how-to-add-an-event-source-iothub/iothub_four.png
[5]: media/time-series-insights-how-to-add-an-event-source-iothub/iothub_five.png