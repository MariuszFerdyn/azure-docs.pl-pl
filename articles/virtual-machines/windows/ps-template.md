---
title: Tworzenie maszyny Wirtualnej z systemem Windows na podstawie szablonu na platformie Azure | Dokumentacja firmy Microsoft
description: Z łatwością tworzyć nową maszynę Wirtualną Windows, należy użyć szablonu usługi Resource Manager i programu PowerShell.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 19129d61-8c04-4aa9-a01f-361a09466805
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/03/2019
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 893ef999907c7f807fdf3a82b2372ece9c9a6a39
ms.sourcegitcommit: fec0e51a3af74b428d5cc23b6d0835ed0ac1e4d8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/12/2019
ms.locfileid: "56112432"
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a>Utwórz maszynę wirtualną Windows za pomocą szablonu usługi Resource Manager

W tym artykule przedstawiono sposób wdrażania szablonu usługi Azure Resource Manager przy użyciu programu PowerShell. Tworzony szablon wdraża pojedynczej maszyny wirtualnej z systemem Windows Server w nowej sieci wirtualnej z jedną podsiecią.

Aby uzyskać szczegółowy opis zasobu maszyny wirtualnej, zobacz [maszyn wirtualnych w szablonie usługi Azure Resource Manager](template-description.md). Aby uzyskać więcej informacji na temat wszystkich zasobów w szablonie, zobacz [Przewodnik po szablonie usługi Azure Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Wykonaj kroki w tym artykule powinno zająć około pięciu minut.

[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

Jeśli chcesz zainstalować program PowerShell i używać go lokalnie, ten samouczek wymaga modułu Azure PowerShell w wersji 5.3 lub nowszej. Uruchom polecenie `Get-Module -ListAvailable AzureRM`, aby dowiedzieć się, jaka wersja jest używana. Jeśli konieczne będzie uaktualnienie, zobacz [Instalowanie modułu Azure PowerShell](/powershell/azure/azurerm/install-azurerm-ps). Jeśli używasz programu PowerShell lokalnie, musisz też uruchomić polecenie `Connect-AzAccount`, aby utworzyć połączenie z platformą Azure.

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Wszystkie zasoby, musi zostać wdrożony w [grupy zasobów](../../azure-resource-manager/resource-group-overview.md).

1. Pobierz listę dostępnych lokalizacji, w których można utworzyć zasoby.
   
    ```powershell   
    Get-AzLocation | sort-object DisplayName | Select DisplayName
    ```

2. Utwórz grupę zasobów w wybranej lokalizacji. W tym przykładzie pokazano tworzenie grupy zasobów o nazwie **myResourceGroup** w **zachodnie stany USA** lokalizacji:

    ```powershell   
    New-AzResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-the-files"></a>Tworzenie plików

W tym kroku utworzysz plik szablonu, który służy do wdrażania zasobów i plik parametrów, który dostarcza wartości parametrów do szablonu. Możesz również utworzyć plik autoryzacji, który służy do wykonywania operacji usługi Azure Resource Manager. 

1. Utwórz plik o nazwie *CreateVMTemplate.json* i Dodaj swój kod JSON do niego. Zastąp wartość `domainNameLabel` własną unikatową nazwą.

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]" 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
              "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "2012-R2-Datacenter",
                "version": "latest"
              },
              "osDisk": {
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

2. Utwórz plik o nazwie *Parameters.json* i dodać do niego ten kod JSON:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
      "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

3. Utwórz nowe konto magazynu i kontener:

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. Przekaż pliki do konta magazynu:

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    Zmiana - ścieżki do plików do lokalizacji, w którym przechowywane są pliki.

## <a name="create-the-resources"></a>Tworzenie zasobów

Wdrażanie szablonu przy użyciu parametrów:

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> Można także wdrożyć szablony i parametrów z plików lokalnych. Aby dowiedzieć się więcej, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Storage](../../storage/common/storage-powershell-guide-full.md).

## <a name="next-steps"></a>Następne kroki

- Jeśli wystąpiły problemy dotyczące wdrożenia, może zająć się [Rozwiązywanie typowych problemów wdrażania na platformie Azure przy użyciu usługi Azure Resource Manager](../../resource-manager-common-deployment-errors.md).
- Dowiedz się, jak tworzyć i zarządzać nimi maszynę wirtualną w [Utwórz Windows maszyn wirtualnych i zarządzanie przy użyciu modułu Azure PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Aby dowiedzieć się więcej na temat tworzenia szablonów, wyświetlić składnię JSON i właściwości dla typów zasobów, które można wdrożyć:

* [Microsoft.Network/publicIPAddresses](/azure/templates/microsoft.network/publicipaddresses)
* [Microsoft.Network/virtualNetworks](/azure/templates/microsoft.network/virtualnetworks)
* [Microsoft.Network/networkInterfaces](/azure/templates/microsoft.network/networkinterfaces)
* [Microsoft.Compute/virtualMachines](/azure/templates/microsoft.compute/virtualmachines)

