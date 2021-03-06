---
title: Omówienie konfiguracji stanu usługi Azure Automation
description: Omówienie programu Azure automatyzacji stanu Configuration (DSC), jego warunki i znane problemy
keywords: PowerShell dsc, konfiguracja żądanego stanu, azure dsc programu powershell
services: automation
ms.service: automation
ms.subservice: dsc
author: bobbytreed
ms.author: robreed
ms.date: 11/06/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: ca7a1913e94242af46e777be308ef92fc5a5abb3
ms.sourcegitcommit: 9999fe6e2400cf734f79e2edd6f96a8adf118d92
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/22/2019
ms.locfileid: "54427070"
---
# <a name="azure-automation-state-configuration-overview"></a>Omówienie konfiguracji stanu usługi Azure Automation

Konfiguracja usługi Azure Automation stanu jest usługą platformy Azure, która pozwala na zapis, zarządzanie i skompilować PowerShell Desired State Configuration (DSC) [konfiguracje](/powershell/dsc/configurations), zaimportuj [zasoby DSC](/powershell/dsc/resources), i Przypisz konfiguracje do węzłów docelowych, wszystko to w chmurze.

## <a name="why-use-azure-automation-state-configuration"></a>Dlaczego warto korzystać z usługi Azure Automation stanu konfiguracji

Konfiguracja stanu usługi Azure Automation oferuje następujące korzyści za pośrednictwem za pomocą DSC spoza platformy Azure.

### <a name="built-in-pull-server"></a>Serwerze ściągania wbudowane

Konfiguracja stanu usługi Azure Automation zapewnia DSC serwera ściągania, podobnie jak [Windows funkcji DSC usługi](/powershell/dsc/pullserver) tak, aby węzły docelowe automatycznie otrzymywać konfiguracje, są zgodne z żądanego stanu i raportować o ich zgodność. Serwerze ściągania wbudowane w usłudze Azure Automation eliminuje potrzebę konfiguracji i utrzymania własnym serwerze ściągania. Usługa Azure Automation mogą określać docelową maszyn wirtualnych lub fizycznych Windows lub Linux, w chmurze lub lokalnie.

### <a name="management-of-all-your-dsc-artifacts"></a>Zarządzanie Twoimi artefaktami DSC

Konfiguracja stanu usługi Azure Automation oferuje tę samą warstwę zarządzania [PowerShell Desired State Configuration](/powershell/dsc/overview) usługa Azure Automation zapewnia skryptów programu PowerShell.

W witrynie Azure portal lub za pomocą programu PowerShell można zarządzać wszystkie usługi DSC konfiguracji, zasobów i węzły docelowe.

