---
title: Pomoc techniczna usługi Azure Table Storage w usłudze Azure Cosmos DB
description: Dowiedz się, jak współpracują ze sobą Interfejs API tabel usługi Azure Cosmos DB i tabele usługi Azure Storage.
ms.service: cosmos-db
ms.subservice: cosmosdb-table
ms.topic: overview
ms.date: 11/15/2017
author: wmengmsft
ms.author: wmeng
ms.reviewer: sngun
ms.openlocfilehash: b105cf6c220534927a16be83ca5db8801c88f6c0
ms.sourcegitcommit: 8330a262abaddaafd4acb04016b68486fba5835b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/04/2019
ms.locfileid: "54035597"
---
# <a name="developing-with-azure-cosmos-db-table-api-and-azure-table-storage"></a>Programowanie za pomocą interfejsu API tabel usługi Azure Cosmos DB oraz usługi Azure Table Storage

Interfejs API tabel usługi Azure Cosmos DB oraz usługa Azure Table Storage mają ten sam model danych tabeli oraz udostępniają te same operacje tworzenia, usuwania, aktualizacji i zapytań w swoich zestawach SDK. 

[!INCLUDE [storage-table-cosmos-comparison](../../includes/storage-table-cosmos-comparison.md)]

## <a name="developing-with-the-azure-cosmos-db-table-api"></a>Programowanie z użyciem interfejsu API tabel usługi Azure Cosmos DB

W tej chwili [interfejs API tabel usługi Azure Cosmos DB](table-introduction.md) ma cztery zestawy SDK dostępne do programowania: 
- [Microsoft.Azure.CosmosDB.Table](https://aka.ms/tableapinuget) .NET SDK. Ta biblioteka ma takie same klasy i podpisy metod jak publiczny [zestaw SDK usługi Windows Azure Storage](https://www.nuget.org/packages/WindowsAzure.Storage), ale ma również możliwość łączenia się z kontami usługi Azure Cosmos DB przy użyciu interfejsu API tabel. Pamiętaj, że biblioteka `Microsoft.Azure.CosmosDB.Table` jest obecnie dostępna tylko dla platformy .NET Standard, nie jest jeszcze dostępna dla platformy .NET Core.
- [Zestaw SDK dla języka Python](table-sdk-python.md). Nowy zestaw SDK języka Python dla usługi Azure Cosmos DB jest jedynym zestawem SDK, który obsługuje usługę Azure Table Storage w języku Python. Ten zestaw SDK łączy się z usługą Azure Table Storage oraz interfejsem API tabel usługi Azure Cosmos DB.
- [Zestaw SDK Java](table-sdk-java.md). Ten zestaw SDK usługi Azure Storage ma możliwość łączenia z kontami usługi Azure Cosmos DB przy użyciu interfejsu API tabel.
- [Zestaw SDK dla platformy Node.js](table-sdk-nodejs.md). Ten zestaw SDK usługi Azure Storage ma możliwość łączenia z kontami usługi Azure Cosmos DB przy użyciu interfejsu API tabel.

Dodatkowe informacje dotyczące pracy z interfejsem API tabel jest dostępna w artykule [Często zadawane pytania: programowanie przy użyciu interfejsu API tabel](faq.md#table).

## <a name="developing-with-azure-table-storage"></a>Programowanie z wykorzystaniem usługi Azure Table Storage

Magazyn tabel Azure oferuje do programowania następujące zestawy SDK:

- [Zestaw SDK dla platformy .NET WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/). Ta biblioteka umożliwia pracę z usługą Table Storage.
- [Zestaw SDK dla języka Python](table-sdk-python.md). Zestaw SDK tabel usługi Azure Cosmos DB dla języka Python obsługuje również usługę Table Storage.
- [Zestaw SDK usługi Azure Storage dla języka Java](https://github.com/azure/azure-storage-java). Ten zestaw SDK usługi Azure Storage zapewnia bibliotekę klienta w środowisku Java do pracy z usługą Azure Table Storage.
- [Zestaw SDK dla platformy Node.js](table-sdk-nodejs.md). Zestaw SDK zawiera pakiet Node.js i bibliotekę klienta JavaScript zgodną z przeglądarką, aby korzystać z usługi Table Storage.
- [Moduł programu PowerShell AzureRmStorageTable ](https://www.powershellgallery.com/packages/AzureRmStorageTable/1.0.0.7). Ten moduł programu PowerShell zawiera polecenia cmdlet do pracy z tabelami usługi Storage.
- [Biblioteka klienta usługi Azure Storage dla języka C++](https://github.com/Azure/azure-storage-cpp/). Ta biblioteka umożliwia tworzenie aplikacji w usłudze Azure Storage.
- [Biblioteka klienta tabel usługi Azure Storage dla Ruby](https://github.com/azure/azure-storage-ruby/tree/master/table). Ten projekt zapewnia pakiet Ruby, który ułatwia dostęp do tabel usługi Azure Storage.
- [Biblioteka klienta PHP tabel usługi Azure Storage](https://github.com/Azure/azure-storage-php/tree/master/azure-storage-table). Ten projekt zapewnia bibliotekę klienta PHP, która ułatwia dostęp do tabel usługi Azure Storage.


   





