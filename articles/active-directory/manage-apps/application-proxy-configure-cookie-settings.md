---
title: Ustawienia plików cookie serwera Proxy aplikacji — Azure Active Directory | Dokumentacja firmy Microsoft
description: Azure Active Directory (Azure AD) ma pliki cookie dostępu i sesji do uzyskiwania dostępu do lokalnych aplikacji za pośrednictwem serwera Proxy aplikacji. W tym artykule znajdziesz informacje dotyczące sposobu użycia, a następnie skonfiguruj ustawienia plików cookie.
services: active-directory
author: CelesteDG
manager: mtillman
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.topic: concept
ms.date: 01/16/2019
ms.author: celested
ms.reviewer: japere
ms.collection: M365-identity-device-management
ms.openlocfilehash: c1d97e2542200703201b1c20738581a938ba209e
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56165998"
---
# <a name="cookie-settings-for-accessing-on-premises-applications-in-azure-active-directory"></a>Ustawienia plików cookie na potrzeby uzyskiwania dostępu do aplikacji lokalnych w usłudze Azure Active Directory

Azure Active Directory (Azure AD) ma pliki cookie dostępu i sesji do uzyskiwania dostępu do lokalnych aplikacji za pośrednictwem serwera Proxy aplikacji. Dowiedz się, jak używać ustawienia plików cookie serwera Proxy aplikacji. 

## <a name="what-are-the-cookie-settings"></a>Co to są ustawienia plików cookie?

[Serwer Proxy aplikacji](application-proxy.md) następujące ustawienia pliku cookie dostępu i sesji.

| Ustawienie pliku cookie | Domyślne | Opis | Zalecenia |
| -------------- | ------- | ----------- | --------------- |
| Użyj pliku cookie tylko HTTP | **Nie** | **Tak** umożliwia serwera Proxy aplikacji, które mają zostać objęte flagi HTTPOnly nagłówków odpowiedzi HTTP. Ta flaga zapewnia dodatkowe zabezpieczenia korzyści, na przykład zapobiega po stronie klienta skryptów (CSS) kopiowanie i modyfikowanie plików cookie.<br></br><br></br>Zanim obsługiwane ustawienie tylko do protokołu HTTP, serwer Proxy aplikacji zaszyfrowany i przekazywanych plików cookie za pośrednictwem bezpiecznego kanału SSL do ochrony przed zmianami. | Użyj **tak** ze względu na korzyści dodatkowe zabezpieczenia.<br></br><br></br>Użyj **nie** dla klientów lub agentów użytkownika, które wymagają dostępu do pliku cookie sesji. Na przykład użyć **nie** dla protokołu RDP lub MTSC klienta, który nawiązuje połączenie z serwerem bramy usług pulpitu zdalnego za pośrednictwem serwera Proxy aplikacji.|
| Użyj bezpiecznego pliku cookie | **Nie** | **Tak** umożliwia serwera Proxy aplikacji uwzględnić Zabezpiecz Flaga nagłówków odpowiedzi HTTP. Bezpiecznych plików cookie zwiększa bezpieczeństwo poprzez przekazanie plików cookie za pośrednictwem bezpiecznego kanału TLS, taki jak HTTPS. Zapobiega to pliki cookie z czym muszą być spełnione przez osoby nieupoważnione ze względu na przekazywanie pliku cookie w postaci zwykłego tekstu. | Użyj **tak** ze względu na korzyści dodatkowe zabezpieczenia.|
| Używaj trwałego pliku cookie | **Nie** | **Tak** umożliwia serwera Proxy aplikacji do jej używania plików cookie dostępu nie wygaśnie po zamknięciu przeglądarki sieci web. Trwałość obowiązuje do czasu wygaśnięcia tokenu dostępu lub do momentu ręcznego usunięcia trwały plik cookie przez użytkownika. | Użyj **nie** ze względu na zagrożenie bezpieczeństwa związane z utrzymywaniem użytkowników uwierzytelnionych.<br></br><br></br>Zalecane jest używanie tylko **tak** dla starszych aplikacji, które nie mogą udostępniać pliki cookie między procesami. Zaleca się zaktualizować aplikację w celu obsługi udostępniania plików cookie między procesami, zamiast trwały plik cookie. Na przykład może być konieczne trwały plik cookie, aby umożliwić użytkownikowi otwieranie dokumentów pakietu Office w widoku Eksploratora z witryny programu SharePoint. Bez trwały plik cookie ta operacja może się niepowodzeniem, jeśli pliki cookie dostępu nie są współużytkowane przez przeglądarkę, proces Eksploratora i proces pakietu Office. |

## <a name="set-the-cookie-settings---azure-portal"></a>Ustaw ustawienia plików cookie — witryna Azure portal
Aby skonfigurować ustawienia plików cookie, przy użyciu witryny Azure portal:

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com). 
2. Przejdź do **usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.
3. Wybierz aplikację, dla której chcesz włączyć ustawienie pliku cookie.
4. Kliknij przycisk **serwera Proxy aplikacji**.
5. W obszarze **dodatkowe ustawienia**, ustawienia plików cookie **tak** lub **nie**.
6. Kliknij przycisk **Zapisz** Aby zastosować zmiany. 

<!---

## View current cookie settings - PowerShell

To see the current cookie settings for the application, use this PowerShell command:  

```PowerShell
Get-AzureADApplicationProxyApplication -ObjectId <ObjectId> | fl * 
```

## Set cookie settings - PowerShell

In the following PowerShell commands, ```<ObjectId>``` is the ObjectId of the application. 

**Http-Only Cookie** 

```PowerShell
Set-AzureADApplicationProxyApplication -ObjectId <ObjectId> -IsHttpOnlyCookieEnabled $true 
Set-AzureADApplicationProxyApplication -ObjectId <ObjectId> -IsHttpOnlyCookieEnabled $false 
```

**Secure Cookie**

```PowerShell
Set-AzureADApplicationProxyApplication -ObjectId <ObjectId> -IsSecureCookieEnabled $true 
Set-AzureADApplicationProxyApplication -ObjectId <ObjectId> -IsSecureCookieEnabled $false 
```

**Persistent Cookies**

```PowerShell
Set-AzureADApplicationProxyApplication -ObjectId <ObjectId> -IsPersistentCookieEnabled $true 
Set-AzureADApplicationProxyApplication -ObjectId <ObjectId> -IsPersistentCookieEnabled $false 
```

-->
