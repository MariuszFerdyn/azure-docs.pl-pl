---
title: Omówienie usługi Azure Blueprints
description: Azure Blueprints to usługa platformy Azure, która umożliwia tworzenie, definiowanie i wdrażanie artefaktów w środowisku platformy Azure.
services: blueprints
author: DCtheGeek
ms.author: dacoulte
ms.date: 02/01/2019
ms.topic: overview
ms.service: blueprints
manager: carmonm
ms.custom: mvc
ms.openlocfilehash: 7803ed99a61a9b4ad819da882daf38cbfd6fffe9
ms.sourcegitcommit: ba035bfe9fab85dd1e6134a98af1ad7cf6891033
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/01/2019
ms.locfileid: "55563375"
---
# <a name="what-is-azure-blueprints"></a>Czym jest usługa Azure Blueprints?

Usługę Azure Blueprints można porównać do planu, który pozwala inżynierowi lub architektowi naszkicować parametry projektu. Usługa ta umożliwia architektom chmury i centralnym grupom technologii informatycznych zdefiniowanie powtarzalnego zestawu zasobów platformy Azure, który implementuje standardy, wzorce i wymagania organizacji oraz jest z nimi zgodny. Usługa Azure Blueprints umożliwia zespołom programistów szybkie tworzenie i wdrażanie nowych środowisk z przekonaniem, że zostały one utworzone zgodnie z zasadami organizacji za pomocą zestawu wbudowanych składników — takich jak sieć — przyspieszających opracowywanie i dostarczanie.

Usługa Blueprints umożliwia deklaratywne organizowanie i wdrażanie różnych szablonów zasobów i innych artefaktów, takich jak:

- Przypisania ról
- Przypisania zasad
- Szablony usługi Azure Resource Manager
- Grupy zasobów

Usługa Azure Blueprints jest wspierana przez globalnie dystrybuowaną [usługę Azure Cosmos DB](../../cosmos-db/introduction.md).
Obiekty strategii są replikowane w wielu regionach świadczenia usługi Azure. Ta replikacja zapewnia małe opóźnienia, wysoką dostępność oraz spójny dostęp do obiektów strategii niezależnie od regionu, w którym usługa Blueprints wdraża Twoje zasoby.

## <a name="how-its-different-from-resource-manager-templates"></a>W czym różni się ona od szablonów usługi Resource Manager

Usługa została zaprojektowana w celu ułatwienia _konfiguracji środowiska_. Ta konfiguracja często składa się z zestawu grup zasobów, zasad, przypisań ról i wdrożeń szablonów usługi Resource Manager. Strategia usługi Blueprints to pakiet umożliwiający połączenie każdego z tych typów _artefaktów_ w jedną całość. Pakiety można tworzyć i kontrolować ich wersje — w tym za pośrednictwem potoku ciągłej integracji/ciągłego wdrażania. Każdy pakiet jest ostatecznie przypisywany do subskrypcji w ramach jednej operacji, którą można poddawać inspekcji i śledzić.

Prawie wszystkie elementy możliwe do uwzględnienia podczas wdrażania za pomocą usługi Blueprints można wdrożyć przy użyciu szablonów usługi Resource Manager. Szablony usługi Resource Manager są jednak dokumentami, które nie istnieją natywnie na platformie Azure — każdy z nich jest przechowywany lokalnie lub w kontroli źródła. Szablon jest używany na potrzeby wdrożenia jednego lub większej liczby zasobów platformy Azure, ale po wdrożeniu tych zasobów nie ma aktywnego połączenia z wykorzystanym szablonem ani relacji z nim.

Dzięki użyciu usługi Blueprints relacja między definicją strategii (to, co _powinno zostać_ wdrożone) i przypisaniem strategii (to, co _zostało_ wdrożone) jest zachowywana. To połączenie obsługuje ulepszone śledzenie i inspekcję wdrożeń. Strategie umożliwiają również uaktualnienie jednocześnie kilku subskrypcji, które są zarządzane przez tę samą strategię.

Nie ma potrzeby dokonywania wyboru między szablonem usługi Resource Manager i strategią. Każda strategia może zawierać dowolną liczbę _artefaktów_ szablonu usługi Resource Manager. Tego rodzaju pomoc oznacza, że podejmowane poprzednio wysiłki mające na celu utworzenie i utrzymanie biblioteki szablonów usługi Resource Manager można wykorzystywać wielokrotnie w usłudze Blueprints.

