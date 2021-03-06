---
title: 'Szybki start: Uzyskiwanie odpowiedzi z bazy wiedzy przy użyciu narzędzia Postman — QnA Maker'
titlesuffix: Azure Cognitive Services
description: W tym samouczku Szybki start opisano sposób uzyskiwania odpowiedzi z bazy wiedzy przy użyciu narzędzia Postman.
services: cognitive-services
author: diberry
manager: nitinme
ms.service: cognitive-services
ms.subservice: qna-maker
ms.topic: quickstart
ms.date: 01/03/2019
ms.author: diberry
ms.openlocfilehash: a3d2d195614f0eab1b382e9a0967d921459ff553
ms.sourcegitcommit: 90cec6cccf303ad4767a343ce00befba020a10f6
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/07/2019
ms.locfileid: "55884107"
---
# <a name="quickstart-get-an-answer-from-knowledge-base-using-postman"></a>Szybki start: Uzyskiwanie odpowiedzi z bazy wiedzy przy użyciu narzędzia Postman

W tym samouczku Szybki start opisano sposób uzyskiwania odpowiedzi z bazy wiedzy przy użyciu narzędzia Postman.

## <a name="prerequisites"></a>Wymagania wstępne

* Najnowsza wersja narzędzia [**Postman**](https://www.getpostman.com/).
* Konieczne jest posiadanie [usługi QnA Maker](../How-To/set-up-qnamaker-service-azure.md) oraz [bazy wiedzy zawierającej pytania i odpowiedzi](../Tutorials/create-publish-query-in-portal.md). 

## <a name="publish-to-get-endpoint"></a>Publikowanie w celu pobrania punktu końcowego

Aby wygenerować odpowiedź na pytanie z bazy wiedzy, [opublikuj](../How-to/publish-knowledge-base.md) bazę wiedzy.

## <a name="use-production-endpoint-with-postman"></a>Używanie produkcyjnego punktu końcowego z narzędziem Postman

Po opublikowaniu bazy wiedzy na stronie **Publikowanie** zostaną wyświetlone ustawienia żądania HTTP do generowania odpowiedzi. W widoku domyślnym są wyświetlane ustawienia wymagane do generowania odpowiedzi przy użyciu narzędzia [Postman](https://www.getpostman.com).

Żółte cyfry na poniższym obrazie wskazują, których par nazwa/wartość należy użyć w kolejnych krokach.

[![Publikowanie wyników](../media/qnamaker-quickstart-get-answer-with-postman/publish-settings.png)](../media/qnamaker-quickstart-get-answer-with-postman/publish-settings.png#lightbox)

Aby wygenerować odpowiedź za pomocą narzędzia Postman, wykonaj następujące czynności:

1. Otwórz narzędzie Postman. Jeśli zostanie wyświetlony monit o wybranie bloku konstrukcyjnego, wybierz blok konstrukcyjny **Żądanie podstawowe**. Jako **nazwę żądania** ustaw `Generate QnA Maker answer`, a jako nazwę **kolekcji** ustaw `Generate QnA Maker answers`. Jeśli nie chcesz zapisywać w kolekcji, wybierz przycisk **Anuluj**.
1. W obszarze roboczym wybierz metodę HTTP **POST**.

    [![W narzędziu Postman ustaw metodę POST](../media/qnamaker-quickstart-get-answer-with-postman/postman-select-post-method.png)](../media/qnamaker-quickstart-get-answer-with-postman/postman-select-post-method.png#lightbox)

1. Aby utworzyć pełny adres URL, połącz wartości HOST (n2 na obrazie) i Post (nr 1 na obrazie). Pełny przykładowy adres URL wygląda następująco: 

    `https://qnamaker-f0.azurewebsites.net/qnamaker/knowledgebases/e1115f8c-d01b-4698-a2ed-85b0dbf3348c/generateAnswer`

    [![W narzędziu Postman ustaw pełny adres URL](../media/qnamaker-quickstart-get-answer-with-postman/set-postman-method-and-url.png)](../media/qnamaker-quickstart-get-answer-with-postman/set-postman-method-and-url.png#lightbox)

1. Wybierz kartę **Nagłówki** pod adresem URL, a następnie wybierz pozycję **Edycja zbiorcza**. 

1. Skopiuj nagłówki (nr 3 i 4 na obrazie) do obszaru tekstu.

    [![W narzędziu Postman ustaw nagłówki](../media/qnamaker-quickstart-get-answer-with-postman/set-postman-headers.png)](../media/qnamaker-quickstart-get-answer-with-postman/set-postman-headers.png#lightbox).

1. Wybierz kartę **Treść**.
1. Wybierz format **raw** i wprowadź wartość JSON (nr 5 na obrazie) reprezentującą pytanie.

    `{"question":"How do I programmatically update my Knowledge Base?"}`

    [![W narzędziu Postman ustaw wartość JSON treści](../media/qnamaker-quickstart-get-answer-with-postman/set-postman-body-json-value.png)](../media/qnamaker-quickstart-get-answer-with-postman/set-postman-body-json-value.png#lightbox).

1. Kliknij przycisk **Wyślij**.
1. Odpowiedź zawiera odpowiedź oraz inne informacje, które mogą być istotne dla aplikacji klienckiej. 

    [![W narzędziu Postman ustaw wartość JSON treści](../media/qnamaker-quickstart-get-answer-with-postman/receive-postman-response.png)](../media/qnamaker-quickstart-get-answer-with-postman/receive-postman-response.png#lightbox).

## <a name="use-staging-endpoint"></a>Korzystanie z przejściowego punktu końcowego

Aby uzyskać odpowiedź z przejściowego punktu końcowego, dołącz adres URL z parametrem logicznym ciągu kwerendy `isTest` o wartości `true`.

`?isTest=true`

## <a name="next-steps"></a>Następne kroki

Strona publikowania zawiera również informacje dotyczące [generowania odpowiedzi](get-answer-from-kb-using-curl.md) przy użyciu programu cURL. 

> [!div class="nextstepaction"]
> [Korzystanie z metadanych podczas generowania odpowiedzi](../How-to/metadata-generateanswer-usage.md)
