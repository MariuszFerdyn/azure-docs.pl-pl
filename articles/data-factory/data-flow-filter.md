---
title: Mapowanie transformacji filtru przepływu danych w usłudze Azure Data Factory
description: Mapowanie transformacji filtru przepływu danych w usłudze Azure Data Factory
author: kromerm
ms.author: makromer
ms.reviewer: douglasl
ms.service: data-factory
ms.topic: conceptual
ms.date: 02/03/2019
ms.openlocfilehash: b7e7b123560aae3a2d3086c8536969297d31f7ba
ms.sourcegitcommit: f715dcc29873aeae40110a1803294a122dfb4c6a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/14/2019
ms.locfileid: "56271999"
---
# <a name="azure-data-factory-mapping-data-flow-filter-transformation"></a>Mapowanie transformacji filtru przepływu danych w usłudze Azure Data Factory

[!INCLUDE [notes](../../includes/data-factory-data-flow-preview.md)]

Przekształcenia filtru zapewnia filtrowanie wierszy. Twórz wyrażenia, który definiuje warunek filtru. Kliknij w polu tekstowym, aby uruchomić Kreatora wyrażeń. Wewnątrz Konstruktor wyrażeń kompilacji do kontroli wiersze, które z bieżącym strumienia danych mogą przechodzić przez (filtr) dalej transformację wyrażenie filtru.

Czyli filtru w kolumnie loan_status:

```
in([‘Default’, ‘Charged Off’, ‘Fully Paid’], loan_status).
```

Odfiltruj kolumnę roku, w wersji demonstracyjnej filmów:

```
year > 1980
```
