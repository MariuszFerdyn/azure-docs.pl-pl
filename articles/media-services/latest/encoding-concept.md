---
title: Kodowanie w chmurze za pomocą usługi Media Services — Azure | Dokumentacja firmy Microsoft
description: W tym temacie opisano proces kodowania, korzystając z usługi Azure Media Services
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.date: 02/17/2019
ms.author: juliako
ms.custom: seodec18
ms.openlocfilehash: 52e7fdf6de25300d4f78ee9822aca4ad83f646e9
ms.sourcegitcommit: 4bf542eeb2dcdf60dcdccb331e0a336a39ce7ab3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/19/2019
ms.locfileid: "56408429"
---
# <a name="encoding-with-media-services"></a>Kodowanie za pomocą usługi Media Services

Usługa Azure Media Services umożliwia kodowanie plików multimediów cyfrowych wysokiej jakości do formatów, które można odtwarzać na różnych przeglądarek i urządzeń. Na przykład może zaistnieć potrzeba strumieniowego odtwarzania treści w formatach HLS lub MPEG DASH firmy Apple. Ten temat zawiera wskazówki na temat kodowania zawartości za pomocą usługi Media Services v3.

Kodowanie za pomocą usługi Media Services v3, musisz utworzyć [Przekształcanie](https://docs.microsoft.com/rest/api/media/transforms) i [zadania](https://docs.microsoft.com/rest/api/media/jobs). Przekształcenie definiuje przepis na kodowania ustawień i danych wyjściowych, a zadanie jest wystąpieniem przepisu. Aby uzyskać więcej informacji, zobacz [transformacje i zadania](transforms-jobs-concept.md)

Podczas kodowania za pomocą usługi Media Services, umożliwia wstępne Poinformuj kodera w przetwarzaniu multimedialnych plików wejściowych. Na przykład można określić rozdzielczość wideo i/lub liczbę kanałów audio, który ma w zakodowanej zawartości. 

Użytkownik może szybko rozpocząć pracę z jedną z zalecanych wbudowane ustawienia wstępne, oparte na najlepszych branżowych rozwiązań lub można utworzyć niestandardowe ustawienie wstępne pod kątem określonych wymagań scenariusza lub urządzenia. Aby uzyskać więcej informacji, zobacz [kodowanie przy użyciu niestandardowej transformacji](customize-encoder-presets-how-to.md). 

Począwszy od stycznia 2019 r, podczas kodowania za pomocą usługi Media Encoder Standard do tworzenia plików w formacie MP4, nowy plik .mpi jest generowane i dodawane do wyjściowego elementu zawartości. Ten plik MPI ma na celu poprawę wydajności [funkcję dynamicznego tworzenia pakietów](dynamic-packaging-overview.md) i przesyłania strumieniowego scenariuszy.

> [!NOTE]
> Nie należy modyfikować lub usuń plik MPI lub wykonać żadnych zależności usługi o istnieniu (lub nie) z takiego pliku.

## <a name="built-in-presets"></a>Wbudowane ustawienia wstępne

Usługa Media Services obsługuje obecnie następujące wbudowane ustawienia wstępne kodowania:  

### <a name="builtinstandardencoderpreset-preset"></a>Ustawienie wstępne BuiltInStandardEncoderPreset

[BuiltInStandardEncoderPreset](https://docs.microsoft.com/rest/api/media/transforms/createorupdate#builtinstandardencoderpreset) służy do ustawiania wbudowaną ustawienie wstępne kodowania wejściowy plik wideo za pomocą kodera w warstwie standardowa. 

Obecnie obsługiwane są następujące ustawienia:

- **EncoderNamedPreset.AdaptiveStreaming** (zalecane). Aby uzyskać więcej informacji, zobacz [automatyczne generowanie drabiny szybkości transmisji bitów](autogen-bitrate-ladder.md).
- **EncoderNamedPreset.AACGoodQualityAudio** — tworzy pojedynczego pliku MP4, zawierający tylko dźwięk stereo zakodowane w 192 kb/s.
- **EncoderNamedPreset.H264MultipleBitrate1080p** — tworzy zbiór 8 wyrównane GOP pliki MP4 z, od 6000 KB/s do 400 KB/s i stereo AAC audio. Rozdzielczość rozpoczyna się od 1080p i prowadzi w dół do 360 p.
- **EncoderNamedPreset.H264MultipleBitrate720p** — tworzy zbiór 6 wyrównane GOP pliki MP4 z, od 3400 KB/s do 400 KB/s i stereo AAC audio. Rozdzielczość rozpoczyna się od 720p i prowadzi w dół do 360 p.
- **EncoderNamedPreset.H264MultipleBitrateSD** — tworzy zbiór 5 wyrównane GOP pliki MP4 z, od 1600 KB/s do 400 KB/s i stereo AAC audio. Rozdzielczość rozpoczyna się od 480p i prowadzi w dół do 360 p.<br/><br/>Aby uzyskać więcej informacji, zobacz [przekazywanie, kodowanie i przesyłanie strumieniowe plików](stream-files-tutorial-with-api.md).

### <a name="standardencoderpreset-preset"></a>Ustawienie wstępne StandardEncoderPreset

[StandardEncoderPreset](https://docs.microsoft.com/rest/api/media/transforms/createorupdate#standardencoderpreset) opisano ustawienia, które będą używane podczas kodowania wejściowy plik wideo za pomocą kodera w warstwie standardowa. Użyj tego ustawienia wstępnego podczas dostosowywania ustawień wstępnych transformacji. 

#### <a name="custom-presets"></a>Ustawienia niestandardowe

Usługa Media Services w pełni obsługuje dostosowywania wszystkie wartości w ustawieniach wstępnych w celu spełnienia specyficznych potrzeb kodowania i wymagań dotyczących usługi. Możesz użyć **StandardEncoderPreset** wstępnie ustawione podczas dostosowywania ustawień wstępnych transformacji. Aby uzyskać szczegółowe wyjaśnienie i przykład zobacz [Dostosowywanie ustawień wstępnych kodera](customize-encoder-presets-how-to.md).

## <a name="scaling-encoding-in-v3"></a>Skalowanie kodowania w wersji 3

Obecnie klienci mają używać witryny Azure portal lub interfejsów API w wersji 2 usługi Media Services do zestawu jednostek ru (zgodnie z opisem w [skalowanie przetwarzania multimediów](../previous/media-services-scale-media-processing-overview.md). 

## <a name="next-steps"></a>Kolejne kroki

* [Transformacje i zadania](transforms-jobs-concept.md)
* [Przekazywanie, kodowanie i przesyłanie strumieniowe przy użyciu usługi Media Services](stream-files-tutorial-with-api.md)
