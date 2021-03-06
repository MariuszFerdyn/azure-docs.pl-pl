---
title: Plik dyrektywy include
description: Plik dyrektywy include
services: media-services
author: Juliako
ms.service: media-services
ms.topic: include
ms.date: 11/11/2018
ms.author: juliako
ms.custom: include file
ms.openlocfilehash: 4207031652db7ec4b2ae5468dc159320f6efdbc2
ms.sourcegitcommit: 95822822bfe8da01ffb061fe229fbcc3ef7c2c19
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/29/2019
ms.locfileid: "55228818"
---
## <a name="create-a-media-services-account"></a>Tworzenie konta usługi Media Services

Najpierw należy utworzyć konto usługi Media Services. W tej sekcji przedstawiono, co jest potrzebne do tworzenia konta przy użyciu wiersza polecenia platformy Azure.

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów przy użyciu poniższego polecenia. Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów, takich jak konta usługi Azure Media Services i skojarzone konta usługi Storage, oraz zarządzania nimi.

```azurecli
az group create --name amsResourceGroup --location westus2
```

### <a name="create-a-storage-account"></a>Tworzenie konta magazynu

Podczas tworzenia konta usługi Media Services musisz podać nazwę zasobu konta usługi Azure Storage. Podane konto magazynu jest dołączane do konta usługi Media Services. 

Musisz mieć jedno **główne** konto magazynu i możesz mieć dowolną liczbę **dodatkowych** kont magazynu skojarzonych z Twoim kontem usługi Media Services. Usługa Media Services obsługuje konta **Ogólnego przeznaczenia, wersja 2** (GPv2) i **Ogólnego przeznaczenia, wersja 1** (GPv1). Konta tylko obiektów blob nie są dozwolone jako **główne**. Jeśli chcesz dowiedzieć się więcej o kontach magazynu, zobacz [Opcje konta usługi Azure Storage](../articles/storage/common/storage-account-options.md). 

Aby uzyskać więcej informacji na temat używania kont magazynu w usłudze Media Services, zobacz [Konta magazynu](../articles/media-services/latest/storage-account-concept.md).

Poniższe polecenie tworzy konto usługi Storage, które ma zostać skojarzone z kontem usługi Media Services. W poniższym skrypcie możesz zastąpić wartość `storageaccountforams` swoją wartością. Nazwa konta musi mieć długość mniejszą niż 24.

```azurecli
az storage account create --name storageaccountforams \  
--kind StorageV2 \
--sku Standard_RAGRS \
--resource-group amsResourceGroup
```

### <a name="create-a-media-services-account"></a>Tworzenie konta usługi Media Services

Poniższe polecenie interfejsu wiersza polecenia platformy Azure tworzy nowe konto usługi Media Services. Można zastąpić następujące wartości: `amsaccount` `storageaccountforams` (musi odpowiadać wartości nadanej kontu magazynu) i `amsResourceGroup` (musi odpowiadać wartości nadanej grupie zasobów).

```azurecli
az ams account create --name amsaccount --resource-group amsResourceGroup --storage-account storageaccountforams
```
