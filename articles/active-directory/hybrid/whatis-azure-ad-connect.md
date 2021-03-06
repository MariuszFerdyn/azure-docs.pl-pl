---
title: Co to są programy Azure AD Connect i Connect Health | Microsoft Docs
description: Opisuje narzędzia używane do synchronizowania i monitorowania środowiska lokalnego w usłudze Azure AD.
services: active-directory
author: billmath
manager: daveba
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 01/30/2019
ms.subservice: hybrid
ms.author: billmath
ms.collection: M365-identity-device-management
ms.openlocfilehash: d364421794452f8ccf95a60ec86a161934c87528
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56167987"
---
# <a name="what-is-azure-ad-connect"></a>Co to jest program Azure AD Connect?

Azure AD Connect to narzędzie firmy Microsoft, które umożliwia spełnienie wymagań związanych z tożsamością hybrydową.  Oferuje ono następujące funkcje:
    
- [Synchronizacja skrótów haseł](whatis-phs.md) — metoda logowania, która umożliwia synchronizowanie skrótów haseł lokalnych użytkowników usługi AD w usłudze Azure AD.
- [Uwierzytelnianie przekazywane](how-to-connect-pta.md) — metoda logowania, która pozwala użytkownikom używać tego samego hasła w infrastrukturze lokalnej i w chmurze, ale nie wymaga dodatkowej infrastruktury w środowisku federacyjnym.
- [Integracja federacyjna](how-to-connect-fed-whatis.md) — usługi federacyjne to opcjonalny składnik programu Azure AD Connect, za pomocą którego można skonfigurować środowisko hybrydowe przy użyciu lokalnej infrastruktury usług AD FS. Składnik ten udostępnia również funkcje zarządzania usługami AD FS, takie jak odnawianie certyfikatów i dodatkowe wdrożenia serwera usług AD FS.
- [Synchronizacja](how-to-connect-sync-whatis.md) — odpowiada za tworzenie użytkowników, grup i innych obiektów.  Odpowiada też za zapewnienie zgodności informacji o tożsamości lokalnych użytkowników i grup z informacjami w chmurze.  Synchronizacja dotyczy również skrótów haseł.
-   [Monitorowanie kondycji](whatis-hybrid-identity-health.md) — składnik Azure AD Connect Health zapewnia zaawansowane monitorowanie z możliwością wyświetlania aktywności w centralnej lokalizacji w witrynie Azure Portal. 


![Co to jest program Azure AD Connect](./media/whatis-hybrid-identity/arch.png)



## <a name="what-is-azure-ad-connect-health"></a>Co to jest program Azure AD Connect Health?

Program Azure Active Directory (Azure AD) Connect Health zapewnia niezawodne monitorowanie lokalnej infrastruktury do obsługi tożsamości. Umożliwia utrzymywanie niezawodnego połączenia z usługami Office 365 i Microsoft Online Services.  Ta niezawodność wynika z dodania funkcji monitorowania kluczowych składników tożsamości. Zapewnia także łatwy dostęp do kluczowych punktów danych dotyczących tych składników.

