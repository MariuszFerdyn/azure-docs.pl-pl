---
title: Automatyczne inicjowanie obsługi użytkowników aplikacji SaaS w usłudze Azure AD | Dokumentacja firmy Microsoft
description: Wprowadzenie, jak używać usługi Azure AD, aby automatycznie aprowizować cofania aprowizacji i aktualizowane na bieżąco kont użytkowników dla wielu aplikacji SaaS innych firm.
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman
ms.service: active-directory
ms.subservice: app-mgmt
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/30/2018
ms.author: celested
ms.reviewer: asmalser
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3e8b099f845df66dfe8c43bc6f968fd63b30d09d
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56186356"
---
# <a name="automate-user-provisioning-and-deprovisioning-to-saas-applications-with-azure-active-directory"></a>Automatyzowanie użytkownika aprowizacji i cofania aprowizacji do aplikacji SaaS w usłudze Azure Active Directory

## <a name="what-is-automated-user-provisioning-for-saas-apps"></a>Co to jest automatyczna aprowizacja użytkowników dla aplikacji SaaS?
Azure Active Directory (Azure AD) pozwala zautomatyzować procesy tworzenia, obsługi i usuwania tożsamości użytkowników w chmurze ([SaaS](https://azure.microsoft.com/overview/what-is-saas/)) aplikacji, takich jak Dropbox, Salesforce, ServiceNow i nie tylko.

> [!VIDEO https://www.youtube.com/embed/_ZjARPpI6NI]

**Poniżej przedstawiono kilka przykładów co ta funkcja umożliwia to:**

* Automatycznie tworzyć nowych kont w systemach odpowiednie dla nowych użytkowników w celu dołączenia Twój zespół lub organizacja.
* Automatycznie Dezaktywuj kont w systemach odpowiednie w przypadku osób pozostawia zespołu lub organizacji.
* Upewnij się, że tożsamości w aplikacji i systemów są zawsze na bieżąco na podstawie zmian w katalogu lub systemie zarządzania zasobami ludzkimi.
* Udostępnianie obiektów niebędących użytkownikami, takich jak grupy do aplikacji, które je obsługują.

**Inicjowanie obsługi użytkowników automatycznych zawiera również następujące funkcje:**

* Możliwość dopasowania istniejących tożsamości między systemami źródłowym i docelowym.
* Mapowania atrybutów można dostosowywać, które określają, jakie dane użytkownika powinna przepływać z systemu źródłowego do systemu docelowego.
* Alerty e-mail opcjonalne do inicjowania obsługi błędów.
* Raportowanie i Dzienniki aktywności ułatwiające monitorowanie i rozwiązywanie problemów.

## <a name="why-use-automated-provisioning"></a>Dlaczego warto używać automatyczne Inicjowanie obsługi?

Niektóre typowe zresztą za używanie tej funkcji to:

* Unikanie kosztów, nieefektywności i błędu ludzkiego związanego z ręcznego procesu inicjowania obsługi administracyjnej.
* Unikanie kosztów związanych z udostępniania i utrzymywania niestandardowej inicjowania obsługi administracyjnej rozwiązania i skryptów.
* Aby zabezpieczyć Twoją organizację, natychmiastowe usuwanie tożsamości użytkowników z kluczowych aplikacjach SaaS, gdy opuszczają organizację.
* Łatwo zaimportować dużą liczbę użytkowników do określonej aplikacji SaaS lub systemu.
* Aby cieszyć się o jeden zestaw zasad, aby określić, kto jest aprowizowana i kto może się zalogować do aplikacji.

## <a name="how-does-automatic-provisioning-work"></a>Jak działa automatyczna aprowizacja?
    
**Inicjowania obsługi usługi programu Azure AD** aprowizuje użytkowników do aplikacji SaaS i innych systemów, łącząc się z punktów końcowych interfejsu API zarządzania użytkownika dostarczonego przez producenta każdej aplikacji. Te punkty końcowe interfejsu API zarządzania użytkownika umożliwia usłudze Azure AD, można programowo tworzyć, aktualizować i usuwać użytkowników. Wybrane aplikacje, które usługi aprowizacji można również tworzyć aktualizować i usuwać dodatkowe obiektów związanych z tożsamościami, takich jak grupy i role. 

![Inicjowanie obsługi administracyjnej](./media/user-provisioning/provisioning0.PNG)
*rysunek 1: Usługa inicjowania obsługi administracyjnej Azure AD*

![Wychodzące aprowizacji](./media/user-provisioning/provisioning1.PNG)
*rysunek 2: Użytkownik "Wychodzące" aprowizacja przepływu z usługi Azure AD do popularnych aplikacji SaaS*

![Dla ruchu przychodzącego aprowizacji](./media/user-provisioning/provisioning2.PNG)
*rysunek 3: "Dla ruchu przychodzącego" przepływu pracy aprowizacji użytkownika, z popularnymi aplikacjami ludzi Capital Management (HCM) do usługi Azure Active Directory i usługi Active Directory systemu Windows Server*


## <a name="what-applications-and-systems-can-i-use-with-azure-ad-automatic-user-provisioning"></a>Jakie aplikacje i systemy można używać z połączeniami usługi Azure AD automatyczna aprowizacja użytkowników?

Funkcje usługi Azure AD są wstępnie zintegrowane pomocy technicznej dla różnych popularnych aplikacji SaaS i systemami zarządzania zasobami ludzkimi, a także ogólne pomocy technicznej dla aplikacji, które implementują określonych części standard 2.0 Standard SCIM.

### <a name="pre-integrated-applications"></a>Wstępnie zintegrowane aplikacje

Aby uzyskać listę wszystkich aplikacji, dla którego usługa Azure AD obsługuje wstępnie zintegrowanych łącznika inicjowania obsługi administracyjnej, zobacz [lista samouczków aplikacji do obsługi administracyjnej użytkowników](../saas-apps/tutorial-list.md).

Skontaktuj się z usługą Azure AD inżynierii zespołu do żądania aprowizacji Obsługa dodatkowych aplikacji i przesłać wiadomość za pośrednictwem [forum opinii w usłudze Azure Active Directory](https://feedback.azure.com/forums/374982-azure-active-directory-application-requests/filters/new?category_id=172035).

> [!NOTE]
> Aby aplikacja do obsługi użytkowników automatyczne Inicjowanie obsługi administracyjnej jego Podaj Zarządzanie użytkownikami niezbędne interfejsy API, które umożliwiają automatyzację tworzenia, obsługi i usuwania użytkowników zewnętrznych programów. W związku z tym nie wszystkie aplikacje SaaS są zgodne z tą funkcją. W przypadku aplikacji, które obsługują interfejsy API umożliwiające zarządzanie użytkownika zespół inżynierów usługi Azure AD będzie można tworzyć inicjowania obsługi administracyjnej łącznika do tych aplikacji, a prac ma ustalone priorytety, zgodnie z potrzebami bieżącego i potencjalnych klientów. 

### <a name="connecting-applications-that-support-scim-20"></a>Łączenie aplikacji obsługujących standard SCIM w wersji 2.0

Aby uzyskać informacje dotyczące ogólnej połączyć aplikacje, które implementują Standard SCIM 2.0 — Zarządzanie użytkownikami na podstawie interfejsów API, zobacz [przy użyciu Standard SCIM, aby automatycznie aprowizować użytkowników i grup z usługi Azure Active Directory do aplikacji](use-scim-to-provision-users-and-groups.md).

    
## <a name="how-do-i-set-up-automatic-provisioning-to-an-application"></a>Jak skonfigurować automatycznej aprowizacji dla aplikacji?

> [!VIDEO https://www.youtube.com/embed/pKzyts6kfrw]

Konfiguracja programu Azure AD i usługi aprowizacji dla wybranej aplikacji, który rozpoczyna się  **[witryny Azure portal](https://portal.azure.com)**. W **usługi Azure Active Directory > aplikacje dla przedsiębiorstw** zaznacz **Dodaj**, następnie **wszystkich**, a następnie dodaj jedną z następujących czynności w zależności od scenariusza:

* Wszystkie aplikacje w **polecane aplikacje** sekcji pomocy technicznej automatycznej aprowizacji. Zobacz [lista samouczków aplikacji do obsługi administracyjnej użytkowników](../saas-apps/tutorial-list.md) dla dodatkowych reguł.

* Użyj opcji "aplikacji spoza galerii" niestandardowej integracji Standard SCIM

![Galeria](./media/user-provisioning/gallery.png)

Na ekranie zarządzania aplikacji aprowizacji jest skonfigurowana w **aprowizacji** kartę.

![Ustawienia](./media/user-provisioning/provisioning_settings0.PNG)


* **Poświadczenia administratora** musi być podana w usłudze Azure AD inicjowania obsługi usługi, która pozwoli na łączenie do zarządzania użytkownikami udostępniany przez aplikację interfejsu API. Ta sekcja umożliwia również włączyć powiadomienia e-mail, jeśli poświadczenia się nie powieść lub zadanie inicjowania obsługi administracyjnej przechodzi w stan [kwarantanny](#quarantine).

* **Mapowania atrybutów** można skonfigurować, określających, które pola w systemie źródłowym (przykład: Usługa Azure AD) będzie mieć ich zawartość synchronizowane z pola, które w systemie docelowym (przykład: ServiceNow). Jeśli aplikacja docelowa obsługuje tę funkcję, w tej sekcji pozwala opcjonalnie skonfigurować aprowizacji grup, oprócz kont użytkowników. "Dopasowania właściwości" pozwalają wybrać pola, które są używane do dopasowania kont między systemami. "[Wyrażeń](functions-for-customizing-application-data.md)" pozwalają na modyfikowanie i Przekształć wartościami pobranymi z systemu źródłowego, przed ich zapisaniu w systemie docelowym. Aby uzyskać więcej informacji, zobacz [Dostosowywanie mapowań atrybutów](customize-application-attributes.md).

![Ustawienia](./media/user-provisioning/provisioning_settings1.PNG)

* **Filtrami zakresu** poinformować usługę aprowizacji użytkowników i grup w systemie źródłowym powinny zostać aprowizowane i/lub anulowanie aprowizacji do systemu docelowego. Istnieją dwa aspekty filtrami, które są oceniane razem zakresu określające, który znajduje się w zakresie do inicjowania obsługi:

    * **Filtrować dane według wartości atrybutów** — menu "Zakres obiektów źródłowych" w mapowania atrybutów umożliwia filtrowanie według wartości określonych atrybutów. Na przykład można określić, że tylko użytkownicy z atrybutem "Dział" w "Sprzedaż" musi należeć do zakresu do inicjowania obsługi. Aby uzyskać więcej informacji, zobacz [przy użyciu filtrów określania zakresu](define-conditional-rules-for-provisioning-user-accounts.md).

    * **Filtr przypisania** — menu aprowizacji na "Scope" > sekcji ustawień portalu pozwala określić, czy tylko "przypisanych" użytkowników i grup powinny być w zakresie udostępniania, lub jeśli wszyscy użytkownicy w katalogu usługi Azure AD powinien Zainicjowano obsługę administracyjną. Aby uzyskać informacji na temat "przypisywanie" użytkowników i grup, zobacz [przypisać użytkownika lub grupy do aplikacji przedsiębiorstwa w usłudze Azure Active Directory](assign-user-or-group-access-portal.md).
    
* **Ustawienia** sterowania działaniem usługi aprowizacji dla aplikacji, w tym, czy jest ono aktualnie uruchomione, czy nie.

* **Dzienniki inspekcji** dostarczają informacji na temat każdej operacji wykonywane przez usługę Azure AD usługi aprowizacji. Aby uzyskać więcej informacji, zobacz [inicjowania obsługi administracyjnej Przewodnik po raportowaniu](check-status-user-account-provisioning.md).

![Ustawienia](./media/user-provisioning/audit_logs.PNG)

> [!NOTE]
> Usługa aprowizowania użytkowników w usłudze Azure AD mogą być również konfigurowane i zarządzane przy użyciu [interfejsu API Microsoft Graph](https://developer.microsoft.com/graph/docs/api-reference/beta/resources/synchronization-overview).


## <a name="what-happens-during-provisioning"></a>Co się dzieje podczas inicjowania obsługi?

Gdy usługa Azure AD jest w systemie źródłowym, korzysta z usługi aprowizacji [zapytanie różnicowe funkcji interfejsu API usługi Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-differential-query) do monitorowania, użytkowników i grup. Usługa aprowizowania uruchamia początkowej synchronizacji przed systemu źródłowego i docelowego systemu, a następnie okresowo synchronizacje przyrostowe. 

### <a name="initial-sync"></a>Synchronizacja początkowa

Po uruchomieniu usługi aprowizacji, pierwsza synchronizacja nigdy nie wykonał wykonują następujące czynności:

1. Zapytanie, wszyscy użytkownicy i grupy z systemu źródłowego podczas pobierania wszystkie atrybuty zdefiniowane w [mapowania atrybutów](customize-application-attributes.md).
2. Filtrowanie użytkowników i grup, zwrócone, przy użyciu dowolnej skonfigurowane [przypisania](assign-user-or-group-access-portal.md) lub [opartych na atrybutach filtrami zakresu](define-conditional-rules-for-provisioning-user-accounts.md).
3. Gdy użytkownik znajduje się do przypisania lub w zakresie udostępniania, usługa wysyła kwerendę do systemu docelowego, użytkownik pasującego przy użyciu wyznaczonej [pasujące atrybuty](customize-application-attributes.md#understanding-attribute-mapping-properties). Przykład: Jeśli nazwa userPrincipal w systemie źródłowym jest pasujący atrybut i mapuje nazwę użytkownika systemu docelowego, a następnie usługę aprowizacji wysyła zapytanie do systemu docelowego dla nazwy użytkownika, który pasuje do wartości nazwy userPrincipal w systemie źródłowym.
4. Jeśli użytkownik pasującego nie zostanie znaleziony w systemie docelowym, zostanie utworzony przy użyciu atrybutów zwracane z systemu źródłowego. Po utworzeniu konta użytkownika usługi aprowizacji wykrywa i buforuje identyfikator systemu docelowego dla nowego użytkownika, który jest używany do wykonywania wszystkich przyszłych operacji na tego użytkownika.
5. Jeśli użytkownik pasującego zostanie znaleziony, jest aktualizowany przy użyciu atrybutów udostępnianej przez system źródłowy. Po dopasowaniu konta użytkownika usługi aprowizacji wykrywa i buforuje identyfikator systemu docelowego dla nowego użytkownika, który jest używany do wykonywania wszystkich przyszłych operacji na tego użytkownika.
6. Jeśli mapowania atrybutów zawiera atrybuty "odwołanie", usługa wykonuje dodatkowe aktualizacje umożliwia tworzenie i łączenie przywoływane obiekty w systemie docelowym. Na przykład użytkownik może mieć z atrybutem "Manager" w systemie docelowym, który został połączony z innym użytkownikiem utworzony w systemie docelowym.
7. Znak wodny po zakończeniu początkowej synchronizacji znajdują się punkty wyjścia dotyczące kolejne synchronizacje przyrostowe są zachowywane.

Niektóre aplikacje, takie jak obsługa usługi ServiceNow, Google Apps i pole nie tylko aprowizacji użytkowników, ale również Inicjowanie obsługi administracyjnej grupy i ich elementów członkowskich. W takich przypadkach jeśli aprowizacji grupy jest włączona w [mapowania](customize-application-attributes.md), usługi aprowizacji synchronizuje użytkowników i grup, a następnie synchronizuje członkostwa w grupach. 

### <a name="incremental-syncs"></a>Synchronizacje przyrostowe

Po synchronizacji początkowej wszystkie kolejne synchronizacje wykonują następujące czynności:

1. Kwerendy systemie źródłowym żadnych użytkowników i grup, które zostały zaktualizowane od czasu ostatniego znaku wodnego została zapisana.
2. Filtrowanie użytkowników i grup, zwrócone, przy użyciu dowolnej skonfigurowane [przypisania](assign-user-or-group-access-portal.md) lub [opartych na atrybutach filtrami zakresu](define-conditional-rules-for-provisioning-user-accounts.md).
3. Gdy użytkownik znajduje się do przypisania lub w zakresie udostępniania, usługa wysyła kwerendę do systemu docelowego, użytkownik pasującego przy użyciu wyznaczonej [pasujące atrybuty](customize-application-attributes.md#understanding-attribute-mapping-properties).
4. Jeśli użytkownik pasującego nie zostanie znaleziony w systemie docelowym, zostanie utworzony przy użyciu atrybutów zwracane z systemu źródłowego. Po utworzeniu konta użytkownika usługi aprowizacji wykrywa i buforuje identyfikator systemu docelowego dla nowego użytkownika, który jest używany do wykonywania wszystkich przyszłych operacji na tego użytkownika.
5. Jeśli użytkownik pasującego zostanie znaleziony, jest aktualizowany przy użyciu atrybutów udostępnianej przez system źródłowy. Jeśli jest nowo przypisani konta, który jest zgodny, usługę aprowizacji wykrywa i buforuje identyfikator systemu docelowego dla nowego użytkownika, który jest używany do wykonywania wszystkich przyszłych operacji na tego użytkownika.
6. Jeśli mapowania atrybutów zawiera atrybuty "odwołanie", usługa wykonuje dodatkowe aktualizacje umożliwia tworzenie i łączenie przywoływane obiekty w systemie docelowym. Na przykład użytkownik może mieć z atrybutem "Manager" w systemie docelowym, który został połączony z innym użytkownikiem utworzony w systemie docelowym.
7. Jeśli użytkownik, który został wcześniej w zakresie udostępniania zostanie usunięty z zakresu (w tym trwa nieprzypisane), usługa wyłącza użytkownika w systemie docelowym za pośrednictwem aktualizacji.
8. Jeśli użytkownik, który został wcześniej w zakresie udostępniania jest wyłączone lub usunięte nietrwale w systemie źródłowym, usługa wyłącza użytkownika w systemie docelowym za pośrednictwem aktualizacji.
9. Jeśli użytkownika, który był wcześniej w zakresie udostępniania jest całkowicie usunięty w systemie źródłowym, usługa usunie użytkownika w systemie docelowym. W usłudze Azure AD użytkownicy są całkowicie usunięty 30 dni po ich wszystkie usunięte nietrwale.
10. Utrwalanie nową wartością limitu na końcu synchronizacja przyrostowa, które znajdują się punkty wyjścia dotyczące kolejne synchronizacje przyrostowe.

>[!NOTE]
> Za pomocą Opcjonalnie można wyłączyć tworzenia, aktualizacji i operacje usuwania **docelowe Akcje obiektu** pola wyboru w [mapowania atrybutów](customize-application-attributes.md) sekcji. Logika wyłączenia użytkownika w trakcie aktualizacji również jest kontrolowany przez mapowanie atrybutu z polem, takie jak "accountEnabled".

Usługa aprowizowania będzie w dalszym ciągu przez czas nieokreślony, uruchom symetryczna synchronizacje przyrostowe w odstępach czasu zdefiniowanych w [samouczek specyficzne dla poszczególnych aplikacji](../saas-apps/tutorial-list.md), dopóki nie wystąpi jedno z następujących zdarzeń:

* Usługa została zatrzymana ręcznie przy użyciu witryny Azure portal lub za pomocą odpowiedniego polecenia interfejsu API programu Graph 
* Nowe synchronizacji początkowej jest wyzwalany przy użyciu **Wyczyść stan i uruchom ponownie** opcji w witrynie Azure portal lub za pomocą odpowiedniego polecenia interfejsu API programu Graph. Czyści wszystkie przechowywane znaku wodnego i powoduje, że wszystkie obiekty źródłowy ma zostać obliczone ponownie.
* Nowe synchronizacji początkowej zostanie wywołany z powodu zmiany atrybutów mapowania lub filtrów określania zakresu. To także czyści wszystkie przechowywane znaku wodnego i powoduje, że wszystkie obiekty źródłowy ma zostać obliczone ponownie.
* Proces inicjowania obsługi administracyjnej przechodzi do kwarantanny (patrz poniżej), ze względu na wysoki współczynnik błędów, a pozostaje w kwarantannie dla więcej niż czterech tygodni. W takiej sytuacji usługa zostanie automatycznie wyłączone.

### <a name="errors-and-retries"></a>Błędy i ponownych prób

Jeśli użytkownik nie dodane, zaktualizowane lub usunięte w systemie docelowym z powodu błędu w systemie docelowym, operacja zostanie ponowiona w następnym cyklu synchronizacji. Jeśli użytkownik nadal nie będzie działać, ponowne próby rozpoczną się się występują rzadziej, stopniowo skalowanie do tylko jednej próby dziennie. Aby rozwiązać błąd, Administratorzy muszą sprawdzić [dzienniki inspekcji](check-status-user-account-provisioning.md) dla "Przetwórz depozyt" spowodować, że zdarzenia w celu określenia katalogu głównego i podejmij odpowiednie działanie. Typowe błędy mogą obejmować:

* Użytkownicy nie mają atrybutu wypełnione w systemie źródłowym, który jest wymagany w systemie docelowym
* Użytkownicy mający wartość atrybutu w systemie źródłowym, dla których ma unikatowego ograniczenia w systemie docelowym i tę samą wartość znajduje się w innym rekord użytkownika

Te błędy można rozwiązać przez zmianę wartości atrybutów użytkownika w systemie źródłowym lub przez dostosowywanie mapowań atrybutów, aby nie powodować konflikty.   

### <a name="quarantine"></a>Kwarantanna

Większości lub wszystkich wywołań skierowanego do systemu docelowego stale się niepowodzeniem z powodu błędu (takie jak w przypadku poświadczeń Nieprawidłowa wartość pola administrator), a następnie zadanie inicjowania obsługi administracyjnej przechodzi w stan "kwarantanny". Jest to wskazywane w [aprowizacji raport z podsumowaniem](check-status-user-account-provisioning.md)i za pośrednictwem poczty e-mail, jeśli powiadomienia e-mail zostały skonfigurowane w witrynie Azure portal. 

W przypadku kwarantanny, częstotliwość synchronizacje przyrostowe jest stopniowo zmniejszać, aby raz dziennie. 

Zadanie inicjowania obsługi administracyjnej zostaną usunięte z kwarantanny po wszystkich błędów powodujący problemy, zostanie naprawiony, a następnie rozpoczyna się w następnym cyklu synchronizacji. Jeśli zadanie inicjowania obsługi administracyjnej pozostaje w kwarantannie przez więcej niż cztery tygodnie, zadanie inicjowania obsługi administracyjnej jest wyłączone.


## <a name="how-long-will-it-take-to-provision-users"></a>Jak długo potrwa inicjowania obsługi użytkowników?

Wydajność zależy od tego, czy wykonuje inicjowania obsługi administracyjnej zadania synchronizacji początkowej lub synchronizacja przyrostowa zgodnie z opisem w poprzedniej sekcji.

Aby uzyskać **początkowej synchronizacje**, czas zadania zależy od wielu czynników, takich jak liczba użytkowników i grup w zakresie udostępniania, a łączna liczba użytkowników i grup w systemie źródłowym. Wyczerpujący wykaz czynniki mające wpływ na wydajność synchronizacji początkowej są podsumowywane w dalszej części w tej sekcji.

Aby uzyskać **synchronizacje przyrostowe**, czas zadania zależy od liczby zmian wykrytych w tym cyklu synchronizacji. W przypadku mniej niż 5000 użytkownika lub zmiany członkostwa w grupie, zakończyć zadanie w jednej synchronizacji przyrostowych cyklu. 

Poniższa tabela podsumowuje godziny synchronizacji dla typowych scenariuszy inicjowania obsługi administracyjnej. W tych scenariuszach w systemie źródłowym jest usługa Azure AD i system docelowy jest aplikacją SaaS. Czas synchronizacji są uzyskiwane z analizy statystycznej zadania synchronizacji pod kątem aplikacji SaaS usługi ServiceNow, obszar roboczy, Salesforce i Google Apps.


| Konfiguracja zakresu | Użytkownicy, grupy i elementy członkowskie w zakresie | Czas synchronizacji początkowej | Czas synchronizacji przyrostowej |
| -------- | -------- | -------- | -------- |
| Synchronizuj przypisanych użytkowników i tylko grupy |  < 1,000 |  < 30 minut | < 30 minut |
| Synchronizuj przypisanych użytkowników i tylko grupy |  1000–10 000 | 142 - minut 708 | < 30 minut |
| Synchronizuj przypisanych użytkowników i tylko grupy |   10,000 - 100,000 | 1,170 - 2,340 minut | < 30 minut |
| Synchronizuj wszystkich użytkowników i grup w usłudze Azure AD |  < 1,000 | < 30 minut  | < 30 minut |
| Synchronizuj wszystkich użytkowników i grup w usłudze Azure AD |  1000–10 000 | < 30 – 120 minut | < 30 minut |
| Synchronizuj wszystkich użytkowników i grup w usłudze Azure AD |  10,000 - 100,000  | 713 - 1,425 minut | < 30 minut |
| Synchronizuj wszystkich użytkowników w usłudze Azure AD|  < 1,000  | < 30 minut | < 30 minut |
| Synchronizuj wszystkich użytkowników w usłudze Azure AD | 1000–10 000  | 43 - 86 minut | < 30 minut |


Dla konfiguracji **synchronizacji przypisane tylko grupy użytkowników i**, następujące formuły można użyć do określenia przybliżony minimalne i maksymalne, oczekiwano **początkowej synchronizacji** razy:

    Minimum minutes =  0.01 x [Number of assigned users, groups, and group members]
    Maximum minutes = 0.08 x [Number of assigned users, groups, and group members] 
    
Podsumowanie czynniki wpływające na czas potrzebny do ukończenia **początkowej synchronizacji**:

* Całkowita liczba użytkowników i grup w zakresie udostępniania.

* Całkowita liczba użytkowników, grup i członków grupy obecne w systemie źródłowym (Azure AD).

* Określa, czy użytkownicy w zakresie udostępniania są dopasowywane do istniejących użytkowników w aplikacji docelowej lub konieczne będzie utworzenie po raz pierwszy. Zadania synchronizacji, dla których wszyscy użytkownicy są tworzone po raz pierwszy, potrwa około *dwa razy dłużej* synchronizacji jako zadania, dla których wszyscy użytkownicy są dopasowywane do istniejących użytkowników.

* Liczba błędów w [dzienniki inspekcji](check-status-user-account-provisioning.md). Wydajność jest niższa, jeśli ma wiele błędów i usługi aprowizacji włożono w stan kwarantanny.    

* Żądanie, limitów szybkości i ograniczania przepustowości zaimplementowana przez system docelowy. Niektóre systemy docelowe zaimplementować żądania limitów szybkości i ograniczania przepustowości, co może mieć wpływ na wydajność podczas operacji synchronizacji dużej. W tych warunkach aplikację, która odbiera zbyt wiele żądań zbyt szybko może spowolnić jej wskaźnika odpowiedzi lub zamknąć połączenie. Aby zwiększyć wydajność, łącznik wymaga dostosowania przez nie wysyła szybciej niż aplikacji mogły je przetwarzać żądań aplikacji. Inicjowania obsługi administracyjnej łączniki utworzone przez firmę Microsoft, należy to dostosowanie. 

* Liczby i rozmiarów przypisanych grup. Trwa synchronizowanie przydzielonych grup trwa dłużej niż synchronizowaniem użytkowników. Liczba i rozmiary przypisanych grup obniżenie wydajności. Jeśli aplikacja ma [mapowania włączone do celów synchronizacji obiektu grupy](customize-application-attributes.md#editing-group-attribute-mappings)właściwości grupy, takie jak nazwy grup i członkostw są synchronizowane oprócz użytkowników. Te dodatkowe synchronizacje będzie trwać dłużej niż tylko synchronizacja obiektów użytkowników.


## <a name="how-can-i-tell-if-users-are-being-provisioned-properly"></a>Jak sprawdzić, jeśli użytkownicy są aprowizowane prawidłowo?

Wszystkie operacje wykonywane przez użytkownika usługi aprowizacji są rejestrowane w usłudze Azure AD dzienniki inspekcji. Dotyczy to wszystkich operacji wprowadzone w systemach źródłowych i docelowych, jakie dane użytkownika został odczytywanych lub zapisywanych podczas każdej operacji odczytu i zapisu.

Aby uzyskać informacji na temat sposobu odczytu, dzienniki inspekcji, w witrynie Azure portal, zobacz [inicjowania obsługi administracyjnej Przewodnik po raportowaniu](check-status-user-account-provisioning.md).


## <a name="how-do-i-troubleshoot-issues-with-user-provisioning"></a>Jak rozwiązywać problemy z aprowizowaniem użytkowników?

Na podstawie scenariusza wskazówki na temat rozwiązywania problemów automatycznej aprowizacji użytkowników w temacie [problemy z konfigurowaniem i aprowizowaniem użytkowników z aplikacją](application-provisioning-config-problem.md).


## <a name="what-are-the-best-practices-for-rolling-out-automatic-user-provisioning"></a>Jakie są najlepsze rozwiązania dotyczące wdrażania programów automatyczna aprowizacja użytkowników?

> [!VIDEO https://www.youtube.com/embed/MAy8s5WSe3A]

Aby uzyskać przykładowe wdrożenie krok po kroku planowanie Inicjowanie obsługi ruchu wychodzącego użytkowników do aplikacji, zobacz [tożsamości — przewodnik wdrażania dla aprowizacji użytkowników](https://aka.ms/userprovisioningdeploymentplan).

## <a name="more-frequently-asked-questions"></a>Więcej często zadawanych pytań

### <a name="does-automatic-user-provisioning-to-saas-apps-work-with-b2b-users-in-azure-ad"></a>Jest automatyczna aprowizacja użytkowników na działanie aplikacji SaaS przy użyciu użytkowników B2B w usłudze Azure AD?

Tak, jest możliwe przy użyciu poświadczeń użytkownika usługi Azure AD inicjowania obsługi użytkowników usługi do aprowizacji B2B (lub gościa) w usłudze Azure AD z aplikacjami SaaS.

Jednak dla użytkowników B2B móc zalogować się do aplikacji SaaS przy użyciu usługi Azure AD, aplikacja SaaS musi mieć jej opartej na SAML pojedynczego logowania jednokrotnego skonfigurowano możliwość w określony sposób. Aby uzyskać więcej informacji na temat konfigurowania aplikacji SaaS w celu obsługi logowania użytkowników B2B, zobacz [aplikacje SaaS skonfigurować współpracę B2B dzięki]( https://docs.microsoft.com/azure/active-directory/b2b/configure-saas-apps).

### <a name="does-automatic-user-provisioning-to-saas-apps-work-with-dynamic-groups-in-azure-ad"></a>Jest automatyczna aprowizacja użytkowników na działanie aplikacji SaaS z grupami dynamicznymi w usłudze Azure AD?

Tak. Gdy skonfigurowany do "Synchronizuj tylko przypisanych użytkowników i grupy", usługa aprowizowania użytkowników w usłudze Azure AD można udostępnić lub anulować obsługę użytkowników w aplikacji SaaS w oparciu o informację, czy są oni członkami [grupy dynamicznej](../users-groups-roles/groups-create-rule.md). Grupy dynamiczne również działać przy użyciu opcji "Synchronizuj wszystkich użytkowników i grupy".

Jednak użycie grup dynamicznych może mieć wpływ na ogólną wydajność end-to-end Inicjowanie obsługi użytkowników z usługi Azure AD z aplikacjami SaaS. Podczas korzystania z grup dynamicznych, należy pamiętać te zastrzeżenia i zalecenia:

* Jak zainicjowano obsługę administracyjną lub anulowanie aprowizacji w aplikacji SaaS fast użytkownika w grupie dynamicznej są zależy od tego, jak szybko ocenić zmiany członkostwa grupy dynamicznej. Aby uzyskać informacje na temat sprawdzić stan przetwarzania grupy dynamicznej, zobacz [sprawdzić stan przetwarzania reguły członkostwa](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-create-rule#check-processing-status-for-a-membership-rule).

* Podczas korzystania z grup dynamicznych, zasad musi być starannie przemyślane użytkownikowi aprowizację i cofanie aprowizacji, pamiętając, ponieważ spowoduje utratę członkostwa anulowania obsługi zdarzeń.

### <a name="does-automatic-user-provisioning-to-saas-apps-work-with-nested-groups-in-azure-ad"></a>Jest automatyczna aprowizacja użytkowników na działanie aplikacji SaaS przy użyciu zagnieżdżonych grup w usłudze Azure AD?

Nie. Po skonfigurowaniu "Synchronizuj tylko przypisanych użytkowników i grup" Usługa aprowizowania użytkowników w usłudze Azure AD nie będzie mógł odczytać lub inicjowania obsługi użytkowników, które znajdują się w grupach zagnieżdżonych. Jest tylko możliwość odczytu i zainicjowanie obsługi administracyjnej użytkowników należących do natychmiastowego grupy jawnie przypisane.

Jest to ograniczenie "oparte na grupach przypisania do aplikacji", która także ma wpływ na logowanie jednokrotne i jest opisany w [przy użyciu grupy, aby zarządzać dostępem do aplikacji SaaS](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-saasapps ).

Jako obejście można należy jawnie przypisać (lub w inny sposób [zakresu z](https://docs.microsoft.com/azure/active-directory/manage-apps/define-conditional-rules-for-provisioning-user-accounts)) grupy zawierające użytkowników, którzy potrzebują do zainicjowania obsługi administracyjnej.

## <a name="related-articles"></a>Pokrewne artykuły:

* [Lista samouczków dotyczących integrowania aplikacji SaaS](../saas-apps/tutorial-list.md)
* [Dostosowywanie mapowań atrybutów dla aprowizacji użytkowników](customize-application-attributes.md)
* [Pisanie wyrażeń do mapowania atrybutów](functions-for-customizing-application-data.md)
* [Filtrów określania zakresu na potrzeby aprowizacji użytkownika](define-conditional-rules-for-provisioning-user-accounts.md)
* [Włączanie automatycznej aprowizacji użytkowników i grup z usługi Azure Active Directory do aplikacji przy użyciu SCIM](use-scim-to-provision-users-and-groups.md)
* [Omówienie synchronizacji interfejsu API w usłudze Azure AD](https://developer.microsoft.com/graph/docs/api-reference/beta/resources/synchronization-overview)
