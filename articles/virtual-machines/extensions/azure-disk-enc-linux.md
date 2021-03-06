---
title: Usługa Azure Disk Encryption dla systemu Linux | Dokumentacja firmy Microsoft
description: Służy do wdrażania usługi Azure Disk Encryption dla systemu Linux na maszynę wirtualną przy użyciu rozszerzenia maszyny wirtualnej.
services: virtual-machines-linux
documentationcenter: ''
author: ejarvi
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/12/2018
ms.author: ejarvi
ms.openlocfilehash: 36e8875e91e2f04dbb60bab3211f07b2053e78f5
ms.sourcegitcommit: 96f498de91984321614f09d796ca88887c4bd2fb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/02/2018
ms.locfileid: "39414776"
---
# <a name="azure-disk-encryption-for-linux-microsoftazuresecurityazurediskencryptionforlinux"></a>Usługa Azure Disk Encryption dla systemu Linux (Microsoft.Azure.Security.AzureDiskEncryptionForLinux)

## <a name="overview"></a>Przegląd

Usługa Azure Disk Encryption korzysta z podsystemu dm-crypt w systemie Linux, aby zapewnić pełne szyfrowanie dysków na [dystrybucje systemu Linux platformy Azure wybierz](https://aka.ms/adelinux).  To rozwiązanie jest zintegrowana z usługą Azure Key Vault do zarządzania wpisami tajnymi i kluczami szyfrowania dysków.

## <a name="prerequisites"></a>Wymagania wstępne

Aby uzyskać pełną listę wymagań wstępnych, zobacz [wymagań wstępnych szyfrowania dysków Azure](
../../security/azure-security-disk-encryption-prerequisites.md).

### <a name="operating-system"></a>System operacyjny

Usługa Azure Disk Encryption jest obecnie obsługiwane na wybierz opcję dystrybucji i wersji.  Zobacz [często zadawane pytania dotyczące usługi Azure dysku szyfrowanie](../../security/azure-security-disk-encryption-faq.md#bkmk_LinuxOSSupport) listy dystrybucje systemu Linux, które są obsługiwane.

### <a name="internet-connectivity"></a>Łączność z Internetem

Usługa Azure Disk Encryption dla systemu Linux wymaga łączności z Internetem, aby uzyskać dostęp do usługi Active Directory, Key Vault, magazynu i punktów końcowych zarządzania pakietu.  Aby uzyskać więcej informacji, zobacz [wymagań wstępnych szyfrowania dysków Azure](../../security/azure-security-disk-encryption-prerequisites.md).

## <a name="extension-schema"></a>Schemat rozszerzenia

```json
{
  "type": "extensions",
  "name": "[name]",
  "apiVersion": "2015-06-15",
  "location": "[location]",
  "properties": {
    "protectedSettings": {
      "AADClientSecret": "[aadClientSecret]",
      "Passphrase": "[passphrase]"
    },
    "publisher": "Microsoft.Azure.Security",
    "settings": {
      "AADClientID": "[aadClientID]",
      "DiskFormatQuery": "[diskFormatQuery]",
      "EncryptionOperation": "[encryptionOperation]",
      "KeyEncryptionAlgorithm": "[keyEncryptionAlgorithm]",
      "KeyEncryptionKeyURL": "[keyEncryptionKeyURL]",
      "KeyVaultURL": "[keyVaultURL]",
      "SequenceVersion": "sequenceVersion]",
      "VolumeType": "[volumeType]"
    },
    "type": "AzureDiskEncryptionForLinux",
    "typeHandlerVersion": "[extensionVersion]"
  }
}
```

### <a name="property-values"></a>Wartości właściwości

| Name (Nazwa) | Wartość / przykład | Typ danych |
| ---- | ---- | ---- |
| apiVersion | 2015-06-15 | data |
| Wydawcy | Microsoft.Azure.Security | ciąg |
| type | AzureDiskEncryptionForLinux | ciąg |
| typeHandlerVersion | 0.1, 1.1 (ZESTAWU SKALOWANIA MASZYN WIRTUALNYCH) | Int |
| AADClientID | xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx | Identyfikator GUID | 
| AADClientSecret | hasło | ciąg |
| AADClientCertificate | Odcisk palca | ciąg |
| DiskFormatQuery | {"dev_path": "", "name": "","file_system": ""} | Słownik JSON |
| EncryptionOperation | EnableEncryption, EnableEncryptionFormatAll | ciąg | 
| KeyEncryptionAlgorithm | "RSA OAEP", "RSA-OAEP — 256", "RSA1_5" | ciąg |
| KeyEncryptionKeyURL | url | ciąg |
| KeyVaultURL | url | ciąg |
| Hasło | hasło | ciąg | 
| SequenceVersion | uniqueidentifier | ciąg |
| VolumeType | Systemu operacyjnego, danych, wszystkie | ciąg |

## <a name="template-deployment"></a>Wdrażanie na podstawie szablonu

Na przykład wdrożenie szablonu zobacz [włączyć szyfrowanie na uruchomionej maszyny Wirtualnej systemu Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).

## <a name="azure-cli-deployment"></a>Wdrażania interfejs wiersza polecenia platformy Azure

Instrukcje znajdują się najnowsze [dokumentacji interfejsu wiersza polecenia platformy Azure](/cli/azure/vm/encryption?view=azure-cli-latest). 

## <a name="troubleshoot-and-support"></a>Rozwiązywanie problemów i pomocy technicznej

### <a name="troubleshoot"></a>Rozwiązywanie problemów

Rozwiązywanie problemów, można znaleźć [przewodnik rozwiązywania problemów z usługi Azure Disk Encryption](../../security/azure-security-disk-encryption-tsg.md).

### <a name="support"></a>Pomoc techniczna

Jeśli potrzebujesz dodatkowej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się ze ekspertów platformy Azure na [forów platformy Azure z subskrypcją MSDN i Stack Overflow](https://azure.microsoft.com/support/community/). Alternatywnie mogą zgłaszać zdarzenia pomocy technicznej platformy Azure. Przejdź do [witryny pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i wybierz Uzyskaj pomoc techniczną. Aby uzyskać informacje o korzystaniu z pomocy technicznej platformy Azure, przeczytaj [pomocy technicznej Microsoft Azure — często zadawane pytania](https://azure.microsoft.com/support/faq/).

## <a name="next-steps"></a>Kolejne kroki

Aby uzyskać więcej informacji na temat rozszerzeń maszyn wirtualnych, zobacz [rozszerzenia maszyn wirtualnych i funkcji dla systemu Linux](features-linux.md).