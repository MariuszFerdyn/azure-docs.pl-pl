---
title: Azure elementu interfejsu użytkownika VirtualNetworkCombo | Dokumentacja firmy Microsoft
description: Opis elementu Microsoft.Network.VirtualNetworkCombo interfejsu użytkownika do portalu Azure.
services: managed-applications
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: managed-applications
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2018
ms.author: tomfitz
ms.openlocfilehash: 2c2553d9ffb1dfbe032385fb77e234a8b96cb239
ms.sourcegitcommit: 5a7f13ac706264a45538f6baeb8cf8f30c662f8f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/29/2018
ms.locfileid: "37110069"
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a>Microsoft.Network.VirtualNetworkCombo UI element
Grupa służy do wybierania nowej lub istniejącej sieci wirtualnej.

## <a name="ui-sample"></a>Przykład interfejsu użytkownika
Gdy użytkownik wybiera nowej sieci wirtualnej, użytkownik może dostosować nazwę każdej podsieci i prefiksu adresu. Konfigurowanie podsieci jest opcjonalne.

![Nowe Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo-new.png)

Gdy użytkownik wybiera istniejącej sieci wirtualnej, użytkownik musi być zamapowany każdej podsieci, wymagane przez szablon wdrożenia na istniejącą podsieć. W takim przypadku Konfigurowanie podsieci jest wymagana.

![Istniejące Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo-existing.png)

## <a name="schema"></a>Schemat
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a>Uwagi
- Jeśli jest określony, pierwszy nienakładający adres prefiks rozmiar `defaultValue.addressPrefixSize` jest określane automatycznie w oparciu o istniejących sieci wirtualnych w subskrypcji użytkownika.
- Wartość domyślna dla `defaultValue.name` i `defaultValue.addressPrefixSize` jest **null**.
- `constraints.minAddressPrefixSize` musi być określona. Istniejących sieci wirtualnych się na przestrzeń adresową mniejszą niż określona wartość są niedostępne do wybrania.
- `subnets` musi być określona, i `constraints.minAddressPrefixSize` musi być określona dla każdej podsieci.
- Podczas tworzenia nowej sieci wirtualnej, prefiks adresu w każdej podsieci jest obliczana automatycznie na podstawie prefiksów adresów sieci wirtualnej i odpowiednio `addressPrefixSize`.
- Podczas korzystania z istniejącej wirtualnych sieci, żadnych podsieci mniejsze niż odpowiednie `constraints.minAddressPrefixSize` nie są dostępne do wyboru. Ponadto jeśli jest określony, podsieci, które nie mają co najmniej `minAddressCount` dostępne adresy są niedostępne do wybrania. Wartość domyślna to **0**. Aby upewnić się, że dostępnych adresów są ciągłe, określ **true** dla `requireContiguousAddresses`. Wartość domyślna to **true**.
- Tworzenie podsieci w istniejącej sieci wirtualnej nie jest obsługiwane.
- Jeśli `options.hideExisting` jest **true**, użytkownik nie może wybrać istniejącej sieci wirtualnej. Wartość domyślna to **false**.

## <a name="sample-output"></a>Przykładowe dane wyjściowe

```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a>Kolejne kroki
* Aby obejrzeć wprowadzenie do tworzenia definicji interfejsu użytkownika, zobacz [wprowadzenie CreateUiDefinition](create-uidefinition-overview.md).
* Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](create-uidefinition-elements.md).
