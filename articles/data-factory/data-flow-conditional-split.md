---
title: Mapowanie transformacji warunkowego dzielenia przepływu danych w usłudze Azure Data Factory
description: Usługi Azure Data Factory danych przepływ warunkowego dzielenia transformacji
author: kromerm
ms.author: makromer
ms.reviewer: douglasl
ms.service: data-factory
ms.topic: conceptual
ms.date: 02/03/2019
ms.openlocfilehash: 9fe650465160ab837d8c8c191887d0f952976682
ms.sourcegitcommit: f715dcc29873aeae40110a1803294a122dfb4c6a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/14/2019
ms.locfileid: "56272011"
---
# <a name="azure-data-factory-mapping-data-flow-conditional-split-transformation"></a>Mapowanie transformacji warunkowego dzielenia przepływu danych w usłudze Azure Data Factory

[!INCLUDE [notes](../../includes/data-factory-data-flow-preview.md)]

Przekształcenie warunkowego dzielenia może kierować wiersze danych do różnych strumieni w zależności od zawartości danych. Implementację transformacji warunkowego dzielenia jest podobne do struktury decyzji wielkości liter w języku programowania. Przekształcenie daje w wyniku wyrażenia i na podstawie wyników, określa, że wiersz danych do określonego strumienia. Ta transformacja udostępnia również domyślne dane wyjściowe, tak, że jeśli wiersz odpowiada wyrażeniu nie zostaje skierowany do domyślne dane wyjściowe.

![Podziel warunkowego](media/data-flow/cd1.png "warunkowego dzielenia")

Aby dodać dodatkowe warunki, wybierz pozycję "Dodaj Stream" w dolnym okienku konfiguracji, a następnie kliknij przycisk w polu tekstowym Konstruktor wyrażeń do kompilacji w wyrażeniu.