![Zrzut ekranu przedstawiający stronę usługi Azure Automation](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a>Importuj dane raportowania w usłudze Log Analytics

Węzły, które są zarządzane za pomocą usługi Azure Automation stan konfiguracji Wyślij szczegółowe dane raportowania stanu na serwerze ściągania wbudowanych. Można skonfigurować konfiguracji stan automatyzacji platformy Azure, aby wysyłać te dane do swojego obszaru roboczego usługi Log Analytics. Aby dowiedzieć się, jak wysyłać dane stanu konfiguracji stanu do obszaru roboczego usługi Log Analytics, zobacz [do przodu usługi Azure Automation konfiguracji stanu raportowania danych do usługi Log Analytics](automation-dsc-diagnostics.md).

## <a name="network-planning"></a>Konfigurowanie sieci

Następujących portów i adresów URL są wymagane dla stanu Configuration (DSC) do komunikacji z usługą Automation:

* Port: Tylko TCP 443 jest wymagany dla wychodzącego dostępu do Internetu.
* Globalny adres URL: *.azure-automation.net
* Globalny adres URL Administracja USA — Wirginia: *.azure-automation.us
* Usługa agenta: https://\<workspaceId\>.agentsvc.azure-automation.net

Zaleca się używania adresów wymienionych podczas definiowania wyjątków. Adresy IP, możesz pobrać [zakresów IP centrum danych Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653). Ten plik jest aktualizowana co tydzień i ma aktualnie wdrożone zakresy i wszystkie nadchodzące zmiany w zakresach adresów IP.

Jeśli masz konto usługi Automation, która jest zdefiniowana dla konkretnego regionu, można ograniczyć komunikację z tym regionalnym centrum danych. Poniższa tabela zawiera rekord DNS dla każdego regionu:

| **Region** | **Rekord DNS** |
| --- | --- |
| Środkowo-zachodnie stany USA | wcus-jobruntimedata-prod-su1.azure-automation.net</br>wcus-agentservice-prod-1.azure-automation.net |
| Środkowo-południowe stany USA |scus-jobruntimedata-prod-su1.azure-automation.net</br>scus-agentservice-prod-1.azure-automation.net |
| Wschodnie stany USA 2 |eus2-jobruntimedata-prod-su1.azure-automation.net</br>eus2-agentservice-prod-1.azure-automation.net |
| Kanada Środkowa |cc-jobruntimedata-prod-su1.azure-automation.net</br>cc-agentservice-prod-1.azure-automation.net |
| Europa Zachodnia |we-jobruntimedata-prod-su1.azure-automation.net</br>we-agentservice-prod-1.azure-automation.net |
| Europa Północna |ne-jobruntimedata-prod-su1.azure-automation.net</br>ne-agentservice-prod-1.azure-automation.net |
| Azja Południowo-Wschodnia |sea-jobruntimedata-prod-su1.azure-automation.net</br>sea-agentservice-prod-1.azure-automation.net|
| Indie Środkowe |cid-jobruntimedata-prod-su1.azure-automation.net</br>cid-agentservice-prod-1.azure-automation.net |
| Japonia Wschodnia |jpe-jobruntimedata-prod-su1.azure-automation.net</br>jpe-agentservice-prod-1.azure-automation.net |
| Australia Południowo-Wschodnia |ase-jobruntimedata-prod-su1.azure-automation.net</br>ase-agentservice-prod-1.azure-automation.net |
| Południowe Zjednoczone Królestwo | uks-jobruntimedata-prod-su1.azure-automation.net</br>uks-agentservice-prod-1.azure-automation.net |
| Administracja USA — Wirginia | usge-jobruntimedata-prod-su1.azure-automation.us<br>usge-agentservice-prod-1.azure-automation.us |

Aby uzyskać listę adresów IP regionu zamiast nazwy regionów, Pobierz [adres IP centrum danych Azure](https://www.microsoft.com/download/details.aspx?id=41653) plik XML z Microsoft Download Center.

> [!NOTE]
> Plik XML adres IP centrum danych platformy Azure zawiera listę zakresów adresów IP, które są używane w centrach danych platformy Microsoft Azure. Plik zawiera zakresy obliczeń, SQL i storage.
>
>Tydzień jest publikowany zaktualizowany plik. Plik odzwierciedla aktualnie wdrożone zakresy i wszystkie nadchodzące zmiany w zakresach adresów IP. Nowe zakresy, które pojawiają się w pliku nie są używane w centrach danych, przez co najmniej jeden tydzień.
>
> To dobry pomysł, aby pobrać nowy plik XML, co tydzień. Następnie należy zaktualizować lokację do prawidłowo identyfikować usługi uruchomione na platformie Azure. Użytkownicy usługi Azure ExpressRoute należy zauważyć, że ten plik jest używany do aktualizacji anonsu protokołu BGP (Border Gateway) miejsca platformy Azure w pierwszym tygodniu każdego miesiąca.

## <a name="introduction-video"></a>Wideo z wprowadzeniem

Wolisz obejrzeć film niż przeczytać artykuł? Poniższy klip wideo z maja 2015 r. podczas konfiguracji stan automatyzacji platformy Azure została po raz pierwszy zapoznaj się z.

> [!NOTE]
> Gdy pojęć i cyklu życia omówione w tym filmie są poprawne, Konfiguracja stanu automatyzacji Azure rozwinęła ponieważ zarejestrowano ten film wideo. Ona jest teraz ogólnie dostępna, jest znacznie bardziej rozległe interfejsu użytkownika w witrynie Azure portal i obsługuje wiele dodatkowych możliwości.

[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a>Kolejne kroki

- Aby rozpocząć pracę, zobacz [wprowadzenie do usługi Azure Automation stanu konfiguracji](automation-dsc-getting-started.md)
- Aby dowiedzieć się, jak dodawanie węzłów, zobacz [dołączanie maszyn w celu zarządzania usługi Azure Automation stanu konfiguracji](automation-dsc-onboarding.md)
- Aby dowiedzieć się więcej na temat kompilowanie konfiguracji DSC, dzięki czemu można je przypisać do węzłów docelowych, zobacz [kompilowanie konfiguracji w konfiguracji stan automatyzacji platformy Azure](automation-dsc-compile.md)
- Dokumentacja poleceń cmdlet programu PowerShell, można zobaczyć [poleceń cmdlet usługi Azure Automation stanu konfiguracji](/powershell/module/azurerm.automation/#automation)
- Aby uzyskać informacje o cenach, zobacz [cennika usługi Azure Automation stanu konfiguracji](https://azure.microsoft.com/pricing/details/automation/)
- Aby wyświetlić przykład użycia usługi Azure Automation stanu konfiguracji w potoku ciągłego wdrażania, zobacz [ciągłe przy użyciu usługi Azure Automation stan konfiguracji wdrożenia i narzędzia Chocolatey](automation-dsc-cd-chocolatey.md)
