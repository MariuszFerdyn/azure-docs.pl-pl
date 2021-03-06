---
title: 'Samouczek: Integracja usługi Azure Active Directory z aplikacją Appraisd | Microsoft Docs'
description: Dowiedz się, jak skonfigurować logowanie jednokrotne między usługą Azure Active Directory i aplikacją Appraisd.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: db063306-4d0d-43ca-aae0-09f0426e7429
ms.service: Azure-Active-Directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/17/2019
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8afd2201d55dfed94cf8f0dd34ca26870c0cc324
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56169364"
---
# <a name="tutorial-azure-active-directory-integration-with-appraisd"></a>Samouczek: Integracja usługi Azure Active Directory z aplikacją Appraisd

Z tego samouczka dowiesz się, jak zintegrować aplikację Appraisd z usługą Azure Active Directory (Azure AD).
Integracja aplikacji Appraisd z usługą Azure AD zapewnia następujące korzyści:

* Możesz kontrolować w usłudze Azure AD, kto ma dostęp do aplikacji Appraisd.
* Możesz zezwolić swoim użytkownikom na automatyczne logowanie do aplikacji Appraisd (logowanie jednokrotne) przy użyciu kont usługi Azure AD.
* Możesz zarządzać swoimi kontami w jednej centralnej lokalizacji — witrynie Azure Portal.

