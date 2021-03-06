---
title: 'Samouczek: Integracja usługi Azure Active Directory za pomocą stada | Dokumentacja firmy Microsoft'
description: Dowiedz się, jak skonfigurować logowanie jednokrotne między usługi Azure Active Directory i stada.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7b2c3ac5-17f1-49a0-8961-c541b258d4b1
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2018
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 44204813e44dc725db774eec2cbecb35852cffde
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56198651"
---
# <a name="tutorial-azure-active-directory-integration-with-flock"></a>Samouczek: Integracja usługi Azure Active Directory za pomocą stada

W tym samouczku dowiesz się, jak zintegrować stada w usłudze Azure Active Directory (Azure AD).

Stada zintegrowanie z usługą Azure AD zapewnia następujące korzyści:

- Możesz kontrolować, czy w usłudze Azure AD, kto ma dostęp do stada.
- Aby umożliwić użytkownikom automatyczne pobieranie zalogowanych do stada (logowanie jednokrotne) przy użyciu konta usługi Azure AD.
- Możesz zarządzać swoimi kontami w jednej centralnej lokalizacji — witrynie Azure Portal.

Jeśli chcesz dowiedzieć się więcej na temat integracji aplikacji SaaS z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD za pomocą stada, potrzebne są następujące elementy:

- Subskrypcji usługi Azure AD
- Stada logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.

Aby przetestować czynności opisane w tym samouczku, należy postępować zgodnie z następującymi zaleceniami:

