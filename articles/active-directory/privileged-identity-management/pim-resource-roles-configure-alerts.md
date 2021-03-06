---
title: Konfigurowanie alertów zabezpieczeń dla ról zasobów platformy Azure w usłudze PIM | Dokumentacja firmy Microsoft
description: Dowiedz się, jak skonfigurować alerty zabezpieczeń dla ról zasobów platformy Azure w usłudze Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.subservice: pim
ms.date: 04/02/2018
ms.author: rolyon
ms.custom: pim
ms.collection: M365-identity-device-management
ms.openlocfilehash: 538661df85ca0960992cb40a53b0e149c3b566b6
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56189535"
---
# <a name="configure-security-alerts-for-azure-resource-roles-in-pim"></a>Konfigurowanie alertów zabezpieczeń dla ról zasobów platformy Azure w usłudze PIM
Privileged Identity Management (PIM) dla zasobów platformy Azure generuje alerty w przypadku działania związane z niebezpieczne lub podejrzane w danym środowisku. Po wyzwoleniu alertu ona wyświetlona na stronie alertów. 

![Strona alertów](media/azure-pim-resource-rbac/RBAC-alerts-home.png)

## <a name="review-alerts"></a>Przeglądanie alertów
Wybierz alert, aby wyświetlić raport zawierający listę użytkowników lub ról, które wyzwolony alert, wraz z porad korygowania.

![Raport o alertach](media/azure-pim-resource-rbac/rbac-alert-info.png)

## <a name="alerts"></a>Alerty
| Alerty | Ważność | Wyzwalacz | Zalecenie |
| --- | --- | --- | --- |
| **Zbyt wielu właścicieli przypisanych do zasobu** |Medium |Zbyt wielu użytkowników korzysta z roli właściciela. |Przejrzyj użytkowników na liście, a następnie ponownie przypisać niektóre mniej uprzywilejowanych ról. |
| **Zbyt wiele trwałych właścicieli przypisanych do zasobu** |Medium |Zbyt wielu użytkowników są trwale przypisane do roli. |Przejrzyj użytkowników na liście, a następnie ponownie przypisać niektóre do wymagana aktywacja w celu użycia roli. |
| **Utworzono zduplikowaną rolę** |Medium |Wiele ról ma takich samych kryteriów. |Użyj tylko jednej z tych ról. |


### <a name="severity"></a>Ważność
* **Wysoka**: Wymaga natychmiastowego działania z powodu naruszenia zasad. 
* **Średnia**: Nie wymagać natychmiastowego działania, ale sygnalizuje potencjalne naruszenie zasad.
* **Niska**: Nie wymagać natychmiastowego działania, ale sugeruje zmiana preferowanego zasad.

## <a name="configure-security-alert-settings"></a>Konfigurowanie ustawień alertów zabezpieczeń
Na stronie alertów, przejdź do **ustawienia**.
![Ustawienia](media/azure-pim-resource-rbac/rbac-navigate-settings.png)

Dostosowywanie ustawień na różne alerty chcesz pracować w swoim środowisku i cele zabezpieczeń.
![Dostosowywanie ustawień](media/azure-pim-resource-rbac/rbac-alert-settings.png)

## <a name="next-steps"></a>Kolejne kroki

- [Konfigurowanie alertów zabezpieczeń dla ról zasobów platformy Azure w usłudze PIM](pim-resource-roles-configure-alerts.md)
