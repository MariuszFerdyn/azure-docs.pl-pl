---
title: Wyświetl Odmów przydziały dla zasobów platformy Azure przy użyciu witryny Azure portal | Dokumentacja firmy Microsoft
description: Dowiedz się, jak wyświetlić użytkowników, grup, nazw głównych usług i zarządzanych tożsamości, na których nastąpiła odmowa dostępu do akcji określony zasób platformy Azure w zakresie określonym w witrynie Azure portal.
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: role-based-access-control
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/30/2018
ms.author: rolyon
ms.reviewer: bagovind
ms.openlocfilehash: ec5e3daf1d4d799aab043f241548a3b4177f567c
ms.sourcegitcommit: fcb674cc4e43ac5e4583e0098d06af7b398bd9a9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/18/2019
ms.locfileid: "56343242"
---
# <a name="view-deny-assignments-for-azure-resources-using-the-azure-portal"></a>Wyświetl Odmów przydziały dla zasobów platformy Azure przy użyciu witryny Azure portal

[Odmów przypisania](deny-assignments.md) Zablokuj użytkownikom możliwość wykonywania akcji na określony zasób platformy Azure, nawet wtedy, gdy przypisanie roli przyznaje im dostęp. Mimo że nie można utworzyć własne Odmów przypisania, musisz mieć możliwość wyświetlania Odmów przypisania, ponieważ może mieć wpływ na ogólną uprawnień. Aby uzyskać informacje o przypisaniu Odmów, konieczne jest posiadanie `Microsoft.Authorization/denyAssignments/read` uprawnień, który jest dostępny w większości [wbudowane role zasobów platformy Azure](built-in-roles.md).

W tym artykule opisano sposób użycia witryny Azure portal do wyświetlania Odmów przypisania.

> [!NOTE]
> W tej chwili odmówić przypisania są przeznaczone tylko do odczytu i może zostać ustawiona tylko przez platformę Azure.

## <a name="view-deny-assignments"></a>Wyświetlanie przypisań odmowy

Wykonaj poniższe kroki, aby wyświetlić odmówić przypisania w zakresie grupy subskrypcji lub zarządzania.

1. W witrynie Azure portal kliknij pozycję **wszystkich usług** i następnie **grup zarządzania** lub **subskrypcje**.

1. Kliknij grupę zarządzania lub subskrypcji, którą chcesz wyświetlić.

1. Kliknij pozycję **Kontrola dostępu (IAM)**.

1. Kliknij przycisk **Odmów przypisania** karty (lub kliknij przycisk **widoku** przycisk w widoku Odmów kafelka przypisania).

    Jeśli istnieją przypisania odmowy występujące w tym zakresie lub dziedziczone przez ten zakres, zostaną wyświetlone.

    ![Kontrola dostępu — odmowa karta przypisania](./media/deny-assignments-portal/access-control-deny-assignments.png)

1. Aby wyświetlić dodatkowe kolumny, kliknij przycisk **Edytowanie kolumn**.

    ![Odmów przypisania — kolumn](./media/deny-assignments-portal/deny-assignments-columns.png)

    |  |  |
    | --- | --- |
    | **Nazwa** | Nazwa przypisania Odmów. |
    | **Typ podmiotu zabezpieczeń** | Użytkownika, grupy, grupy zdefiniowane przez system lub jednostki usługi. |
    | **Odmowa dostępu**  | Nazwa podmiotu zabezpieczeń, który znajduje się w przypisaniu Odmów. |
    | **Identyfikator** | Unikatowy identyfikator przypisania Odmów. |
    | **Podmioty wykluczone** | Czy istnieją podmiotów zabezpieczeń, które są wykluczone z przypisania Odmów. |
    | **Nie ma zastosowania do elementów podrzędnych** | Czy przypisanie Odmów jest dziedziczone do subscopes. |
    | **System chronione** | Czy przydział Odmów jest zarządzane przez platformę Azure. Obecnie tak zawsze. |
    | **Zakres** | Grupa zarządzania, subskrypcji, grupy zasobów lub zasobu. |

1. Dodaj znacznik wyboru do wszystkich włączonych elementów, a następnie kliknij przycisk **OK** do wyświetlenia w zaznaczonych kolumnach.

## <a name="view-details-about-a-deny-assignment"></a>Wyświetl szczegóły o przypisaniu Odmów

Wykonaj następujące kroki, aby wyświetlić dodatkowe szczegóły dotyczące przypisywania Odmów.

1. Otwórz **Odmów przypisania** okienko zgodnie z opisem w poprzedniej sekcji.

1. Kliknij nazwę przypisania Odmów, aby otworzyć **użytkowników** bloku.

    ![Odrzucanie przypisanie — użytkowników](./media/deny-assignments-portal/deny-assignment-users.png)

    **Użytkowników** blok zawiera dwie sekcje.

    |  |  |
    | --- | --- |
    | **Odmów dotyczy przypisania**  | Podmioty zabezpieczeń, których dotyczy przypisania Odmów. |
    | **Odmów wyklucza przypisania** | Podmioty zabezpieczeń, które są wykluczone z przypisania Odmów. |

    **Zdefiniowane przez system jednostki** reprezentuje wszystkich użytkowników, grup, nazw głównych usług i zarządzanych tożsamości w katalogu usługi Azure AD.

1. Aby wyświetlić listę uprawnień, które zostaną odrzucone, kliknij przycisk **odmowa uprawnień**.

    ![Przypisanie — odmowa odrzucenie uprawnień przez użytkownika](./media/deny-assignments-portal/deny-assignment-denied-permissions.png)

    | Typ akcji | Opis |
    | --- | --- |
    | **Akcje**  | Odmowa operacje zarządzania. |
    | **notActions** | Operacje zarządzania wykluczone z operacji zarządzania odmowy. |
    | **Elementy DataActions**  | Odmowa operacje na danych. |
    | **NotDataActions** | Operacje na danych spod odmowa operacji danych. |

    W przykładzie pokazano na poprzednim zrzucie ekranu poniżej przedstawiono czynne uprawnienia:

    - Cały magazyn, który operacji na płaszczyźnie danych są odrzucane, z wyjątkiem operacji obliczeniowych.

1. Aby wyświetlić właściwości przypisania Odmów, kliknij przycisk **właściwości**.

    ![Zezwalaj na przypisanie — właściwości](./media/deny-assignments-portal/deny-assignment-properties.png)

    Na **właściwości** bloku widać nazwa przypisania Odmów, identyfikator, opis i zakres. **Nie ma zastosowania do elementów podrzędnych** przełącznika wskazuje, czy Odmów przypisanie jest dziedziczone do subscopes. **System chronione** przełącznika wskazuje, czy odmówić to przypisanie jest zarządzana przez platformę Azure. Obecnie jest to **tak** we wszystkich przypadkach.

## <a name="next-steps"></a>Kolejne kroki

* [Zrozumienie Odmów przydziały dla zasobów platformy Azure](deny-assignments.md)
* [Lista Odmów przydziały dla zasobów platformy Azure przy użyciu interfejsu API REST](deny-assignments-rest.md)