## <a name="how-its-different-from-azure-policy"></a>W czym różni się ona od usługi Azure Policy

Strategia to pakiet lub kontener umożliwiający tworzenie specyficznych dla kontekstu zestawów standardów, wzorców i wymagań dotyczących implementacji usług Azure Cloud Services, zabezpieczeń i projektów, które mogą zostać ponownie użyte w celu zachowania spójności i zgodności.

[Zasady](../policy/overview.md) to system z domyślnym zezwalaniem i wyraźnym zabranianiem, który jest skoncentrowany na właściwościach wdrażanych i istniejących już zasobów. Obsługuje on zarządzanie chmurą przez weryfikowanie, czy zasoby w ramach subskrypcji są zgodne z wymaganiami i standardami.

Uwzględnienie zasad w strategii umożliwia utworzenie odpowiedniego wzorca lub projektu podczas jej przypisywania. Dołączenie zasad gwarantuje, że w środowisku mogą być wprowadzane tylko zatwierdzone lub oczekiwane zmiany, co umożliwia ochronę stałej zgodności z intencją strategii.

Zasady mogą być dołączane jako jedne z wielu _artefaktów_ w definicji strategii. Strategie obsługują również używanie parametrów z zasadami i inicjatywami.

## <a name="blueprint-definition"></a>Definicja strategii

Strategia składa się z _artefaktów_. Usługa Blueprints obsługuje obecnie następujące zasoby jako artefakty:

|Zasób  | Opcje hierarchii| Opis  |
|---------|---------|---------|
|Grupy zasobów | Subskrypcja | Umożliwia utworzenie nowej grupy zasobów do użytku przez inne artefakty w ramach strategii.  Te zastępcze grupy zasobów umożliwiają organizowanie zasobów dokładnie w taką strukturę, jaka jest pożądana. Udostępniają one ogranicznik zakresu na potrzeby uwzględnionych zasad i artefakty przypisania roli oraz szablony usługi Azure Resource Manager. |
|Szablon usługi Azure Resource Manager | Subskrypcja, grupa zasobów | Szablony służą do tworzenia złożonych środowisk. Przykładowe środowiska: farma programu SharePoint, konfiguracja stanu usługi Azure Automation lub obszar roboczy usługi Log Analytics. |
|Przypisanie zasad | Subskrypcja, grupa zasobów | Umożliwia przypisanie zasad lub inicjatywy do subskrypcji, do której przypisano strategię. Zasady lub inicjatywa muszą znajdować się w zakresie lokalizacji definicji strategii. Jeśli zasady lub inicjatywa mają parametry, są one przypisywane podczas tworzenia strategii bądź podczas jej przypisywania. |
|Przypisanie roli | Subskrypcja, grupa zasobów | Dodawanie istniejącego użytkownika lub grupy do wbudowanej roli w celu zagwarantowania, że odpowiednie osoby zawsze będą mieć odpowiedni dostęp do zasobów. Przypisania ról mogą być definiowane dla całej subskrypcji lub mogą być zagnieżdżone w konkretnej grupie zasobów uwzględnionej w strategii. |

### <a name="blueprint-definition-locations"></a>Lokalizacje definicji strategii

Podczas tworzenia definicji strategii należy zdefiniować miejsce, w którym strategia zostanie zapisana. Strategie można zapisywać tylko w [grupie zarządzania](../management-groups/overview.md) lub subskrypcji, do której użytkownik ma dostęp jako **Współautor**. Jeśli lokalizacja znajduje się w grupie zarządzania, strategię można przypisać do dowolnej subskrypcji podrzędnej tej grupy zarządzania.

### <a name="blueprint-parameters"></a>Parametry strategii

Usługa Blueprints może przekazywać parametry do zasad/inicjatywy lub szablonu usługi Azure Resource Manager.
Podczas dodawania dowolnego _artefaktu_ do strategii autor decyduje o udostępnieniu zdefiniowanej wartości dla każdego przypisania strategii lub zezwoleniu, aby każde przypisanie strategii udostępniało wartość w czasie przypisywania. Dzięki tej elastyczności można zdefiniować wstępnie ustaloną wartość dla wszystkich zastosowań strategii lub umożliwić podjęcie decyzji w czasie przypisywania.

> [!NOTE]
> Strategia może mieć własne parametry, ale obecnie można je tworzyć tylko w przypadku, kiedy strategia jest generowana w interfejsie API REST, a nie za pomocą portalu.

