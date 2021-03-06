---
title: Łączenie z innymi usługami podczas moderowanie zawartości — Content Moderator
titlesuffix: Azure Cognitive Services
description: Dowiedz się, jak dostęp do innych interfejsów API usługi Content Moderator przepływów pracy za pomocą łączników.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.subservice: content-moderator
ms.topic: article
ms.date: 01/10/2019
ms.author: sajagtap
ms.openlocfilehash: 5e56579a856f7b6259acddcbe34f2e5361505cb5
ms.sourcegitcommit: 95822822bfe8da01ffb061fe229fbcc3ef7c2c19
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/29/2019
ms.locfileid: "55217615"
---
# <a name="connect-to-other-cognitive-services"></a>Łączenie z innymi usługami cognitive

Usługa Azure Content Moderator przepływów pracy można użyć innych interfejsów API, oprócz Content Moderator interfejsów API. Możesz uzyskać dostęp do innych interfejsów API przy użyciu łącznika w pakiecie Content Moderator. Łącznik zawiera łącze do innych interfejsów API.

Pakiet Content Moderator obejmuje te łączniki domyślne:

* Interfejs API rozpoznawania emocji
* Interfejs API rozpoznawania twarzy
* Usługa w chmurze PhotoDNA

![Content Moderator dostępne łączniki.](images/connectors-1.png)

## <a name="verify-your-credentials"></a>Weryfikowanie poświadczeń 

Przed zdefiniowaniem przepływu pracy, upewnij się, czy masz prawidłowe poświadczenia dla łącznika interfejsu API, którego chcesz używać:

1.  Narzędzie do przeglądu pulpitu nawigacyjnego, wybierz **ustawienia** > **łączników**.

  ![Content Moderator wybierz łączników.](images/connectors-2.png)

2.  Wybierz **Edytuj** symbol obok łącznik, który chcesz zweryfikować poświadczeń.

  ![Pakiet Content Moderator wybierz symbol edycji](images/connectors-3.png)

3.  Zostanie wyświetlony klucz subskrypcji. Jeśli wprowadzisz zmiany, wybierz **Zapisz** po zakończeniu.

  ![Strona zawartości łączników Edytuj moderatora](images/connectors-4-1.png)
 
## <a name="add-a-connector"></a>Dodaj łącznik

1.  Przed dodaniem łącznika, potrzebujesz klucza subskrypcji. Narzędzie do przeglądu pulpitu nawigacyjnego, wybierz **ustawienia** > **poświadczenia**. Zaznacz i skopiuj wartość, która znajduje się w **Ocp-Admin-Subscription-Key** pole.

2.  Wybierz **łączników**. Wybierz jedną z dostępnych łączników, które są wyświetlane na narzędzie do przeglądu pulpitu nawigacyjnego. Następnie wybierz **Connect**. 

  ![Strona zawartości Moderator Dodaj łącznik](images/connectors-5.png)

3.  W **Ocp-Admin-Subscription-Key** pole, Wklej klucz, który został skopiowany. Następnie wybierz pozycję **Zapisz**.

## <a name="next-steps"></a>Kolejne kroki

* Dowiedz się, jak i używanie łączników do [Definiowanie niestandardowych przepływów pracy](workflows.md).
