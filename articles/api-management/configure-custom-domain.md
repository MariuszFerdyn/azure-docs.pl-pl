---
title: Konfigurowanie niestandardowej nazwy domeny dla swojego wystąpienia usługi Azure API Management | Dokumentacja firmy Microsoft
description: W tym temacie opisano, jak skonfigurować niestandardową nazwę domeny dla swojego wystąpienia usługi Azure API Management.
services: api-management
documentationcenter: ''
author: vladvino
manager: anneta
editor: ''
ms.service: api-management
ms.workload: integration
ms.topic: article
ms.date: 12/14/2017
ms.author: apimpm
ms.openlocfilehash: f613995dbdd787d0a031cb2c24d67c682b2d7cec
ms.sourcegitcommit: 5aed7f6c948abcce87884d62f3ba098245245196
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/28/2018
ms.locfileid: "52446380"
---
# <a name="configure-a-custom-domain-name"></a>Konfigurowanie niestandardowej nazwy domeny 

Podczas tworzenia wystąpienia usługi API Management (APIM), platforma Azure przypisuje go do poddomeny azure-api.net (na przykład `apim-service-name.azure-api.net`). Jednakże, należy udostępnić punktami końcowymi usługi APIM, przy użyciu własnej nazwy domeny, takich jak **contoso.com**. W tym samouczku przedstawiono sposób mapowania istniejącej niestandardowej nazwy DNS do punktów końcowych udostępnianych przez wystąpienie usługi Azure API Management.

> [!WARNING]
> Klienci, którzy mają być używane przypinania certyfikatu, aby poprawić bezpieczeństwo swoich aplikacji, należy użyć niestandardowej nazwy domeny > i certyfikatu, który zarządza, nie domyślnego certyfikatu. Klienci, którzy przypiąć domyślnego certyfikatu zamiast tego będzie > zależna twardych we właściwościach certyfikatu nie kontrolują one, który nie jest zalecanym rozwiązaniem.

## <a name="prerequisites"></a>Wymagania wstępne

Aby wykonać kroki opisane w tym artykule, musisz mieć:

+ Aktywna subskrypcja platformy Azure.

    [!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

+ Wystąpienie usługi APIM. Aby uzyskać więcej informacji, zobacz [Utwórz wystąpienie usługi Azure API Management](get-started-create-service-instance.md).
+ Nazwa domeny niestandardowej, którego właścicielem jest użytkownik. Nazwa domeny niestandardowej, którego chcesz użyć, należy kupowane niezależnie i hostowany na serwerze DNS. W tym temacie nie daje instrukcje na temat sposobu hostowania niestandardowej nazwy domeny.
+ Musi mieć ważny certyfikat przy użyciu klucza publicznego i prywatnego (. PLIK PFX). Podmiotu lub alternatywna nazwa podmiotu (SAN) musi być zgodna z nazwą domeny (umożliwia usługi APIM, oznacza bezpieczne Uwidacznianie adresy URL za pośrednictwem protokołu SSL).

[!INCLUDE [premium-dev-standard-basic.md](../../includes/api-management-availability-premium-dev-standard-basic.md)]

## <a name="use-the-azure-portal-to-set-a-custom-domain-name"></a>Użyj witryny Azure portal, aby ustawić niestandardową nazwę domeny

1. Przejdź do swojego wystąpienia usługi APIM w [witryny Azure portal](https://portal.azure.com/).
2. Wybierz **domeny niestandardowe i protokół SSL**.
    
    Istnieje wiele punktów końcowych, do których można przypisać niestandardową nazwę domeny. Obecnie dostępne są następujące punkty końcowe: 
    + **Serwer proxy** (wartość domyślna to: `<apim-service-name>.azure-api.net`), 
    + **Portal** (wartość domyślna to: `<apim-service-name>.portal.azure-api.net`),     
    + **Zarządzanie** (wartość domyślna to: `<apim-service-name>.management.azure-api.net`), 
    + **Menedżer sterowania usługami** (wartość domyślna to: `<apim-service-name>.scm.azure-api.net`).

    >[!NOTE]
    > Możesz zaktualizować wszystkie punkty końcowe lub niektóre z nich. Często klienci zaktualizować **Proxy** (ten adres URL jest używany do wywoływania interfejsu API dostępne za pośrednictwem usługi API Management) i **Portal** (portalu dla deweloperów adres URL). **Zarządzanie** i **SCM** punkty końcowe są używane wewnętrznie przez klientów usługi APIM i dlatego rzadziej przypisanych niestandardowej nazwy domeny.
3. Wybierz punkt końcowy, który chcesz zaktualizować. 
4. W oknie po prawej stronie kliknij **niestandardowe**.

    + W **niestandardowej nazwy domeny**, określ nazwę, której chcesz użyć. Na przykład `api.contoso.com`. <br/>Nazwy domen z symbolami wieloznacznymi (na przykład *. domena.com) są również obsługiwane.
    + W **certyfikatu**, podaj prawidłową. Plik PFX, który chcesz przekazać. 
    + Jeśli certyfikat jest zabezpieczony hasłem, wprowadź go w **hasło** pola.
1. Kliknij przycisk Zastosuj.

    >[!NOTE]
    >Proces przypisywania certyfikatu może potrwać 15 minut lub dłużej w zależności od rozmiaru wdrożenia. Deweloper jednostki SKU ma Przestój, podstawowa i wyższych wersji bez przestojów.

[!INCLUDE [api-management-custom-domain](../../includes/api-management-custom-domain.md)]

## <a name="next-steps"></a>Kolejne kroki

[Uaktualnij i zmieniać skalę swojej usługi](upgrade-and-scale.md)
