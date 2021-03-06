---
title: 'Samouczek: integracja usługi Azure Active Directory z aplikacją Cisco Webex | Microsoft Docs'
description: Dowiedz się, jak skonfigurować logowanie jednokrotne między usługą Azure Active Directory i aplikacją Cisco Webex.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.reviewer: barbkess
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: Azure-Active-Directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 1/4/2019
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7629d602362b9a76691dbf79a0a8ecd874d750a9
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56189671"
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a>Samouczek: integracja usługi Azure Active Directory z aplikacją Cisco Webex

Z tego samouczka dowiesz się, jak zintegrować aplikację Cisco Webex z usługą Azure Active Directory (Azure AD).
Integracja aplikacji Cisco Webex z usługą Azure AD oferuje następujące korzyści:

* Możesz kontrolować w usłudze Azure AD, kto ma dostęp do aplikacji Cisco Webex.
* Możesz zezwolić swoim użytkownikom na automatyczne logowanie do aplikacji Cisco Webex (logowanie jednokrotne) przy użyciu kont usługi Azure AD.
* Możesz zarządzać swoimi kontami w jednej centralnej lokalizacji — witrynie Azure Portal.

Jeśli chcesz dowiedzieć się więcej na temat integracji aplikacji SaaS z usługą Azure AD, zobacz [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis).
Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem [utwórz bezpłatne konto](https://azure.microsoft.com/free/).

## <a name="prerequisites"></a>Wymagania wstępne

Do skonfigurowania integracji usługi Azure AD z aplikacją Cisco Webex potrzebne są następujące elementy:

* Subskrypcja usługi Azure AD. Jeśli nie masz środowiska usługi Azure AD, możesz skorzystać z miesięcznej wersji próbnej [tutaj](https://azure.microsoft.com/pricing/free-trial/)
* Subskrypcja aplikacji Cisco Webex z obsługą logowania jednokrotnego

## <a name="scenario-description"></a>Opis scenariusza

W tym samouczku skonfigurujesz i przetestujesz logowanie jednokrotne usługi Azure AD w środowisku testowym.

* Aplikacja Cisco Webex obsługuje logowanie jednokrotne inicjowane przez **dostawcę usługi**

* Aplikacja Cisco Webex obsługuje aprowizowanie użytkowników typu **Just In Time**

* Aplikacja Cisco Webex obsługuje **zautomatyzowaną** aprowizację użytkowników

## <a name="adding-cisco-webex-from-the-gallery"></a>Dodawanie aplikacji Cisco Webex z galerii

Aby skonfigurować integrację aplikacji Cisco Webex z usługą Azure AD, musisz dodać aplikację Cisco Webex z galerii do swojej listy zarządzanych aplikacji SaaS.

**Aby dodać aplikację Cisco Webex z galerii, wykonaj następujące kroki:**

1. W witrynie **[Azure Portal](https://portal.azure.com)** w panelu nawigacyjnym po lewej stronie kliknij ikonę usługi **Azure Active Directory**.

    ![Przycisk Azure Active Directory](common/select-azuread.png)

2. Przejdź do grupy **Aplikacje dla przedsiębiorstw** i wybierz opcję **Wszystkie aplikacje**.

    ![Blok Aplikacje dla przedsiębiorstw](common/enterprise-applications.png)

3. Aby dodać nową aplikację, kliknij przycisk **Nowa aplikacja** w górnej części okna dialogowego.

    ![Przycisk Nowa aplikacja](common/add-new-app.png)

4. W polu wyszukiwania wpisz ciąg **Cisco Webex**, wybierz pozycję **Cisco Webex** w panelu wyników, a następnie kliknij przycisk **Dodaj**, aby dodać aplikację.

     ![Aplikacja Cisco Webex na liście wyników](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie logowania jednokrotnego usługi Azure AD

W tej sekcji skonfigurujesz i przetestujesz logowanie jednokrotne usługi Azure AD z aplikacją Cisco Webex, korzystając z danych użytkownika testowego **Britta Simon**.
Aby logowanie jednokrotne działało, należy ustanowić relację połączenia między użytkownikiem usługi Azure AD i powiązanym użytkownikiem aplikacji Cisco Webex.

Aby skonfigurować i przetestować logowanie jednokrotne usługi Azure AD z aplikacją Cisco Webex, należy utworzyć poniższe bloki konstrukcyjne:

1. **[Konfigurowanie logowania jednokrotnego usługi Azure AD](#configure-azure-ad-single-sign-on)** — aby umożliwić użytkownikom korzystanie z tej funkcji.
2. **[Konfigurowanie logowania jednokrotnego w aplikacji Cisco Webex](#configure-cisco-webex-single-sign-on)** — aby skonfigurować ustawienia logowania jednokrotnego po stronie aplikacji.
3. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)** — aby przetestować logowanie jednokrotne usługi Azure AD z użytkownikiem Britta Simon.
4. **[Przypisywanie użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)** — aby umożliwić użytkownikowi Britta Simon korzystanie z logowania jednokrotnego usługi Azure AD.
5. **[Tworzenie użytkownika testowego aplikacji Cisco Webex](#create-cisco-webex-test-user)** — aby mieć w aplikacji Cisco Webex odpowiednik użytkownika Britta Simon połączony z reprezentacją użytkownika w usłudze Azure AD.
6. **[Testowanie logowania jednokrotnego](#test-single-sign-on)** — aby sprawdzić, czy konfiguracja działa.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie logowania jednokrotnego usługi Azure AD

W tej sekcji włączysz logowanie jednokrotne usługi Azure AD w witrynie Azure Portal.

Aby skonfigurować logowanie jednokrotne usługi Azure AD w aplikacji Cisco Webex, wykonaj następujące kroki:

1. W witrynie [Azure Portal](https://portal.azure.com/) na stronie integracji aplikacji **Cisco Webex** wybierz pozycję **Logowanie jednokrotne**.

    ![Link do konfigurowania logowania jednokrotnego](common/select-sso.png)

2. W oknie dialogowym **Wybieranie metody logowania jednokrotnego** wybierz tryb **SAML/WS-Fed**, aby włączyć logowanie jednokrotne.

    ![Wybieranie trybu logowania jednokrotnego](common/select-saml-option.png)

3. W innym oknie przeglądarki internetowej zaloguj się do firmowej witryny aplikacji Cisco Webex jako administrator.

4. Kliknij pozycję **Settings** (Ustawienia) w menu po lewej stronie.

    ![Konfigurowanie logowania jednokrotnego](./media/cisco-webex-tutorial/tutorial_cisco_webex_10.png)

5. Na stronie ustawień przewiń w dół i w sekcji **Authentication** (Uwierzytelnianie) kliknij pozycję **Modify** (Modyfikuj).

    ![Konfigurowanie logowania jednokrotnego](./media/cisco-webex-tutorial/tutorial_cisco_webex_14.png)

6. Wybierz pozycję **Integrate a 3rd-party identity provider. (Advanced)** (Integracja innego dostawcy tożsamości. (Zaawansowane)) i przejdź do następnego ekranu.

    ![Konfigurowanie logowania jednokrotnego](./media/cisco-webex-tutorial/tutorial_cisco_webex_15.png)

7. Na stronie **Export Directory Metadata** (Eksportowanie metadanych katalogu) kliknij pozycję **Download Metadata File** (Pobierz plik metadanych), aby pobrać plik metadanych.

    ![Konfigurowanie logowania jednokrotnego](./media/cisco-webex-tutorial/tutorial_cisco_webex_16.png)

8. W witrynie Azure Portal na stronie **Konfigurowanie logowania jednokrotnego za pomocą protokołu SAML** kliknij ikonę **Edytuj**, aby otworzyć okno dialogowe **Podstawowa konfiguracja protokołu SAML**.

    ![Edycja podstawowej konfiguracji protokołu SAML](common/edit-urls.png)

9. W sekcji **Podstawowa konfiguracja protokołu SAML** przekaż pobrany plik **metadanych dostawcy usług** i skonfiguruj aplikację, wykonując następujące kroki:

    a. Kliknij pozycję **Przekaż plik metadanych**.

    ![Przekazywanie pliku metadanych](common/upload-metadata.png)

    b. Kliknij **logo folderu**, aby wybrać plik metadanych, a następnie kliknij pozycję **Przekaż**.

    ![wybierz plik metadanych](common/browse-upload-metadata.png)

    d. Po pomyślnym ukończeniu przekazywania pliku metadanych dostawcy usług wartości **Identyfikator** i **Adres URL odpowiedzi** w sekcji **Podstawowa konfiguracja protokołu SAML** zostaną wypełnione automatycznie:

    ![Informacje dotyczące domeny i adresów URL logowania jednokrotnego aplikacji Cisco Webex](common/sp-identifier-reply.png)

    W polu tekstowym **Adres URL logowania** wpisz adres URL, korzystając z następującego wzorca: `https://<SUBDOMAIN>.webex.com/`

    > [!Note]
    > Wartość adresu URL logowania nie jest prawdziwa. Zaktualizuj tę wartość za pomocą rzeczywistego adresu URL logowania. W celu uzyskania tej wartości skontaktuj się z [zespołem pomocy technicznej klienta Cisco Webex](https://www.webex.co.in/support/support-overview.html).

10. Aplikacja Cisco Webex oczekuje asercji SAML w określonym formacie. Skonfiguruj następujące oświadczenia dla tej aplikacji. Wartościami tych atrybutów możesz zarządzać w sekcji **Atrybuty użytkownika** na stronie integracji aplikacji. Na stronie **Konfigurowanie logowania jednokrotnego za pomocą protokołu SAML** kliknij przycisk **Edytuj**, aby otworzyć okno dialogowe **Atrybuty użytkownika**.

    ![image](common/edit-attribute.png)

11. W sekcji **Oświadczenia użytkownika** w oknie dialogowym **Atrybuty użytkownika** skonfiguruj atrybut tokenu SAML, jak pokazano na ilustracji powyżej, i wykonaj następujące czynności:
    
    | Nazwa | Atrybut źródłowy|
    | ---------------| --------------- | --------- |
    |   firstname    | user.givenname |
    |   lastname    | user.surname |
    |   Identyfikator UID    | user.mail |

    a. Kliknij przycisk **Dodaj nowe oświadczenie**, aby otworzyć okno dialogowe **Zarządzanie oświadczeniami użytkownika**.

    ![image](common/new-save-attribute.png)

    ![image](common/new-attribute-details.png)

    b. W polu tekstowym **Nazwa** wpisz nazwę atrybutu pokazaną dla tego wiersza.

    d. Pozostaw pole **Przestrzeń nazw** puste.

    d. Dla opcji Źródło wybierz wartość **Atrybut**.

    e. Na liście **Atrybut źródłowy** wpisz wartość atrybutu pokazaną dla tego wiersza.

    f. Kliknij przycisk **OK**.

    g. Kliknij pozycję **Zapisz**.

12. Na stronie **Konfigurowanie logowania jednokrotnego za pomocą protokołu SAML** w sekcji **Certyfikat podpisywania SAML** kliknij link **Pobierz**, aby pobrać **kod XML metadanych federacji** na podstawie podanych opcji zgodnie z wymaganiami i zapisać go na komputerze.

    ![Link do pobierania certyfikatu](common/metadataxml.png)

13. W sekcji **Skonfiguruj aplikację Cisco Webex** skopiuj odpowiednie adresy URL zgodnie z wymaganiami.

    ![Kopiowanie adresów URL konfiguracji](common/copy-configuration-urls.png)

    a. Adres URL logowania

    b. Identyfikator usługi Azure AD

    d. Adres URL wylogowywania

### <a name="configure-cisco-webex-single-sign-on"></a>Konfigurowanie logowania jednokrotnego w aplikacji Cisco Webex

1. Na stronie administratora firmowej witryny aplikacji Cisco Webex użyj opcji przeglądania plików, aby znaleźć i przekazać plik metadanych usługi Azure AD. Następnie zaznacz opcję **Require certificate signed by a certificate authority in Metadata (more secure)** (Wymagaj certyfikatu podpisanego przez urząd certyfikacji w metadanych (bezpieczniejsze)) i przejdź do następnego ekranu. 

    ![Konfigurowanie logowania jednokrotnego](./media/cisco-webex-tutorial/tutorial_cisco_webex_11.png)

2. Wybierz pozycję **Test SSO Connection** (Testuj połączenie logowania jednokrotnego) i gdy zostanie otwarta nowa karta przeglądarki, uwierzytelnij się przy użyciu usługi Azure AD, logując się.

3. Wróć do karty przeglądarki **Cisco Cloud Collaboration Management**. Jeśli test zakończył się pomyślnie, wybierz pozycję **This test was successful. Enable Single Sign-On option** (Test zakończył się pomyślnie. Włącz opcję logowania jednokrotnego) i kliknij przycisk **Save** (Zapisz).

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

W tej sekcji włączysz dla użytkownika Britta Simon możliwość korzystania z logowania jednokrotnego platformy Azure, udzielając dostępu do aplikacji Cisco Webex.

1. W witrynie Azure Portal wybierz pozycję **Aplikacje dla przedsiębiorstw**, wybierz pozycję **Wszystkie aplikacje**, a następnie wybierz pozycję **Cisco Webex**.

    ![Blok Aplikacje dla przedsiębiorstw](common/enterprise-applications.png)

2. Na liście aplikacji wybierz pozycję **Cisco Webex**.

    ![Link aplikacji Cisco Webex na liście aplikacji](common/all-applications.png)

3. W menu po lewej stronie wybierz pozycję **Użytkownicy i grupy**.

    ![Link „Użytkownicy i grupy”](common/users-groups-blade.png)

4. Kliknij przycisk **Dodaj użytkownika**, a następnie wybierz pozycję **Użytkownicy i grupy** w oknie dialogowym **Dodawanie przypisania**.

    ![Okienko Dodawanie przypisania](common/add-assign-user.png)

5. W oknie dialogowym **Użytkownicy i grupy** wybierz użytkownika **Britta Simon** na liście użytkowników, a następnie kliknij przycisk **Wybierz** u dołu ekranu.

6. Jeśli oczekujesz wartości roli w asercji SAML, w oknie dialogowym **Wybieranie roli** wybierz z listy odpowiednią rolę dla użytkownika, a następnie kliknij przycisk **Wybierz** u dołu ekranu.

7. W oknie dialogowym **Dodawanie przypisania** kliknij przycisk **Przypisz**.

### <a name="create-cisco-webex-test-user"></a>Tworzenie użytkownika testowego aplikacji Cisco Webex

Celem tej sekcji jest utworzenie użytkownika o nazwie Britta Simon w aplikacji Cisco Webex. Aplikacja Cisco Webex obsługuje aprowizację typu just-in-time i automatyczną aprowizację użytkowników, która jest domyślnie włączona. W tej sekcji nie musisz niczego robić. Jeśli użytkownik jeszcze nie istnieje w aplikacji Cisco Webex, zostanie utworzony podczas próby uzyskania dostępu do aplikacji Cisco Webex.

### <a name="test-single-sign-on"></a>Testowanie logowania jednokrotnego

W tej sekcji przetestujesz konfigurację logowania jednokrotnego usługi Azure AD przy użyciu panelu dostępu.

Po kliknięciu kafelka Cisco Webex w panelu dostępu powinno nastąpić automatyczne zalogowanie do aplikacji Cisco Webex, dla której skonfigurowano logowanie jednokrotne. Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [Introduction to the Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) (Wprowadzenie do panelu dostępu).

## <a name="additional-resources"></a>Dodatkowe zasoby

- [ Lista samouczków dotyczących sposobu integrowania aplikacji SaaS z usługą Azure Active Directory ](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [Co to jest dostęp warunkowy w usłudze Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

