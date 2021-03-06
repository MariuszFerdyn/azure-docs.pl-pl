---
title: Publikowanie bazy wiedzy
titleSuffix: QnA Maker - Azure Cognitive Services
description: Publikowanie bazy wiedzy jest ostatnim krokiem w zakresie udostępniania wiedzy jako punktu końcowego udzielenie odpowiedzi na pytanie. Podczas publikowania bazy wiedzy pytań i odpowiedzi zawartość bazy wiedzy przenosi się z Indeks testu do produkcji indeksu w usłudze Azure search.
services: cognitive-services
author: tulasim88
manager: nitinme
ms.service: cognitive-services
ms.subservice: qna-maker
ms.topic: article
ms.date: 12/11/2018
ms.author: tulasim
ms.custom: seodec18
ms.openlocfilehash: 585e5f8f955a405b08bef42588ab5caff71c7bba
ms.sourcegitcommit: 90cec6cccf303ad4767a343ce00befba020a10f6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/07/2019
ms.locfileid: "55865917"
---
# <a name="publish-a-knowledge-base-using-the-qna-maker-portal"></a>Publikowanie bazy wiedzy przy użyciu portalu narzędzia QnA Maker

Publikowanie bazy wiedzy jest ostatnim krokiem w zakresie udostępniania wiedzy jako punktu końcowego udzielenie odpowiedzi na pytanie do aplikacji klienta. 

Podczas publikowania bazy wiedzy pytań i odpowiedzi zawartość bazy wiedzy przenosi się z Indeks testu do produkcji indeksu w usłudze Azure search.

![Publikowanie prod Indeks testu](../media/qnamaker-how-to-publish-kb/publish-prod-test.png)

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F). 

## <a name="publish-a-knowledge-base"></a>Publikowanie bazy wiedzy

1. Po zakończeniu wprowadzania zmian w wiedzy wybierz **Publikuj** w górnym pasku nawigacyjnym. Maksymalnie przypisanej liczby baz wiedzy można publikować dla usługi Azure Search. 

    ![Publikowanie bazy wiedzy](../media/qnamaker-how-to-publish-kb/publish.png)

2. Wybierz **Publikuj** ponownie, aby zobaczyć szczegóły punktu końcowego, które mogą być używane w kodzie aplikacji lub dowolnemu botowi.

    ![Pomyślnie opublikowano bazy wiedzy](../media/qnamaker-how-to-publish-kb/publish-success.png)
    
## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Gdy skończysz z bazy wiedzy knowledge base, usuń go w portalu narzędzia QnA Maker.

## <a name="next-steps"></a>Kolejne kroki

> [!div class="nextstepaction"]
> [Przeprowadzić analizę bazy wiedzy](./get-analytics-knowledge-base.md)
