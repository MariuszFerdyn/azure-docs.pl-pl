---
title: Plik dyrektywy include
description: Plik dyrektywy include
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 03/21/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 21dbec52dded5a195cc764741ab9e8d79737c549
ms.sourcegitcommit: b3d74ce0a4acea922eadd96abfb7710ae79356e0
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/14/2019
ms.locfileid: "56247054"
---
1. Zaloguj się do subskrypcji platformy Azure za pomocą polecenia [az login](/cli/azure/) i postępuj zgodnie z instrukcjami wyświetlanymi na ekranie. Aby uzyskać więcej informacji na temat logowania się, zobacz artykuł [Rozpoczynanie pracy z interfejsem wiersza polecenia platformy Azure](/cli/azure/get-started-with-azure-cli).

   ```azurecli
   az login
   ```
2. Jeśli masz więcej niż jedną subskrypcję platformy Azure, wyświetl subskrypcje dla konta.

   ```azurecli
   az account list --all
   ```
3. Wskaż subskrypcję, której chcesz użyć.

   ```azurecli
   az account set --subscription <replace_with_your_subscription_id>
   ```
