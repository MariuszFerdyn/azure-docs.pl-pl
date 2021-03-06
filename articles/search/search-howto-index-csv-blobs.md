---
title: Indeksowanie obiektów blob CSV za pomocą indeksatora obiektów Blob platformy Azure Search — usługa Azure Search
description: Można przeszukiwać obiektów blob CSV w usłudze Azure Blob storage w celu wyszukiwania pełnotekstowego przy użyciu indeksu usługi Azure Search. Indeksatory zautomatyzować pozyskiwanie danych dla wybranych źródeł danych takich jak usługi Azure Blob storage.
ms.date: 10/17/2018
author: mgottein
manager: cgronlun
ms.author: magottei
services: search
ms.service: search
ms.devlang: rest-api
ms.topic: conceptual
ms.custom: seodec2018
ms.openlocfilehash: eac0c1f2f7ded35cf09eec12f0406c754621f49c
ms.sourcegitcommit: cf88cf2cbe94293b0542714a98833be001471c08
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/23/2019
ms.locfileid: "54465466"
---
# <a name="indexing-csv-blobs-with-azure-search-blob-indexer"></a>Indeksowanie obiektów blob CSV za pomocą indeksatora obiektów blob usługi Azure Search
Domyślnie [indeksatora obiektów blob usługi Azure Search](search-howto-indexing-azure-blob-storage.md) analizuje rozdzielany tekst obiektów blob jako jeden fragment tekstu. Jednak za pomocą obiektów blob zawierający dane w formacie CSV, często zachodzi potrzeba traktują każdy wiersz w obiekcie blob jako oddzielny dokument. Na przykład, biorąc pod uwagę następujący tekst rozdzielany, warto go przeanalizować pod dwa dokumenty, zawierających każdego pola "tags", "datePublished" i "id": 

    id, datePublished, tags
    1, 2016-01-12, "azure-search,azure,cloud" 
    2, 2016-07-07, "cloud,mobile" 

W tym artykule dowiesz się, jak analizować obiektów blob CSV za pomocą indeksatora obiektów blob usługi Azure Search. 

> [!IMPORTANT]
> Indeksowanie obiektów blob CSV jest obecnie dostępna w publicznej wersji zapoznawczej i nie powinny być używane w środowiskach produkcyjnych. Aby uzyskać więcej informacji, zobacz [REST api-version = 2017-11-11-Preview](search-api-2017-11-11-preview.md). 
> 

## <a name="setting-up-csv-indexing"></a>Konfigurowanie indeksowania CSV
Aby indeksowanie obiektów blob CSV, Utwórz lub zaktualizuj definicję indeksatora z `delimitedText` tryb analizy:  

    {
      "name" : "my-csv-indexer",
      ... other indexer properties
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "firstLineContainsHeaders" : true } }
    }

Aby uzyskać szczegółowe informacje na temat tworzenia interfejsu API indeksatora, zapoznaj się [tworzenie indeksatora](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

`firstLineContainsHeaders` Wskazuje, że pierwszy wiersz (niepustych) każdy obiekt blob zawiera nagłówki.
Jeśli obiekty BLOB nie zawierają wiersz nagłówka początkowej, należy określić nagłówków w konfiguracji indeksatora: 

    "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } } 

Można dostosować przy użyciu znaku ogranicznika `delimitedTextDelimiter` ustawienia konfiguracji. Na przykład:

    "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextDelimiter" : "|" } }

> [!NOTE]
> Aktualnie obsługiwana jest tylko kodowanie UTF-8. Jeśli potrzebujesz pomocy technicznej dla innego kodowania głosować na na [UserVoice](https://feedback.azure.com/forums/263029-azure-search).

> [!IMPORTANT]
> Korzystając z tekstu rozdzielanego tryb analizy usługi Azure Search przyjęto założenie, że wszystkie obiekty BLOB ze źródła danych będą CSV. Jeśli potrzebujesz do obsługi różnych obiektów blob CSV i niebędący woluminem CSV, w tym samym źródle danych, można głosować na na [UserVoice](https://feedback.azure.com/forums/263029-azure-search).
> 
> 

## <a name="request-examples"></a>Przykładowe żądanie
Umieszczenie to wszystkie ze sobą, poniżej przedstawiono przykłady pełny ładunek. 

Źródło danych: 

    POST https://[service name].search.windows.net/datasources?api-version=2017-11-11-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional, my-folder>" }
    }   

Indeksator:

    POST https://[service name].search.windows.net/indexers?api-version=2017-11-11-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-csv-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } }
    }

## <a name="help-us-make-azure-search-better"></a>Pomóż nam ulepszyć usługę Azure Search
Jeśli masz sugestie funkcji lub pomysły dotyczące ulepszeń, podaj dane wejściowe na [UserVoice](https://feedback.azure.com/forums/263029-azure-search/).

