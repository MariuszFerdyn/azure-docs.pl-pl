---
title: Tworzenie maszyny Wirtualnej z systemem Linux na platformie Azure na podstawie szablonu | Dokumentacja firmy Microsoft
description: Jak utworzyć Maszynę wirtualną systemu Linux na podstawie szablonu usługi Resource Manager za pomocą wiersza polecenia platformy Azure
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 01/03/2019
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 62ef6cad2f1c8f8f871043a8d1f70cbd08ccd65f
ms.sourcegitcommit: 3aa0fbfdde618656d66edf7e469e543c2aa29a57
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/05/2019
ms.locfileid: "55729391"
---
# <a name="how-to-create-a-linux-virtual-machine-with-azure-resource-manager-templates"></a>Jak utworzyć maszynę wirtualną z systemem Linux przy użyciu szablonów usługi Azure Resource Manager

W tym artykule pokazano, jak szybko wdrożyć maszynę wirtualną systemu Linux (VM) za pomocą szablonów usługi Azure Resource Manager i interfejsu wiersza polecenia platformy Azure. Można również wykonać te czynności przy użyciu [klasycznego wiersza polecenia platformy Azure](create-ssh-secured-vm-from-template-nodejs.md).


W tym artykule pokazano, jak szybko wdrożyć maszynę wirtualną systemu Linux (VM) za pomocą szablonów usługi Azure Resource Manager i interfejsu wiersza polecenia platformy Azure. 

## <a name="templates-overview"></a>Przegląd szablonów
Szablony usługi Azure Resource Manager są plikami JSON definiującymi infrastruktury i konfiguracji rozwiązania platformy Azure. Dzięki szablonowi można wielokrotnie wdrażać rozwiązanie w całym jego cyklu życia z gwarancją spójnego stanu zasobów po każdym wdrożeniu. Aby dowiedzieć się więcej o formacie szablonu i sposobie jego konstruowania, zobacz [Tworzenie pierwszego szablonu usługi Azure Resource Manager](../../azure-resource-manager/resource-manager-create-first-template.md). Aby wyświetlić składnię JSON dla typów zasobów, zobacz [Define resources in Azure Resource Manager templates](/azure/templates/) (Definiowanie zasobów w szablonach usługi Azure Resource Manager).

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów
Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi. Grupę zasobów należy utworzyć przed maszyną wirtualną. Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupVM* w *eastus* regionu:

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a>Tworzenie maszyny wirtualnej
Poniższy przykład obejmuje tworzenie maszyny Wirtualnej z [tego szablonu usługi Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) z [Utwórz wdrożenie grupy az](/cli/azure/group/deployment). Dozwolone jest tylko uwierzytelnianie SSH. Po wyświetleniu monitu podaj wartość własny klucz publiczny SSH, takie jak zawartość *~/.ssh/id_rsa.pub*. Jeśli musisz utworzyć parę kluczy SSH, zobacz [jak tworzenie i używanie pary kluczy SSH dla maszyn wirtualnych systemu Linux na platformie Azure](mac-create-ssh-keys.md).

```azurecli
az group deployment create \
    --resource-group myResourceGroup \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

W poprzednim przykładzie określono szablonu przechowywanego w usłudze GitHub. Możesz również pobrać lub utworzyć szablon i określ ścieżkę lokalną za pomocą `--template-file` parametru.


## <a name="connect-to-virtual-machine"></a>Nawiązywanie połączenia z maszyną wirtualną
Aby SSH z maszyną Wirtualną, Uzyskaj publiczny adres IP z [az vm show](/cli/azure/vm#az-vm-show):

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name sshvm \
    --show-details \
    --query publicIps \
    --output tsv
```

Możesz następnie SSH z maszyną wirtualną, jak zwykle. Podaj własny publiczny adres IP z poprzedniego polecenia:

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a>Kolejne kroki
W tym przykładzie utworzono Maszynę wirtualną systemu Linux podstawowe. Aby uzyskać dodatkowe szablony usługi Resource Manager, które obejmują struktur aplikacji lub utworzyć bardziej złożonych środowisk, przejdź [galerii szablonów szybkiego startu platformy Azure](https://azure.microsoft.com/documentation/templates/).

Aby dowiedzieć się więcej na temat tworzenia szablonów, wyświetlić składnię JSON i właściwości dla typów zasobów, które można wdrożyć:

* [Microsoft.Network/networkSecurityGroups](/azure/templates/microsoft.network/networksecuritygroups)
* [Microsoft.Network/publicIPAddresses](/azure/templates/microsoft.network/publicipaddresses)
* [Microsoft.Network/virtualNetworks](/azure/templates/microsoft.network/virtualnetworks)
* [Microsoft.Network/networkInterfaces](/azure/templates/microsoft.network/networkinterfaces)
* [Microsoft.Compute/virtualMachines](/azure/templates/microsoft.compute/virtualmachines)
