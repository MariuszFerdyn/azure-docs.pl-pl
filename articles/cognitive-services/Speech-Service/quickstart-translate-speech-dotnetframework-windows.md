---
title: 'Szybki start: tłumaczenie mowy, C# (.NET Framework Windows) — usługi mowy'
titleSuffix: Azure Cognitive Services
description: W tym przewodniku Szybki start utworzysz prostą aplikację .NET Framework do przechwytywania mowy użytkownika, tłumaczenia jej na inny język i przekazywania tekstu do wiersza polecenia. Ten przewodnik jest przeznaczony dla użytkowników systemu Windows.
services: cognitive-services
author: wolfma61
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: quickstart
ms.date: 12/13/2018
ms.author: erhopf
ms.openlocfilehash: db0ff8b8cc305bb9f7b4625cf060de72a5c7d276
ms.sourcegitcommit: fec0e51a3af74b428d5cc23b6d0835ed0ac1e4d8
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/12/2019
ms.locfileid: "56109796"
---
# <a name="quickstart-translate-speech-with-the-speech-sdk-for-net-framework"></a>Szybki start: tłumaczenie mowy przy użyciu zestawu SDK usługi Mowa dla platformy .NET Framework

W tym przewodniku Szybki start utworzysz prostą aplikację .NET Framework, która przechwytuje mowę użytkownika z mikrofonu komputera, tłumaczy tę mowę i transkrybuje przetłumaczony tekst do wiersza polecenia w czasie rzeczywistym. Ta aplikacja jest przeznaczona do uruchamiania w 64-bitowych systemach Windows i jest kompilowana przy użyciu [pakietu NuGet zestawu SDK usługi Mowa](https://aka.ms/csspeech/nuget) i programu Microsoft Visual Studio 2017.

Aby uzyskać pełną listę języków dostępnych na potrzeby tłumaczenia mowy, zapoznaj się z [listą obsługiwanych języków](language-support.md).

## <a name="prerequisites"></a>Wymagania wstępne

Ten przewodnik Szybki start wymaga następujących elementów:

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
* Klucz subskrypcji platformy Azure dla usługi Mowa. [Uzyskaj bezpłatnie](get-started.md).

## <a name="create-a-visual-studio-project"></a>Tworzenie projektu programu Visual Studio

[!INCLUDE [Create project ](../../../includes/cognitive-services-speech-service-create-speech-project-vs-csharp.md)]

## <a name="add-sample-code"></a>Dodawanie przykładowego kodu

1. Otwórz plik `Program.cs` i zastąp cały jego kod poniższym kodem.

    [!code-csharp[Quickstart Code](~/samples-cognitive-services-speech-sdk/quickstart/speech-translation/csharp-dotnet-windows/helloworld/Program.cs#code)]

1. W tym samym pliku zastąp ciąg `YourSubscriptionKey` kluczem subskrypcji.

1. Zastąp także ciąg `YourServiceRegion` [regionem](regions.md) skojarzonym z subskrypcją (na przykład `westus` w przypadku subskrypcji bezpłatnej wersji próbnej).

1. Zapisz zmiany w projekcie.

## <a name="build-and-run-the-app"></a>Kompilowanie i uruchamianie aplikacji

1. Skompiluj aplikację. Na pasku menu wybierz kolejno pozycje **Kompiluj** > **Kompiluj rozwiązanie**. Kod powinien zostać skompilowany bez błędów.

    ![Zrzut ekranu aplikacji Visual Studio z wyróżnioną opcją Kompiluj rozwiązanie](media/sdk/qs-csharp-dotnetcore-windows-05-build.png "Kompilacja ukończona pomyślnie")

1. Uruchom aplikację. Na pasku menu wybierz kolejno pozycje **Debuguj** > **Rozpocznij debugowanie** lub naciśnij klawisz **F5**.

    ![Zrzut ekranu aplikacji Visual Studio z wyróżnioną opcją Rozpocznij debugowanie](media/sdk/qs-csharp-dotnetcore-windows-06-start-debugging.png "Uruchamianie aplikacji do debugowania")

1. Zostanie wyświetlone okno konsoli z monitem o wypowiedzenie słów. Wypowiedz zwrot lub zdanie w języku angielskim. Mowa zostanie przesłana do usługi Mowa, przetłumaczona i przetranskrybowana na tekst, który zostanie wyświetlony w tym samym oknie.

    ![Zrzut ekranu przedstawiający dane wyjściowe konsoli po pomyślnym ukończeniu tłumaczenia](media/sdk/qs-translate-csharp-dotnetcore-windows-output.png "Dane wyjściowe konsoli po pomyślnym ukończeniu tłumaczenia")

## <a name="next-steps"></a>Następne kroki

Dodatkowe przykłady, dotyczące między innymi odczytywania mowy z pliku audio i zwracania przetłumaczonego tekstu jako syntetyzowanej mowy, są dostępne w usłudze GitHub.

> [!div class="nextstepaction"]
> [Zapoznaj się z przykładami dla języka C# w usłudze GitHub](https://aka.ms/csspeech/samples)

## <a name="see-also"></a>Zobacz też

- [Samouczek: tworzenie niestandardowego modelu akustycznego](how-to-customize-acoustic-models.md)
- [Samouczek: tworzenie niestandardowego modelu językowego](how-to-customize-language-model.md)
