---
title: Rozwiązywanie typowych problemów indeksatora wyszukiwania — usługa Azure Search
description: Napraw błędy i często spotykanych problemów z indeksatorów w usłudze Azure Search w tym połączenia ze źródłem danych, Zapora i brakujących dokumentów.
author: mgottein
manager: cgronlun
services: search
ms.service: search
ms.devlang: na
ms.topic: conceptual
ms.date: 11/19/2018
ms.author: magottei
ms.custom: seodec2018
ms.openlocfilehash: 7696f1628edd3b81568382fd7892a877c6f54ef7
ms.sourcegitcommit: eb9dd01614b8e95ebc06139c72fa563b25dc6d13
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/12/2018
ms.locfileid: "53312395"
---
# <a name="troubleshooting-common-indexer-issues-in-azure-search"></a>Rozwiązywanie typowych problemów indeksatora w usłudze Azure Search

Indeksatory można uruchamiać na kilka problemów podczas indeksowania danych do usługi Azure Search. Główne kategorie awarii:

* [Łączenie ze źródłem danych](#Data-Source-Connection-Errors)
* [Przetwarzanie dokumentu](#Document-Processing-Errors)
* [Pozyskiwanie dokumentów do indeksu](#Index-Errors)

## <a name="data-source-connection-errors"></a>Błędy połączenia źródła danych

### <a name="blob-storage"></a>Blob Storage

#### <a name="storage-account-firewall"></a>Zapora konta magazynu

Usługa Azure Storage udostępnia można skonfigurować zapory. Domyślnie Zapora jest wyłączona, usługa Azure Search do połączenia się z kontem magazynu.

Istnieje nie określony komunikat o błędzie, gdy Zapora jest włączona. Zazwyczaj błędy zapory wyglądać `The remote server returned an error: (403) Forbidden`.

Możesz sprawdzić, czy Zapora jest włączona w [portal](https://docs.microsoft.com/azure/storage/common/storage-network-security#azure-portal). Jeśli Zapora jest włączona, masz dwie opcje poruszanie się tego problemu:

1. Wyłącz zaporę, wybierając pozycję zezwolić na dostęp z ["Wszystkie sieci"](https://docs.microsoft.com/azure/storage/common/storage-network-security#azure-portal)
1. [Dodaj wyjątek](https://docs.microsoft.com/azure/storage/common/storage-network-security#managing-ip-network-rules) dla adresu IP usługi wyszukiwania. Aby znaleźć ten adres IP, użyj następującego polecenia:

`nslookup <service name>.search.windows.net`

Wyjątki nie pracują dla [wyszukiwania kognitywnego](cognitive-search-concept-intro.md). Jedynym obejściem jest, aby wyłączyć zaporę.

### <a name="cosmos-db"></a>Cosmos DB

#### <a name="indexing-isnt-enabled"></a>Indeksowanie nie jest włączona

Usługa Azure Search ma niejawne zależność indeksowania usługi Cosmos DB. Po wyłączeniu automatycznego indeksowania w usłudze Cosmos DB, Azure Search zwraca stan pomyślne, ale nie może zawartość kontenerów indeksu. Aby uzyskać instrukcje dotyczące Sprawdź ustawienia i włączyć indeksowanie, zobacz [zarządzania indeksowaniem w usłudze Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/how-to-manage-indexing-policy#manage-indexing-using-azure-portal).

## <a name="document-processing-errors"></a>Błędy przetwarzania dokumentu

### <a name="unprocessable-or-unsupported-documents"></a>Brakuje lub nieobsługiwany dokumentów

Indeksowanie obiektów blob [dokumentów, które formaty dokumentów są jawnie obsługiwane.](search-howto-indexing-azure-blob-storage.md#supported-document-formats). Czasami kontenera magazynu obiektów blob zawiera nieobsługiwany dokumenty. Czasami może występować problematyczne dokumentów. Możesz uniknąć zatrzymywanie indeksator nad tymi dokumentami, [zmieniając opcje konfiguracji](search-howto-indexing-azure-blob-storage.md#dealing-with-errors):

```
PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2017-11-11
Content-Type: application/json
api-key: [admin key]

{
  ... other parts of indexer definition
  "parameters" : { "configuration" : { "failOnUnsupportedContentType" : false, "failOnUnprocessableDocument" : false } }
}
```

### <a name="missing-document-content"></a>Brak zawartości dokumentu

Indeksowanie obiektów blob [wyszukuje i wyodrębnia tekst z obiektów blob w kontenerze](search-howto-indexing-azure-blob-storage.md#how-azure-search-indexes-blobs). Niektórych problemów dzięki możliwości wyodrębniania tekstu obejmują:

* Dokument zawiera wyłącznie skanowaniu. Obiektów blob plików PDF, które mają zawartość nietekstową, np. skanowaniu (jpg), nie generują wyników w potoku indeksowania standardowych obiektów blob. Jeśli masz zawartość obrazu za pomocą elementów tekstowych, możesz użyć [wyszukiwania kognitywnego](cognitive-search-concept-image-scenarios.md) do znalezienia i wyodrębnianie tekstu.
* Indeksowanie obiektów blob jest skonfigurowany do tylko metadane indeksu. Aby wyodrębnić zawartość, indeksatora obiektów blob musi być skonfigurowana do [wyodrębnić zawartość i metadane](search-howto-indexing-azure-blob-storage.md#controlling-which-parts-of-the-blob-are-indexed):

```
PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2017-11-11
Content-Type: application/json
api-key: [admin key]

{
  ... other parts of indexer definition
  "parameters" : { "configuration" : { "dataToExtract" : "contentAndMetadata" } }
}
```

## <a name="index-errors"></a>Indeks błędów

### <a name="missing-documents"></a>Brak dokumentów

Indeksatory wyszukiwania dokumentów z [źródła danych](https://docs.microsoft.com/rest/api/searchservice/create-data-source). Czasami dokumentów ze źródła danych, do którego należy indeksować prawdopodobnie brakuje z indeksu. Istnieje kilka typowych przyczyn, że te błędy mogą występować:

* Zindeksował dokumentu. Sprawdź portal dla uruchomienia pomyślne indeksatora.
* Dokument został zaktualizowany po uruchomienie indeksatora. Jeśli indeksator znajduje się na [harmonogram](https://docs.microsoft.com/rest/api/searchservice/create-indexer#indexer-schedule), będzie ostatecznie ponowne uruchomienie i wybierze dokumentu.
* [Zapytania](https://docs.microsoft.com/rest/api/searchservice/create-data-source#request-body-syntax) określone w danych źródłowych wyłącza dokument. Indeksatory nie można indeksować dokumenty, które nie należą do źródła danych.
* [Mapowania pól](https://docs.microsoft.com/rest/api/searchservice/create-indexer#fieldmappings) lub [wyszukiwania kognitywnego](https://docs.microsoft.com/azure/search/cognitive-search-concept-intro) zmieniono dokument i jego wygląda inaczej, niż jest to oczekiwane.
* Użyj [odnośników w dokumencie interfejsu API](https://docs.microsoft.com/rest/api/searchservice/lookup-document) można znaleźć w dokumencie.