Aby uzyskać więcej informacji, zobacz [parametry strategii](./concepts/parameters.md).

### <a name="blueprint-publishing"></a>Publikowanie strategii

Kiedy strategia jest tworzona po raz pierwszy, przyjmuje się, że jest w trybie **wersji roboczej**. Kiedy jest gotowa do przypisania, należy ją **opublikować**. Publikowanie wymaga zdefiniowania ciągu **wersji** (liter, cyfr i łączników o maksymalnej długości 20 znaków) wraz z opcjonalnymi **uwagami dotyczącymi zmian**. Dzięki zastosowaniu **wersji** przyszłe zmiany wprowadzone w strategii mogą być traktowane jako osobne wersje z możliwością ich przypisania. Obsługa wersji oznacza również, że różne **wersje** tej samej strategii można przypisać do jednej subskrypcji. Jeśli w strategii zostaną dokonane dodatkowe zmiany, **opublikowana** **wersja** będzie nadal istniała, podobnie jak **nieopublikowane zmiany**. Po zakończeniu wprowadzania zmian zaktualizowana strategia jest **publikowana** jako nowa unikatowa **wersja**, którą teraz również można przypisać.

## <a name="blueprint-assignment"></a>Przypisywanie strategii

Każdą **opublikowaną** **wersję** strategii można przypisać do istniejącej subskrypcji. W portalu domyślną **wersją** strategii jest ta, która została **opublikowana** jako ostatnia. Jeśli istnieją parametry artefaktów (lub parametry strategii), są one definiowane w procesie przypisania.

## <a name="permissions-in-azure-blueprints"></a>Uprawnienia w usłudze Azure Blueprints

Aby móc korzystać ze strategii, użytkownik musi mieć udzielone uprawnienia za pośrednictwem [kontroli dostępu opartej na rolach](../../role-based-access-control/overview.md). Aby użytkownik mógł tworzyć strategie, jego konto musi mieć następujące uprawnienia:

- `Microsoft.Blueprint/blueprints/write` — tworzenie definicji strategii
- `Microsoft.Blueprint/blueprints/artifacts/write` — tworzenie artefaktów w definicji strategii
- `Microsoft.Blueprint/blueprints/versions/write` — publikowanie strategii

Aby użytkownik mógł usuwać strategie, jego konto musi mieć następujące uprawnienia:

- `Microsoft.Blueprint/blueprints/delete`
- `Microsoft.Blueprint/blueprints/artifacts/delete`
- `Microsoft.Blueprint/blueprints/versions/delete`

> [!NOTE]
> Uprawnienia definicji strategii muszą zostać nadane lub odziedziczone w grupie zarządzania lub w zakresie subskrypcji, w których zostały zapisane.

Aby użytkownik mógł przypisywać strategie lub anulować ich przypisanie, jego konto musi mieć następujące uprawnienia:

- `Microsoft.Blueprint/blueprintAssignments/write` — przypisywanie strategii
- `Microsoft.Blueprint/blueprintAssignments/delete` — anulowanie przypisania strategii

> [!NOTE]
> Przypisania strategii są tworzone w ramach subskrypcji, dlatego uprawnienia przypisywania strategii lub anulowania takiego przypisania muszą zostać przyznane w zakresie subskrypcji bądź muszą być dziedziczone w zakresie subskrypcji.

Wszystkie powyższe uprawnienia są uwzględnione w roli **Właściciel**. Rola **Współautor** ma uprawnienia do tworzenia i usuwania uprawnień planu, ale nie ma uprawnień do przypisywania planu. Jeśli te wbudowane role nie spełniają wymagań dotyczących zabezpieczeń, należy rozważyć utworzenie [roli niestandardowej](../../role-based-access-control/custom-roles.md).

> [!NOTE]
> Jednostka usługi Azure Blueprint wymaga roli **Właściciel** dla przypisanej subskrypcji, aby można było włączyć wdrażanie. W przypadku korzystania z portalu ta rola jest automatycznie przyznawana i odwoływana dla wdrożenia. W przypadku korzystania z interfejsu API REST ta rola musi zostać ręcznie przyznana, ale jest automatycznie odwoływana po zakończeniu wdrożenia.

## <a name="next-steps"></a>Następne kroki

- [Tworzenie strategii — portal](create-blueprint-portal.md)
- [Tworzenie strategii — interfejs API REST](create-blueprint-rest-api.md)