Jeśli chcesz dowiedzieć się więcej na temat integracji aplikacji SaaS z usługą Azure AD, zobacz [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis).
Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem [utwórz bezpłatne konto](https://azure.microsoft.com/free/).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD z aplikacją Appraisd, potrzebne są następujące elementy:

* Subskrypcja usługi Azure AD. Jeśli nie masz środowiska usługi Azure AD, możesz skorzystać z miesięcznej wersji próbnej [tutaj](https://azure.microsoft.com/pricing/free-trial/)
* Subskrypcja aplikacji Appraisd z obsługą logowania jednokrotnego

## <a name="scenario-description"></a>Opis scenariusza

W tym samouczku skonfigurujesz i przetestujesz logowanie jednokrotne usługi Azure AD w środowisku testowym.

* Aplikacja Appraisd obsługuje logowanie jednokrotne inicjowane przez **dostawcę usług i dostawcę tożsamości**

## <a name="adding-appraisd-from-the-gallery"></a>Dodawanie aplikacji Appraisd z galerii

Aby skonfigurować integrację aplikacji Appraisd z usługą Azure AD, należy z poziomu galerii dodać tę aplikację do listy zarządzanych aplikacji SaaS.

**Aby dodać aplikację Appraisd z galerii, należy wykonać następujące kroki:**

1. W witrynie **[Azure Portal](https://portal.azure.com)** w panelu nawigacyjnym po lewej stronie kliknij ikonę usługi **Azure Active Directory**.

    ![Przycisk Azure Active Directory](common/select-azuread.png)

2. Przejdź do grupy **Aplikacje dla przedsiębiorstw** i wybierz opcję **Wszystkie aplikacje**.

    ![Blok Aplikacje dla przedsiębiorstw](common/enterprise-applications.png)

3. Aby dodać nową aplikację, kliknij przycisk **Nowa aplikacja** w górnej części okna dialogowego.

    ![Przycisk Nowa aplikacja](common/add-new-app.png)

4. W polu wyszukiwania wpisz **Appraisd**, wybierz pozycję **Appraisd** z panelu wyników i kliknij przycisk **Dodaj**, aby dodać aplikację.

     ![Aplikacja Appraisd na liście wyników](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie logowania jednokrotnego usługi Azure AD

W tej sekcji skonfigurujesz i przetestujesz logowanie jednokrotne usługi Azure AD z aplikacją Appraisd, korzystając z danych testowego użytkownika **Britta Simon**.
Aby logowanie jednokrotne działało, należy ustanowić relację połączenia między użytkownikiem usługi Azure AD i powiązanym użytkownikiem aplikacji Appraisd.

Aby skonfigurować i przetestować logowanie jednokrotne usługi Azure AD z aplikacją Appraisd, należy wykonać czynności opisane w poniższych blokach konstrukcyjnych:

1. **[Konfigurowanie logowania jednokrotnego usługi Azure AD](#configure-azure-ad-single-sign-on)** — aby umożliwić użytkownikom korzystanie z tej funkcji.
2. **[Konfigurowanie logowania jednokrotnego w aplikacji Appraisd](#configure-appraisd-single-sign-on)** — aby skonfigurować ustawienia logowania jednokrotnego po stronie aplikacji.
3. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)** — aby przetestować logowanie jednokrotne usługi Azure AD z użytkownikiem Britta Simon.
4. **[Przypisywanie użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)** — aby umożliwić użytkownikowi Britta Simon korzystanie z logowania jednokrotnego usługi Azure AD.
5. **[Tworzenie użytkownika testowego aplikacji Appraisd](#create-appraisd-test-user)** — aby mieć w aplikacji Appraisd odpowiednik użytkownika Britta Simon połączony z reprezentacją użytkownika w usłudze Azure AD.
6. **[Testowanie logowania jednokrotnego](#test-single-sign-on)** — aby sprawdzić, czy konfiguracja działa.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie logowania jednokrotnego usługi Azure AD

W tej sekcji włączysz logowanie jednokrotne usługi Azure AD w witrynie Azure Portal.

Aby skonfigurować logowanie jednokrotne usługi Azure AD w aplikacji Appraisd, wykonaj następujące kroki:

1. W witrynie [Azure Portal](https://portal.azure.com/) na stronie integracji aplikacji **Appraisd** wybierz pozycję **Logowanie jednokrotne**.

    ![Link do konfigurowania logowania jednokrotnego](common/select-sso.png)

2. W oknie dialogowym **Wybieranie metody logowania jednokrotnego** wybierz tryb **SAML/WS-Fed**, aby włączyć logowanie jednokrotne.

    ![Wybieranie trybu logowania jednokrotnego](common/select-saml-option.png)

3. Na stronie **Konfigurowanie logowania jednokrotnego za pomocą protokołu SAML** kliknij ikonę **Edytuj**, aby otworzyć okno dialogowe **Podstawowa konfiguracja protokołu SAML**.

    ![Edycja podstawowej konfiguracji protokołu SAML](common/edit-urls.png)

4. Jeśli chcesz skonfigurować aplikację w trybie inicjowanym przez **dostawcę tożsamości**, w sekcji **Podstawowa konfiguracja protokołu SAML** wykonaj następujące kroki:

    ![Informacje o domenie i adresach URL aplikacji Appraisd na potrzeby logowania jednokrotnego](common/both-preintegrated-advanced-urls.png)

    a. Kliknij pozycję **Ustaw dodatkowe adresy URL**.

    b. W polu tekstowym **Stan przekaźnika** wpisz adres URL: `<TENANTCODE>`

    d. Jeśli chcesz skonfigurować aplikację w trybie inicjowanym przez **dostawcę usług**, w polu tekstowym **Adres URL logowania** wpisz adres URL przy użyciu następującego wzorca: `https://app.appraisd.com/saml/<TENANTCODE>`

    > [!NOTE]
    > Uzyskasz rzeczywisty adres URL logowania i wartość stanu przekaźnika na stronie konfiguracji logowania jednokrotnego aplikacji Appraisd, co zostało wyjaśnione w dalszej części tego samouczka.

5. Aplikacja Appraisd oczekuje asercji SAML w określonym formacie. Skonfiguruj następujące oświadczenia dla tej aplikacji. Wartościami tych atrybutów możesz zarządzać w sekcji **Atrybuty użytkownika** na stronie integracji aplikacji. Na stronie **Konfigurowanie logowania jednokrotnego za pomocą protokołu SAML** kliknij przycisk **Edytuj**, aby otworzyć okno dialogowe **Atrybuty użytkownika**.

    ![image](common/edit-attribute.png)

6. W sekcji **Oświadczenia użytkownika** w oknie dialogowym **Atrybuty użytkownika** edytuj oświadczenia, korzystając z **ikony edycji**, lub dodaj je za pomocą opcji **Dodaj nowe oświadczenie**, aby skonfigurować atrybut tokenu języka SAML, jak pokazano na ilustracji powyżej, a następnie wykonaj następujące czynności:

    | Name (Nazwa) |  Atrybut źródłowy|
    | ---------------| --------------- |
    | nameidentifier | user.mail |
    | | |

    a. Kliknij przycisk **Dodaj nowe oświadczenie**, aby otworzyć okno dialogowe **Zarządzanie oświadczeniami użytkownika**.

    ![image](common/new-save-attribute.png)

    ![image](common/new-attribute-details.png)

    b. W polu tekstowym **Nazwa** wpisz nazwę atrybutu pokazaną dla tego wiersza.

    d. Pozostaw pole **Przestrzeń nazw** puste.

    d. Dla opcji Źródło wybierz wartość **Atrybut**.

    e. Na liście **Atrybut źródłowy** wpisz wartość atrybutu pokazaną dla tego wiersza.

    f. Kliknij przycisk **OK**.

    g. Kliknij pozycję **Zapisz**.

7. Na stronie **Konfigurowanie logowania jednokrotnego za pomocą protokołu SAML** w sekcji **Certyfikat podpisywania SAML** kliknij link **Pobierz**, aby pobrać **certyfikat (Base64)** z podanych opcji zgodnie z wymaganiami i zapisać go na komputerze.

    ![Link do pobierania certyfikatu](common/certificatebase64.png)

8. W sekcji **Konfigurowanie aplikacji Appraisd** skopiuj odpowiednie adresy URL zgodnie z wymaganiami.

    ![Kopiowanie adresów URL konfiguracji](common/copy-configuration-urls.png)

    a. Adres URL logowania

    b. Identyfikator usługi Azure AD

    d. Adres URL wylogowywania

### <a name="configure-appraisd-single-sign-on"></a>Konfigurowanie logowania jednokrotnego aplikacji Appraisd

1. W innym oknie przeglądarki internetowej zaloguj się do aplikacji Appraisd jako administrator zabezpieczeń.

2. U góry po prawej stronie kliknij ikonę **Settings** (Ustawienia), a następnie przejdź do pozycji  **Configuration** (Konfiguracja).

    ![image](./media/appraisd-tutorial/tutorial_appraisd_sett.png)

3. Po lewej stronie menu kliknij pozycję **SAML single sign-on** (Logowanie jednokrotne SAML).

    ![image](./media/appraisd-tutorial/tutorial_appraisd_single.png)

4. Na stronie **SAML 2.0 Single Sign-On configuration** (Konfiguracja logowania jednokrotnego SAML 2.0) wykonaj następujące kroki:

    ![image](./media/appraisd-tutorial/tutorial_appraisd_saml.png)

    a. Skopiuj wartość **Default Relay State** (Domyślny stan przekaźnika) i wklej ją w polu tekstowym  **Stan przekaźnika** na stronie  **Podstawowa konfiguracja SAML** w witrynie Azure Portal.

    b. Skopiuj wartość **Service-initiated login URL** (Adres URL logowania inicjowanego przez usługę) i wklej ją w polu tekstowym  **Adres URL logowania jednokrotnego** na stronie  **Podstawowa konfiguracja SAML** w witrynie Azure Portal.

5. Przewiń tę samą stronę do pozycji **Identifying users** (Identyfikowanie użytkowników) i wykonaj następujące kroki:

    ![image](./media/appraisd-tutorial/tutorial_appraisd_identifying.png)

    a. W polu tekstowym **Identity Provider Single Sign-On URL** (Adres URL logowania jednokrotnego dostawcy tożsamości) wklej wartość **Adres URL logowania** skopiowaną z witryny Azure Portal, a następnie kliknij przycisk **Save** (Zapisz).

    b. W polu tekstowym **Identity Provider Issuer URL** (Adres URL wystawcy dostawcy tożsamości) wklej wartość **Identyfikator usługi Azure AD** skopiowaną z witryny Azure Portal, a następnie kliknij przycisk **Save** (Zapisz).

    d. W programie Notatnik otwórz certyfikat zakodowany w formacie Base-64 pobrany z witryny Azure Portal, skopiuj jego zawartość, a następnie wklej go w polu  **X.509 Certificate**  (Certyfikat X.509) i kliknij przycisk **Save** (Zapisz).

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

W tej sekcji w witrynie Azure Portal utworzysz użytkownika testowego o nazwie Britta Simon.

1. W witrynie Azure Portal w okienku po lewej stronie wybierz pozycję **Azure Active Directory**, wybierz opcję **Użytkownicy**, a następnie wybierz pozycję **Wszyscy użytkownicy**.

    ![Linki „Użytkownicy i grupy” i „Wszyscy użytkownicy”](common/users.png)

2. Wybierz przycisk **Nowy użytkownik** w górnej części ekranu.

    ![Przycisk Nowy użytkownik](common/new-user.png)

3. We właściwościach użytkownika wykonaj następujące kroki.

    ![Okno dialogowe Użytkownik](common/user-properties.png)

    a. W polu **Nazwa** wprowadź **BrittaSimon**.
  
    b. W polu **Nazwa użytkownika** wpisz **brittasimon@yourcompanydomain.extension**  
    Na przykład: BrittaSimon@contoso.com

    d. Zaznacz pole wyboru **Pokaż hasło** i zanotuj wartość wyświetlaną w polu Hasło.

    d. Kliknij pozycję **Utwórz**.

### <a name="assign-the-azure-ad-test-user"></a>Przypisywanie użytkownika testowego usługi Azure AD

W tej sekcji włączysz dla użytkownika Britta Simon możliwość korzystania z logowania jednokrotnego platformy Azure, udzielając dostępu do aplikacji Appraisd.

1. W witrynie Azure Portal wybierz pozycję **Aplikacje dla przedsiębiorstw**, wybierz pozycję **Wszystkie aplikacje**, a następnie wybierz pozycję **Appraisd**.

    ![Blok Aplikacje dla przedsiębiorstw](common/enterprise-applications.png)

2. Na liście aplikacji wybierz **Appraisd**.

    ![Link do aplikacji Appraisd na liście aplikacji](common/all-applications.png)

3. W menu po lewej stronie wybierz pozycję **Użytkownicy i grupy**.

    ![Link „Użytkownicy i grupy”](common/users-groups-blade.png)

4. Kliknij przycisk **Dodaj użytkownika**, a następnie wybierz pozycję **Użytkownicy i grupy** w oknie dialogowym **Dodawanie przypisania**.

    ![Okienko Dodawanie przypisania](common/add-assign-user.png)

5. W oknie dialogowym **Użytkownicy i grupy** wybierz użytkownika **Britta Simon** na liście użytkowników, a następnie kliknij przycisk **Wybierz** u dołu ekranu.

6. Jeśli oczekujesz wartości roli w asercji SAML, w oknie dialogowym **Wybieranie roli** wybierz z listy odpowiednią rolę dla użytkownika, a następnie kliknij przycisk **Wybierz** u dołu ekranu.

7. W oknie dialogowym **Dodawanie przypisania** kliknij przycisk **Przypisz**.

### <a name="create-appraisd-test-user"></a>Tworzenie użytkownika testowego aplikacji Appraisd

Aby umożliwić użytkownikom usługi Azure AD logowanie się w aplikacji Appraisd, należy ich aprowizować w tej aplikacji. W aplikacji Appraisd aprowizowanie jest zadaniem ręcznym.

**Aby aprowizować konto użytkownika, wykonaj następujące kroki:**

1. Zaloguj się do aplikacji Appraisd jako administrator zabezpieczeń.

2. U góry po prawej stronie kliknij ikonę **Settings** (Ustawienia), a następnie przejdź do pozycji  **Administration centre** (Centrum administracyjne).

    ![image](./media/appraisd-tutorial/tutorial_appraisd_admin.png)

3. Na pasku narzędzi w górnej części strony kliknij opcję  **People** (Osoby), a następnie przejdź do pozycji  **Add a new user** (Dodaj nowego użytkownika).

    ![image](./media/appraisd-tutorial/tutorial_appraisd_user.png)

4. Na stronie **Add a new user** (Dodawanie nowego użytkownika) wykonaj następujące kroki:

    ![image](./media/appraisd-tutorial/tutorial_appraisd_newuser.png)

    a. W polu tekstowym **First name** (Imię) wprowadź imię użytkownika, na przykład **Britta**.

    b. W polu tekstowym **Last name** (Nazwisko) wprowadź nazwisko użytkownika, na przykład **Simon**.

    d. W polu tekstowym **Email** (Adres e-mail) wprowadź adres e-mail użytkownika, na przykład **Brittasimon@contoso.com**.

    d. Kliknij pozycję **Dodaj użytkownika**.

### <a name="test-single-sign-on"></a>Testowanie logowania jednokrotnego

W tej sekcji przetestujesz konfigurację logowania jednokrotnego usługi Azure AD przy użyciu panelu dostępu.

Po kliknięciu kafelka Appraisd w panelu dostępu powinno nastąpić automatyczne zalogowanie do aplikacji Appraisd, dla której skonfigurowano logowanie jednokrotne. Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [Introduction to the Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) (Wprowadzenie do panelu dostępu).

## <a name="additional-resources"></a>Dodatkowe zasoby

- [ Lista samouczków dotyczących sposobu integrowania aplikacji SaaS z usługą Azure Active Directory ](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [Co to jest dostęp warunkowy w usłudze Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
