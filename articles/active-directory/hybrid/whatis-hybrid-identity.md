---
title: Łączenie usługi Active Directory z usługą Azure Active Directory. | Microsoft Docs
description: Program Azure AD Connect umożliwia integrowanie katalogów lokalnych z usługą Azure Active Directory. Dzięki temu można posługiwać się wspólną tożsamością dla usługi Office 365, platformy Azure i aplikacji SaaS zintegrowanych z usługą Azure AD.
keywords: wprowadzenie do programu Azure AD Connect, omówienie programu Azure AD Connect, co to jest program Azure AD Connect, instalowanie usługi Active Directory
services: active-directory
author: billmath
manager: daveba
ms.assetid: 59bd209e-30d7-4a89-ae7a-e415969825ea
ms.service: active-directory
ms.workload: identity
ms.topic: overview
ms.date: 11/28/2018
ms.subservice: hybrid
ms.author: billmath
ms.openlocfilehash: fc18353ff89f8613847c977066e51620fb3e834f
ms.sourcegitcommit: 5978d82c619762ac05b19668379a37a40ba5755b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/31/2019
ms.locfileid: "55494668"
---
# <a name="what-is-hybrid-identity"></a>Co to jest tożsamość hybrydowa? 

Obecnie małe i duże firmy w coraz większym stopniu korzystają zarówno z aplikacji lokalnych, jak i aplikacji w chmurze.  Użytkownicy wymagają dostępu do aplikacji zarówno lokalnie, jak i w chmurze. To wymaganie stało się wyzwaniem. 

Rozwiązania firmy Microsoft do obsługi tożsamości obejmują zarówno funkcje lokalne, jak i chmurowe.  Te rozwiązania tworzą wspólną tożsamość użytkownika na potrzeby uwierzytelniania i autoryzacji w kontekście wszystkich zasobów, niezależnie od lokalizacji. Nazywamy to **tożsamością hybrydową**.

Aby uzyskać tożsamość hybrydową, można użyć jednej z trzech metoda uwierzytelniania, w zależności od scenariusza.   Te trzy metody to: 

- **[Synchronizacja skrótów haseł](whatis-phs.md)**  
- **[Uwierzytelnianie przekazywane](how-to-connect-pta.md)**  
- **[Federacja](whatis-fed.md)** 

Te metody uwierzytelniania oferują również funkcję [logowania jednokrotnego](how-to-connect-sso.md).  Logowanie jednokrotne umożliwia automatyczne logowanie użytkowników, gdy ich urządzenia firmowe są połączone z siecią firmową.

Aby uzyskać więcej informacji, zobacz [Choose the right authentication method for your Azure Active Directory hybrid identity solution (Wybieranie właściwej metody uwierzytelniania w przypadku rozwiązania hybrydowego do obsługi tożsamości w usłudze Azure Active Directory)](https://docs.microsoft.com/azure/security/azure-ad-choose-authn). 

## <a name="common-scenarios-and-recommendations"></a>Typowe scenariusze i zalecenia 

Poniżej przedstawiono kilka typowych scenariuszy związanych z tożsamościami hybrydowymi i zarządzaniem dostępem wraz z zaleceniami co do tego, która opcja (lub opcje) obsługi tożsamości hybrydowych może być najbardziej odpowiednia w danym przypadku. 

|Wymagana funkcjonalność:|PHS i SSO<sup>1</sup>| PTA i SSO<sup>2</sup> | AD FS<sup>3</sup>| 
|-----|-----|-----|-----| 
|Automatyczne synchronizowanie z chmurą nowych kont użytkowników, kontaktów i grup utworzonych w lokalnej usłudze Active Directory.|![Zalecane](./media/whatis-hybrid-identity/ic195031.png)| ![Zalecane](./media/whatis-hybrid-identity/ic195031.png) |![Zalecane](./media/whatis-hybrid-identity/ic195031.png)| 
|Konfigurowanie dzierżawy na potrzeby scenariuszy hybrydowych usługi Office 365.|![Zalecane](./media/whatis-hybrid-identity/ic195031.png)| ![Zalecane](./media/whatis-hybrid-identity/ic195031.png) |![Zalecane](./media/whatis-hybrid-identity/ic195031.png)| 
|Umożliwienie użytkownikom logowania się i uzyskiwania dostępu do usług w chmurze przy użyciu swojego lokalnego hasła.|![Zalecane](./media/whatis-hybrid-identity/ic195031.png)| ![Zalecane](./media/whatis-hybrid-identity/ic195031.png) |![Zalecane](./media/whatis-hybrid-identity/ic195031.png)| 
|Zaimplementowanie logowania jednokrotnego przy użyciu poświadczeń firmowych.|![Zalecane](./media/whatis-hybrid-identity/ic195031.png)| ![Zalecane](./media/whatis-hybrid-identity/ic195031.png) |![Zalecane](./media/whatis-hybrid-identity/ic195031.png)|  
|Zagwarantowanie, że żadne skróty haseł nie będą przechowywane w chmurze.| |![Zalecane](./media/whatis-hybrid-identity/ic195031.png)|![Zalecane](./media/whatis-hybrid-identity/ic195031.png)| 
|Umożliwienie działania rozwiązań obsługujących uwierzytelnianie wieloskładnikowe w chmurze.| |![Zalecane](./media/whatis-hybrid-identity/ic195031.png)|![Zalecane](./media/whatis-hybrid-identity/ic195031.png)| 
|Umożliwienie działania rozwiązań obsługujących lokalne uwierzytelnianie wieloskładnikowe.| | |![Zalecane](./media/whatis-hybrid-identity/ic195031.png)| 
|Obsługa uwierzytelniania użytkowników za pomocą kart inteligentnych<sup>4</sup>| | |![Zalecane](./media/whatis-hybrid-identity/ic195031.png)| 
|Wyświetlanie powiadomień dotyczących wygasania haseł w portalu pakietu Office i na pulpicie systemu Windows 10.| | |![Zalecane](./media/whatis-hybrid-identity/ic195031.png)| 

> <sup>1</sup> Synchronizacja skrótów haseł za pomocą logowania jednokrotnego. 
> 
> <sup>2</sup> Uwierzytelnianie przekazywane i logowanie jednokrotne.  
> 
> <sup>3</sup> Federacyjne logowanie jednokrotne z użyciem usług AD FS.  
>  
> <sup>4</sup> Usługi AD FS można zintegrować z infrastrukturą kluczy publicznych przedsiębiorstwa, aby umożliwić logowanie przy użyciu certyfikatów. Mogą to być certyfikaty programowe wdrażane za pośrednictwem zaufanych kanałów aprowizowania, takich jak zarządzanie danymi głównymi lub obiekt zasad grupy, lub certyfikaty na kartach inteligentnych (w tym na kartach PIV/CAC) albo w usłudze Hello dla firm (zaufanie certyfikatu). Aby uzyskać więcej informacji na temat obsługi uwierzytelniania za pomocą kart inteligentnych, zobacz [ten blog](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/). 
> 

## <a name="next-steps"></a>Następne kroki 

- [Co to są programy Azure AD Connect i Connect Health?](whatis-azure-ad-connect.md) 
- [Co to jest synchronizacja skrótów haseł?](whatis-phs.md) 
- [Co to jest uwierzytelnianie przekazywane?](how-to-connect-pta.md) 
- [Co to jest federacja?](whatis-fed.md) 
- [Co to jest logowanie jednokrotne?](how-to-connect-sso.md) 

