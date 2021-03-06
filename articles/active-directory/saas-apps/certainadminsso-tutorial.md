---
title: 'Samouczek: Integracja usługi Azure Active Directory przy użyciu wybranych administratora logowania jednokrotnego | Dokumentacja firmy Microsoft'
description: Dowiedz się, jak skonfigurować logowanie jednokrotne między usługi Azure Active Directory i niektóre administratora logowania jednokrotnego.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98ba0174-be02-408a-8634-c8113b12dedb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2018
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7d85e8dbac47bd41c759e9c225df5544c659cc05
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56205532"
---
# <a name="tutorial-azure-active-directory-integration-with-certain-admin-sso"></a>Samouczek: Integracja usługi Azure Active Directory przy użyciu wybranych administratora logowania jednokrotnego

W tym samouczku dowiesz się, jak zintegrować niektóre administratora logowanie Jednokrotne z usługą Azure Active Directory (Azure AD).

Integrowanie niektóre administratora logowanie Jednokrotne z usługą Azure AD zapewnia następujące korzyści:

- Możesz kontrolować, czy w usłudze Azure AD, kto ma dostęp do niektórych administratora logowania jednokrotnego.
- Użytkowników, aby automatycznie uzyskać zalogowanych do niektórych administratora jednokrotnego (-) można włączyć za pomocą kont usługi Azure AD.
- Możesz zarządzać swoimi kontami w jednej centralnej lokalizacji — witrynie Azure Portal.

Jeśli chcesz dowiedzieć się więcej na temat integracji aplikacji SaaS z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD przy użyciu wybranych administratora logowania jednokrotnego, potrzebne są następujące elementy:

- Subskrypcji usługi Azure AD
- Niektóre administratora logowanie Jednokrotne logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.

Aby przetestować czynności opisane w tym samouczku, należy postępować zgodnie z następującymi zaleceniami:

- Nie używaj środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko usługi Azure AD w wersji próbnej, możesz to zrobić [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W ramach tego samouczka można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz opisany w tym samouczku składa się z dwóch głównych bloków konstrukcyjnych:

1. Dodawanie wybranych administrator rejestracji Jednokrotnej z galerii
1. Konfigurowanie i testowania usługi Azure AD logowanie jednokrotne

## <a name="adding-certain-admin-sso-from-the-gallery"></a>Dodawanie wybranych administrator rejestracji Jednokrotnej z galerii
Aby skonfigurować integrację z niektórych administrator rejestracji Jednokrotnej w usłudze Azure AD, należy dodać niektórych administrator rejestracji Jednokrotnej z galerii z listą zarządzanych aplikacji SaaS.

**Aby dodać niektóre administrator rejestracji Jednokrotnej z galerii, wykonaj następujące czynności:**

1. W **[witryny Azure portal](https://portal.azure.com)**, w panelu nawigacyjnym po lewej stronie kliknij pozycję **usługi Azure Active Directory** ikony. 

    ![Przycisk usługi Azure Active Directory][1]

1. Przejdź do **aplikacje dla przedsiębiorstw**. Następnie przejdź do **wszystkie aplikacje**.

    ![W bloku aplikacji przedsiębiorstwa][2]
    
1. Aby dodać nową aplikację, kliknij przycisk **Nowa aplikacja** w górnej części okna dialogowego.

    ![Przycisk Nowa aplikacja][3]

1. W polu wyszukiwania wpisz **niektóre administrator rejestracji Jednokrotnej**, wybierz opcję **niektóre administrator rejestracji Jednokrotnej** z panelu wynik następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.

    ![Usługa rejestracji Jednokrotnej w niektórych administratora na liście wyników](./media/certainadminsso-tutorial/tutorial_certainadminsso_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie logowania jednokrotnego usługi Azure AD

W tej sekcji służy do konfigurowania i testowanie usługi Azure AD logowanie jednokrotne za pomocą niektórych administratora Usługa rejestracji Jednokrotnej w oparciu o użytkownika testu o nazwie "Britta Simon".

Dla logowania jednokrotnego do pracy usługi Azure AD musi znać użytkownika odpowiednika w niektórych administratora logowanie Jednokrotne do użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i powiązanych użytkownika, w niektórych administratora logowania jednokrotnego musi można ustanowić.

Aby skonfigurować i testowanie usługi Azure AD logowania jednokrotnego przy użyciu wybranych administratora logowania jednokrotnego, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie logowania jednokrotnego usługi Azure AD](#configure-azure-ad-single-sign-on)** — aby umożliwić użytkownikom korzystanie z tej funkcji.
1. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)** — aby przetestować logowanie jednokrotne usługi Azure AD z użytkownikiem Britta Simon.
1. **[Tworzenie użytkownika testowego niektóre administrator rejestracji Jednokrotnej](#create-a-certain-admin-sso-test-user)**  — aby odpowiednikiem Britta Simon w niektórych logowania jednokrotnego administratora, połączonego z usługi Azure AD reprezentacja użytkownika.
1. **[Przypisywanie użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)** — aby umożliwić użytkownikowi Britta Simon korzystanie z logowania jednokrotnego usługi Azure AD.
1. **[Testowanie logowania jednokrotnego](#test-single-sign-on)** — aby sprawdzić, czy konfiguracja działa.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie logowania jednokrotnego usługi Azure AD

W tej sekcji Włączanie usługi Azure AD logowania jednokrotnego w witrynie Azure portal i konfigurowanie logowania jednokrotnego w aplikacji niektórych administratora logowania jednokrotnego.

**Aby skonfigurować usługę Azure AD logowania jednokrotnego przy użyciu wybranych administratora logowania jednokrotnego, wykonaj następujące czynności:**

1. W witrynie Azure portal na **niektóre administrator rejestracji Jednokrotnej** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Link do konfigurowania logowania jednokrotnego][4]

1. Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **opartej na SAML logowania jednokrotnego** włączyć logowanie jednokrotne.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/certainadminsso-tutorial/tutorial_certainadminsso_samlbase.png)

1. Na **niektóre administrator rejestracji Jednokrotnej domena i adresy URL** sekcji, wykonaj następujące czynności:

    ![Niektóre administrator rejestracji Jednokrotnej domena i adresy URL pojedynczego logowania jednokrotnego informacje](./media/certainadminsso-tutorial/tutorial_certainadminsso_url.png)

    a. W polu tekstowym **Adres URL logowania** wpisz adres URL, korzystając z następującego wzorca: `https://<YOUR DOMAIN URL>/svcs/sso_admin_login/handleRequest/<ID>`

    b. W polu tekstowym **Identyfikator** wpisz adres URL, korzystając z następującego wzorca: `https://<SUBDOMAIN>.certain.com`

    > [!NOTE] 
    > Te wartości nie są prawdziwe. Zaktualizuj je, używając faktycznego adresu URL i identyfikatora logowania. Skontaktuj się z pomocą [niektóre klienta logowania jednokrotnego administratora zespołu pomocy technicznej](mailto:integrations@certain.com) do uzyskania tych wartości. 
 
1. Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Raw)** , a następnie zapisz plik certyfikatu na komputerze.

    ![Link do pobierania certyfikatu](./media/certainadminsso-tutorial/tutorial_certainadminsso_certificate.png) 

1. Kliknij przycisk **Zapisz** przycisku.

    ![Konfigurowanie przycisku Zapisz logowania jednokrotnego](./media/certainadminsso-tutorial/tutorial_general_400.png)

1. Na **niektórych konfiguracji logowania jednokrotnego administratora** , kliknij przycisk **Konfigurowanie logowania jednokrotnego niektóre administratora** otworzyć **Konfigurowanie logowania jednokrotnego** okna. Kopiuj **adres URL wylogowania, identyfikator jednostki języka SAML i SAML pojedynczego logowania jednokrotnego usługi adresu URL** z **krótki przewodnik po sekcji.**

    ![Niektórych konfiguracji logowania jednokrotnego administratora](./media/certainadminsso-tutorial/tutorial_certainadminsso_configure.png) 

1. Aby skonfigurować logowanie jednokrotne na **niektóre administrator rejestracji Jednokrotnej** stronie, musisz wysłać pobrany **certyfikatu (Raw)**, **adres URL wylogowania, identyfikator jednostki języka SAML i SAML pojedynczego logowania jednokrotnego usługi adresu URL**do [niektóre SSO administratora zespołu pomocy technicznej](mailto:integrations@certain.com). Ustawią oni to ustawienie tak, aby połączenie logowania jednokrotnego SAML było ustawione właściwie po obu stronach.

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem tej sekcji jest tworzenie użytkownika testowego w witrynie Azure portal, o nazwie Britta Simon.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W witrynie Azure portal w okienku po lewej stronie kliknij pozycję **usługi Azure Active Directory** przycisku.

    ![Przycisk usługi Azure Active Directory](./media/certainadminsso-tutorial/create_aaduser_01.png)

1. Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    !["Użytkownicy i grupy" i "All users" linki](./media/certainadminsso-tutorial/create_aaduser_02.png)

1. Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.

    ![Przycisk Dodaj](./media/certainadminsso-tutorial/create_aaduser_03.png)

1. W **użytkownika** okna dialogowego pole, wykonaj następujące czynności:

    ![Okno dialogowe użytkownika](./media/certainadminsso-tutorial/create_aaduser_04.png)

    a. W **nazwa** wpisz **BrittaSimon**.

    b. W **nazwa_użytkownika** wpisz adres e-mail użytkownika Britta Simon.

    c. Wybierz **Pokaż hasło** pole wyboru, a następnie zapisz wartość, która jest wyświetlana w **hasło** pole.

    d. Kliknij pozycję **Utwórz**.
 
### <a name="create-a-certain-admin-sso-test-user"></a>Tworzenie użytkownika testowego niektóre administrator rejestracji Jednokrotnej

W tej sekcji utworzysz użytkownika o nazwie Britta Simon w niektórych administratora logowania jednokrotnego. Praca z [niektóre SSO administratora zespołu pomocy technicznej](mailto:integrations@certain.com) Aby dodać użytkowników na platformie niektóre administratora logowania jednokrotnego. Użytkownicy muszą być utworzeni i aktywowani przed rozpoczęciem korzystania z logowania jednokrotnego.

### <a name="assign-the-azure-ad-test-user"></a>Przypisywanie użytkownika testowego usługi Azure AD

W tej sekcji możesz włączyć Britta Simon do używania platformy Azure logowanie jednokrotne za udzielanie dostępu do niektórych administratora logowania jednokrotnego.

![Przypisanie roli użytkownika][200] 

**Aby przypisać Britta Simon niektóre administrator rejestracji Jednokrotnej, wykonaj następujące czynności:**

1. W witrynie Azure portal Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

1. Na liście aplikacji wybierz **niektóre administrator rejestracji Jednokrotnej**.

    ![Link niektóre administratora logowanie Jednokrotne na liście aplikacji](./media/certainadminsso-tutorial/tutorial_certainadminsso_app.png)  

1. W menu po lewej stronie kliknij **użytkowników i grup**.

    ![Link "Użytkownicy i grupy"][202]

1. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz pozycję **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodawanie przypisania][203]

1. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Britta Simon** na liście Użytkownicy.

1. Kliknij przycisk **wybierz** znajdujący się na **użytkowników i grup** okna dialogowego.

1. Kliknij przycisk **przypisać** znajdujący się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Testowanie logowania jednokrotnego

W tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu panelu dostępu.

Po kliknięciu kafelka niektóre administrator rejestracji Jednokrotnej w panelu dostępu, możesz należy pobrać automatycznie zalogowanych do niektórych administratora logowania jednokrotnego aplikacji.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Zasoby dodatkowe

* [Lista samouczków dotyczących integrowania aplikacji SaaS w usłudze Azure Active Directory](tutorial-list.md)
* [Czym jest dostęp do aplikacji i logowanie jednokrotne za pomocą usługi Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/certainadminsso-tutorial/tutorial_general_01.png
[2]: ./media/certainadminsso-tutorial/tutorial_general_02.png
[3]: ./media/certainadminsso-tutorial/tutorial_general_03.png
[4]: ./media/certainadminsso-tutorial/tutorial_general_04.png

[100]: ./media/certainadminsso-tutorial/tutorial_general_100.png

[200]: ./media/certainadminsso-tutorial/tutorial_general_200.png
[201]: ./media/certainadminsso-tutorial/tutorial_general_201.png
[202]: ./media/certainadminsso-tutorial/tutorial_general_202.png
[203]: ./media/certainadminsso-tutorial/tutorial_general_203.png

