---
title: Opis sposobu użycia odwołania Twins cyfrowego Azure struktury Swagger | Dokumentacja firmy Microsoft
description: Zrozumienia sposobu używania Azure cyfrowego Twins Swagger dokumentację referencyjną.
author: kingdomofends
manager: alinast
ms.service: digital-twins
services: digital-twins
ms.topic: conceptual
ms.date: 12/31/2018
ms.author: adgera
ms.custom: seodec18
ms.openlocfilehash: 9a1d328f79405b14ffd84e07cb915566bd686c8e
ms.sourcegitcommit: 818d3e89821d101406c3fe68e0e6efa8907072e7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/09/2019
ms.locfileid: "54120958"
---
# <a name="azure-digital-twins-swagger-reference-documentation"></a>Dokumentacja platformy Azure cyfrowego Twins struktury Swagger

Każde elastycznie wystąpienie Twins cyfrowych platformy Azure zawiera swój własny automatycznie wygenerowaną dokumentację referencyjną struktury Swagger.

[Struktury swagger](https://swagger.io/), lub [OpenAPI](https://www.openapis.org/), łączy w sobie złożone informacje interfejsu API do zasobów odwołanie interakcyjne i niezależny od języka. Struktury swagger zawiera materiały referencyjne krytycznych, o których ładunki JSON, metody HTTP i punkty końcowe służące do wykonywania operacji dotyczących interfejsu API.

> [!IMPORTANT]
> Obsługa uwierzytelniania struktury Swagger jest tymczasowo wyłączona w publicznej wersji zapoznawczej.

## <a name="swagger-summary"></a>Podsumowanie swagger

Struktury swagger zawiera podsumowanie interaktywnego interfejsu API, który zawiera:

* Interfejs API i obiekt informacji o modelu.
* Punkty końcowe interfejsu API REST, określających, ładunki żądania wymagany, nagłówki, parametrów, kontekstu ścieżki i metody HTTP.
* Testowanie funkcji interfejsu API.
* Przykładowe informacje o odpowiedzi używany do sprawdzania poprawności i Potwierdź odpowiedzi HTTP.
* Informacje o kodzie błędu.

Struktury swagger jest wygodne narzędzie na potrzeby programowania i testowania wywołań do cyfrowego Twins zarządzania interfejsów API usługi Azure.

[!INCLUDE [Digital Twins Swagger](../../includes/digital-twins-swagger.md)]

## <a name="reference-material"></a>Materiały referencyjne

Automatycznie generowanych materiały referencyjne dla struktury Swagger zawiera krótkie podsumowanie dotyczące ważnych pojęć, dostępnych punktów końcowych interfejsu API zarządzania oraz opis każdego modelu obiektu ułatwiające projektowanie i testowanie.

Krótkie podsumowanie Opisuje interfejs API.

![Top struktury swagger][1]

Modele obiektów interfejsu API zarządzania są także wyświetlane.

![Modele struktury swagger][2]

Możesz wybrać każdego modelu obiektów uwzględnione na liście, aby uzyskać bardziej szczegółowe podsumowanie kluczowych atrybutów.

![Model struktury swagger][3]

Wygenerowany modele obiektów struktury Swagger są wygodne wyświetlić wszystkie dostępne Azure cyfrowego bliźniaczych reprezentacji [obiektów i interfejsów API](./concepts-objectmodel-spatialgraph.md). Deweloperzy mogą używać tego zasobu, podczas ich tworzenia rozwiązań na Twins cyfrowych platformy Azure.

## <a name="endpoint-summary"></a>Podsumowanie punktu końcowego

Struktury swagger zawiera również szczegółowe omówienie wszystkich punktów końcowych, które tworzą interfejsy API Management.

Każdy punkt końcowy, wymienionych obejmowały żądanie wymaganych informacji, takich jak:

* Wymagane parametry.
* Typy danych wymaganego parametru.
* Metoda HTTP, aby uzyskać dostęp do zasobu.

![Punkty końcowe programu swagger][4]

Aby wyświetlić bardziej szczegółowym omówieniem, wybierz poszczególne zasoby.

## <a name="use-swagger-to-test-endpoints"></a>Użyj platformy Swagger, aby przetestować punktów końcowych

Jednym z zaawansowane funkcje, jakie zapewnia struktury Swagger jest możliwość testowania punkt końcowy interfejsu API bezpośrednio w ramach dokumentacji interfejsu użytkownika.

Po wybraniu określonego punktu końcowego, zobacz **wypróbuj działanie rozwiązania**.

![Spróbuj struktury swagger][5]

Rozwiń tę sekcję, aby wyświetlić pola wejściowe dla wszystkich wymaganych i opcjonalnych parametrów. Wprowadź prawidłowe wartości, a następnie wybierz pozycję **Execute**.

![Nastąpiła struktury swagger][6]

Po wykonaniu testu, można sprawdzić poprawność danych odpowiedzi.

## <a name="swagger-response-data"></a>Dane odpowiedzi programu swagger

Każdy punkt końcowy, wymienionych obejmuje również dane treści odpowiedzi weryfikowanie programowania i testów. Te przykłady obejmują kodów stanu i chcesz zobaczyć, czy liczba pomyślnych żądań HTTP w formacie JSON.

![Odpowiedź struktury swagger][7]

Przykłady obejmują również kody błędów, aby ułatwić debugowanie lub ulepszenia niepowodzenie testów.

## <a name="swagger-oauth-20-authorization"></a>Struktury swagger autoryzacji OAuth 2.0

Aby dowiedzieć się więcej o testowaniu interaktywnie żądania chronione przez OAuth 2.0, zobacz [oficjalną dokumentacją](https://swagger.io/docs/specification/authentication/oauth2/).

> [!NOTE]
> Obsługa uwierzytelniania OAuth 2.0 jest tymczasowo wyłączona w publicznej wersji zapoznawczej.

## <a name="next-steps"></a>Kolejne kroki

- Dowiedz się więcej o modele obiektów Twins cyfrowych platformy Azure i wykres analizy przestrzennej, przeczytaj [zrozumieć Azure cyfrowego bliźniaczych reprezentacji obiektów modeli](./concepts-objectmodel-spatialgraph.md).

- Aby dowiedzieć się, jak można uwierzytelnić przy użyciu interfejsu API zarządzania, przeczytaj [Uwierzytelnij za pomocą interfejsów API](./security-authenticating-apis.md).

<!-- Images -->
[1]: media/how-to-use-swagger/swagger_management_top.PNG
[2]: media/how-to-use-swagger/swagger_management_models.PNG
[3]: media/how-to-use-swagger/swagger_management_model.PNG
[4]: media/how-to-use-swagger/swagger_management_endpoints.PNG
[5]: media/how-to-use-swagger/swagger_management_try.PNG
[6]: media/how-to-use-swagger/swagger_management_tried.PNG
[7]: media/how-to-use-swagger/swagger_management_response.PNG
