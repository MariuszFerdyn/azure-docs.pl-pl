---
title: Migrowanie istniejącej usługi Azure SQL Data Warehouse do Gen2 | Dokumentacja firmy Microsoft
description: Instrukcje dotyczące migracji istniejącego magazynu danych na Gen2 oraz harmonogram migracji według regionów.
services: sql-data-warehouse
author: mlee3gsd
ms.author: anumjs
ms.reviewer: jrasnick
manager: craigg
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.topic: article
ms.date: 02/09/2019
ms.openlocfilehash: a3ec74d0b22bfafb4353eca400b389b07a58ba39
ms.sourcegitcommit: b3d74ce0a4acea922eadd96abfb7710ae79356e0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/14/2019
ms.locfileid: "56246362"
---
# <a name="upgrade-your-data-warehouse-to-gen2"></a>Uaktualnienie magazynu danych do Gen2
Firma Microsoft pomaga dysku szczegółów klasy podstawowej koszt uruchamiania wymagających zapytania, dodając dolnej warstwy wystąpień obliczeniowych dla usługi Azure SQL Data Warehouse do obsługi magazynu danych, przeczytaj pełne ogłoszenie [małe obliczeniowych warstwy obsługi Gen2](https://azure.microsoft.com/blog/azure-sql-data-warehouse-gen2-now-supports-lower-compute-tiers/). Nowa oferta jest już dostępna w regionach wymienionych w poniższej tabeli. Obsługiwane regiony można uaktualnić istniejących magazynów danych Gen1 do Gen2 przy użyciu jednej:
- **Proces automatycznego uaktualniania:** Nie należy uruchamiać automatycznych uaktualnień, jak usługa jest dostępna w regionie.  Po uruchomieniu automatycznych uaktualnień w określonym regionie, poszczególne uaktualnienia magazynu danych ma miejsce podczas harmonogramu konserwacji wybrane. 
- **Samodzielnie uaktualnienie do Gen2:** Jeśli wolisz decyduje, uaktualniania, możesz wykonać własnym uaktualnienie do Gen2. Jeśli w Twoim regionie nie jest jeszcze obsługiwana, należy przeprowadzić migrację usługi magazynu danych w regionie, który jest obsługiwany, a następnie wykonaj, samodzielnie uaktualnienie do generacji 2.

## <a name="automated-schedule-and-region-availability-table"></a>Harmonogram automatycznego i regionu w tabeli Dostępność
Poniższa tabela zawiera podsumowanie według regionu, gdy warstwa wystąpień obliczeniowych niższe Gen2 będą dostępne i po uruchomieniu automatycznych uaktualnień. Daty mogą ulec zmianie. Sprawdź ponownie po swój region staje się dostępna.

\* Wskazuje, że określonego harmonogramu dla regionu jest obecnie niedostępna.

| **Region** | **Niższe Gen2 dostępne** | **Rozpocznij automatycznych uaktualnień** |
|:--- |:--- |:--- |
| Australia Środkowa 1 |1 marca 2019 r. |15 czerwca 2019 r. |
| Australia Środkowa 2 |1 marca 2019 r. |15 czerwca 2019 r. |
| Australia Wschodnia |Dostępne |1 maja 2019 r. |
| Australia Południowo-Wschodnia |1 marca 2019 r. |15 czerwca 2019 r. |
| Brazylia Południowa |\* |\* |
| Kanada Środkowa |Dostępne |1 maja 2019 r. |
| Kanada Wschodnia |\* |\* |
| Środkowe stany USA |Dostępne |1 maja 2019 r. |
| Chiny Wschodnie |\* |\* |
| Chiny Północne 1 |\* |\* |
| Azja Wschodnia |Dostępne |1 maja 2019 r. |
| Wschodnie stany USA 1 |Dostępne |16 marca 2019 r. |
| Wschodnie stany USA 2 |Dostępne |16 marca 2019 r. |
| Francja Środkowa |1 marca 2019 r. |1 maja 2019 r. |
| Niemcy Środkowe |\* |\* |
| Indie Środkowe |Dostępne |1 maja 2019 r. |
| Indie Południowe 1 |1 marca 2019 r. |15 czerwca 2019 r. |
| Japonia Wschodnia |Dostępne |1 maja 2019 r. |
| Japonia Zachodnia |Dostępne |15 czerwca 2019 r. |
| Korea Środkowa |1 marca 2019 r. |1 maja 2019 r. |
| Korea South 1 |1 marca 2019 r. |15 czerwca 2019 r. |
| Środkowo-północne stany USA |1 marca 2019 r. |15 czerwca 2019 r. |
| Europa Północna |Dostępne |16 marca 2019 r. |
| Środkowo-południowe stany USA |Dostępne |1 maja 2019 r. |
| Azja Południowo-Wschodnia |Dostępne |16 marca 2019 r. |
| Południowe Zjednoczone Królestwo |1 marca 2019 r. |1 maja 2019 r. |
| Zachodnie Zjednoczone Królestwo 1 |1 marca 2019 r. |15 czerwca 2019 r. |
| Środkowo-zachodnie stany USA |\* |\* |
| Europa Zachodnia |Dostępne |16 marca 2019 r. |
| Zachodnie stany USA 1 |1 marca 2019 r. |15 czerwca 2019 r. |
| Zachodnie stany USA 2 |Dostępne |16 marca 2019 r. |

## <a name="automatic-upgrade-process"></a>Automatyczne uaktualnianie

Od 16 marca 2019 roku firma Microsoft rozpocznie się planowania automatycznych uaktualnień dla wystąpień Gen1. Aby uniknąć przerw nieoczekiwany na dostępności w magazynie danych, automatyczne uaktualnienia zostanie zaplanowana w harmonogramie konserwacji. Aby uzyskać więcej informacji dotyczących harmonogramów, zobacz [wyświetlić harmonogram konserwacji](viewing-maintenance-schedule.md)

Proces uaktualniania będzie obejmować krótki zrzutu w łączności (około 5 minut), jak możemy ponownie uruchomić Magazyn danych.  Po ponownym uruchomieniu usługi data warehouse będzie w pełni dostępne do użytku jednak, może wystąpić pogorszenie wydajności, podczas procesu uaktualniania w dalszym ciągu uaktualniania pliki danych w tle. Łączny czas spadek wydajności będą się różnić zależy od rozmiaru plików danych.

Można również przyspieszyć proces uaktualniania pliku danych, uruchamiając [Alter Index rebuild](sql-data-warehouse-tables-index.md) dla wszystkich tabel magazynu kolumn głównej przy użyciu większej klasy celu poziomu usługi i zasobów, po ponownym uruchomieniu.

> [!NOTE]
> ALTER Index rebuild jest operacją w trybie offline i tabele nie będą dostępne do momentu ukończenia ponownej kompilacji.

## <a name="self-upgrade-to-gen2"></a>Samodzielnie uaktualnienie do Gen2

Opcjonalnie Jeśli chcesz uaktualnić, można samodzielnie uaktualnienia, wykonując następujące czynności na istniejący magazyn danych Gen1. Jeśli wybierzesz tę opcję, należy wykonać uaktualnienie własnym przed rozpoczęciem procesu uaktualniania automatyczne, w tym regionie. Daje to gwarancję, że uniknąć ryzyka automatycznych uaktualnień, co powoduje konflikt.

Dostępne są dwie opcje podczas przeprowadzania uaktualnienia samodzielnie.  Możesz albo uaktualnić swoje bieżące dane magazynu w miejscu lub Gen1 magazyn danych można przywrócić do wystąpienia Gen2.

- [Uaktualnienie w miejscu](upgrade-to-latest-generation.md) — ta opcja spowoduje uaktualnienie istniejącego magazynu danych Gen1 do Gen2. Proces uaktualniania będzie obejmować krótki zrzutu w łączności (około 5 minut), jak możemy ponownie uruchomić Magazyn danych.  Po ponownym uruchomieniu usługi data warehouse będzie w pełni dostępne do użycia. Jeśli z jakiegokolwiek powodu, musisz przywrócić Gen1 z wystąpienia Gen2, otwórz [żądania pomocy technicznej](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-create-support-ticket).
- [Uaktualnianie z punktu przywracania](sql-data-warehouse-restore.md) — Utwórz punkt przywracania zdefiniowanych przez użytkownika na bieżącym Gen1 magazynu danych, a następnie przywróć bezpośrednio do wystąpienia Gen2. Istniejący magazyn danych Gen1 pozostaną w miejscu. Po ukończeniu przywracania Gen2 magazynu danych będzie w pełni dostępne do użycia.  Po uruchomieniu wszystkich procesów testowanie i sprawdzanie poprawności wystąpieniu Gen2 przywrócone oryginalne wystąpienie Gen1 mogą zostać usunięte.
    - Krok 1: W witrynie Azure portal [Utwórz punkt przywracania użytkownika](sql-data-warehouse-restore.md#create-a-user-defined-restore-point-using-the-azure-portal).
    - Krok 2: Przy przywracaniu z zdefiniowane przez użytkownika punkt przywracania, należy ustawić "performance poziom" preferowaną warstwę Gen2.

Okres pogorszenie wydajności mogą wystąpić podczas procesu uaktualniania w dalszym ciągu uaktualniania pliki danych w tle. Łączny czas spadek wydajności będą się różnić zależy od rozmiaru plików danych.

Aby przyspieszyć proces migracji danych w tle, możesz od razu wymusić przenoszenia danych, uruchamiając [Alter Index rebuild](sql-data-warehouse-tables-index.md) dla wszystkich tabel magazynu kolumn głównej będzie wykonywana kwerenda na większą klasę poziomu usługi i zasobów.

> [!NOTE]
> ALTER Index rebuild jest operacją w trybie offline i tabele nie będą dostępne do momentu ukończenia ponownej kompilacji.

Jeśli napotkasz jakiekolwiek problemy z magazynem danych, Utwórz [żądania pomocy technicznej](sql-data-warehouse-get-started-create-support-ticket.md) i odwoływać się do "Gen2 uaktualnienia" jako możliwa przyczyna.

Aby uzyskać więcej informacji, zobacz [uaktualnienie do Gen2](upgrade-to-latest-generation.md).

## <a name="migration-frequently-asked-questions"></a>Często zadawane pytania dotyczące migracji

**Pyt.: Gen2 kosztuje taka sama jak Gen1?**
- Odp.: Tak.

**Pyt.: Wpływ uaktualnienia na Moje skryptów automatyzacji?**
- Odp.: Dowolny skrypt automatyzacji, który odwołuje się do celu poziomu usług, należy je zmienić odpowiadają odpowiednik Gen2.  Zobacz szczegóły [tutaj](upgrade-to-latest-generation.md#sign-in-to-the-azure-portal).

**Pyt.: Jak uaktualnić własnym zwykle długo?**
- Odp.: Można uaktualnić w miejscu lub uaktualnić z punktu przywracania.  
   - Uaktualnianie w miejscu spowoduje, że magazyn danych chwilowo wstrzymać i wznowić.  Proces w tle będzie, gdy magazyn danych jest w trybie online.  
   - Trwa dłużej, Jeśli uaktualniasz za pośrednictwem punktu przywracania, ponieważ uaktualnienie będzie przechodzić przez proces pełne przywracanie.

**Pyt.: Jak długo będzie Trwa automatyczne uaktualnianie?**
- Odp.: Rzeczywisty przestój dla uaktualnienie jest czas potrzebny na wstrzymywanie i wznawianie usługi, która jest od 5 do 10 minut. Po krótki czas przestoju proces w tle będzie uruchomić migrację magazynu. Czas na proces w tle jest zależna od rozmiaru magazynu danych.

**Pyt.: Gdy to automatyczne uaktualnienie będzie miała miejsce?**
- Odp.: W harmonogramie konserwacji. Korzystanie z harmonogramu konserwacji wybrany zostanie zminimalizować zakłócenia dla Twojej firmy.

**Pyt.: Co należy zrobić, jeśli proces uaktualniania Moje tła wydają się być zablokowane?**
 - Odp.: Czy uruchamiał reindex tabel magazynu kolumn. Należy pamiętać, że indeksowanie tabeli będzie w trybie offline podczas tej operacji.

**Pyt.: Co zrobić, jeśli Gen2 — nie ma celu poziomu usługi mają na Gen1?**
- Odp.: Jeśli używasz wartości DW600 lub DW1200 na Gen1 zalecane jest użycie DW500c lub DW1000c odpowiednio ponieważ Gen2 oferuje więcej pamięci, zasoby i wyższą wydajność niż Gen1.

**Pyt.: Czy można wyłączyć geograficznej kopii zapasowej?**
- Odp.: Nie. Geograficznej kopii zapasowej to funkcja przedsiębiorstwa, aby zachować dane dostępności magazynu, w przypadku, gdy region staje się niedostępny. Otwórz [żądania pomocy technicznej](sql-data-warehouse-get-started-create-support-ticket.md) Jeśli masz więcej wątpliwości.

**Pyt.: Czy istnieje różnica w składni języka T-SQL między Gen1 i Gen2?**
- Odp.: Nie ma zmian w składni języka T-SQL z Gen1 Gen2.

**Pyt.: Gen2 obsługuje Windows konserwacji?**
- Odp.: Tak.

**Pyt.: Czy mogę będzie można utworzyć nowego wystąpienia Gen1 po uaktualnieniu moim regionie?**
- Odp.: Nie. Po uaktualnieniu region tworzenie nowych wystąpień Gen1 zostaną wyłączone.

## <a name="next-steps"></a>Kolejne kroki

- [Procedura uaktualniania](upgrade-to-latest-generation.md)
- [Okna obsługi](maintenance-scheduling.md)
- [Monitor kondycji zasobu](https://docs.microsoft.com/azure/service-health/resource-health-overview)
- [Sprawdź przed rozpoczęciem migracji](upgrade-to-latest-generation.md#before-you-begin)
- [Uaktualnienie w miejscu i uaktualnienia z punktu przywracania](upgrade-to-latest-generation.md)
- [Utwórz punkt przywracania zdefiniowanych przez użytkownika](sql-data-warehouse-restore.md#restore-through-the-azure-portal)
- [Dowiedz się, jak przywrócić Gen2](sql-data-warehouse-restore.md#restore-an-active-or-paused-database-using-the-azure-portal)
- [Otwórz żądanie obsługi usługa SQL Data Warehouse](https://go.microsoft.com/fwlink/?linkid=857950)