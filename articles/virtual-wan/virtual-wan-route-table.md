---
title: Tworzenie sieci platformy Azure z wirtualnych WAN tabelę tras koncentrator wirtualny w celu kierowania do urządzenia WUS | Dokumentacja firmy Microsoft
description: Wirtualne sieci WAN koncentrator wirtualny tabelę tras w celu kierowania ruchu do wirtualnego urządzenia sieciowego.
services: virtual-wan
author: cherylmc
ms.service: virtual-wan
ms.topic: conceptual
ms.date: 01/09/2019
ms.author: cherylmc
Customer intent: As someone with a networking background, I want to work with routing tables for NVA.
ms.openlocfilehash: 45e5c43cf5eb8df1df5b26ffae50d2881bb086e4
ms.sourcegitcommit: fec0e51a3af74b428d5cc23b6d0835ed0ac1e4d8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/12/2019
ms.locfileid: "56115202"
---
# <a name="create-a-virtual-hub-route-table-to-steer-traffic-to-a-network-virtual-appliance"></a>Utwórz koncentrator wirtualny tabelę tras w celu kierowania ruchu do wirtualnego urządzenia sieciowego

W tym artykule przedstawiono sposób kierowania ruchu z koncentratora wirtualnego do wirtualnego urządzenia sieciowego. 

![Diagram usługi Virtual WAN](./media/virtual-wan-route-table/vwanroute.png)

W tym artykule omówiono sposób wykonywania następujących zadań:

* Tworzenie sieci WAN
* Tworzenie koncentratora
* Tworzenie Centrum połączeń sieci wirtualnej
* Utwórz trasę koncentratora
* Tworzenie tabeli tras
* Zastosowanie tabeli tras

## <a name="before-you-begin"></a>Przed rozpoczęciem

Sprawdź, czy są spełnione następujące kryteria:

1. Masz wirtualnego urządzenia sieciowego (WUS) to oprogramowanie innych firm wybranych przez użytkownika jest zazwyczaj zainicjowanym do obsługi administracyjnej z witryny Azure Marketplace (Link) w sieci wirtualnej.
2. Masz prywatny adres IP przypisany do interfejsu sieciowego urządzenia WUS. 
3. Nie można wdrożyć urządzenie WUS w koncentrator wirtualny. Musi zostać wdrożony w oddzielnych sieci wirtualnej. W tym artykule sieci wirtualnej urządzenie WUS nazywa się "strefy DMZ sieci wirtualnej".
4. "Strefy DMZ sieci wirtualnej" może zawierać jeden lub wiele sieci wirtualnych połączonych z nim. W tym artykule ta sieć wirtualna nazywa się "Pośrednich sieć wirtualną będącą szprychą". Tych sieciach wirtualnych mogą być połączone z siecią wirtualną strefy DMZ przy użyciu komunikacji równorzędnej sieci wirtualnych.
5. Sprawdź, czy masz 2 sieci wirtualne, które już utworzone. Zostaną one użyte jako sieci wirtualne będące szprychami. W tym artykule przestrzenie adresów sieci wirtualnej szprychy są 10.0.2.0/24 i 10.0.3.0/24. Jeśli potrzebujesz informacji na temat tworzenia sieci wirtualnej, zobacz [Utwórz sieć wirtualną przy użyciu programu PowerShell](../virtual-network/quick-create-powershell.md).
6. Upewnij się, że nie ma żadnych bram sieci wirtualnej w dowolnej sieci wirtualnych.

## <a name="signin"></a>1. Logowanie

Upewnij się, że możesz zainstalować najnowszą wersję poleceń cmdlet programu PowerShell usługi Resource Manager. Aby uzyskać więcej informacji na temat instalowania poleceń cmdlet programu PowerShell, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/azurerm/overview). Jest to ważne, ponieważ wcześniejsze wersje poleceń cmdlet nie zawierają bieżących wartości potrzebnych w tym ćwiczeniu. Moduły w ją zgodnie z przykładami są usługi Azure Menedżera zasobów. Ten artykuł będzie można zaktualizować Az platformy Azure w przyszłości.

