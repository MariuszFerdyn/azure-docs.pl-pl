---
title: Omówienie tworzenia aplikacji korzystających z usługi SQL Database | Microsoft Docs
description: Informacje o dostępnych bibliotekach łączności i najlepsze praktyki dotyczące aplikacji łączących się z usługą SQL Database.
services: sql-database
ms.service: sql-database
ms.subservice: development
ms.custom: ''
ms.devlang: ''
ms.topic: howto
author: stevestein
ms.author: sstein
ms.reviewer: genemi
manager: craigg
ms.date: 02/07/2019
ms.openlocfilehash: 01c4bcfcea038f3e69620cdce78719c8c5128faf
ms.sourcegitcommit: d1c5b4d9a5ccfa2c9a9f4ae5f078ef8c1c04a3b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/08/2019
ms.locfileid: "55964801"
---
# <a name="sql-database-application-development-overview"></a>Omówienie tworzenia aplikacji bazy danych SQL

W tym artykule przedstawiono podstawowe zagadnienia, jakie powinien mieć na uwadze programista podczas pisania kodu nawiązującego połączenie z usługą Azure SQL Database. Ten artykuł dotyczy wszystkich modelach wdrażania usługi Azure SQL Database (pojedynczą bazę danych, pul elastycznych, wystąpienie zarządzane).

> [!TIP]
> Przyjrzeć dotyczącym pracę przewodniki dotyczące [pojedyncze bazy danych](sql-database-single-database-quickstart-guide.md) i [wystąpienia zarządzane](sql-database-managed-instance-quickstart-guide.md) Jeśli musisz skonfigurować usługi Azure SQL Database.
>

## <a name="language-and-platform"></a>Język i platforma

Można użyć różnych [programowania języków i platform](sql-database-connect-query.md) do nawiązywania połączeń i zapytań usługi Azure SQL Database. Możesz znaleźć [przykładowe aplikacje](https://azure.microsoft.com/resources/samples/?service=sql-database&sort=0) używanego do łączenia z usługą Azure SQL Database.

Można korzystać z narzędzi open source, takich jak [cheetah](https://github.com/wunderlist/cheetah), [sql-cli](https://www.npmjs.com/package/sql-cli), [programu VS Code](https://code.visualstudio.com/). Ponadto usługa Azure SQL Database współpracuje z narzędziami firmy Microsoft, takimi jak [Visual Studio](https://www.visualstudio.com/downloads/) i [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx). Można również użyć witryny Azure portal, programu PowerShell i interfejsów API REST można uzyskać większą produktywność.

## <a name="authentication"></a>Authentication

Dostęp do usługi Azure SQL Database jest chroniony za pomocą danych logowania i zapory. Usługa Azure SQL Database obsługuje programu SQL Server i [uwierzytelniania usługi Azure Active Directory (AAD)](sql-database-aad-authentication.md) użytkownicy i logowania. Logowania do usługi AAD są dostępne tylko w wystąpieniu zarządzanym. 

Dowiedz się więcej o [zarządzanie dostępem do bazy danych i logowania](sql-database-manage-logins.md).

## <a name="connections"></a>Połączenia

W logice połączenia klienta zastąp domyślny limit czasu wartością 30 sekund. Domyślna wartość 15 sekund jest zbyt mała w przypadku połączeń zależnych od Internetu.

Jeśli korzystasz z [puli połączeń](https://msdn.microsoft.com/library/8xx3tyca.aspx), pamiętaj o zamknięciu połączenia, gdy tylko Twój program nie korzysta z niego aktywnie i nie przygotowuje się do jego ponownego użycia.

Należy unikać długotrwałych transakcji, ponieważ jakiekolwiek niepowodzenie infrastruktury lub połączenie może być Wycofaj tę transakcję. Jeśli to możliwe, Podziel transakcji w wielu mniejszych transakcji i użyj [przetwarzanie wsadowe w celu zwiększenia wydajności](sql-database-use-batching-to-improve-performance.md).

## <a name="resiliency"></a>Odporność

Usługa Azure SQL Database to usługa w chmurze, w której można by oczekiwać błędów przejściowych, które występują w podstawowej infrastruktury lub w ramach komunikacji między jednostkami w chmurze. Mimo że bazy danych SQL Azure jest odporna na awarie przechodnie infrastruktury, te błędy mogą mieć wpływ na łączność. Gdy wystąpi błąd przejściowy podczas nawiązywania połączenia z bazą danych SQL, kod powinien [ponowić wywołanie](sql-database-connectivity-issues.md). Zalecamy, aby logika ponawiania korzystała z logiki wycofywania, co pozwoli uniknąć przeciążenia usługi SQL Database z powodu jednoczesnych ponownych prób ze strony wielu klientów. Logika ponawiania jest zależna od [komunikaty o błędach dotyczących programów klienckich usługi SQL Database](sql-database-develop-error-messages.md).

Aby uzyskać więcej informacji na temat przygotowywania w planowanych pracach konserwacyjnych na bazie danych Azure SQL, zobacz [planowanie zdarzenia konserwacji platformy Azure w usłudze Azure SQL Database](sql-database-planned-maintenance.md).

## <a name="network-considerations"></a>Zagadnienia dotyczące sieci

- Upewnij się, że zapora na komputerze hostującym program kliencki zezwala na wychodzącą komunikację TCP na porcie 1433.  Więcej informacji: [Konfigurowanie zapory usługi Azure SQL Database](sql-database-configure-firewall-settings.md).
- Jeśli program kliencki łączy z bazą danych SQL, gdy kliencki jest uruchomiony na maszynie wirtualnej (VM) platformy Azure, musisz otworzyć określone zakresy portów na maszynie Wirtualnej. Więcej informacji: [Porty inne niż 1433 dla platformy ADO.NET 4.5 i usługi SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).
- Połączenia klientów z usługi Azure SQL Database czasami pomijają serwer proxy i bezpośrednią interakcję z bazy danych. Porty inne niż 1433 nabierają znaczenia. Aby uzyskać więcej informacji [architektura łączności usługi Azure SQL Database](sql-database-connectivity-architecture.md) i [portów wyższych niż 1433 dla platformy ADO.NET 4.5 i usługi SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).
- Dla sieci configation dla wystąpienia zarządzanego, zobacz [konfigurację sieci dla wystąpienia zarządzanego](sql-database-howto-managed-instance.md#network-configuration).

## <a name="next-steps"></a>Kolejne kroki

Poznaj wszystkie [możliwości usługi SQL Database](sql-database-technical-overview.md).
