---
title: Uaktualnianie narzędzia Azure Dev miejsca do magazynowania | Dokumentacja firmy Microsoft
titleSuffix: Azure Dev Spaces
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.subservice: azds-kubernetes
author: zr-msft
ms.author: zarhoads
ms.date: 07/03/2018
ms.topic: article
ms.technology: azds-kubernetes
description: Szybkie tworzenie w środowisku Kubernetes za pomocą kontenerów i mikrousług na platformie Azure
keywords: Docker, Kubernetes, Azure, AKS, Azure Container Service, containers
ms.openlocfilehash: ad4c608d773dd6838fa95ab05c59e09c29906f8a
ms.sourcegitcommit: 698a3d3c7e0cc48f784a7e8f081928888712f34b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/31/2019
ms.locfileid: "55476489"
---
# <a name="how-to-upgrade-azure-dev-spaces-tools"></a>Uaktualnianie narzędzia Azure Dev miejsca do magazynowania

Jeśli już używasz usługi Azure Dev miejsca do magazynowania ma nowej wersji, może być konieczne uaktualnienie narzędzia klienta usługi Azure Dev miejsca do magazynowania.

## <a name="update-the-azure-cli"></a>Aktualizowanie interfejsu wiersza polecenia platformy Azure

Po zaktualizowaniu najnowszego interfejsu wiersza polecenia platformy Azure, możesz także uzyskać najnowszą wersję rozszerzenie interfejsu wiersza polecenia deweloperów miejsca do magazynowania.

Nie musisz odinstalować poprzednią wersję, po prostu znajdowanie odpowiednich pobieranie w [wiersza polecenia platformy Azure](/cli/azure/install-azure-cli?view=azure-cli-latest).


## <a name="update-the-dev-spaces-cli-extension-and-command-line-tools"></a>Aktualizuj rozszerzenie interfejsu wiersza polecenia deweloperów miejsca do magazynowania i narzędzi wiersza polecenia

Uruchom następujące polecenie:

```cmd
az aks use-dev-spaces -n <your-aks-cluster> -g <your-aks-cluster-resource-group> --update
```

## <a name="update-the-vs-code-extension"></a>Aktualizuj rozszerzenie programu VS Code

Po zainstalowaniu rozszerzenia jest aktualizowany automatycznie. Może być konieczne ponowne załadowanie rozszerzenia Aby korzystać z nowych funkcji. Otwórz w programie VS Code **rozszerzenia** okienku wybierz **miejsca do magazynowania Azure Dev** rozszerzenia i wybierz polecenie **Załaduj ponownie**.

## <a name="update-the-visual-studio-extension"></a>Aktualizuj rozszerzenie programu Visual Studio

Podobnie jak inne rozszerzenia i aktualizacje, Visual Studio otrzymasz powiadomienie, gdy aktualizacja jest dostępna dla Visual Studio Tools dla platformy Kubernetes, w tym usługi Azure Dev miejsca do magazynowania. Poszukaj ikony flagi w górnym prawym rogu ekranu.

Aby zaktualizować narzędzia programu Visual Studio, wybierz opcję **Narzędzia > rozszerzenia i aktualizacje** menu elementu, a po lewej stronie wybierz **aktualizuje**. Znajdź **Visual Studio Tools dla platformy Kubernetes** i wybierz polecenie **aktualizacji** przycisku.

## <a name="next-steps"></a>Kolejne kroki

Tworzenie nowego klastra, aby przetestować się nowych narzędzi. Spróbuj przewodników Szybki Start i samouczków w [miejsca do magazynowania Azure Dev](/azure/dev-spaces).

> [!WARNING]
> Azure Dev miejsca do magazynowania w istniejących klastrach będzie nie można od razu poprawić, dlatego należy upewnić się, że używasz najnowszej wersji we wszystkich wdrożeniach platformy Azure, Utwórz nowy klaster po uaktualnieniu narzędzia.
