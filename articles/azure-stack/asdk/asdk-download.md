---
title: Pobierz i Wyodrębnij usługi Azure Stack Development Kit (ASDK) | Dokumentacja firmy Microsoft
description: W tym artykule opisano, jak pobierać i wyodrębniać usługi Azure Stack Development Kit (ASDK).
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2019
ms.author: jeffgilb
ms.reviewer: misainat
ms.lastreviewed: 08/10/2018
ms.openlocfilehash: 830a7ef1f25ea52959baf992274b5f7711b646b2
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56165414"
---
# <a name="download-and-extract-the-azure-stack-development-kit-asdk"></a>Pobierz i Wyodrębnij usługi Azure Stack Development Kit (ASDK)
Po upewnieniu się, że komputer hosta zestaw deweloperski spełnia wymagania podstawowe dotyczące instalowania ASDK, następnym krokiem jest Pobierz i Wyodrębnij pakiet wdrożeniowy ASDK, aby uzyskać Cloudbuilder.vhdx.

## <a name="download-the-asdk"></a>Pobierz ASDK
1. Przed rozpoczęciem pobierania, upewnij się, że komputer spełnia następujące wymagania wstępne:

  - Komputer musi mieć co najmniej 60 GB wolnego miejsca na dysku na czterech oddzielnych, identyczne logiczne dyski twarde dodatkowo na dysku systemu operacyjnego.
  - [.NET framework 4.6 (lub nowszy)](https://dotnet.microsoft.com/download/dotnet-framework-runtime/net46) musi być zainstalowany.

2. [Przejdź do strony wprowadzenie](https://azure.microsoft.com/overview/azure-stack/try/?v=try) gdzie można pobrać Azure Stack Development Kit, zapewniają szczegółowe informacje i kliknięcie **przesyłania**.
3. Pobierz i uruchom [narzędzia do sprawdzania wdrożenia dla usługi Azure Stack Development Kit](https://go.microsoft.com/fwlink/?LinkId=828735&clcid=0x409) skryptu narzędzia sprawdzania wymagań wstępnych. Ten skrypt autonomiczny przechodzi przez testy wstępne wykonywane przez Instalatora programu Azure Stack Development Kit. Zapewnia sposób, aby upewnić się, że spełniasz wymagania sprzętowe i programowe, przed pobraniem większy pakiet dla usługi Azure Stack Development Kit.
4. W obszarze **Pobierz oprogramowanie**, kliknij przycisk **Azure Stack Development Kit**.

  > [!NOTE]
  > Pobieranie ASDK (AzureStackDevelopmentKit.exe) wynosi około 10GB.

## <a name="extract-the-asdk"></a>Wyodrębnij ASDK
1. Po ukończeniu pobierania kliknij **Uruchom** można uruchomić ASDK samorozpakowujący się plik typu (AzureStackDevelopmentKit.exe).
2. Przejrzyj i zaakceptuj umowę licencyjną wyświetlanych z **umowy licencyjnej** strony kreatora samorozpakowujący się plik typu, a następnie kliknij przycisk **dalej**.
3. Zapoznaj się z informacjami instrukcji ochrony prywatności, które są wyświetlane na **ważna Uwaga** strony kreatora samorozpakowujący się plik typu, a następnie kliknij przycisk **dalej**.
4. Wybierz lokalizację plików instalacyjnych usługi Azure Stack, aby wyodrębnić na **wybierz lokalizację docelową** strony kreatora samorozpakowujący się plik typu, a następnie kliknij przycisk **dalej**. Domyślna lokalizacja to *bieżący folder*\Azure Stack Development Kit. 
5. Przejrzyj podsumowanie w lokalizacji docelowej **gotowy do wyodrębniania** strony kreatora samorozpakowujący się plik typu, a następnie kliknij przycisk **wyodrębnić** można wyodrębnić CloudBuilder.vhdx (około 28 GB) i Pliki ThirdPartyLicenses.rtf. Ten proces trwa trochę czasu.
6. Skopiuj lub Przenieś plik CloudBuilder.vhdx w folderze głównym dysku C:\ (C:\CloudBuilder.vhdx) na komputerze-hoście ASDK.

> [!NOTE]
> Po wyodrębnieniu plików, można usunąć. Plik EXE i. POJEMNIK plików, aby odzyskać miejsce na dysku twardym. Alternatywnie można utworzyć kopię zapasową tych plików, dzięki czemu nie trzeba pobrać pliki ponownie, jeśli będzie konieczne ponowne wdrożenie ASDK.


## <a name="next-steps"></a>Kolejne kroki
[Przygotuj komputer-host ASDK](asdk-prepare-host.md)