- Nie używaj środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko usługi Azure AD w wersji próbnej, możesz to zrobić [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W ramach tego samouczka można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz opisany w tym samouczku składa się z dwóch głównych bloków konstrukcyjnych:

1. Dodawanie stada z galerii
1. Konfigurowanie i testowania usługi Azure AD logowanie jednokrotne

## <a name="adding-flock-from-the-gallery"></a>Dodawanie stada z galerii
Aby skonfigurować integrację stada w usłudze Azure AD, należy dodać stada z galerii z listą zarządzanych aplikacji SaaS.

**Aby dodać stada z galerii, wykonaj następujące czynności:**

1. W **[witryny Azure portal](https://portal.azure.com)**, w panelu nawigacyjnym po lewej stronie kliknij pozycję **usługi Azure Active Directory** ikony. 

    ![Przycisk usługi Azure Active Directory][1]

1. Przejdź do **aplikacje dla przedsiębiorstw**. Następnie przejdź do **wszystkie aplikacje**.

    ![W bloku aplikacji przedsiębiorstwa][2]
    
1. Aby dodać nową aplikację, kliknij przycisk **Nowa aplikacja** w górnej części okna dialogowego.

    ![Przycisk Nowa aplikacja][3]

1. W polu wyszukiwania wpisz **stada**, wybierz opcję **stada** z panelu wynik kliknięcie **Dodaj** przycisk, aby dodać aplikację.

    ![Stadzie na liście wyników](./media/flock-tutorial/tutorial_flock_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie logowania jednokrotnego usługi Azure AD

W tej sekcji służy do konfigurowania i testowanie usługi Azure AD logowanie jednokrotne za pomocą stada, w oparciu o użytkownika testu o nazwie "Britta Simon".

Dla logowania jednokrotnego do pracy usługi Azure AD musi znać użytkownika odpowiednika w stada do użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i powiązanego użytkownika z stada musi można ustanowić.

Aby skonfigurować i testowanie usługi Azure AD logowanie jednokrotne za pomocą stada, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie logowania jednokrotnego usługi Azure AD](#configure-azure-ad-single-sign-on)** — aby umożliwić użytkownikom korzystanie z tej funkcji.
1. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)** — aby przetestować logowanie jednokrotne usługi Azure AD z użytkownikiem Britta Simon.
1. **[Tworzenie użytkownika testowego stada](#create-a-flock-test-user)**  — aby odpowiednikiem Britta Simon w stada połączonego z usługi Azure AD reprezentacja użytkownika.
1. **[Przypisywanie użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)** — aby umożliwić użytkownikowi Britta Simon korzystanie z logowania jednokrotnego usługi Azure AD.
1. **[Testowanie logowania jednokrotnego](#test-single-sign-on)** — aby sprawdzić, czy konfiguracja działa.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie logowania jednokrotnego usługi Azure AD

W tej sekcji możesz włączyć usługi Azure AD logowania jednokrotnego w witrynie Azure portal i konfigurowanie logowania jednokrotnego w aplikacji stada.

**Aby skonfigurować usługę Azure AD logowanie jednokrotne z stada, wykonaj następujące czynności:**

1. W witrynie Azure portal na **stada** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Link do konfigurowania logowania jednokrotnego][4]

1. Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **opartej na SAML logowania jednokrotnego** włączyć logowanie jednokrotne.

    ![Okno dialogowe rejestracji jednokrotnej](./media/flock-tutorial/tutorial_flock_samlbase.png)

1. Na **stada domena i adresy URL** sekcji, wykonaj następujące czynności:

    ![Stada domena i adresy URL pojedynczego logowania jednokrotnego informacji](./media/flock-tutorial/tutorial_flock_url.png)

    a. W polu tekstowym **Adres URL logowania** wpisz adres URL, korzystając z następującego wzorca: `https://<subdomain>.flock.com/`

    b. W polu tekstowym **Identyfikator** wpisz adres URL, korzystając z następującego wzorca: `https://<subdomain>.flock.com/`

    > [!NOTE]
    > Te wartości nie są prawdziwe. Zaktualizuj je, używając faktycznego adresu URL i identyfikatora logowania. Skontaktuj się z pomocą [zespołem pomocy technicznej klienta stada](mailto:support@flock.com) do uzyskania tych wartości.

1. Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na komputerze.

    ![Link do pobierania certyfikatu](./media/flock-tutorial/tutorial_flock_certificate.png)

1. Kliknij przycisk **Zapisz** przycisku.

    ![Konfigurowanie przycisku Zapisz logowania jednokrotnego](./media/flock-tutorial/tutorial_general_400.png)

1. Na **konfiguracji stada** , kliknij przycisk **skonfigurować stada** otworzyć **Konfigurowanie logowania jednokrotnego** okna. Kopiuj **identyfikator jednostki języka SAML i SAML pojedynczego logowania jednokrotnego adres URL usługi** z **krótki przewodnik po sekcji.**

    ![Konfiguracja stada](./media/flock-tutorial/tutorial_flock_configure.png) 

1. W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy stada.

1. Wybierz **uwierzytelniania** w panelu nawigacyjnym po lewej stronie, a następnie wybierz pozycję **uwierzytelnianie SAML**.

    ![Konfiguracja stada](./media/flock-tutorial/configure1.png)

1. W **uwierzytelnianie SAML** sekcji, wykonaj następujące czynności:

    ![Konfiguracja stada](./media/flock-tutorial/configure2.png)

    a. W **SAML 2.0 Endpoint(HTTP)** pola tekstowego, Wklej **SAML pojedynczego logowania jednokrotnego usługi adresu URL** wartości, które zostały skopiowane z witryny Azure portal.

    b. W **wystawca dostawcy tożsamości** pola tekstowego, Wklej **identyfikator jednostki SAML** wartości, które zostały skopiowane z witryny Azure portal.

    c. Otwórz pobrany **Certificate(Base64)** z witryny Azure portal w programie Notatnik, Wklej zawartość **certyfikatu publicznego** pola tekstowego.

    d. Kliknij pozycję **Zapisz**.

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem tej sekcji jest tworzenie użytkownika testowego w witrynie Azure portal, o nazwie Britta Simon.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W witrynie Azure portal w okienku po lewej stronie kliknij pozycję **usługi Azure Active Directory** przycisku.

    ![Przycisk usługi Azure Active Directory](./media/flock-tutorial/create_aaduser_01.png)

1. Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    !["Użytkownicy i grupy" i "All users" linki](./media/flock-tutorial/create_aaduser_02.png)

1. Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.

    ![Przycisk Dodaj](./media/flock-tutorial/create_aaduser_03.png)

1. W **użytkownika** okna dialogowego pole, wykonaj następujące czynności:

    ![Okno dialogowe użytkownika](./media/flock-tutorial/create_aaduser_04.png)

    a. W **nazwa** wpisz **BrittaSimon**.

    b. W **nazwa_użytkownika** wpisz adres e-mail użytkownika Britta Simon.

    c. Wybierz **Pokaż hasło** pole wyboru, a następnie zapisz wartość, która jest wyświetlana w **hasło** pole.

    d. Kliknij pozycję **Utwórz**.

### <a name="create-a-flock-test-user"></a>Tworzenie użytkownika testowego stada

Aby umożliwić użytkownikom usługi Azure AD zalogować się do stada, musi być obsługiwana w stada. W przypadku stada Inicjowanie obsługi administracyjnej jest zadanie ręczne.

**Aby aprowizować konto użytkownika, wykonaj następujące kroki:**

1. Zaloguj się do witryny firmy stada jako administrator.

1. Kliknij przycisk **zespołu zarządzania** w panelu nawigacyjnym po lewej stronie.

    ![Dodawanie pracownika](./media/flock-tutorial/user1.png)

1. Kliknij przycisk **Dodawanie elementu członkowskiego** , a następnie wybierz pozycję **członków zespołu**.

    ![Dodawanie pracownika](./media/flock-tutorial/user2.png)

1. Wprowadź adres e-mail użytkownika, takich jak **Brittasimon@contoso.com** , a następnie wybierz **Add Users**.

    ![Dodawanie pracownika](./media/flock-tutorial/user3.png)

### <a name="assign-the-azure-ad-test-user"></a>Przypisywanie użytkownika testowego usługi Azure AD

W tej sekcji możesz włączyć Britta Simon do udzielania dostępu do stada za pomocą platformy Azure logowania jednokrotnego.

![Przypisanie roli użytkownika][200]

**Aby przypisać Britta Simon stada, wykonaj następujące czynności:**

1. W witrynie Azure portal Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201]

1. Na liście aplikacji wybierz **stada**.

    ![Link stada na liście aplikacji](./media/flock-tutorial/tutorial_flock_app.png)

1. W menu po lewej stronie kliknij **użytkowników i grup**.

    ![Link "Użytkownicy i grupy"][202]

1. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz pozycję **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodawanie przypisania][203]

1. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Britta Simon** na liście Użytkownicy.

1. Kliknij przycisk **wybierz** znajdujący się na **użytkowników i grup** okna dialogowego.

1. Kliknij przycisk **przypisać** znajdujący się na **Dodaj przydziału** okna dialogowego.

### <a name="test-single-sign-on"></a>Testowanie logowania jednokrotnego

W tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu panelu dostępu.

Po kliknięciu kafelka stada w panelu dostępu, użytkownik powinien uzyskać automatycznie zalogowanych do aplikacji stada.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Zasoby dodatkowe

* [Lista samouczków dotyczących integrowania aplikacji SaaS w usłudze Azure Active Directory](tutorial-list.md)
* [Czym jest dostęp do aplikacji i logowanie jednokrotne za pomocą usługi Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/flock-tutorial/tutorial_general_01.png
[2]: ./media/flock-tutorial/tutorial_general_02.png
[3]: ./media/flock-tutorial/tutorial_general_03.png
[4]: ./media/flock-tutorial/tutorial_general_04.png

[100]: ./media/flock-tutorial/tutorial_general_100.png

[200]: ./media/flock-tutorial/tutorial_general_200.png
[201]: ./media/flock-tutorial/tutorial_general_201.png
[202]: ./media/flock-tutorial/tutorial_general_202.png
[203]: ./media/flock-tutorial/tutorial_general_203.png
