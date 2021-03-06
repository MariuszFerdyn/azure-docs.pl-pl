---
title: 'Samouczek: Integracja usługi Azure Active Directory za pomocą NetBenefits wierności | Dokumentacja firmy Microsoft'
description: Dowiedz się, jak skonfigurować logowanie jednokrotne między usługi Azure Active Directory i NetBenefits wierności.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 77dc8a98-c0e7-4129-ab88-28e7643e432a
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2018
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: bf7de6d0416c60f33f57fd83768fd23b0a09e0f1
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56184877"
---
# <a name="tutorial-azure-active-directory-integration-with-fidelity-netbenefits"></a>Samouczek: Integracja usługi Azure Active Directory za pomocą NetBenefits wierności

W tym samouczku dowiesz się, jak zintegrować NetBenefits jakości z usługi Azure Active Directory (Azure AD).

Integrowanie NetBenefits wierności z usługą Azure AD zapewnia następujące korzyści:

- Możesz kontrolować, czy w usłudze Azure AD, kto ma dostęp do NetBenefits wierności.
- Użytkowników, aby automatycznie uzyskać zalogowanych do NetBenefits wierności (logowanie jednokrotne) można włączyć za pomocą kont usługi Azure AD.
- Możesz zarządzać swoimi kontami w jednej centralnej lokalizacji — witrynie Azure Portal.

Jeśli chcesz dowiedzieć się więcej na temat integracji aplikacji SaaS z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD z NetBenefits wierności, potrzebne są następujące elementy:

- Subskrypcji usługi Azure AD
- NetBenefits wierności logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.

Aby przetestować czynności opisane w tym samouczku, należy postępować zgodnie z następującymi zaleceniami:

