---
title: Omówienie usługi Azure Resource Graph
description: Azure Resource Graph to usługa platformy Azure, która umożliwia wykonywanie złożonych zapytań o zasoby w odpowiedniej skali.
services: resource-graph
author: DCtheGeek
ms.author: dacoulte
ms.date: 02/06/2019
ms.topic: overview
ms.service: resource-graph
manager: carmonm
ms.openlocfilehash: 6b3bad4e4619f8909f5c6d71111b4fad9ddb3098
ms.sourcegitcommit: 359b0b75470ca110d27d641433c197398ec1db38
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/07/2019
ms.locfileid: "55813283"
---
# <a name="what-is-azure-resource-graph"></a>Co to jest usługa Azure Resource Graph

Azure Resource Graph to usługa platformy Azure, której celem jest rozszerzenie usługi Azure Resource Management, zapewniając wydajną i działającą eksplorację zasobów z możliwością wysyłania zapytań na dużą skalę we wszystkich subskrypcjach i grupach zarządzania, aby można było wydajnie zarządzać swoim środowiskiem. Te zapytania zapewniają następujące funkcje:

- Zdolność do wysyłania zapytań do zasobów przy użyciu złożonego filtrowania, grupowania i sortowania według właściwości zasobu.
- Zdolność do iteracyjnej eksploracji zasobów w oparciu o wymagania ładu i konwertowania wyrażenia wynikowego na definicję zasad.
- Zdolność do oceny wpływu stosowania zasad na ogromne środowisko chmury.

W tej dokumentacji każda funkcja zostanie szczegółowo omówiona.

> [!NOTE]
> Usługa Azure Resource Graph jest używana przez nowe środowisko przeglądania „Wszystkie zasoby” witryny Azure Portal. Jest ono zaprojektowane, aby ułatwić klientom zarządzanie środowiskami o dużej skali.

## <a name="how-does-resource-graph-complement-azure-resource-manager"></a>Jak usługa Resource Graph uzupełnia usługę Azure Resource Manager

Usługa Azure Resource Manager aktualnie wysyła dane do ograniczonej pamięci podręcznej zasobu, który udostępnia kilka pól zasobów, a w szczególności — nazwę zasobu, identyfikator, typ, grupę zasobów, subskrypcje i lokalizację. Wcześniej praca z różnymi właściwościami zasobu wymagała wywołania poszczególnych dostawców zasobów i zażądania szczegółów dotyczących właściwości dla każdego zasobu.

Za pomocą usługi Azure Resource Graph możesz uzyskać dostęp do tych właściwości, które zwracają dostawców zasobów, bez konieczności wykonywania poszczególnych wywołań do każdego dostawcy zasobów.

## <a name="the-query-language"></a>Język zapytań

Teraz, gdy lepiej rozumiesz, czym jest usługa Azure Resource Graph, przyjrzyjmy się bliżej temu, jak tworzyć zapytania.

Ważne jest zrozumienie, że język zapytań usługi Azure Resource Graph opiera się na [języku zapytań usługi Azure Data Explorer](../../data-explorer/data-explorer-overview.md).

Po pierwsze, aby poznać szczegółowe informacje dotyczące operacji i funkcji, które mogą być używane z usługą Azure Resource Graph, zobacz [język zapytań usługi Resource Graph](./concepts/query-language.md). Aby przejrzeć zasoby, zobacz [badanie zasobów](./concepts/explore-resources.md).

## <a name="permissions-in-azure-resource-graph"></a>Uprawnienia w usłudze Azure Resource Graph

Aby użyć usługi Resource Graph, musisz mieć odpowiednie prawa w [kontroli dostępu na podstawie ról](../../role-based-access-control/overview.md) (RBAC) dające co najmniej dostęp do odczytu do zasobów, które chcesz zbadać. Bez uprawnień do obiektu lub grupy obiektów platformy Azure na poziomie co najmniej `read` wyniki nie będą zwracane.

## <a name="throttling"></a>Ograniczanie przepływności

Zapytania kierowane do usługi Resource Graph są ograniczane, aby zapewnić wszystkim klientom najlepsze środowisko i najkrótszy czas odpowiedzi. Jeśli Twoja organizacja chce używać interfejsu API usługi Resource Graph do obsługi częstych zapytań na dużą skalę, skorzystaj z pozycji „Opinia” w portalu z poziomu strony usługi Resource Graph. Koniecznie opisz swój przypadek biznesowy i zaznacz pole wyboru „Firma Microsoft może skontaktować się z Tobą pocztą e-mail w sprawie Twojej opinii”, aby zespół mógł się z Tobą skontaktować.

## <a name="running-your-first-query"></a>Uruchamianie pierwszego zapytania

Usługa Resource Graph obsługuje zarówno interfejs wiersza polecenia platformy Azure, jak i program Azure PowerShell. Struktura zapytania jest taka sama dla obu języków. Dowiedz się, jak włączyć usługę Resource Graph w [interfejsie wiersza polecenia platformy Azure](first-query-azurecli.md#add-the-resource-graph-extension) i [programie Azure PowerShell](first-query-powershell.md#add-the-resource-graph-module).

## <a name="next-steps"></a>Następne kroki

- Uruchamianie pierwszego zapytania za pomocą [interfejsu wiersza polecenia platformy Azure](first-query-azurecli.md)
- Uruchamianie pierwszego zapytania przy użyciu [programu Azure PowerShell](first-query-powershell.md)
- Rozpoczynanie od [zapytań dla początkujących](./samples/starter.md)
- Lepsze zrozumienie [zapytań zaawansowanych](./samples/advanced.md)