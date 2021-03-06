---
title: Odwoływać się do obrazu niestandardowego w szablonie zestawu skalowania na platformie Azure | Dokumentacja firmy Microsoft
description: Dowiedz się, jak dodać obraz niestandardowy do istniejącego szablonu zestawu skalowania maszyn wirtualnych platformy Azure
services: virtual-machine-scale-sets
documentationcenter: ''
author: mayanknayar
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/10/2017
ms.author: manayar
ms.openlocfilehash: 2e3c8177a32082c251be74e597a18730ae1c9d37
ms.sourcegitcommit: ae45eacd213bc008e144b2df1b1d73b1acbbaa4c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/01/2018
ms.locfileid: "50739651"
---
# <a name="add-a-custom-image-to-an-azure-scale-set-template"></a>Dodaj obraz niestandardowy do szablonu zestawu skalowania na platformie Azure

W tym artykule przedstawiono sposób modyfikowania [minimalnego możliwego do użycia zestawu skalowania szablonu](./virtual-machine-scale-sets-mvss-start.md) wdrażania za pomocą niestandardowego obrazu.

## <a name="change-the-template-definition"></a>Zmiana definicji szablonu

Szablon zestawu minimalnej wielkości są widoczne [tutaj](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), a szablon wdrażania skalowania ustawioną na podstawie niestandardowego obrazu będzie widoczne [tutaj](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json). Przeanalizujmy diff, używany do tworzenia tego szablonu (`git diff minimum-viable-scale-set custom-image`) eliminujemy:

### <a name="creating-a-managed-disk-image"></a>Tworzenie obrazu dysku zarządzanego

Jeśli masz już obrazu niestandardowego dysku zarządzanego (zasób typu `Microsoft.Compute/images`), a następnie pominąć tę sekcję.

Najpierw dodaj `sourceImageVhdUri` parametr, który jest identyfikatorem URI do ogólnych obiektów blob w usłudze Azure Storage, który zawiera niestandardowy obraz do wdrożenia z.


```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "sourceImageVhdUri": {
+      "type": "string",
+      "metadata": {
+        "description": "The source of the generalized blob containing the custom image"
+      }
     }
   },
   "variables": {},
```

Następnie dodaj zasób typu `Microsoft.Compute/images`, czyli obrazu dysku zarządzanego na podstawie uogólnionego obiektu blob znajdującego się w identyfikatorze URI `sourceImageVhdUri`. Ten obraz musi być w tym samym regionie co zestaw skalowania, która go używa. We właściwościach obrazu, należy określić typ systemu operacyjnego, lokalizację obiektu blob (z `sourceImageVhdUri` parametru), a typ konta magazynu:

```diff
   "resources": [
     {
+      "type": "Microsoft.Compute/images",
+      "apiVersion": "2016-04-30-preview",
+      "name": "myCustomImage",
+      "location": "[resourceGroup().location]",
+      "properties": {
+        "storageProfile": {
+          "osDisk": {
+            "osType": "Linux",
+            "osState": "Generalized",
+            "blobUri": "[parameters('sourceImageVhdUri')]",
+            "storageAccountType": "Standard_LRS"
+          }
+        }
+      }
+    },
+    {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "location": "[resourceGroup().location]",

```

Zasobu zestawu skalowania, Dodaj `dependsOn` klauzuli odwołujące się do niestandardowego obrazu, aby upewnić się, że obraz zostanie utworzona zanim stara się wdrażanie na podstawie tego obrazu zestawu skalowania:

```diff
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
       "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
+        "Microsoft.Network/virtualNetworks/myVnet",
+        "Microsoft.Compute/images/myCustomImage"
       ],
       "sku": {
         "name": "Standard_A1",

```

### <a name="changing-scale-set-properties-to-use-the-managed-disk-image"></a>Zmiana skali Ustaw właściwości, aby użyć obrazu dysku zarządzanego

W `imageReference` skalowania ustaw `storageProfile`, zamiast określania wydawcy, oferty, jednostki sku, i określ wersję obrazu platformy, `id` z `Microsoft.Compute/images` zasobów:

```diff
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
-              "publisher": "Canonical",
-              "offer": "UbuntuServer",
-              "sku": "16.04-LTS",
-              "version": "latest"
+              "id": "[resourceId('Microsoft.Compute/images', 'myCustomImage')]"
             }
           },
           "osProfile": {
```

W tym przykładzie użyj `resourceId` funkcję, aby uzyskać identyfikator zasobu obrazu utworzonego w tym samym szablonie. Jeśli wcześniej utworzono obrazu dysku zarządzanego, zamiast tego należy podać identyfikator tego obrazu. Ten identyfikator musi mieć postać: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.


## <a name="next-steps"></a>Następne kroki

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