- Nie używaj środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko usługi Azure AD w wersji próbnej, możesz to zrobić [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza

W ramach tego samouczka można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.
Scenariusz opisany w tym samouczku składa się z dwóch głównych bloków konstrukcyjnych:

1. Dodawanie NetBenefits wierności z galerii
2. Konfigurowanie i testowania usługi Azure AD logowanie jednokrotne

## <a name="adding-fidelity-netbenefits-from-the-gallery"></a>Dodawanie NetBenefits wierności z galerii

Aby skonfigurować integrację NetBenefits wierność w usłudze Azure AD, należy dodać NetBenefits wierności z galerii z listą zarządzanych aplikacji SaaS.

**Aby dodać NetBenefits wierności z galerii, wykonaj następujące czynności:**

1. W **[witryny Azure portal](https://portal.azure.com)**, w panelu nawigacyjnym po lewej stronie kliknij pozycję **usługi Azure Active Directory** ikony.

    ![Przycisk usługi Azure Active Directory][1]

2. Przejdź do **aplikacje dla przedsiębiorstw**. Następnie przejdź do **wszystkie aplikacje**.

    ![W bloku aplikacji przedsiębiorstwa][2]

3. Aby dodać nową aplikację, kliknij przycisk **Nowa aplikacja** w górnej części okna dialogowego.

    ![Przycisk Nowa aplikacja][3]

4. W polu wyszukiwania wpisz **NetBenefits wierności**, wybierz opcję **NetBenefits wierności** z panelu wynik kliknięcie **Dodaj** przycisk, aby dodać aplikację.

    ![NetBenefits wierność na liście wyników](./media/fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie logowania jednokrotnego usługi Azure AD

W tej sekcji służy do konfigurowania i testowanie usługi Azure AD logowanie jednokrotne za pomocą NetBenefits wierność w oparciu o użytkownika testu o nazwie "Britta Simon".

Dla logowania jednokrotnego do pracy usługi Azure AD musi znać użytkownika odpowiednika w NetBenefits wierności dla użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i powiązanego użytkownika w NetBenefits wierności musi można ustanowić.

W NetBenefits wierności **użytkownika** mapowanie powinno się odbywać z **użytkownika usługi Azure AD** do ustanawiania relacji łączy.

Aby skonfigurować i testowanie usługi Azure AD logowanie jednokrotne za pomocą NetBenefits wierności, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie logowania jednokrotnego usługi Azure AD](#configure-azure-ad-single-sign-on)** — aby umożliwić użytkownikom korzystanie z tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)** — aby przetestować logowanie jednokrotne usługi Azure AD z użytkownikiem Britta Simon.
3. **[Tworzenie użytkownika testowego NetBenefits wierności](#create-a-fidelity-netbenefits-test-user)**  — aby odpowiednikiem Britta Simon w NetBenefits wierności, połączonego z usługi Azure AD reprezentacja użytkownika.
4. **[Przypisywanie użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)** — aby umożliwić użytkownikowi Britta Simon korzystanie z logowania jednokrotnego usługi Azure AD.
5. **[Testowanie logowania jednokrotnego](#test-single-sign-on)** — aby sprawdzić, czy konfiguracja działa.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie logowania jednokrotnego usługi Azure AD

W tej sekcji możesz włączyć usługi Azure AD logowania jednokrotnego w witrynie Azure portal i konfigurowanie logowania jednokrotnego w aplikacji NetBenefits wierności.

**Aby skonfigurować usługę Azure AD logowanie jednokrotne z NetBenefits wierności, wykonaj następujące czynności:**

1. W witrynie Azure portal na **NetBenefits wierności** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Link do konfigurowania logowania jednokrotnego][4]

2. Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **opartej na SAML logowania jednokrotnego** włączyć logowanie jednokrotne.

    ![Okno dialogowe rejestracji jednokrotnej](./media/fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_samlbase.png)

3. Na **wierności NetBenefits domena i adresy URL** sekcji, wykonaj następujące czynności:

    ![Wierności NetBenefits domena i adresy URL pojedynczego logowania jednokrotnego informacji](./media/fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_url.png)

    a. W **identyfikator** pole tekstowe, wpisz adres URL:

    W przypadku testowania środowiska:  `urn:sp:fidelity:geninbndnbparts20:uat:xq1`

    W środowisku produkcyjnym:  `urn:sp:fidelity:geninbndnbparts20`

    b. W **adres URL odpowiedzi** polu tekstowym wprowadź adres URL, aby być dostarczona przez wierność w czasie wdrażania lub skontaktuj się z menedżerem przypisanej jakości klienta usługi.

4. Aplikacja NetBenefits wierności oczekuje twierdzenia SAML, w określonym formacie. Firma Microsoft zmapowane **identyfikator użytkownika** z **user.userprincipalname**. Możesz zamapować za pomocą **employeeid** lub innego roszczenia, które jest odpowiednie dla Twojej organizacji jako **identyfikator użytkownika**. Poniższy zrzut ekranu przedstawia przykładowe tego.

    ![Atrybut NetBenefits wierności](./media/fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_attribute.png)

    >[!Note]
    >NetBenefits wierności obsługuje statyczne i dynamiczne federacji. Statyczna oznacza, że nie będzie używać protokołu SAML, na podstawie dokładnie na czas użytkownika inicjowania obsługi administracyjnej i dynamiczne oznacza, że obsługuje ona dokładnie na czas Inicjowanie obsługi użytkowników. Dla przy użyciu JIT na podstawie inicjowania obsługi administracyjnej klientów jest dodać niektóre im więcej oświadczeń w usłudze Azure AD, takie jak data urodzenia użytkownika itd. Te informacje są udostępniane przez usługi przypisane **wierności klienta z programu Service Manager** i muszą włączyć ten dynamiczny Federację dla wystąpienia usługi.

5. Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.

    ![Link pobierania certyfikatu](./media/fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_certificate.png)

6. Kliknij przycisk **Zapisz** przycisku.

    ![Konfigurowanie przycisku Zapisz logowania jednokrotnego](./media/fidelitynetbenefits-tutorial/tutorial_general_400.png)

7. Na **konfiguracji NetBenefits wierności** , kliknij przycisk **skonfigurować NetBenefits wierności** otworzyć **Konfigurowanie logowania jednokrotnego** okna. Kopiuj **identyfikator jednostki języka SAML i SAML pojedynczego logowania jednokrotnego adres URL usługi** z **krótki przewodnik po sekcji.**

    ![Konfiguracja NetBenefits wierności](./media/fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_configure.png)

8. Aby skonfigurować logowanie jednokrotne na **NetBenefits wierności** stronie, musisz wysłać pobrany **XML metadanych**, **SAML pojedynczego logowania jednokrotnego usługi adresu URL** i  **Identyfikator jednostki SAML** do **przypisany Menedżer usług klienta wierności**. Ustawią oni to ustawienie tak, aby połączenie logowania jednokrotnego SAML było ustawione właściwie po obu stronach.

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem tej sekcji jest tworzenie użytkownika testowego w witrynie Azure portal, o nazwie Britta Simon.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W witrynie Azure portal w okienku po lewej stronie kliknij pozycję **usługi Azure Active Directory** przycisku.

    ![Przycisk usługi Azure Active Directory](./media/fidelitynetbenefits-tutorial/create_aaduser_01.png)

2. Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    !["Użytkownicy i grupy" i "All users" linki](./media/fidelitynetbenefits-tutorial/create_aaduser_02.png)

3. Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.

    ![Przycisk Dodaj](./media/fidelitynetbenefits-tutorial/create_aaduser_03.png)

4. W **użytkownika** okna dialogowego pole, wykonaj następujące czynności:

    ![Okno dialogowe użytkownika](./media/fidelitynetbenefits-tutorial/create_aaduser_04.png)

    a. W **nazwa** wpisz **BrittaSimon**.

    b. W **nazwa_użytkownika** wpisz adres e-mail użytkownika Britta Simon.

    c. Wybierz **Pokaż hasło** pole wyboru, a następnie zapisz wartość, która jest wyświetlana w **hasło** pole.

    d. Kliknij pozycję **Utwórz**.
  
### <a name="create-a-fidelity-netbenefits-test-user"></a>Tworzenie użytkownika testowego NetBenefits wierności

W tej sekcji utworzysz użytkownika o nazwie Britta Simon w NetBenefits wierności. W przypadku tworzenia Federacji statyczne, skontaktuj się z Twojego przypisane **wierności klienta z programu Service Manager** do tworzenia użytkowników platformie NetBenefits wierności. Tacy użytkownicy muszą być tworzone i aktywowana, aby używać logowania jednokrotnego.

Dla dynamicznych Federacji użytkowników są tworzone przy użyciu aprowizacji użytkowników Just In Time. Dla przy użyciu JIT na podstawie inicjowania obsługi administracyjnej klientów jest dodać niektóre im więcej oświadczeń w usłudze Azure AD, takie jak data urodzenia użytkownika itd. Te informacje są udostępniane przez usługi przypisane **wierności klienta z programu Service Manager** i muszą włączyć ten dynamiczny Federację dla wystąpienia usługi.

### <a name="assign-the-azure-ad-test-user"></a>Przypisywanie użytkownika testowego usługi Azure AD

W tej sekcji możesz włączyć Britta Simon do używania platformy Azure logowanie jednokrotne za udzielanie dostępu do NetBenefits wierności.

![Przypisanie roli użytkownika][200]

**Aby przypisać Britta Simon NetBenefits wierności, wykonaj następujące czynności:**

1. W witrynie Azure portal Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201]

2. Na liście aplikacji wybierz **NetBenefits wierności**.

    ![Link NetBenefits wierność na liście aplikacji](./media/fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_app.png)  

3. W menu po lewej stronie kliknij **użytkowników i grup**.

    ![Link "Użytkownicy i grupy"][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz pozycję **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodawanie przypisania][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Britta Simon** na liście Użytkownicy.

6. Kliknij przycisk **wybierz** znajdujący się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdujący się na **Dodaj przydziału** okna dialogowego.

### <a name="test-single-sign-on"></a>Testowanie logowania jednokrotnego

W tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu panelu dostępu.

Po kliknięciu kafelka NetBenefits wierność w panelu dostępu, możesz należy pobrać automatycznie zalogowanych do aplikacji NetBenefits wierności.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Zasoby dodatkowe

* [Lista samouczków dotyczących integrowania aplikacji SaaS w usłudze Azure Active Directory](tutorial-list.md)
* [Czym jest dostęp do aplikacji i logowanie jednokrotne za pomocą usługi Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/fidelitynetbenefits-tutorial/tutorial_general_01.png
[2]: ./media/fidelitynetbenefits-tutorial/tutorial_general_02.png
[3]: ./media/fidelitynetbenefits-tutorial/tutorial_general_03.png
[4]: ./media/fidelitynetbenefits-tutorial/tutorial_general_04.png

[100]: ./media/fidelitynetbenefits-tutorial/tutorial_general_100.png

[200]: ./media/fidelitynetbenefits-tutorial/tutorial_general_200.png
[201]: ./media/fidelitynetbenefits-tutorial/tutorial_general_201.png
[202]: ./media/fidelitynetbenefits-tutorial/tutorial_general_202.png
[203]: ./media/fidelitynetbenefits-tutorial/tutorial_general_203.png
