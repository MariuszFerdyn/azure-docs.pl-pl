---
title: Funkcje i platformach obsługiwanych przez usługę Azure Security Center | Dokumentacja firmy Microsoft
description: Ten dokument zawiera listę funkcji i platformach obsługiwanych przez usługę Azure Security Center.
services: security-center
documentationcenter: na
author: rkarlin
manager: barbkess
editor: ''
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 1/9/2019
ms.author: rkarlin
ms.openlocfilehash: 5422ba1b29ac48a7255f25ac0beb43e3481d256a
ms.sourcegitcommit: fec0e51a3af74b428d5cc23b6d0835ed0ac1e4d8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/12/2019
ms.locfileid: "56105896"
---
# <a name="platforms-and-features-supported-by-azure-security-center"></a>Platformy i funkcji obsługiwanych przez usługę Azure Security Center

Monitorowanie stanu zabezpieczeń i zalecenia są dostępne dla maszyn wirtualnych (VM) utworzonych przy użyciu zarówno klasyczny i modelem wdrażania usługi Resource Manager i komputery.

> [!NOTE]
> Dowiedz się więcej o [klasycznej sieci wirtualnej i modelem wdrażania usługi Resource Manager](../azure-classic-rm.md) dla zasobów platformy Azure.
>
>

## <a name="platforms-that-support-the-data-collection-agent"></a>Temat platform obsługujących agent zbierania danych 

W tej sekcji przedstawiono platform, na których można uruchomić agenta usługi Azure Security Center i z którego mógł zbierać dane.

### <a name="supported-platforms-for-windows-computers-and-vms"></a>Obsługiwane platformy dla maszyn wirtualnych i komputerów Windows
Obsługiwane są następujące systemy operacyjne Windows:

* Windows Server 2008
* Windows Server 2008 R2
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

> [!NOTE]
> Integracja z usługą Windows Defender ATP obsługuje tylko systemu Windows Server 2012 R2 i Windows Server 2016.
>
>

### <a name="supported-platforms-for-linux-computers-and-vms"></a>Obsługiwane platformy dla maszyn wirtualnych i komputerów z systemem Linux
Obsługiwane są następujące systemy operacyjne Linux:

* Wersje Ubuntu 12.04 LTS, 14.04 LTS i 16.04 LTS.
* Wersje debian 6, 7, 8 i 9.
* CentOS w wersji 5, 6 i 7.
* Wersje Red Hat Enterprise Linux (RHEL), 5, 6 i 7.
* SUSE Linux Enterprise Server (SLES) w wersji 11 i 12.
* Wersje systemu Linux Oracle, 5, 6 i 7.
* Linux Amazon 2012.09 2017 r.
* OpenSSL 1.1.0 jest obsługiwana tylko na platformach x86_64, 64-bitowych.

## <a name="vms-and-cloud-services"></a>Maszyny wirtualne i usługi w chmurze
Obsługiwane są również maszyny wirtualne, które są uruchamiane w usłudze w chmurze. Monitorowane są tylko usługi sieci web i proces roboczy role w chmurze działających w miejsce produkcyjne. Aby dowiedzieć się więcej o usługach cloud services, zobacz [Omówienie usługi Azure Cloud Services](../cloud-services/cloud-services-choose-me.md).


## <a name="supported-iaas-features"></a>Obsługiwane funkcje IaaS

> [!div class="mx-tableFixed"]
> 

