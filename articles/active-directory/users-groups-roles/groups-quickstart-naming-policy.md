---
title: 'Szybki start: dodawanie zasad nadawania nazw dla grup usługi Office 365 — Azure Active Directory | Microsoft Docs'
description: Wyjaśniono, jak dodać nowych użytkowników lub usunąć istniejących użytkowników w usłudze Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 01/31/2019
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9905e3d8b2e0760fca82e9d2c0bfb0164d8fc9fa
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56210428"
---
# <a name="quickstart-naming-policy-for-groups-in-azure-active-directory"></a>Szybki start: Zasady nazewnictwa grup w usłudze Azure Active Directory

W tym przewodniku Szybki start utworzysz zasady nazewnictwa w dzierżawie usługi Azure Active Directory (Azure AD) dla grup usługi Office 365 tworzonych przez użytkowników, aby umożliwić sortowanie i wyszukiwanie grup w ramach dzierżawy. Zasady nazewnictwa umożliwiają na przykład:

* Przekazywanie informacji na temat funkcji grupy, członkostwa, regionu geograficznego lub twórcy grupy.
* Łatwiejsze kategoryzowanie grup w książce adresowej.
* Blokowanie konkretnych słów, aby uniemożliwić ich używanie w nazwach grup i aliasach.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem [utwórz bezpłatne konto](https://azure.microsoft.com/free/).

## <a name="install-powershell-cmdlets"></a>Instalowanie poleceń cmdlet programu PowerShell

Pamiętaj, aby odinstalować starszą wersję modułu Azure Active Directory PowerShell dla programu Graph z programu Windows PowerShell i zainstalować moduł [Azure Active Directory PowerShell dla programu Graph w publicznej wersji zapoznawczej 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137) przed uruchomieniem poleceń programu PowerShell. 

1. Otwórz aplikację Windows PowerShell jako administrator.
2. Odinstaluj poprzednią wersję programu AzureADPreview.
  
  ```
  Uninstall-Module AzureADPreview
  ```
3. Zainstaluj najnowszą wersję programu AzureADPreview.
  
  ```
  Install-Module AzureADPreview
  ```
Jeśli zostanie wyświetlony monit dotyczący dostępu do niezaufanego repozytorium, wpisz **Y**. Zainstalowanie nowego modułu może zająć kilka minut.

## <a name="set-up-naming-policy"></a>Tworzenie zasad nazewnictwa

### <a name="step-1-sign-in-using-powershell-cmdlets"></a>Krok 1: logowanie się przy użyciu poleceń cmdlet programu PowerShell

1. Otwórz aplikację Windows PowerShell. Podniesione przywileje nie są konieczne.

2. Uruchom następujące polecenia, aby przygotować się do uruchomienia poleceń cmdlet.
  
  ```
  Import-Module AzureADPreview
  Connect-AzureAD
  ```
  Na ekranie **Zaloguj się na swoje konto** wprowadź swoje konto administratora i hasło, aby połączyć się z usługą, a następnie wybierz polecenie **Zaloguj**.

3. Postępuj zgodnie z instrukcjami zawartymi w artykule [Azure Active Directory cmdlets for configuring group settings (Polecenia cmdlet usługi Azure Active Directory służące do konfigurowania ustawień grupy)](groups-settings-cmdlets.md), aby utworzyć ustawienia grupy dla tej dzierżawy.

### <a name="step-2-view-the-current-settings"></a>Krok 2: wyświetlanie bieżących ustawień

1. Wyświetl bieżące ustawienia zasad nazewnictwa.
  
  ```
  $Setting = Get-AzureADDirectorySetting -Id (Get-AzureADDirectorySetting | where -Property DisplayName -Value "Group.Unified" -EQ).id
  ```
  
2. Wyświetl bieżące ustawienia grupy.
  
  ```
  $Setting.Values
  ```
  
### <a name="step-3-set-the-naming-policy-and-any-custom-blocked-words"></a>Krok 3: konfigurowanie zasad nazewnictwa i wszelkich niestandardowych słów zablokowanych

1. Ustaw prefiksy i sufiksy nazw grup w usłudze Azure AD PowerShell. Aby ta funkcja działała poprawnie, należy dodać element [GroupName] do ustawienia.
  
  ```
  $Setting["PrefixSuffixNamingRequirement"] =“GRP_[GroupName]_[Department]"
  ```
  
2. Ustaw niestandardowe słowa zablokowane. W poniższym przykładzie pokazano, jak dodać własne słowa niestandardowe.
  
  ```
  $Setting["CustomBlockedWordsList"]=“Payroll,CEO,HR"
  ```
  
3. Zapisz ustawienia nowych zasad, aby zaczęły obowiązywać, tak jak w poniższym przykładzie.
  
  ```
  Set-AzureADDirectorySetting -Id (Get-AzureADDirectorySetting | where -Property DisplayName -Value "Group.Unified" -EQ).id -DirectorySetting $Setting
  ```
  
Gotowe. Skonfigurowano zasady nazewnictwa i dodano niestandardowe słowa zablokowane.

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

1. Usuń prefiksy i sufiksy nazw grup w usłudze Azure AD PowerShell.
  
  ```
  $Setting["PrefixSuffixNamingRequirement"] =""
  ```
  
2. Usuń niestandardowe słowa zablokowane.
  
  ```
  $Setting["CustomBlockedWordsList"]=""
  ```
  
3. Zapisz ustawienia.
  
  ```
  Set-AzureADDirectorySetting -Id (Get-AzureADDirectorySetting | where -Property DisplayName -Value "Group.Unified" -EQ).id -DirectorySetting $Setting
  ```

## <a name="next-steps"></a>Następne kroki

W tym przewodniku Szybki start wyjaśniono, w jaki sposób skonfigurować zasady nazewnictwa w dzierżawie usługi Azure AD przy użyciu poleceń cmdlet programu PowerShell.

Aby uzyskać więcej informacji na temat ograniczeń technicznych, dodawania listy niestandardowych słów zablokowanych lub środowiska użytkownika końcowego w aplikacjach usługi Office 365, przejdź do kolejnego artykułu i dowiedz się więcej na temat zasad nazewnictwa.
> [!div class="nextstepaction"]
> [Naming policy all details (Wszystkie szczegóły dotyczące zasad nazewnictwa)](groups-naming-policy.md)
