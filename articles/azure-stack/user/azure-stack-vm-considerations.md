---
title: Różnice i zagadnienia dotyczące maszyn wirtualnych w usłudze Azure Stack | Dokumentacja firmy Microsoft
description: Poznaj różnice i zagadnienia podczas pracy z maszynami wirtualnymi w usłudze Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2019
ms.author: mabrigg
ms.reviewer: kivenkat
ms.lastreviewed: 12/19/2018
ms.openlocfilehash: 112e9aa023fb29bd960b61139861db4007c61b4d
ms.sourcegitcommit: d1c5b4d9a5ccfa2c9a9f4ae5f078ef8c1c04a3b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/08/2019
ms.locfileid: "55962251"
---
# <a name="considerations-for-using-virtual-machines-in-azure-stack"></a>Zagadnienia dotyczące korzystania z maszyn wirtualnych w usłudze Azure Stack

*Dotyczy: Zintegrowane usługi Azure Stack, systemy i usługi Azure Stack Development Kit*

Maszyny wirtualne w usłudze Azure Stack zapewnia zasoby obliczeniowe na żądanie, skalowalnych. Przed przystąpieniem do wdrażania maszyn wirtualnych (VM), musisz poznać różnice między funkcjami maszyny wirtualnej dostępne w usłudze Azure Stack i platformą Microsoft Azure. W tym artykule opisano te różnice i identyfikuje Najważniejsze kwestie dotyczące planowania wdrożenia maszyn wirtualnych. Aby dowiedzieć się więcej o różnicach wysokiego poziomu usługi Azure Stack i platformą Azure, zobacz [kluczowe zagadnienia](azure-stack-considerations.md) artykułu.

## <a name="cheat-sheet-virtual-machine-differences"></a>Ściągawka: Różnice maszyny wirtualnej

