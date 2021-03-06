---
title: Partycjonowanie i skalowanie w poziomie w usłudze Azure Cosmos DB
description: Więcej informacji na temat sposobu partycjonowania działa w usługi Azure Cosmos DB, jak skonfigurować partycje i kluczy partycji i Wybieranie klucza partycji odpowiednie dla twojej aplikacji.
ms.author: mjbrown
author: markjbrown
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 10/30/2018
ms.openlocfilehash: 55e9ef0f8bd268f36378c7d34cea95384c6f725e
ms.sourcegitcommit: eecd816953c55df1671ffcf716cf975ba1b12e6b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2019
ms.locfileid: "55099349"
---
# <a name="partitioning-and-horizontal-scaling-in-azure-cosmos-db"></a>Partycjonowanie i skalowanie w poziomie w usłudze Azure Cosmos DB

W tym artykule opisano fizycznie i logicznie partycji w usłudze Azure Cosmos DB i najlepsze rozwiązania dotyczące skalowania i partycjonowanie. 

## <a name="logical-partitions"></a>Partycje logiczne

Partycja logiczna składa się z zbiór elementów z tym samym kluczem partycji. Na przykład, należy wziąć pod uwagę kontenera, w którym zawierają wszystkie elementy `City` właściwość, należy użyć `City` jako klucza partycji dla kontenera. Grupy elementów z określonymi wartościami dla `City` takich jak "Londyn", "Paryż", "Warszawa" itp. będzie stanowić oddzielnej partycji logicznej.

W usłudze Azure Cosmos DB kontener jest podstawową jednostką skalowalności. Dane dodane do kontenera i przepływność, które można aprowizować w kontenerze są automatycznie (w poziomie) podzielonej na partycje w określonym zestawie partycji logicznej. Są one partycjonowane na podstawie określonego klucza partycji dla kontenera Cosmos. Aby dowiedzieć się więcej, zobacz [sposobu określania klucza partycji dla kontenera usługi Cosmos](how-to-create-container.md) artykułu.

Partycja logiczna definiuje zakres transakcji bazy danych. Należy zaktualizować elementów w ramach partycji logicznej przy użyciu transakcji z użyciem izolacji migawki. Kiedy nowe elementy są dodawane do kontenera, nowych partycji logicznej przezroczyste są tworzone przez system.

## <a name="physical-partitions"></a>Partycje fizyczne

Kontener usługi Azure Cosmos skalowania przez dystrybucję dużej liczby partycji logicznej danych i przepływności. Wewnętrznie, co najmniej jedną partycję logiczne są mapowane na **fizyczną partycję** składający się z zestawu replik, nazywana także zestawu replik. Każdego zestawu replik znajduje się wystąpienie aparatu bazy danych Azure Cosmos. Zestawu replik sprawia, że dane są przechowywane w partycję fizyczną trwałych, wysoce dostępny i spójne. Fizyczną partycję obsługuje maksymalną ilość pamięci masowej i jednostek RU. Każdej repliki partycji fizycznych wchodzących w skład dziedziczy przydział magazynowania. I wszystkie repliki partycji fizycznej obsługuje zbiorczo przepływności przydzielone do fizyczną partycję. Na poniższej ilustracji przedstawiono, jak logicznej partycji są mapowane na partycje fizyczne, które są globalnie rozproszone:

![Partycjonowanie usługi Azure Cosmos DB](./media/partition-data/logical-partitions.png)

Przepływnością aprowizowaną dla kontenera jest równomiernie podzielone między partycje fizyczne. W związku z tym projekt klucza partycji, który nie równomierne rozłożenie żądania przepływności można utworzyć partycji "gorącymi". Gorąca partycji może spowodować ograniczanie szybkości i nieefektywne użycie aprowizowanej przepływności.

W odróżnieniu od partycjami logicznymi partycje fizyczne są wewnętrznej implementacji systemu. Nie można kontrolować, ich rozmiar, położenie, liczba lub mapowanie między partycjami logicznymi i partycje fizyczne. Jednak można kontrolować liczbę partycji logicznej i dystrybucję danych i przepływności, wybierając klawisz prawo partycji.

## <a name="next-steps"></a>Kolejne kroki

W tym artykule omówienie partycjonowanie danych i najlepszych rozwiązań dla skalowania i udostępniane partycjonowanie w usłudze Azure Cosmos DB. 

* Dowiedz się więcej o [aprowizowanej przepływności w usłudze Azure Cosmos DB](request-units.md)
* Dowiedz się więcej o [dystrybucję globalną w usłudze Azure Cosmos DB](distribute-data-globally.md)
* Dowiedz się więcej o [wybór klucza partycji](partitioning-overview.md#choose-partitionkey)
* Dowiedz się, [jak aprowizować przepływność na kontenerze Cosmos](how-to-provision-container-throughput.md)
* Dowiedz się, [jak aprowizować przepływność mierzoną w bazie danych Cosmos](how-to-provision-database-throughput.md)
