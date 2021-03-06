---
title: Brama pola danych platformy Azure ogranicza | Dokumentacja firmy Microsoft
description: Opis ograniczeń systemowych i zalecane rozmiary Microsoft Azure Data Box Gateway.
services: databox
author: alkohli
ms.service: databox
ms.subservice: gateway
ms.topic: article
ms.date: 02/14/2019
ms.author: alkohli
ms.openlocfilehash: 34aac9a589516ace080906095ef3c14b34469bbd
ms.sourcegitcommit: f7be3cff2cca149e57aa967e5310eeb0b51f7c77
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/15/2019
ms.locfileid: "56311192"
---
# <a name="azure-data-box-gateway-limits-preview"></a>Limity bramy pola danych platformy Azure (wersja zapoznawcza)


Te limity wziąć pod uwagę wdrażania i obsługi rozwiązania Microsoft Azure Data Box Gateway. 

> [!IMPORTANT] 
> Usługa Data Box Gateway jest dostępna w wersji zapoznawczej. Przed wdrożeniem tego rozwiązania zapoznaj się z [warunkami użytkowania dotyczącymi wersji zapoznawczej](https://azure.microsoft.com/support/legal/preview-supplemental-terms/). 


## <a name="data-box-gateway-service-limits"></a>Limity usługi bramy pola danych

[!INCLUDE [data-box-edge-gateway-service-limits](../../includes/data-box-edge-gateway-service-limits.md)]

## <a name="data-box-gateway-device-limits"></a>Limity urządzeń bramy pola danych

W poniższej tabeli opisano limity dla urządzenia bramy pola danych.

| Opis | Wartość |
|---|---|
|Nie. pliki na urządzenie |100 milionów <br> Limit to ~ 25 milionów plików dla każdego 2 TB miejsca na dysku maksymalny limit na 100 mln |
|Nie. akcji na urządzenie |24 |
|Nie. udziałów na kontener usługi Azure storage |1 |
|Maksymalny rozmiar pliku zapisywane do udziału|Dla urządzenia wirtualnego 2 TB maksymalny rozmiar pliku wynosi 500 GB. <br> Maksymalny rozmiar pliku zwiększa się wraz z rozmiar dysku danych w poprzednim współczynnik aż do napotkania maksymalnie 5 TB. |

## <a name="azure-storage-limits"></a>Limity usługi Azure storage

[!INCLUDE [data-box-edge-gateway-storage-limits](../../includes/data-box-edge-gateway-storage-limits.md)]

## <a name="data-upload-caveats"></a>Przekazywanie danych do zastrzeżenia

[!INCLUDE [data-box-edge-gateway-storage-data-upload-caveats](../../includes/data-box-edge-gateway-storage-data-upload-caveats.md)]

## <a name="azure-storage-account-size-and-object-size-limits"></a>Rozmiar konta magazynu platformy Azure i obiekt ograniczeń rozmiarów

[!INCLUDE [data-box-edge-gateway-storage-acct-limits](../../includes/data-box-edge-gateway-storage-acct-limits.md)]

## <a name="azure-object-size-limits"></a>Limity rozmiaru obiektów platformy Azure

[!INCLUDE [data-box-edge-gateway-storage-object-limits](../../includes/data-box-edge-gateway-storage-object-limits.md)]

## <a name="next-steps"></a>Kolejne kroki

- [Przygotowywanie do wdrażania usługi Azure Data Box Gateway](data-box-gateway-deploy-prep.md)