|Serwer|Windows||Linux||
|----|----|----|----|----|
|Środowisko|Azure|Poza platformą Azure|Azure|Poza platformą Azure|
|Alerty wykrywania zagrożeń VMBA|✔|✔|✔ (w obsługiwanych wersjach)|✔|
|Alerty wykrywania zagrożeń opartego na sieci|✔|X|✔|X|
|Integracja usługi Windows Defender ATP|✔ (w obsługiwanych wersjach)|✔|X|X|
|Brakujące poprawki|✔|✔|✔|✔|
|Konfiguracje zabezpieczeń|✔|✔|✔|✔|
|Ochrona punktów końcowych|✔|✔|X|X|
|Dostęp JIT do maszyny wirtualnej|✔|X|✔|X|
|Funkcje adaptacyjnego sterowania aplikacjami|✔|X|X|X|
|USŁUGI FIM|✔|✔|✔|✔|
|Szyfrowanie dysków|✔|X|✔|X|
|Wdrożenie innych firm|✔|X|✔|X|
|Sieciowe grupy zabezpieczeń|✔|X|✔|X|
|Wykrywanie zagrożeń fileless|✔|✔|X|X|
|Mapa sieci|✔|X|✔|X|
|Kontrolki adaptacyjne sieci|✔|X|✔|X|


### <a name="supported-endpoint-protection-solutions"></a>Rozwiązań ochrony obsługiwanych punktów końcowych

Poniższa tabela zawiera macierz:
 - Czy można użyć usługi Azure Security Center na instalowanie poszczególnych rozwiązań.
 - Można wykryć, które Centrum zabezpieczeń rozwiązania ochrony punktu końcowego. Jeśli jeden z tych rozwiązań do ochrony punktu końcowego zostanie wykryta, usługa Security Center będzie nie zaleca się zainstalowanie jednego.

| Ochrona punktów końcowych| Platformy | Instalacja usługi Security Center | Odnajdywanie usługi Security Center |
|------|------|-----|-----|
| Windows Defender (oprogramowanie firmy Microsoft chroniące przed złośliwym kodem)| Windows Server 2016| Nie, wbudowana w system operacyjny| Yes |
| System Center Endpoint Protection (oprogramowanie firmy Microsoft chroniące przed złośliwym kodem) | Windows Server 2012 R2, 2012, 2008 R2 (zobacz uwaga poniżej) | Za pomocą rozszerzenia | Yes |
| Trend Micro — wszystkie wersje | Rodzina systemów Windows Server  | Nie | Yes |
| Symantec — w wersji co najmniej 12.1.1100| Rodzina systemów Windows Server  | Nie | Yes |
| McAfee — w wersji co najmniej 10 | Rodzina systemów Windows Server  | Nie | Yes |
| Kaspersky| Rodzina systemów Windows Server  | Nie | Nie  |
| Sophos| Rodzina systemów Windows Server  | Nie | Nie  |

> [!NOTE]
> - Wykrywanie programu System Center Endpoint Protection (SCEP) na maszynie wirtualnej systemu Windows Server 2008 R2 wymaga protokołu SCEP do zainstalowania programu PowerShell 3.0 (lub górną wersji).
>
>

## <a name="supported-paas-features"></a>Obsługiwane funkcje PaaS 


|Usługa|Zalecenia|Wykrywanie zagrożeń|
|----|----|----|
|SQL|✔| ✔|
|PostGreSQL*|✔| ✔|
|MySQL*|✔| ✔|
|Usługa Azure Blob storage konta *|✔| ✔|
|Usługi aplikacji|✔| ✔|
|Cloud Services|✔| X|
|Sieci wirtualne|✔| Nie dotyczy|
|Podsieci|✔| Nie dotyczy|
|Karty interfejsów sieciowych|✔| ✔|
|Sieciowe grupy zabezpieczeń|✔| Nie dotyczy|
|Subskrypcja|✔| ✔|

\* Te funkcje są obecnie obsługiwane w publicznej wersji zapoznawczej. 



## <a name="next-steps"></a>Kolejne kroki

- Dowiedz się, jak [planowania i zagadnień projektowych podczas wdrażania usługi Azure Security Center](security-center-planning-and-operations-guide.md).
- Dowiedz się więcej o [analiza zachowania maszyny wirtualnej i awaryjnego zrzutu pamięci analizy w usłudze Security Center](security-center-alerts-type.md#virtual-machine-behavioral-analysis).
- Znajdź [często zadawane pytania dotyczące korzystania z usługi Azure Security Center](security-center-faq.md).
- Znajdź [wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności](https://blogs.msdn.com/b/azuresecurity/).
