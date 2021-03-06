---
title: Transformacje i zadania w usłudze Azure Media Services | Dokumentacja firmy Microsoft
description: Korzystając z usługi Media Services, musisz utworzyć przekształcenie do opisu reguły lub specyfikacje dotyczące przetwarzania filmów wideo. Ten artykuł zawiera omówienie przekształcenie jest i jak z niej korzystać.
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.date: 02/17/2019
ms.author: juliako
ms.openlocfilehash: d93e0de48fd10677ad30e002390dc2e8177cf2eb
ms.sourcegitcommit: 4bf542eeb2dcdf60dcdccb331e0a336a39ce7ab3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/19/2019
ms.locfileid: "56408480"
---
# <a name="transforms-and-jobs"></a>Przekształcenia i zadania
 
Użyj [przekształca](https://docs.microsoft.com/rest/api/media/transforms) skonfigurować typowych zadań związanych z kodowaniem lub analizowanie filmów wideo. Każdy **Przekształcanie** opisuje młyna lub przepływu pracy zadań przetwarzania plików wideo lub audio. Pojedynczy przekształcenia można zastosować więcej niż jedną regułę. Przekształcenie można na przykład określić, że każdy plik wideo można zakodowany w postaci pliku MP4 o danej szybkości transmisji bitów i wygenerowania obraz miniatury z pierwszej ramki filmu wideo. Należy dodać jeden wpis TransformOutput dla każdej reguły, które chcesz uwzględnić w swojej transformacji. Przekształcenia można tworzyć w ramach konta usługi Media Services przy użyciu interfejsu API usługi Media Services v3 lub przy użyciu dowolnej z opublikowanych zestawów SDK. Przekształca Media Services v3, które interfejs API jest wymuszany przez usługę Azure Resource Manager, dzięki czemu można również użyć szablonów usługi Resource Manager do tworzenia i wdrażania w ramach konta usługi Media Services. Kontrola dostępu oparta na rolach może służyć do blokowania dostępu do przekształcenia.

Operacja aktualizacji na [Przekształcanie](https://docs.microsoft.com/rest/api/media/transforms) jednostki jest przeznaczony do wprowadzania zmian w lub priorytety TransformOutputs podstawowy opis. Zaleca się, że takie aktualizacje można wykonać po zakończeniu wszystkich zadań w toku. Jeśli planujesz ponowne zapisywanie adresów przepisu, musisz utworzyć nowe przekształcenie.

A [zadania](https://docs.microsoft.com/rest/api/media/jobs) jest rzeczywistego żądania do usługi Azure Media Services, aby zastosować **Przekształcanie** do danego wejściowego zawartości wideo lub audio. Po utworzeniu przekształcenia można przesłać zadania przy użyciu interfejsów API usług Media Services lub dowolny z opublikowanych zestawów SDK. **Zadania** określa informacje, takie jak lokalizacja wejściowych plików wideo i lokalizację danych wyjściowych. Można określić lokalizację je wideo przy użyciu: Adresy URL HTTPS, adresów URL sygnatury dostępu Współdzielonego, lub [zasoby](https://docs.microsoft.com/rest/api/media/assets). Postęp i stan zadania można uzyskać poprzez monitorowanie zdarzeń za pomocą usługi Event Grid. Aby uzyskać więcej informacji, zobacz [monitorowania zdarzeń za pomocą EventGrid](job-state-events-cli-how-to.md).

Operacja aktualizacji na [zadania](https://docs.microsoft.com/rest/api/media/jobs) jednostki może służyć do modyfikowania *opis*i *priorytet* właściwości po przesłaniu zadania. Zmiana *priorytet* właściwość jest efektywne tylko wtedy, gdy zadanie jest nadal w stanie umieszczenia w kolejce. Jeśli zadanie rozpoczął przetwarzanie lub zostało zakończone, zmiana priorytetu nie ma wpływu.

Na poniższym diagramie przedstawiono przekształcenia/zadania przepływu pracy.

![Przekształcenia](./media/encoding/transforms-jobs.png)

> [!NOTE]
> Właściwości **Przekształcanie** i **zadania** będące daty/godziny są zawsze w formacie UTC.

## <a name="typical-workflow"></a>Typowy przepływ pracy

1. Tworzenie przekształcenia 
2. Przesyłanie zadań w ramach tej transformacji 
3. Lista przekształceń 
4. Usuń przekształcenie, jeśli nie zamierzasz używać go w przyszłości. 

### <a name="example"></a>Przykład

Załóżmy, że chcesz wyodrębnić pierwszej ramki wszystkie filmy wideo dotyczące jako obraz miniatury — są kroki, które można wykonać: 

1. Zdefiniuj przepisu lub reguły dla przetwarzania plików wideo — "jako miniatury przy użyciu pierwszej ramki wideo". 
2. Dla każdego pliku wideo może poinformować usługi: 
    1. Gdzie można znaleźć tego wideo  
    2. Gdzie należy zapisać miniaturę danych wyjściowych. 

A **Przekształcanie** ułatwia tworzenie przepisu raz (krok 1) i przesyłanie zadań za pomocą tego przepisu (krok 2).

## <a name="paging"></a>Stronicowanie

Zobacz [filtrowanie, porządkowanie, stronicowanie jednostek usługi Media Services](entities-overview.md).

## <a name="next-steps"></a>Kolejne kroki

[Przekazywanie, kodowanie i przesyłanie strumieniowe plików wideo](stream-files-tutorial-with-api.md)
