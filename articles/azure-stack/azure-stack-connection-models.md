---
title: Modele połączeń systemy zintegrowane usługi Azure Stack | Dokumentacja firmy Microsoft
description: Określ decyzje dotyczące usługi Azure Stack wielowęzłowego do planowania wdrożenia.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2019
ms.author: jeffgilb
ms.reviewer: wfayed
ms.lastreviewed: 10/15/2018
ms.openlocfilehash: 9760e6b9cdcd6f03f4377277f3426189b1fe0a61
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56182021"
---
# <a name="azure-stack-integrated-systems-connection-models"></a>Modele połączeń systemy zintegrowane usługi Azure Stack
Jeśli interesuje Cię zakupu to system zintegrowany z usługi Azure Stack, musisz zrozumieć [kilka zagadnień integracji datacenter](azure-stack-datacenter-integration.md) dla wdrożenia usługi Azure Stack określić, jak system zmieści się w centrum danych. Ponadto należy zdecydować, jak będzie Zintegruj usługę Azure Stack w środowisku chmury hybrydowej. W tym artykule omówiono następujące główne decyzje, takich jak połączenie platformy Azure, Magazyn tożsamości i rozliczeń decyzji modelu.

Jeśli zdecydujesz się kupić system zintegrowany z dostawcą sprzętu producenta sprzętu (OEM) pomaga przeprowadzą Cię przez proces znaczną część procesu planowania, które bardziej szczegółowo. Będą one również wykonać rzeczywiste wdrożenie.

## <a name="choose-an-azure-stack-deployment-connection-model"></a>Wybierz model połączenia wdrożenia usługi Azure Stack
Można wdrożyć usługę Azure Stack, połączony z Internetem (i na platformie Azure) lub odłączony. Aby uzyskać największe korzyści z usługi Azure Stack, hybrydowe scenariusze między usługi Azure Stack i platformą Azure, w tym należy wdrożyć połączony z platformą Azure. Ten wybór określa, które opcje są dostępne dla magazynu tożsamości (Azure Active Directory lub usług federacyjnych Active Directory) i model rozliczeń (zapłacić jako zgodnie z użycia albo rozliczeniem bądź oparty na pojemności rozliczeń) zgodnie z opisem w następujących tabeli i diagramu: 

![Azure Stack wdrożenia i rozliczeń scenariuszy](media/azure-stack-connection-models/azure-stack-scenarios.png)  
  
> [!IMPORTANT]
> To punkt kluczowe decyzje. Wybór usługi Active Directory Federation Services (AD FS) lub Azure Active Directory (Azure AD) jest jednorazowe decyzji, które należy wykonać w czasie wdrażania. Nie można zmienić to później bez ponownego wdrażania całego systemu.  


|Opcje|Połączony z platformą Azure|Odłączono od platformy Azure|
|-----|-----|-----|
|Azure AD|![Obsługiwane](media/azure-stack-connection-models/check.png)| |
|AD FS|![Obsługiwane](media/azure-stack-connection-models/check.png)|![Obsługiwane](media/azure-stack-connection-models/check.png)|
|Rozliczanie na podstawie użycia|![Obsługiwane](media/azure-stack-connection-models/check.png)| |
|Rozliczanie na podstawie pojemności|![Obsługiwane](media/azure-stack-connection-models/check.png)|![Obsługiwane](media/azure-stack-connection-models/check.png)|
|Pobierz pakiety aktualizacji bezpośrednio do usługi Azure Stack|![Obsługiwane](media/azure-stack-connection-models/check.png)|  |

Po podjęciu model połączenia platformy Azure można użyć do wdrożenia usługi Azure Stack, dodatkowe, zależnych od połączenia decyzji należy przewidzieć magazynem tożsamości i metody rozliczeń. 

## <a name="next-steps"></a>Kolejne kroki

[Usługa Azure połączonej usługi Azure Stack decyzji dotyczących wdrożenia](azure-stack-connected-deployment.md)

[Azure odłączony decyzji dotyczących wdrożenia usługi Azure Stack](azure-stack-disconnected-deployment.md)
