---
title: Pojęcia wysokiej dostępności w usłudze Azure Database for PostgreSQL
description: Ten artykuł zawiera informacje o wysokiej dostępności, gdy przy użyciu usługi Azure Database for PostgreSQL.
author: rachel-msft
ms.author: raagyema
ms.service: postgresql
ms.topic: conceptual
ms.date: 02/01/2019
ms.openlocfilehash: d43647b57469efa4581dc1c74a842a51e9d54ad7
ms.sourcegitcommit: a65b424bdfa019a42f36f1ce7eee9844e493f293
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/04/2019
ms.locfileid: "55699821"
---
# <a name="high-availability-concepts-in-azure-database-for-postgresql"></a>Pojęcia wysokiej dostępności w usłudze Azure Database for PostgreSQL
Usługa Azure Database for PostgreSQL oferuje gwarantowaną wysoką dostępność. Finansowo umowy dotyczącej poziomu usług (SLA) wynosi 99,99% po ogólnym udostępnieniu. Nie ma praktycznie nie aplikacji, czas przestoju podczas korzystania z tej usługi.

## <a name="high-availability"></a>Wysoka dostępność
Model o wysokiej dostępności (HA) opiera się na mechanizmów wbudowany tryb failover, po wystąpieniu przerwania poziomu węzła. Przerwanie poziomu węzła może wystąpić z powodu awarii sprzętu lub w odpowiedzi na wdrożenie usługi.

Przez cały czas zmiany wprowadzone do usługi Azure Database for postgresql w warstwie serwera bazy danych występują w kontekście transakcji. Zmiany są rejestrowane w synchronicznie w usłudze Azure storage, gdy transakcja została zatwierdzona. W przypadku przerwania poziomu węzła serwera bazy danych powoduje utworzenie nowego węzła i automatycznie dołącza magazynu danych do nowego węzła. Wszystkie aktywne połączenia są odrzucane i wszystkich transakcji porządkowych nie są zatwierdzone.

## <a name="application-retry-logic-is-essential"></a>Istotne jest Logika ponawiania aplikacji
Ważne jest, postgresql w warstwie aplikacji baz danych zostały opracowane w celu wykrycia, a następnie spróbuj ponownie usunąć połączenia i nie powiodło się transakcji. Ponawia próbę aplikacji, połączenie aplikacji w sposób niewidoczny dla użytkownika jest przekierowywany do nowo utworzone wystąpienie przejmuje dla tego wystąpienia nie powiodło się.

Na platformie Azure, bramy jest używana wewnętrznie do przekierowania połączenia w nowym wystąpieniu. Po przerwaniu całego procesu pracy awaryjnej zwykle trwa dziesiątki sekund. Ponieważ przekierowanie odbywa się wewnętrznie przez bramę, ciąg połączenia zewnętrznego nie zmienia się dla aplikacji klienckich.

## <a name="scaling-up-or-down"></a>Skalowanie w górę lub w dół
Podobnie jak w modelu wysokiej dostępności usługi Azure Database for PostgreSQL jest skalowany w górę lub w dół, tworzone jest nowe wystąpienie serwera o określonym rozmiarze. Istniejący magazyn danych jest odłączona od oryginalnego wystąpienia i dołączyć do nowego wystąpienia.

Podczas operacji skalowania odbywa się przerwę połączenia bazy danych. Aplikacje klienckie są odłączone, a następnie otwórz niezatwierdzone transakcje są anulowane. Gdy aplikacja kliencka ponawia próbę połączenia lub tworzy nowe połączenie, bramy kieruje połączenia z wystąpieniem o nowym rozmiarze. 

## <a name="next-steps"></a>Kolejne kroki
- Dowiedz się więcej o [obsługi błędów przejściowych łączności](concepts-connectivity.md)
- Dowiedz się, jak [replikowania danych za pomocą odczytu replik](howto-read-replicas-portal.md)
