---
title: Dostępność i wydajność kompromisy dla różnych poziomów spójności w usłudze Azure Cosmos DB
description: Dostępność i wydajność kompromisy dla różnych poziomów spójności w usłudze Azure Cosmos DB.
author: markjbrown
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 2/13/2019
ms.author: mjbrown
ms.reviewer: sngun
ms.openlocfilehash: 99b981e6b5c9bc56c10b0491474c0c8773291b7e
ms.sourcegitcommit: f7be3cff2cca149e57aa967e5310eeb0b51f7c77
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/15/2019
ms.locfileid: "56309204"
---
# <a name="consistency-availability-and-performance-tradeoffs"></a>Kompromisy w zakresie spójności, dostępności i wydajności 

Rozproszonych baz danych, które zależą od replikacji dla wysokiej dostępności i małym opóźnieniu musi kompromisy. Skutków ubocznych należą do zakresu od spójności odczytu, a dostępność, opóźnienia i przepływności.

Wyjaśnienie pojęcia spójności danych jako liczne opcje zbliża się do usługi Azure Cosmos DB. Ta metoda obejmuje więcej opcji niż dwoma skrajnymi poziomami spójności silną i ostateczną. Możesz wybrać z pięciu dobrze zdefiniowanych modeli na spektrum spójności. Od najsilniejszej do najsłabszej, modele są:

- Silna
- Powiązana nieaktualność
- Sesja
- Spójny prefiks
- Ostateczna

Każdy model zawiera wpływ na dostępność i wydajność i jest wspierana przez kompleksowe umowy SLA.

## <a name="consistency-levels-and-latency"></a>Poziomy spójności i opóźnienia

- Opóźnienie odczytu dla wszystkich poziomów spójności zawsze może być mniejsza niż 10 milisekund w 99. percentylu. To opóźnienie odczytu są objęte umową SLA. Średnia, opóźnienie w 50. percentyl odczytu jest zwykle 2 milisekund lub mniej. Azure konta usługi Cosmos span kilku regionach, które są skonfigurowane przy użyciu silnej spójności są wyjątkiem od tej gwarancji.

- Opóźnienie zapisu dla pozostałych poziomów spójności zawsze może być mniejsza niż 10 milisekund w 99. percentylu. To opóźnienie zapisu są objęte umową SLA. Opóźnienie zapisu średnia, na 50. percentyl jest zazwyczaj 5 milisekund lub mniej.

Niektóre konta usługi Azure Cosmos może być kilku regionach skonfigurowane za pomocą silnej spójności. W tym przypadku opóźnienie zapisu może być mniejsza niż dwa razy czas obustronnej konwersji (RTT) plus 10 milisekund w 99. percentylu. RTT między dowolnymi dwoma regionami położony jest skojarzony z Twoim kontem usługi Azure Cosmos. Jest równa RTT między dowolnymi dwoma regionami położony skojarzonych z Twoim kontem usługi Azure Cosmos. Ta opcja jest obecnie w wersji zapoznawczej.

Dokładny czas oczekiwania RTT jest funkcja odległości szybkość świateł i topologię sieci platformy Azure. Sieci platformy Azure nie zapewnia żadnych opóźnień umowy SLA dla RTT między wszystkie dwóch regionach platformy Azure. Konta usługi Azure Cosmos opóźnienia w replikacji są wyświetlane w witrynie Azure portal. Za pomocą witryny Azure portal do monitorowania opóźnienia w replikacji między różnych regionów, które są skojarzone z Twoim kontem.

## <a name="consistency-levels-and-throughput"></a>Poziomy spójności i przepływności

- Sesja, spójny prefiks i poziomy spójności ostatecznej taką samą liczbę jednostek żądania, podaj około dwa razy to przepływność odczytu w porównaniu z silną i powiązana nieaktualność.

- Dla danego typu operacji zapisu, takich jak insert, replace, upsert i usuwania przepływność zapisu dla jednostek żądania jest taka sama dla wszystkich poziomów spójności.

## <a id="rto"></a>Spójność poziomy i danych trwałości

W środowisku globalnie rozproszona baza danych ma bezpośrednią relację między trwałości danych i na spójność obecności awarii całego regionu. Podczas opracowywania planem ciągłości biznesowej, należy zrozumieć maksymalnego dopuszczalnego czasu oczekiwania na pełne odzyskanie aplikacji po wystąpieniu zdarzenia powodującego zakłócenia. Czas wymagany do przeprowadzenia pełnego odzyskania aplikacji jest znany jako cel czasu odzyskiwania (RTO). Należy również zrozumieć maksymalny okres najnowszych aktualizacji danych, aplikacja może tolerować utraty podczas odzyskiwania po wystąpieniu zdarzenia powodującego zakłócenia. Okres aktualizacji, które mogą umożliwić utratę jest określany jako cel punktu odzyskiwania (RPO).

Tabela definiuje relację między relacji między trwałości danych i modelu spójności obecności awarii szerokiego regionu. Należy pamiętać, że w rozproszonym systemie wysoki poziom spójności, nawet w przypadku jest niemożliwe do rozproszonej bazy danych za pomocą RPO i RTO zero z powodu kolejnego elementu teorii CAP. Aby dowiedzieć się więcej o tym, dlaczego, zobacz [poziomy spójności w usłudze Azure Cosmos DB](consistency-levels.md).

|**Regiony**|**Tryb replikacji**|**Poziom spójności**|**RPO**|**RTO**|
|---------|---------|---------|---------|---------|
|1|Jednego lub wielu wzorców|Dowolny poziom spójności|< 240 minut|< 1 tydzień|
|>1|Wzorca pojedynczej|Sesja, spójny prefiks i ostateczna|< 15 minut|< 15 minut|
|>1|Wzorca pojedynczej|Powiązana nieaktualność|K & T|< 15 minut|
|>1|Multi-Master|Sesja, spójny prefiks i ostateczna|< 15 minut|0|
|>1|Multi-Master|Powiązana nieaktualność|K & T|0|
|>1|Jednego lub wielu wzorców|Silna|0|< 15 minut|

K = liczba "K" wersji (aktualizacje) elementu.
T = "T" Godzina przedział czasu od momentu ostatniej aktualizacji.

## <a name="next-steps"></a>Kolejne kroki

Dowiedz się więcej na temat dystrybucji globalnej i wpływ na ogólną spójność w systemach rozproszonych. Zobacz następujące artykuły:

- [Wady i zalety spójności w nowoczesnych rozproszoną bazę danych, projektowanie systemów](https://www.computer.org/web/csdl/index/-/csdl/mags/co/2012/02/mco2012020037-abs.html)
- [Wysoka dostępność](high-availability.md)
- [Azure Cosmos DB w umowie SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/v1_2/)
