---
title: Aplikacja i obiektów nazw głównych usług w usłudze Azure Active Directory
description: Dowiedz się więcej na temat relacji między aplikacją i obiektów nazw głównych usług w usłudze Azure Active Directory.
documentationcenter: dev-center-name
author: CelesteDG
manager: mtillman
services: active-directory
editor: ''
ms.assetid: adfc0569-dc91-48fe-92c3-b5b4833703de
ms.service: active-directory
ms.subservice: develop
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/24/2018
ms.author: celested
ms.custom: aaddev
ms.reviewer: sureshja
ms.collection: M365-identity-device-management
ms.openlocfilehash: 41eeb4c45e4ef2f04a5e53fde081a2c46093d379
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56186084"
---
# <a name="application-and-service-principal-objects-in-azure-active-directory"></a>Aplikacja i obiektów nazw głównych usług w usłudze Azure Active Directory

Czasami znaczenie "aplikacja" mogą być źle zrozumiane gdy są używane w kontekście usługi Azure Active Directory (Azure AD). Ten artykuł wyjaśnia koncepcyjne i konkretnych aspektów integracji aplikacji usługi Azure AD, przy użyciu ilustrację rejestracji i zgody na [aplikację wielodostępną](developer-glossary.md#multi-tenant-application).

## <a name="overview"></a>Przegląd

Aplikacja, która jest zintegrowana z usługą Azure AD ma skutki, które wykraczają poza aspekt oprogramowania. "Aplikacja" jest często używana jako koncepcyjny termin odwołujące się do nie tylko oprogramowanie aplikacji, ale również jego rejestracji w usłudze Azure AD i rolę w uwierzytelniania/autoryzacji "konwersacji" w czasie wykonywania.

Zgodnie z definicją aplikacja może działać w ramach tych ról:

- [Klient](developer-glossary.md#client-application) roli (Korzystanie z zasobem)
- [Serwer zasobów](developer-glossary.md#resource-server) roli (udostępnianie interfejsów API do klientów)
- Zarówno rola klienta, jak i roli serwera zasobów

[Przepływ OAuth 2.0 autoryzację](developer-glossary.md#authorization-grant) definiuje protokołu konwersacji, który umożliwia klienta lub zasobu dostępu/ochrony zasobów danych, odpowiednio.

W poniższych sekcjach zobaczysz, jak reprezentuje aplikacji w czasie projektowania i środowiska wykonawczego w modelu aplikacji usługi Azure AD.

## <a name="application-registration"></a>Rejestracja aplikacji

Podczas rejestrowania aplikacji usługi Azure AD w [witryny Azure portal][AZURE-Portal], dwa obiekty są tworzone w dzierżawie usługi Azure AD:

- Obiekt aplikacji i
- Obiektu jednostki usługi

### <a name="application-object"></a>Obiekt aplikacji

Aplikację usługi Azure AD jest zdefiniowany przez jego jeden i tylko obiekt aplikacji, w której znajduje się w dzierżawie usługi Azure AD, w którym aplikacja została zarejestrowana, znane jako "głównej" dzierżawy aplikacji. Azure AD Graph [Jednostka aplikacji] [ AAD-Graph-App-Entity] definiuje schemat dla właściwości obiektu aplikacji.

### <a name="service-principal-object"></a>obiektu jednostki usługi

Aby uzyskać dostęp do zasobów, które są zabezpieczone przez dzierżawę usługi Azure AD, jednostka, która wymaga dostępu musi być reprezentowana przez podmiot zabezpieczeń. Ta zasada obowiązuje dla użytkowników (nazwy głównej użytkownika) i aplikacji (nazwy głównej usługi).

Podmiot zabezpieczeń definiuje zasady dostępu i uprawnień dla aplikacji/użytkownika w dzierżawie usługi Azure AD. Dzięki temu podstawowe funkcje, takie jak uwierzytelnianie aplikacji/użytkownika podczas logowania i autoryzacji podczas uzyskiwania dostępu do zasobów.

Kiedy aplikacja otrzymuje uprawnień dostępu do zasobów w dzierżawie (rejestracji lub [zgody](developer-glossary.md#consent)), tworzony jest obiekt nazwy głównej usługi. Azure AD Graph [jednostki ServicePrincipal] [ AAD-Graph-Sp-Entity] definiuje schemat dla właściwości obiektu jednostki usługi firmy.

### <a name="application-and-service-principal-relationship"></a>Aplikacja i relacji jednostki usługi

Należy wziąć pod uwagę obiekt aplikacji jako *globalnego* reprezentację aplikacji na potrzeby wszystkich dzierżaw i jednostki usługi jako *lokalnego* reprezentacji do użycia w określonej dzierżawie.

Służy obiekt aplikacji jako szablonu, z których typowe i domyślne właściwości są *pochodne* podczas tworzenia odpowiednich obiektów nazw głównych usług. Obiekt aplikacji ma związku z tym relacji 1:1 z aplikacji i relacji 1: duży zakres, z odpowiednie obiekty nazwy głównej usługi.

Jednostka usługi musi zostać utworzona w każdej dzierżawy, gdy aplikacja jest używana, dzięki czemu może ustanowić tożsamość dla logowania i/lub dostęp do zasobów, które są chronione przez dzierżawy. Aplikacja jednej dzierżawy ma tylko jedną jednostkę usługi (w jego głównej dzierżawy), utworzone i które wyraził zgodę do użycia podczas rejestracji aplikacji. Wielodostępnych aplikacji/interfejsu API sieci Web ma również nazwę główną usługi utworzone w ramach każdej dzierżawy gdzie użytkownik z tej dzierżawy wyraziła zgodę na jego użycia. 

> [!NOTE]
> Wszelkie zmiany wprowadzone do obiektu aplikacji, również są odzwierciedlane w jego obiektu jednostki usługi w głównej dzierżawy aplikacji tylko (dzierżawy, w którym zarejestrowano). W przypadku aplikacji wielodostępnych zmiany wprowadzone w obiekcie aplikacji nie są odzwierciedlane w żadnych dzierżawców konsumenta obiektów nazw głównych usług, do momentu usunięcia dostęp za pośrednictwem [panelu dostępu do aplikacji](https://myapps.microsoft.com) i ponownie przyznane.
>
> Należy również zauważyć, że natywnych aplikacji są rejestrowane jako wielodostępna domyślnie.

## <a name="example"></a>Przykład

Na poniższym diagramie przedstawiono relację między aplikacji obiektu aplikacji i odpowiedniej usługi obiektów nazw głównych w kontekście przykładowej aplikacji wielodostępnych, nazywany **aplikacji działu KADR**. W tym przykładowym scenariuszu istnieją trzy dzierżaw usługi Azure AD:

- **Adatum** -dzierżawy używane przez firmę, który opracował **aplikacji działu KADR**
- **Contoso** -dzierżawcy stosowaną w organizacji Contoso, czyli konsumenta **aplikacji działu KADR**
- **Firma Fabrikam** -dzierżawy używane przez organizację Fabrikam korzysta również **aplikacji działu KADR**

![Relacja między obiekt aplikacji i obiektu jednostki usługi](./media/app-objects-and-service-principals/application-objects-relationship.png)

W tym przykładowym scenariuszu:

| Krok | Opis |
|------|-------------|
| 1    | To proces tworzenia aplikacji i obiektów nazw głównych usług w głównej dzierżawy aplikacji. |
| 2    | Podczas wyrażania zgody został wykonany przez administratorów Contoso i Fabrikam, obiektu jednostki usługi jest utworzone w ramach dzierżawy usługi Azure AD firmy i przypisane uprawnienia, które udzielane przez administratora. Należy również zauważyć, że aplikacji działu KADR może być skonfigurowane/umożliwia zgody przez użytkowników do użytku osobistego. |
| 3    | Dzierżaw klientów HR aplikacji (Contoso i Fabrikam) każdego ma swoje własne obiektu jednostki usługi. Każda reprezentuje ich użycie wystąpienie aplikacji w czasie wykonywania, podlega uprawnienia wyraził zgodę administrator odpowiednich. |

## <a name="next-steps"></a>Kolejne kroki

- Możesz użyć [programu Azure AD Graph Explorer](https://graphexplorer.azurewebsites.net/) do wykonywania zapytań, aplikacji i obiektów nazw głównych usług.
- Dostęp aplikacji obiektu aplikacji przy użyciu interfejsu API programu Graph usługi Azure AD, [witryny Azure portal] [ AZURE-Portal] edytorze manifestu aplikacji, lub [poleceń cmdlet programu Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), reprezentowane przez jego OData [Jednostka aplikacji][AAD-Graph-App-Entity].
- Dostęp do obiektu jednostki usługi aplikacji za pomocą interfejsu API programu Graph usługi Azure AD lub [poleceń cmdlet programu Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), reprezentowany przez jej OData [jednostki ServicePrincipal] [ AAD-Graph-Sp-Entity].

<!--Image references-->

<!--Reference style links -->
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AZURE-Portal]: https://portal.azure.com
