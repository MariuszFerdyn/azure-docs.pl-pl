---
author: msmbaldwin
ms.service: backup
ms.topic: include
ms.date: 01/31/2019
ms.author: mbaldwin
ms.openlocfilehash: 5a4cc3ea822c5613fc7a50b8e370d6846b683721
ms.sourcegitcommit: fea5a47f2fee25f35612ddd583e955c3e8430a95
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/31/2019
ms.locfileid: "55513512"
---
## <a name="preventative"></a>Zapobiegawczych

| Atrybut zabezpieczeń | Tak/Nie | Uwagi |
|---|---|--|
| Szyfrowanie danych magazynowanych:<ul><li>Szyfrowanie po stronie serwera</li><li>Szyfrowanie po stronie serwera za pomocą kluczy zarządzanych przez klienta</li><li>Inne funkcje szyfrowania (na przykład po stronie klienta, są zawsze szyfrowane, itd.)</ul>| Yes | Dzięki szyfrowaniu usługi storage dla kont magazynu. |
| Szyfrowanie podczas przesyłania:<ul><li>Express route szyfrowania</li><li>W przypadku szyfrowania sieci wirtualnej</li><li>Sieć wirtualna-sieć wirtualna szyfrowania</ul>| Nie | Przy użyciu protokołu HTTPS. |
| Obsługa klucza szyfrowania (CMK BYOK, itp.)| Nie |  |
| Szyfrowanie na poziomie kolumny (usługi danych platformy Azure)| Nie |  |
| Wywołania interfejsu API szyfrowane| Yes |  |

## <a name="network-segmentation"></a>Segmentacji sieci

| Atrybut zabezpieczeń | Tak/Nie | Uwagi |
|---|---|--|
| Punkt końcowy usługi pomocy technicznej| Nie |  |
| Obsługa iniekcji sieci wirtualnej| Nie |  |
| Izolacja sieci / Zapora pomocy technicznej| Yes | Wymuszanie tunelowania jest obsługiwana dla kopii zapasowych maszyn wirtualnych. Wymuszone tunelowanie nie jest obsługiwana w przypadku obciążeń uruchomionych maszyn wirtualnych. |
| Obsługa wymuszonego tunelowania | Nie |  |

## <a name="detection"></a>Wykrywanie

| Atrybut zabezpieczeń | Tak/Nie | Uwagi|
|---|---|--|
| Obsługiwane (usługi Log analytics, usługi App insights itp.) do monitorowania platformy Azure| Yes | Usługa log Analytics jest świadczona za pośrednictwem dzienników diagnostycznych. Monitorowanie usługi Azure Backup chroniony obciążeń przy użyciu usługi Log Analytics (https://azure.microsoft.com/blog/monitor-all-azure-backup-protected-workloads-using-log-analytics/) Aby uzyskać więcej informacji. |

## <a name="iam-support"></a>Obsługa zarządzania tożsamościami i Dostępem

| Atrybut zabezpieczeń | Tak/Nie | Uwagi|
|---|---|--|
| Zarządzanie dostępem — uwierzytelnianie| Yes | Uwierzytelnianie jest za pomocą usługi Azure Active Directory. |
| Zarządzanie dostępem - autoryzacji| Yes | Klient utworzył i wbudowane role kontroli RBAC są używane. Zobacz Use Role-Based kontrola dostępu do zarządzania punkty odzyskiwania usługi Azure Backup (https://docs.microsoft.com/azure/backup/backup-rbac-rs-vault) Aby uzyskać więcej informacji. |


## <a name="audit-trail"></a>Dziennik inspekcji

| Atrybut zabezpieczeń | Tak/Nie | Uwagi|
|---|---|--|
| Zarządzania kontrolą/Plan rejestrowania i inspekcji| Yes | Dzienniki aktywności są rejestrowane wszystkie akcje klienta wyzwalane w witrynie Azure portal. |
| Rejestrowanie i inspekcja na płaszczyźnie danych| Nie | Płaszczyzna danych w usłudze Azure Backup nie można nawiązać połączenia z bezpośrednio.  |

## <a name="configuration-management"></a>Zarządzanie konfiguracją

| Atrybut zabezpieczeń | Tak/Nie | Uwagi|
|---|---|--|
| Obsługa zarządzania konfiguracji (przechowywanie wersji konfiguracji itp.)| Yes|  |