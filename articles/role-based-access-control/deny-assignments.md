---
title: Zrozumienie Odmów przydziały dla zasobów platformy Azure | Dokumentacja firmy Microsoft
description: Dowiedz się więcej o Odmów przypisania kontroli dostępu opartej na rolach (RBAC) dla zasobów platformy Azure.
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.assetid: ''
ms.service: role-based-access-control
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/30/2018
ms.author: rolyon
ms.reviewer: bagovind
ms.custom: ''
ms.openlocfilehash: 53716fa343df25026dcc668ed8483673d934d1ad
ms.sourcegitcommit: fcb674cc4e43ac5e4583e0098d06af7b398bd9a9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/18/2019
ms.locfileid: "56339128"
---
# <a name="understand-deny-assignments-for-azure-resources"></a>Zrozumienie Odmów przydziały dla zasobów platformy Azure

Podobnie jak w przypadku przypisania roli *Odmów przypisania* dołącza zbiór akcje odmowy zawsze do użytkownika, grupy lub jednostki usługi w określonym zakresie na potrzeby odmowa dostępu. Odmowa przypisania Zablokuj użytkownikom możliwość wykonywania akcji na określony zasób platformy Azure, nawet wtedy, gdy przypisanie roli przyznaje im dostęp. Niektórych zasobów, które obejmują teraz dostawców na platformie Azure odmówić przypisania. Obecnie Odmów przypisania **tylko do odczytu** i może zostać ustawiona tylko przez firmę Microsoft.

Pod pewnymi względami Odmów przypisania są inne niż przypisań ról. Odmowa przypisania można wykluczyć podmiotów zabezpieczeń i zapobiegać dziedziczeniu na zakresy podrzędne. Odmów dotyczą również przypisania [klasyczny administrator subskrypcji](rbac-and-directory-admin-roles.md) przypisania.

W tym artykule opisano sposób Odmów przypisania są zdefiniowane.

## <a name="deny-assignment-properties"></a>Odmów przypisania właściwości

 Przypisanie Odmów ma następujące właściwości:

> [!div class="mx-tableFixed"]
> | Właściwość | Wymagane | Typ | Opis |
> | --- | --- | --- | --- |
> | `DenyAssignmentName` | Yes | String | Nazwa wyświetlana przypisania Odmów. Nazwy muszą być unikatowe dla danego zakresu. |
> | `Description` | Nie | String | Opis przypisania Odmów. |
> | `Permissions.Actions` | Co najmniej jednej akcji lub jednego elementy DataActions | Ciąg] | Tablica ciągów, które określają operacje zarządzania, do których przypisanie Odmów blokuje dostęp. |
> | `Permissions.NotActions` | Nie | Ciąg] | Tablica ciągów, które określają operacje zarządzania, aby wykluczyć z przypisania Odmów. |
> | `Permissions.DataActions` | Co najmniej jednej akcji lub jednego elementy DataActions | Ciąg] | Tablica ciągów, które określają operacje danych, do których przypisanie Odmów blokuje dostęp. |
> | `Permissions.NotDataActions` | Nie | Ciąg] | Tablica ciągów, które określają operacje na danych, aby wykluczyć z przypisania Odmów. |
> | `Scope` | Nie | String | Ciąg, który określa zakres, który dotyczy przypisania Odmów. |
> | `DoNotApplyToChildScopes` | Nie | Wartość logiczna | Określa, czy przypisanie odmowy mają zastosowanie do zakresy podrzędne. Wartość domyślna to false. |
> | `Principals[i].Id` | Yes | Ciąg] | Tablica obiektów nazwy głównej usługi Azure AD identyfikatorów (użytkownika, grupy, jednostkę usługi lub tożsamość zarządzana), do których zostanie zastosowana przypisania Odmów. Ustaw na pustym identyfikatorem GUID `00000000-0000-0000-0000-000000000000` do reprezentowania wszystkich podmiotów zabezpieczeń. |
> | `Principals[i].Type` | Nie | Ciąg] | Tablica typów obiektów, reprezentowane przez jednostki [i] .id. Ustaw `SystemDefined` do reprezentowania wszystkich podmiotów zabezpieczeń. |
> | `ExcludePrincipals[i].Id` | Nie | Ciąg] | Tablica obiektów nazwy głównej usługi Azure AD identyfikatorów (użytkownika, grupy, jednostkę usługi lub tożsamość zarządzana), do których przypisanie Odmów nie ma zastosowania. |
> | `ExcludePrincipals[i].Type` | Nie | Ciąg] | Tablica typów obiektów, reprezentowane przez .id ExcludePrincipals [i]. |
> | `IsSystemProtected` | Nie | Wartość logiczna | Określa, czy odmówić przypisania został utworzony przez platformę Azure i nie można edytować ani usunąć. Obecnie wszystkie Odmów przypisania są chronione systemu. |

## <a name="system-defined-principal"></a>Jednostki zdefiniowaną przez system

Do obsługi odmowy przypisania, **System-Defined jednostki** zostały wprowadzone. Ten podmiot zabezpieczeń reprezentuje wszystkich użytkowników, grup, nazw głównych usług i zarządzanych tożsamości w katalogu usługi Azure AD. Jeśli identyfikator podmiotu zabezpieczeń jest zerowy identyfikator GUID `00000000-0000-0000-0000-000000000000` i typ podmiotu zabezpieczeń jest `SystemDefined`, podmiot zabezpieczeń reprezentuje wszystkie podmioty zabezpieczeń. `SystemDefined` może być łączone z `ExcludePrincipals` odrzucanie wszystkich podmiotów zabezpieczeń, z wyjątkiem niektórych użytkowników. `SystemDefined` ma następujące ograniczenia:

- Może być używana tylko w `Principals` i nie może być używany w `ExcludePrincipals`.
- `Principals[i].Type` musi być równa `SystemDefined`.

## <a name="next-steps"></a>Kolejne kroki

* [Lista Odmów przydziały dla zasobów platformy Azure przy użyciu interfejsu API REST](deny-assignments-rest.md)
* [Zrozumienie definicje ról na potrzeby zasobów platformy Azure](role-definitions.md)
