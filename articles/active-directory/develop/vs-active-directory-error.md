---
title: Usługa połączona jak diagnozować błędy w usłudze Azure Active Directory
description: Usługa active directory połączone wykryto typ uwierzytelniania niezgodne
services: active-directory
author: ghogen
manager: douge
ms.assetid: dd89ea63-4e45-4da1-9642-645b9309670a
ms.prod: visual-studio-dev15
ms.technology: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 03/12/2018
ms.author: ghogen
ms.custom: aaddev, vs-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8ed328b29c853e5ff75d64332f0228277cff90d4
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56203679"
---
# <a name="diagnosing-errors-with-the-azure-active-directory-connected-service"></a>Diagnozowanie błędów przy użyciu usługi Azure Active Directory połączone

Podczas wykrywania poprzedni kod uwierzytelniania, usługi Azure Active Directory connect serwer wykrył typ uwierzytelniania niezgodne.

Aby prawidłowo wykryć poprzedni kod uwierzytelniania w projekcie, projektu muszą zostać skompilowane.  Jeśli wystąpił błąd i nie ma poprzedniego kodu uwierzytelniania w projekcie, skompiluj i spróbuj ponownie.

## <a name="project-types"></a>Typy projektów

Usługi połączonej sprawdza, czy typ projektu, którą tworzysz, więc jego wstrzyknąć logiki uwierzytelniania prawo do projektu. W przypadku każdego kontrolera, który pochodzi od klasy `ApiController` projektu jest uznawany za projektu interfejsu WebAPI w projekcie. Jeśli istnieją tylko te kontrolery, które wynikają z `MVC.Controller` projektu jest uznawany za projektu MVC w projekcie. Połączone usługi, nie obsługuje innych typów projektów.

## <a name="compatible-authentication-code"></a>Kod uwierzytelniania zgodne

Usługi połączonej wyszukuje również ustawienia uwierzytelniania, które zostały wcześniej skonfigurowane lub są zgodne z usługą. Jeśli wszystkie ustawienia są obecne, jest uznawane za wielobieżnej przypadek, a otworzy usługę połączoną Wyświetl ustawienia.  Jeśli tylko niektóre ustawienia są obecne, jest uznawany za przypadki błędów.

W projekcie MVC usługi połączonej sprawdza, czy dla każdego z następujących ustawień, będące wynikiem z poprzedniego korzystania z usługi:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

Ponadto usługi połączonej sprawdza, czy dla każdego z następujących ustawień w projekcie interfejsu API sieci Web, będące wynikiem z poprzedniego korzystania z usługi:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

## <a name="incompatible-authentication-code"></a>Kod uwierzytelniania niezgodne

Na koniec usługi połączonej próbuje wykryć wersje kodu uwierzytelniania, które zostały skonfigurowane w poprzednich wersjach programu Visual Studio. Jeśli wystąpił ten błąd, oznacza to, że projekt zawiera typ uwierzytelniania niezgodne. Usługi połączonej wykrywa następujące typy uwierzytelniania z poprzednich wersji programu Visual Studio:

* Uwierzytelnianie systemu Windows
* Indywidualne konta użytkowników
* Konta organizacyjne

Do wykrywania uwierzytelniania Windows w projekcie MVC, połączonym szuka `authentication` elementu w swojej `web.config` pliku.

```xml
<configuration>
    <system.web>
        <span style="background-color: yellow"><authentication mode="Windows" /></span>
    </system.web>
</configuration>
```

Aby wykryć uwierzytelniania Windows w projekcie interfejsu API sieci Web, usługi połączonej szuka `IISExpressWindowsAuthentication` elementu w swoim projekcie `.csproj` pliku:

```xml
<Project>
    <PropertyGroup>
        <span style="background-color: yellow"><IISExpressWindowsAuthentication>enabled</IISExpressWindowsAuthentication></span>
    </PropertyGroup>
</Project>
```

Aby wykryć uwierzytelniania indywidualnych kont użytkowników, usługi połączonej szuka elementu pakietu w swojej `packages.config` pliku.

```xml
<packages>
    <span style="background-color: yellow"><package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /></span>
</packages>
```

Aby wykryć starego formularza uwierzytelniania konto organizacyjne, usługi połączonej szuka następujący element w`web.config`:

```xml
<configuration>
    <appSettings>
        <span style="background-color: yellow"><add key="ida:Realm" value="***" /></span>
    </appSettings>
</configuration>
```

Aby zmienić typ uwierzytelniania, Usuń typ uwierzytelniania niezgodne, a następnie spróbuj ponownie dodać podłączoną usługę.

Aby uzyskać więcej informacji, zobacz [scenariusze uwierzytelniania dla usługi Azure AD](authentication-scenarios.md).