Informacje są prezentowane w [portalu programu Azure AD Connect Health](https://aka.ms/aadconnecthealth). Korzystając z portalu programu Azure AD Connect Health, możesz wyświetlać alerty, wyniki monitorowania wydajności, analizy użycia i inne informacje. Program Azure AD Connect Health pokazuje kondycję kluczowych składników tożsamości w jednym miejscu.

![Co to jest program Azure AD Connect Health](./media/whatis-hybrid-identity-health/aadconnecthealth2.png)

## <a name="why-use-azure-ad-connect"></a>Dlaczego warto korzystać z programu Azure AD Connect?
Zintegrowanie katalogów lokalnych z usługą Azure AD zwiększa produktywność użytkowników, zapewniając wspólną tożsamość na potrzeby dostępu do zasobów, zarówno lokalnych, jak i w chmurze. Użytkownicy i organizacje uzyskują następujące korzyści:

* Użytkownicy mogą korzystać z jednej tożsamości w celu uzyskiwania dostępu do aplikacji lokalnych oraz usług w chmurze, takich jak Office 365.
* Jedno narzędzie zapewniające łatwe w użyciu środowisko wdrażania na potrzeby synchronizacji i logowania.
* Najnowsze możliwości we wszystkich scenariuszach. Program Azure AD Connect zastępuje starsze wersje narzędzi do integracji tożsamości, takie jak DirSync i Azure AD Sync. Aby uzyskać więcej informacji, zobacz [Porównanie narzędzi do integracji katalogów tożsamości hybrydowej](plan-hybrid-identity-design-considerations-tools-comparison.md).

## <a name="why-use-azure-ad-connect-health"></a>Dlaczego warto korzystać z programu Azure AD Connect Health?
Usługa Azure AD zwiększa produktywność użytkowników, zapewniając wspólną tożsamość na potrzeby dostępu do zasobów — zarówno lokalnych, jak i w chmurze. Zagwarantowanie niezawodnego środowiska umożliwiającego użytkownikom uzyskanie dostępu do zasobów staje się wyzwaniem.  Program Azure AD Connect Health pomaga monitorować i uzyskiwać informacje o lokalnej infrastrukturze do obsługi tożsamości, dzięki czemu gwarantuje niezawodność środowiska. Wymaga to jedynie zainstalowania agenta na każdym z lokalnych serwerów tożsamości.

Program Azure AD Connect Health dla usług AD FS obsługuje usługi AD FS 2.0 w systemach Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 i Windows Server 2016. Obsługuje także monitorowanie serwerów proxy usług AD FS lub serwerów proxy aplikacji internetowej, które zapewniają obsługę uwierzytelniania w przypadku dostępu do ekstranetu. Dzięki prostej i szybkiej instalacji agenta kondycji program Azure AD Connect Health dla usług AD FS oferuje zestaw kluczowych funkcji.

Kluczowe korzyści i najlepsze rozwiązania:

|Najważniejsze korzyści|Najlepsze rozwiązania|
|-----|-----|
|Ulepszone zabezpieczenia|[Trendy związane z blokadą ekstranetu](how-to-connect-health-adfs.md#usage-analytics-for-ad-fs)</br>[Raport dotyczący nieudanych logowań](how-to-connect-health-adfs.md#risky-ip-report-public-preview)</br>[W zachowania zgodności](reference-connect-health-user-privacy.md)|
|Po otrzymaniu na [wszystkie krytyczne problemy z systemem usług AD FS](how-to-connect-health-alert-catalog.md#alerts-for-active-directory-federation-services)|Konfiguracja i dostępność serwera</br>[Wydajność i łączność](how-to-connect-health-adfs.md#performance-monitoring-for-ad-fs)</br>Regularna konserwacja|
|Łatwe uruchamianie i zarządzanie|[Instalacja agenta szybki](how-to-connect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-fs)</br>Automatyczne uaktualnianie agenta do najnowszej wersji</br>Dane dostępne w portalu w ciągu kilku minut|
Rozbudowane [metryki użycia](how-to-connect-health-adfs.md#usage-analytics-for-ad-fs)|Lista najczęściej używanych aplikacji</br>Lokalizacje sieciowe i połączenia TCP</br>Żądania tokenów dla pojedynczych serwerów|
|Doskonałe środowisko użytkownika|Interfejs podobny do pulpitu nawigacyjnego z witryny Azure Portal</br>[Alerty w wiadomościach e-mail](how-to-connect-health-adfs.md#alerts-for-ad-fs)|




## <a name="next-steps"></a>Kolejne kroki

- [Sprzęt i wymagania wstępne](how-to-connect-install-prerequisites.md) 
- [Ustawienia ekspresowe](how-to-connect-install-express.md)
- [Ustawienia dostosowane](how-to-connect-install-custom.md)
- [Instalowanie agentów programu Azure AD Connect Health](how-to-connect-health-agent-install.md) 
