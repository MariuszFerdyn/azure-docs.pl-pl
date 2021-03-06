---
title: Określ grupę zasobów dla maszyn wirtualnych w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft
description: Dowiedz się, jak i określ grupę zasobów dla maszyn wirtualnych w laboratorium Azure DevTest Labs.
services: devtest-lab, lab-services
documentationcenter: na
author: spelluru
manager: femila
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2019
ms.author: spelluru
ms.openlocfilehash: 94e5f5b29e93409df2373cf6c56e8185dc5373a2
ms.sourcegitcommit: f7be3cff2cca149e57aa967e5310eeb0b51f7c77
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/15/2019
ms.locfileid: "56312978"
---
# <a name="specify-a-resource-group-for-lab-virtual-machines-in-azure-devtest-labs"></a>Określ grupę zasobów dla maszyn wirtualnych laboratorium Azure DevTest Labs
Jako właściciel laboratorium możesz skonfigurować maszyny wirtualne laboratorium ma być utworzony w określonej grupie zasobów. Ta funkcja pomaga w następujących scenariuszach: 

- Ma mniejszą liczbę grup zasobów utworzonych przez laboratoria w ramach subskrypcji.
- Masz laboratoriów działania w ramach ustalony zestaw elementów grup zasobów, skonfigurowane przez użytkownika
- Obejścia ograniczeń i zatwierdzeń wymagane do utworzenia grupy zasobów w ramach subskrypcji platformy Azure.
- Konsolidacja wszystkich zasobów laboratorium w ramach pojedynczej grupy zasobów ułatwiają śledzenie tych zasobów i stosowanie [zasady](../governance/policy/overview.md) do zarządzania nimi na poziomie grupy zasobów.

Dzięki tej funkcji można użyć skryptu, aby określić nową lub istniejącą grupę zasobów w ramach subskrypcji platformy Azure dla wszystkich laboratorium, maszyny wirtualne. Obecnie usługa DevTest Labs obsługuje tę funkcję za pomocą interfejsu API. 

## <a name="api-to-configure-a-resource-group-for-lab-virtual-machines"></a>Interfejs API, aby skonfigurować grupę zasobów dla maszyn wirtualnych laboratorium
Teraz przejdźmy opcje się jako właściciel laboratorium, podczas korzystania z tego interfejsu API: 

- Możesz wybrać **grupy zasobów laboratorium** dla wszystkich maszyn wirtualnych.
- Możesz wybrać **istniejącą grupę zasobów** innej niż grupa zasobów laboratorium dla wszystkich maszyn wirtualnych.
- Możesz wprowadzić **nową grupę zasobów** nazwy wszystkich maszyn wirtualnych.
- Można kontynuować istniejącego zachowania, oznacza to, grupa zasobów jest tworzona dla każdej maszyny Wirtualnej w laboratorium.
 
To ustawienie dotyczy nowe maszyny wirtualne utworzone w środowisku laboratoryjnym. Starsze maszyny wirtualne w laboratorium, które zostały utworzone w ich własnych grupach zasobów w dalszym ciągu pozostaną niezmienione. Środowisk utworzonych w środowisku laboratoryjnym nadal pozostać w ich własnych grupach zasobów.

### <a name="how-to-use-this-api"></a>Jak używać tego interfejsu API:
- Użyj wersji interfejsu API **2018_10_15_preview** podczas korzystania z tego interfejsu API. 
- Jeśli określisz nową grupę zasobów, upewnij się, że **uprawnień do zapisu na temat grup zasobów** w ramach Twojej subskrypcji. Bez uprawnień do zapisu, tworzenie nowych maszyn wirtualnych w wyniku grupa określony zasób błąd. 
- Podczas korzystania z interfejsu API, przekazywanie **pełny identyfikator grupy zasobów**. Na przykład: `/subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>`. Upewnij się, że grupa zasobów znajduje się w tej samej subskrypcji co laboratorium. 

## <a name="use-powershell"></a>Korzystanie z programu PowerShell 
Poniższy przykład zawiera opis sposobu tworzenia wszystkie maszyny wirtualne laboratorium w nowej grupie zasobów przy użyciu skryptu programu PowerShell.

```PowerShell
[CmdletBinding()]
Param(
    $subId,
    $labRg,
    $labName,
    $vmRg
)

az login | out-null

az account set --subscription $subId | out-null

$rgId = "/subscriptions/"+$subId+"/resourceGroups/"+$vmRg

"Updating lab '$labName' with vm rg '$rgId'..."

az resource update -g $labRg -n $labName --resource-type "Microsoft.DevTestLab/labs" --api-version 2018-10-15-preview --set properties.vmCreationResourceGroupId=$rgId

"Done. New virtual machines will now be created in the resource group '$vmRg'."
```

Wywoływanie skryptu, używając następującego polecenia (ResourceGroup.ps1 jest plik który zawiera poprzedniego skryptu): 

```PowerShell
.\ResourceGroup.ps1 -subId <subscriptionID> -labRg <labRGNAme> -labName <LanName> -vmRg <RGName> 
```

## <a name="use-azure-resource-manager-template"></a>Korzystanie z szablonu usługi Azure Resource Manager
Jeśli używasz szablonu usługi Azure Resource Manager, aby utworzyć laboratorium, należy użyć **vmCreationResourceGroupId** właściwości w sekcji właściwości laboratorium w szablonie usługi Resource Manager, jak pokazano w poniższym przykładzie:

```json
        {
            "type": "microsoft.devtestlab/labs",
            "name": "[parameters('lab_name')]",
            "apiVersion": "2018_10_15_preview",
            "location": "eastus",
            "tags": {},
            "scale": null,
            "properties": {
                "vmCreationResourceGroupId": "/subscriptions/<SubscriptionID>/resourcegroups/<ResourceGroupName>",
                "labStorageType": "Premium",
                "premiumDataDisks": "Disabled",
                "provisioningState": "Succeeded",
                "uniqueIdentifier": "000000000f-0000-0000-0000-00000000000000"
            },
            "dependsOn": []
        },
```


## <a name="next-steps"></a>Kolejne kroki
Zobacz następujące artykuły: 

- [Ustawianie zasad laboratorium](devtest-lab-get-started-with-lab-policies.md)
- [Często zadawane pytania](devtest-lab-faq.md)
