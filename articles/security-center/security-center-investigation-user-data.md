---
title: Zarządzanie danymi użytkownika w Centrum zabezpieczeń Azure badanie | Dokumentacja firmy Microsoft
description: " Dowiedz się, jak zarządzać danymi użytkownika w funkcji badania w usłudze Azure Security Center. "
services: operations-management-suite
documentationcenter: na
author: rkarlin
manager: barbkess
editor: ''
ms.assetid: 411d7bae-c9d4-4e83-be63-9f2f2312b075
ms.service: operations-management-suite
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/20/2018
ms.author: rkarlin
ms.openlocfilehash: 81bd34cdbe35f3e12d5afddc929b0fac7631f4cc
ms.sourcegitcommit: fec0e51a3af74b428d5cc23b6d0835ed0ac1e4d8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/12/2019
ms.locfileid: "56113077"
---
# <a name="manage-user-data-found-in-an-azure-security-center-investigation"></a>Zarządzanie danymi użytkownika w Centrum zabezpieczeń Azure badanie
Ten artykuł zawiera informacje na temat sposobu zarządzania danymi użytkownika w funkcji badania w usłudze Azure Security Center. Badanie dane są przechowywane w [usługi Azure Log Analytics](../log-analytics/log-analytics-overview.md) i widoczne w usłudze Security Center. Zarządzanie danymi użytkowników obejmuje możliwość usunięcia lub eksportowanie danych.

[!INCLUDE [gdpr-intro-sentence.md](../../includes/gdpr-intro-sentence.md)]

## <a name="searching-for-and-identifying-personal-data"></a>Wyszukiwanie i identyfikowanie danych osobowych
W witrynie Azure portal, można użyć Centrum zabezpieczeń [funkcji badania](../security-center/security-center-investigation.md) do wyszukiwania danych osobowych. Funkcja badanie jest dostępna w ramach **alerty zabezpieczeń**.

Funkcja badanie pokazuje wszystkie jednostki, informacje o użytkownikach i danych w ramach **jednostek** kartę.

## <a name="securing-and-controlling-access-to-personal-information"></a>Zabezpieczanie i kontrolowanie dostępu do danych osobowych
Użytkownika usługa Security Center przypisaną rolę Czytelnik, właściciela, współautora lub administratora konta mają dostęp do danych klienta w narzędziu.

Zobacz [wbudowane role kontroli dostępu opartej na rolach na platformie Azure](../role-based-access-control/built-in-roles.md) Aby dowiedzieć się więcej o rolach czytnika, właściciel i współautor. Zobacz [Administratorzy subskrypcji platformy Azure](../billing/billing-add-change-azure-subscription-administrator.md) dowiedzieć się więcej o rolach administratora konta.

## <a name="deleting-personal-data"></a>Usuwanie danych osobowych
Użytkownik usługi Security Center przypisaną rolę właściciela, współautora, lub Administrator konta może usunąć informacji badania.

Aby usunąć dochodzenia, możesz przesłać `DELETE` żądania interfejsu API REST usługi Azure Resource Manager:

```HTTP
DELETE
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.OperationalInsights/workspaces/{workspaceName}/features/security/incidents/{incidentName}
```

`incidentName` Danych wejściowych można znaleźć, wyświetlając listę wszystkich zdarzeń za pomocą `GET` żądania:

```HTTP
GET
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.OperationalInsights/workspaces/{workspaceName}/features/security/incidents
```

## <a name="exporting-personal-data"></a>Eksportowanie danych osobowych
Użytkownik usługi Security Center przypisaną rolę właściciela, współautora, lub Administrator konta może wyeksportować informacje badania. Aby wyeksportować informacje badania, przejdź do **jednostek** kartę, aby skopiować i wkleić istotne informacje.

## <a name="next-steps"></a>Kolejne kroki
Aby uzyskać więcej informacji na temat zarządzających danymi użytkowników zobacz [zarządzanie danymi użytkownika w usłudze Azure Security Center](security-center-privacy.md).
Aby dowiedzieć się więcej na temat usuwania danych prywatnych w usłudze Log Analytics, zobacz [sposobu eksportowania i usuwania danych prywatnych](../azure-monitor/platform/personal-data-mgmt.md#how-to-export-and-delete-private-data).