| Cecha | Azure (globalna) | Azure Stack |
| --- | --- | --- |
| Obrazy maszyn wirtualnych | W portalu Azure Marketplace zawiera obrazy, które służą do tworzenia maszyny wirtualnej. Zobacz [portalu Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) strony, aby wyświetlić listę obrazów, które są dostępne w witrynie Azure Marketplace. | Domyślnie nie ma żadnych obrazów dostępnych w witrynie marketplace usługi Azure Stack. Administrator usługi Azure Stack w chmurze, należy opublikować lub pobieranie obrazów w portalu Marketplace usługi Azure Stack, zanim użytkownicy mogą używać ich. |
| Rozmiary maszyn wirtualnych | Platforma Azure obsługuje szeroką gamę rozmiarów maszyn wirtualnych. Aby dowiedzieć się o dostępne rozmiary i opcje, zapoznaj się [rozmiarów maszyn wirtualnych Windows](../../virtual-machines/virtual-machines-windows-sizes.md) i [rozmiarów maszyn wirtualnych systemu Linux](../../virtual-machines/linux/sizes.md) tematów. | Usługa Azure Stack obsługuje rozmiarów maszyn wirtualnych, które są dostępne na platformie Azure. Aby wyświetlić listę obsługiwanych rozmiarów, zobacz [rozmiarów maszyn wirtualnych](#virtual-machine-sizes) dalszej części tego artykułu. |
| Limity przydziału maszyny wirtualnej | [Limity przydziału](../../azure-subscription-service-limits.md#service-specific-limits) są ustawiane przez firmę Microsoft | Administrator usługi Azure Stack w chmurze należy przypisać limity przydziału, zanim oferują one maszyny wirtualne do użytkowników. |
| Rozszerzenia maszyny wirtualnej |Platforma Azure obsługuje szeroką gamę rozszerzenia maszyny wirtualnej. Aby dowiedzieć się więcej na temat dostępnych rozszerzeń, zobacz [rozszerzeniach i funkcjach maszyn wirtualnych](../../virtual-machines/windows/extensions-features.md) artykułu.| Usługa Azure Stack obsługuje podzbiór rozszerzeń, które są dostępne na platformie Azure i rozszerzenia mają określonych wersji. Administrator usługi Azure Stack w chmurze można wybrać które rozszerzenia w celu udostępnienia użytkownikom. Aby wyświetlić listę rozszerzeń obsługiwanych, zapoznaj się [rozszerzenia maszyny wirtualnej](#virtual-machine-extensions) dalszej części tego artykułu. |
| Sieć maszyn wirtualnych | Publiczne adresy IP przypisane do maszyny wirtualnej dzierżawcy, są dostępne za pośrednictwem Internetu.<br><br><br>Maszyny wirtualne platformy Azure o nazwie stałych DNS | Publiczne adresy IP przypisane do maszyny wirtualnej dzierżawy są dostępne w tym środowisku usługi Azure Stack Development Kit. Użytkownik musi mieć dostęp do usługi Azure Stack Development Kit za pośrednictwem [RDP](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop) lub [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) nawiązać połączenia z maszyną wirtualną, który jest tworzony w usłudze Azure Stack.<br><br>Maszyny wirtualne utworzone w ramach określonego wystąpienia usługi Azure Stack ma nazwy DNS na podstawie wartości, który został skonfigurowany przez administratora chmury. |
| Magazyn maszyny wirtualnej | Obsługuje [dysków zarządzanych.](../../virtual-machines/windows/managed-disks-overview.md) | Dyski zarządzane są obsługiwane w usłudze Azure Stack w wersji 1808 lub nowszy. |
| Wydajność dysków maszyny wirtualnej | Zależy od typu dysku oraz jego rozmiaru. | Zależy od rozmiaru maszyny Wirtualnej maszyny wirtualnej, które dyski są dołączone do odwoływania się do [rozmiarów maszyn wirtualnych obsługiwanych w usłudze Azure Stack](azure-stack-vm-sizes.md) artykułu.
| Wersje interfejsu API | Platforma Azure ma zawsze najnowsze wersje interfejsu API dla wszystkich funkcji maszyny wirtualnej. | Usługa Azure Stack obsługuje określonych usług platformy Azure i określonych wersji interfejsu API w przypadku tych usług. Aby wyświetlić listę obsługiwanych wersji interfejsu API, zapoznaj się [wersji interfejsu API](#api-versions) dalszej części tego artykułu. |
| Usługa Azure Instance Metadata service | Azure Instance Metadata Service dostarcza informacji o uruchomionych wystąpień maszyn wirtualnych, które może służyć do zarządzania i konfigurowania maszyn wirtualnych.  | Wystąpienia usługi metadanych nie jest obsługiwana w usłudze Azure Stack. |
| Zestawy dostępności maszyny wirtualnej|Wiele domen błędów (2 lub 3 na region)<br>Wiele domen aktualizacji|Wiele domen błędów (2 lub 3 na region)<br>Wiele domen aktualizacji (maksymalnie 20)|
| Zestawy skalowania maszyn wirtualnych|Automatyczne skalowanie jest obsługiwane|Automatyczne skalowanie nie jest obsługiwane.<br>Dodaj więcej wystąpień zestawu skalowania przy użyciu witryny portal, szablonów usługi Resource Manager lub programu PowerShell. |
| Diagnostyka maszyny wirtualnej | Diagnostyka maszyn wirtualnych systemu Linux | Diagnostyka maszyn wirtualnych systemu Linux nie są obsługiwane w usłudze Azure Stack. Podczas wdrażania maszyny Wirtualnej z systemem Linux przy użyciu włączenia diagnostyki maszyn wirtualnych, wdrożenie zakończy się niepowodzeniem. Wdrażanie nie powiedzie, jeśli włączysz podstawowe metryki maszyny Wirtualnej systemu Linux, za pomocą ustawień diagnostycznych.

## <a name="virtual-machine-sizes"></a>Rozmiary maszyn wirtualnych

Usługa Azure Stack nakłada ograniczenia zasobów, aby uniknąć użycia zasobów (serwer lokalnych i poziomu usług). Te limity ulepszyć dzierżawy przez zmniejszenie wpływu użycia zasobów przez innych dzierżawców.

- W przypadku sieciowych wychodzących z maszyny Wirtualnej istnieją limity przepustowości w miejscu. Limity usługi Azure Stack są takie same jak limity na platformie Azure.
- Dla zasobów magazynu usługi Azure Stack implementuje limity operacji We/Wy magazynu, aby uniknąć podstawowe nadmierne zużycie zasobów przez dzierżawy, aby uzyskać dostęp do magazynu.
- W przypadku maszyn wirtualnych z wieloma dołączonymi dyskami danych maksymalną przepływność każdy dysk z danymi to 500 operacji We/Wy dla dysków twardych i 2300 operacje We/Wy dla dysków SSD.

Poniższa tabela zawiera listę maszyn wirtualnych, które są obsługiwane w usłudze Azure Stack, wraz z ich konfiguracji:

| Type           | Rozmiar          | Zakres obsługiwanych rozmiarów. |
| ---------------| ------------- | ------------------------ |
|Zastosowania ogólne |Podstawowa A        |[A0 – A4](azure-stack-vm-sizes.md#basic-a)                   |
|Zastosowania ogólne |A standardowe     |[A0 – A7](azure-stack-vm-sizes.md#standard-a)              |
|Zastosowania ogólne |Seria D       |[D1 - D4](azure-stack-vm-sizes.md#d-series)              |
|Zastosowania ogólne |Seria Dv2     |[D1_v2 - D5_v2](azure-stack-vm-sizes.md#ds-series)        |
|Zastosowania ogólne |Seria DS      |[DS1 - DS4](azure-stack-vm-sizes.md#dv2-series)            |
|Zastosowania ogólne |Seria DSv2    |[DS1_v2 - DS5_v2](azure-stack-vm-sizes.md#dsv2-series)      |
|Optymalizacja pod kątem pamięci|Seria D       |[D11 - D14](azure-stack-vm-sizes.md#mo-d)            |
|Optymalizacja pod kątem pamięci|Seria DS      |[DS11 - DS14](azure-stack-vm-sizes.md#mo-ds)|
|Optymalizacja pod kątem pamięci|Seria Dv2     |[D11_v2 — DS14_v2](azure-stack-vm-sizes.md#mo-dv2)     |
|Optymalizacja pod kątem pamięci|Seria DSv2 —  |[DS11_v2 — DS14_v2](azure-stack-vm-sizes.md#mo-dsv2)    |

Rozmiary maszyn wirtualnych i ich ilości skojarzonego zasobu są spójne z usługi Azure Stack i platformą Azure. Obejmuje to ilość pamięci, liczbę rdzeni i liczby/rozmiar dysków z danymi, które mogą być tworzone. Jednak wydajność maszyn wirtualnych z takim samym rozmiarze zależy od bazowego cechy danego środowiska usługi Azure Stack.

## <a name="virtual-machine-extensions"></a>Rozszerzenia maszyny wirtualnej

Usługa Azure Stack obejmuje niewielki zestaw rozszerzeń. Aktualizacje i dodatkowe rozszerzenia są dostępne za pośrednictwem witryny Marketplace syndykacji.

Użyj następującego skryptu programu PowerShell można pobrać listy rozszerzeń maszyn wirtualnych, które są dostępne w środowisku usługi Azure Stack:

```powershell
Get-AzureRmVmImagePublisher -Location local | `
  Get-AzureRmVMExtensionImageType | `
  Get-AzureRmVMExtensionImage | `
  Select Type, Version | `
  Format-Table -Property * -AutoSize
```

Jeśli aprowizacja rozszerzenia na wdrożenie maszyny Wirtualnej trwa zbyt długo, poinformuj limit czasu inicjowania obsługi administracyjnej zamiast próby zatrzymania procesu cofnięcie przydziału lub Usuń maszynę Wirtualną.

## <a name="api-versions"></a>Wersje interfejsu API

Funkcje maszyny wirtualnej w usłudze Azure Stack obsługuje następujące wersje interfejsu API:

![Typy zasobów maszyny Wirtualnej](media/azure-stack-vm-considerations/vm-resoource-types.png)

Poniższy skrypt programu PowerShell służy do uzyskania wersji interfejsu API funkcji maszyn wirtualnych, które są dostępne w danym środowisku usługi Azure Stack:

```powershell
Get-AzureRmResourceProvider | `
  Select ProviderNamespace -Expand ResourceTypes | `
  Select * -Expand ApiVersions | `
  Select ProviderNamespace, ResourceTypeName, @{Name="ApiVersion"; Expression={$_}} | `
  where-Object {$_.ProviderNamespace -like “Microsoft.compute”}
```

Lista obsługiwane typy zasobów i wersje interfejsów API mogą się różnić, jeśli operatorowi chmury aktualizuje środowiskiem usługi Azure Stack do nowszej wersji.

## <a name="windows-activation"></a>Aktywacja Windows

Produkty Windows może być używany zgodnie z postanowieniami licencyjnymi firmy Microsoft i prawa do używania produktów. Używa usługi Azure Stack [automatyczna aktywacja maszyny Wirtualnej](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303421(v%3dws.11)) (AVMA), aby aktywować maszyn wirtualnych systemu Windows Server (VM).

- Hosta platformy Azure Stack aktywuje Windows za pomocą kluczy AVMA dla systemu Windows Server 2016. Wszystkie maszyny wirtualne, które jest uruchomiony system Windows Server 2012 R2 lub nowszym zostaną automatycznie aktywowane.
- Maszyny wirtualne, które systemem Windows Server 2012 lub starszym nie zostaną automatycznie aktywowane i muszą zostać aktywowane przy użyciu [klucza MAK](https://technet.microsoft.com/library/ff793438.aspx). Aby zastosować aktywację MAK, należy podać klucz produktu.

Microsoft Azure używa aktywacji usługi KMS można aktywować maszyn wirtualnych Windows. Jeśli przenosisz maszynę Wirtualną z usługi Azure Stack na platformie Azure oraz encounter aktywować problemów, zobacz [problemy dotyczące aktywacji maszyny wirtualnej Windows Azure Rozwiązywanie problemów z](https://docs.microsoft.com/azure/virtual-machines/windows/troubleshoot-activation-problems). Dodatkowe informacje można znaleźć na [Windows Rozwiązywanie problemów z niepowodzeniami aktywacji na maszynach wirtualnych Azure](https://blogs.msdn.microsoft.com/mast/2017/06/14/troubleshooting-windows-activation-failures-on-azure-vms/) wpis w blogu zespołu pomocy technicznej platformy Azure.

## <a name="next-steps"></a>Kolejne kroki

[Utwórz maszynę wirtualną Windows przy użyciu programu PowerShell w usłudze Azure Stack](azure-stack-quick-create-vm-windows-powershell.md)
