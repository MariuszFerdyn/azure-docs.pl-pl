---
title: Tworzenie aplikacji dla usługi Azure Stack | Dokumentacja firmy Microsoft
description: Zagadnienia dotyczące opracowywania zawartości Prototypy aplikacji w usłudze Azure Stack
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: d3ebc6b1-0ffe-4d3e-ba4a-388239d6cdc3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2019
ms.author: sethm
ms.reviewer: unknown
ms.lastreviewed: 01/05/2019
ms.openlocfilehash: 2f0d311851abe1c0fb01ec08dc82626805b35eb1
ms.sourcegitcommit: 898b2936e3d6d3a8366cfcccc0fccfdb0fc781b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/30/2019
ms.locfileid: "55251422"
---
# <a name="develop-for-azure-stack"></a>Opracowywanie zawartości dla usługi Azure Stack

*Dotyczy: Zintegrowane usługi Azure Stack, systemy i usługi Azure Stack Development Kit*

Możesz rozpocząć opracowywanie aplikacji już dziś, nawet jeśli nie masz dostępu do środowiska usługi Azure Stack. Ponieważ usługi Azure Stack zapewnia usług Microsoft Azure, które działają w Twoim centrum danych, można użyć podobnych narzędzi i procesów do opracowywania względem usługi Azure Stack, jak w przypadku usługi Azure.

## <a name="development-considerations"></a>Zagadnienia dotyczące opracowywania zawartości

Pewne przygotowania i zgodnie ze wskazówkami zawartymi w następujących tematach można użyć platformy Azure do emulowania środowiska usługi Azure Stack.

* Na platformie Azure można utworzyć szablony usługi Azure Resource Manager, które są możliwe do wdrożenia w usłudze Azure Stack. Zobacz [zagadnienia dotyczące szablonów](azure-stack-develop-templates.md) wskazówki dotyczące tworzenia szablonów, aby zapewnić Przenoszalność.
* Istnieją różnice w dostępności usługi i przechowywanie wersji usługi między platformą Azure i usługi Azure Stack. Możesz użyć [moduł zasad usługi Azure Stack](azure-stack-policy-module.md) ograniczyć typy dostępności i zasobów usługi platformy Azure do co jest dostępne w usłudze Azure Stack. Ograniczając usług gwarantuje, że aplikacje nie korzysta z usług dostępnych w usłudze Azure Stack.
* [Szablony szybkiego startu usługi Azure Stack](https://github.com/Azure/AzureStack-QuickStart-Templates) są typowe przykłady scenariuszy, które pokazują, jak opracowywać szablony, które mogą być wdrażane na platformie Azure oraz usługi Azure Stack.

## <a name="next-steps"></a>Kolejne kroki

Aby uzyskać więcej informacji o programowaniu dla usługi Azure Stack zobacz następujące artykuły:

* [Usługa Azure Resource Manager szablon najlepszych rozwiązań](azure-stack-develop-templates.md)
* [Szablony szybkiego startu usługi Azure Stack w witrynie GitHub](https://github.com/Azure/AzureStack-QuickStart-Templates)