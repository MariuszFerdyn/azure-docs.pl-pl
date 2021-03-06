---
title: Przewodnik Szybki start platformy Azure — konfigurowanie i pobieranie wpisów tajnych z usługi Key Vault przy użyciu interfejsu wiersza polecenia platformy Azure | Microsoft Docs
description: W tym przewodniku Szybki start pokazano, w jaki sposób skonfigurować i pobrać wpis tajny z usługi Azure Key Vault przy użyciu interfejsu wiersza polecenia platformy Azure
services: key-vault
author: barclayn
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 4acc894f-fee0-4c2f-988e-bc0eceea5eda
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: quickstart
ms.custom: mvc
ms.date: 01/08/2019
ms.author: barclayn
ms.openlocfilehash: a78cc79031a8dc9b0c98beddf759fbc8674c6dd1
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/29/2019
ms.locfileid: "55168264"
---
# <a name="quickstart-set-and-retrieve-a-secret-from-azure-key-vault-using-azure-cli"></a>Szybki start: konfigurowanie i pobieranie wpisów tajnych z usługi Azure Key Vault przy użyciu interfejsu wiersza polecenia platformy Azure

Azure Key Vault to usługa w chmurze, która działa jako bezpieczny magazyn wpisów tajnych. Możesz bezpiecznie przechowywać klucze, hasła, certyfikaty oraz inne wpisy tajne. Aby uzyskać więcej informacji na temat usługi Key Vault, możesz zapoznać się z [omówieniem](key-vault-overview.md). Interfejs wiersza polecenia platformy Azure służy do tworzenia zasobów platformy Azure i zarządzanie nimi za pomocą poleceń lub skryptów. W tym przewodniku Szybki start opisano tworzenie magazynu kluczy, a następnie umieszczanie w nim wpisu tajnego.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-try-it.md)]

Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten przewodnik Szybki start wymaga interfejsu wiersza polecenia platformy Azure w wersji 2.0.4 lub nowszej. Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana. Jeśli konieczna będzie instalacja lub uaktualnienie interfejsu, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure]( /cli/azure/install-azure-cli).

Aby zalogować się do platformy Azure przy użyciu interfejsu wiersza polecenia, możesz wpisać:

```azurecli
az login
```

Aby uzyskać więcej informacji na temat opcji logowania za pośrednictwem interfejsu wiersza polecenia, zobacz [Logowanie za pomocą interfejsu wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/authenticate-azure-cli?view=azure-cli-latest)

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi. W poniższym przykładzie pokazano tworzenie grupy zasobów o nazwie *ContosoResourceGroup* w lokalizacji *eastus*.

```azurecli
az group create --name "ContosoResourceGroup" --location eastus
```

## <a name="create-a-key-vault"></a>Tworzenie magazynu kluczy

Następnie utworzysz usługę Key Vault w grupie zasobów utworzonej w poprzednim kroku. Konieczne będzie podanie pewnych informacji:

- W tym przewodniku Szybki start użyjemy nazwy **Contoso vault2**. W swoim teście musisz podać unikatową nazwę.
- Nazwa grupy zasobów: **ContosoResourceGroup**.
- Lokalizacja: **Wschodnie stany USA**.

```azurecli
az keyvault create --name "Contoso-Vault2" --resource-group "ContosoResourceGroup" --location eastus
```

Dane wyjściowe tego polecenia cmdlet pokazują właściwości nowo utworzonej usługi Key Vault. Zanotuj dwie poniższe właściwości:

- **Nazwa magazynu**: w tym przykładzie jest to **Contoso-Vault2**. Ta nazwa będzie używana do innych poleceń usługi Key Vault.
- **Identyfikator URI magazynu**: w tym przykładzie jest to https://contoso-vault2.vault.azure.net/. Aplikacje korzystające z magazynu za pomocą jego interfejsu API REST muszą używać tego identyfikatora URI.

Twoje konto platformy Azure jest teraz jedynym kontem z uprawnieniami do wykonywania jakichkolwiek operacji na tym nowym magazynie.

## <a name="add-a-secret-to-key-vault"></a>Dodawanie wpisu tajnego do usługi Key Vault

Aby dodać wpis tajny do magazynu, wystarczy tylko wykonać kilka dodatkowych czynności. Tego hasła może używać aplikacja. Hasło będzie miało nazwę **ExamplePassword** i będzie w nim przechowywana wartość **Pa$$w0rd**.

Wpisz poniższe polecenia, aby utworzyć wpis tajny w usłudze Key Vault o nazwie **ExamplePassword**, w którym będzie przechowywana wartość **Pa$$w0rd**:

```azurecli
az keyvault secret set --vault-name "Contoso-Vault2" --name "ExamplePassword" --value "Pa$$w0rd"
```

Teraz możesz odwoływać się do hasła dodanego do usługi Azure Key Vault za pomocą jego identyfikatora URI. Użyj polecenia **https://ContosoVault.vault.azure.net/secrets/ExamplePassword**, aby pobrać bieżącą wersję. 

Aby wyświetlić wartość zawartą we wpisie tajnym jako zwykły tekst:

```azurecli
az keyvault secret show --name "ExamplePassword" --vault-name "Contoso-Vault2"
```

Utworzono usługę Key Vault, umieszczono w niej wpis tajny i pobrano go.

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Inne przewodniki szybkiego startu i samouczki w tej kolekcji bazują na tym przewodniku. Jeśli planujesz korzystać z kolejnych przewodników Szybki start i samouczków, pozostaw te zasoby na swoim miejscu.
Gdy grupa zasobów i wszystkie pokrewne zasoby nie będą już potrzebne, można je usunąć za pomocą polecenia [az group delete](/cli/azure/group). Możesz usunąć zasoby w następujący sposób:

```azurecli
az group delete --name ContosoResourceGroup
```

## <a name="next-steps"></a>Następne kroki

W tym przewodniku Szybki start opisano tworzenie usługi Key Vault i umieszczanie w niej wpisu tajnego. Aby dowiedzieć się więcej na temat usługi Key Vault i sposobu jej używania z aplikacjami, przejdź do samouczka dla aplikacji internetowych współdziałających z usługą Key Vault.

> [!div class="nextstepaction"]
> Aby dowiedzieć się, jak odczytać wpis tajny z usługi Key Vault za pomocą aplikacji internetowej korzystającej z tożsamości zarządzanych dla zasobów platformy Azure, przejdź do samouczka [Konfigurowanie aplikacji internetowej platformy Azure w celu odczytu wpisu tajnego z usługi Key Vault](quick-create-net.md).