1. Otwórz konsolę programu PowerShell z podwyższonym poziomem uprawnień i zaloguj się do konta platformy Azure. To polecenie cmdlet wyświetli monit o podanie poświadczeń logowania. Po zalogowaniu pobiera ono ustawienia konta, tak aby były dostępne dla programu Azure PowerShell.

  ```powershell
  Connect-AzureRmAccount
  ```
2. Pobierz listę subskrypcji platformy Azure.

  ```powershell
  Get-AzureRmSubscription
  ```
3. Wskaż subskrypcję, której chcesz użyć.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```

## <a name="rg"></a>2. Tworzenie zasobów

1. Utwórz grupę zasobów.

  ```powershell
  New-AzureRmResourceGroup -Location "West US" -Name "testRG"
  ```
2. Tworzenie wirtualnej sieci WAN.

  ```powershell
  $virtualWan = New-AzureRmVirtualWan -ResourceGroupName "testRG" -Name "myVirtualWAN" -Location "West US"
  ```
3. Utwórz koncentrator wirtualny.

  ```powershell
  New-AzureRmVirtualHub -VirtualWan $virtualWan -ResourceGroupName "testRG" -Name "westushub" -AddressPrefix "10.0.1.0/24"
  ```

## <a name="connections"></a>3. Tworzenie połączeń

Tworzenie połączenia sieci wirtualnej Centrum z sieci typu gwiazda pośrednich i strefy DMZ sieci wirtualnej do koncentratora wirtualnego.

  ```powershell
  $remoteVirtualNetwork1= Get-AzureRmVirtualNetwork -Name “indirectspoke1” -ResourceGroupName “testRG”
  $remoteVirtualNetwork2= Get-AzureRmVirtualNetwork -Name “indirectspoke2” -ResourceGroupName “testRG”
  $remoteVirtualNetwork3= Get-AzureRmVirtualNetwork -Name “dmzvnet” -ResourceGroupName “testRG”

  New-AzureRmVirtualHubVnetConnection -ResourceGroupName “testRG” -VirtualHubName “westushub” -Name  “testvnetconnection1” -RemoteVirtualNetwork $remoteVirtualNetwork1
  New-AzureRmVirtualHubVnetConnection -ResourceGroupName “testRG” -VirtualHubName “westushub” -Name  “testvnetconnection2” -RemoteVirtualNetwork $remoteVirtualNetwork2
  New-AzureRmVirtualHubVnetConnection -ResourceGroupName “testRG” -VirtualHubName “westushub” -Name  “testvnetconnection3” -RemoteVirtualNetwork $remoteVirtualNetwork3
  ```

## <a name="route"></a>4. Utwórz trasę koncentratora wirtualnego

W tym artykule przestrzenie adresowe sieci typu gwiazda pośrednie są 10.0.2.0/24 i 10.0.3.0/24, a urządzenie WUS w strefie DMZ sieci interfejs prywatny adres IP jest 10.0.4.5.

```powershell
$route1 = New-AzureRmVirtualHubRoute -AddressPrefix @("10.0.2.0/24", "10.0.3.0/24") -NextHopIpAddress "10.0.4.5"
```

## <a name="applyroute"></a>5. Utwórz tabelę tras koncentrator wirtualny

Utwórz tabelę tras koncentrator wirtualny, a następnie zastosowanie utworzona trasa do niej.
 
```powershell
$routeTable = New-AzureRmVirtualHubRouteTable -Route @($route1)
```

## <a name="commit"></a>6. Zatwierdź zmiany

Zatwierdź zmiany do koncentratora wirtualnego.

```powershell
Update-AzureRmVirtualHub -VirtualWanId $virtualWan.Id -ResourceGroupName "testRG" -Name "westushub” -RouteTable $routeTable
```

## <a name="cleanup"></a>Oczyszczanie zasobów

Gdy grupa zasobów i zawarte w niej zasoby nie będą już potrzebne, można je usunąć za pomocą polecenia [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup). Zastąp wartość „myResourceGroup” nazwą grupy zasobów, a następnie uruchom następujące polecenie programu PowerShell:

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="next-steps"></a>Kolejne kroki

Aby uzyskać więcej informacji na temat usługi Virtual WAN, zobacz stronę [Omówienie usługi Virtual WAN](virtual-wan-about.md).
