---
title: 'Samouczek: Integracja usługi Azure Active Directory za pomocą ThirdLight | Dokumentacja firmy Microsoft'
description: Dowiedz się, jak skonfigurować logowanie jednokrotne między usługi Azure Active Directory i ThirdLight.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: 168aae9a-54ee-4c2b-ab12-650a2c62b901
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: f01c870316a4e7c9424bd63766fec0fed1dce7a3
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56167188"
---
# <a name="tutorial-azure-active-directory-integration-with-thirdlight"></a>Samouczek: Integracja usługi Azure Active Directory za pomocą ThirdLight

W tym samouczku dowiesz się, jak zintegrować ThirdLight w usłudze Azure Active Directory (Azure AD).

Integrowanie ThirdLight z usługą Azure AD zapewnia następujące korzyści:

- Możesz kontrolować w usłudze Azure AD, kto ma dostęp do ThirdLight
- Umożliwia użytkownikom automatyczne pobieranie zalogowanych do ThirdLight (logowanie jednokrotne) przy użyciu konta usługi Azure AD
- Możesz zarządzać konta w jednej centralnej lokalizacji — witryny Azure portal

Jeśli chcesz dowiedzieć się więcej na temat integracji aplikacji SaaS z usługą Azure AD, zobacz [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD za pomocą ThirdLight, potrzebne są następujące elementy:

- Subskrypcji usługi Azure AD
- ThirdLight logowania jednokrotnego włączonych subskrypcji

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.

Aby przetestować czynności opisane w tym samouczku, należy postępować zgodnie z następującymi zaleceniami:

- Nie używaj środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowiska próbnego usługi Azure AD, możesz skorzystać z miesięcznej wersji próbnej [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W ramach tego samouczka można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz opisany w tym samouczku składa się z dwóch głównych bloków konstrukcyjnych:

1. Dodawanie ThirdLight z galerii
1. Konfigurowanie i testowania usługi Azure AD logowanie jednokrotne

## <a name="adding-thirdlight-from-the-gallery"></a>Dodawanie ThirdLight z galerii
Aby skonfigurować integrację ThirdLight w usłudze Azure AD, należy dodać ThirdLight z galerii z listą zarządzanych aplikacji SaaS.

**Aby dodać ThirdLight z galerii, wykonaj następujące czynności:**

1. W **[witryny Azure portal](https://portal.azure.com)**, w panelu nawigacyjnym po lewej stronie kliknij pozycję **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

1. Przejdź do **aplikacje dla przedsiębiorstw**. Następnie przejdź do **wszystkie aplikacje**.

    ![Aplikacje][2]
    
1. Aby dodać nową aplikację, kliknij przycisk **Nowa aplikacja** w górnej części okna dialogowego.

    ![Aplikacje][3]

1. W polu wyszukiwania wpisz **ThirdLight**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/thirdlight-tutorial/tutorial_thirdlight_search.png)

1. W panelu wyników wybierz **ThirdLight**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/thirdlight-tutorial/tutorial_thirdlight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowania usługi Azure AD logowanie jednokrotne
W tej sekcji Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne za pomocą ThirdLight w oparciu o użytkownika testu o nazwie "Britta Simon."

Dla logowania jednokrotnego do pracy usługi Azure AD musi znać użytkownika odpowiednika w ThirdLight do użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i powiązanego użytkownika w ThirdLight musi można ustanowić.

Ustanowieniu tej relacji łączy, przypisując wartość **nazwa_użytkownika** w usłudze Azure AD jako wartość **Username** w ThirdLight.

Aby skonfigurować i testowanie usługi Azure AD logowanie jednokrotne za pomocą ThirdLight, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie usługi Azure AD logowania jednokrotnego](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.
1. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD logowanie jednokrotne za pomocą Britta Simon.
1. **[Tworzenie użytkownika testowego ThirdLight](#creating-a-thirdlight-test-user)**  — aby odpowiednikiem Britta Simon w ThirdLight połączonego z usługi Azure AD reprezentacja użytkownika.
1. **[Przypisywanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — Aby włączyć Britta Simon korzystać z usługi Azure AD logowania jednokrotnego.
1. **[Testowanie logowania jednokrotnego](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD logowania jednokrotnego

W tej sekcji możesz włączyć usługi Azure AD logowania jednokrotnego w witrynie Azure portal i konfigurowanie logowania jednokrotnego w aplikacji ThirdLight.

**Aby skonfigurować usługę Azure AD logowanie jednokrotne z ThirdLight, wykonaj następujące czynności:**

1. W witrynie Azure portal na **ThirdLight** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie logowania jednokrotnego][4]

1. Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **opartej na SAML logowania jednokrotnego** włączyć logowanie jednokrotne.
 
    ![Konfigurowanie logowania jednokrotnego](./media/thirdlight-tutorial/tutorial_thirdlight_samlbase.png)

1. Na **ThirdLight domena i adresy URL** sekcji, wykonaj następujące czynności:

    ![Konfigurowanie logowania jednokrotnego](./media/thirdlight-tutorial/tutorial_thirdlight_url.png)

    a. W polu tekstowym **Adres URL logowania** wpisz adres URL, korzystając z następującego wzorca: `https://<subdomain>.thirdlight.com/`

    b. W polu tekstowym **Identyfikator** wpisz adres URL, korzystając z następującego wzorca: `https://<subdomain>.thirdlight.com/saml/sp`

    > [!NOTE] 
    > Te wartości nie są prawdziwe. Rzeczywisty adres URL logowania i Identiifer, należy zaktualizować te wartości. Skontaktuj się z pomocą [zespołem pomocy technicznej klienta ThirdLight](https://www.thirdlight.com/support) do uzyskania tych wartości. 
 
1. Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.

    ![Konfigurowanie logowania jednokrotnego](./media/thirdlight-tutorial/tutorial_thirdlight_certificate.png) 

1. Kliknij przycisk **Save** (Zapisz).

    ![Konfigurowanie logowania jednokrotnego](./media/thirdlight-tutorial/tutorial_general_400.png)

1. W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy ThirdLight.

1. Przejdź do **konfiguracji \> administrowania systemem**, a następnie kliknij przycisk **SAML2**.
   
    ![Administrowanie systemem](./media/thirdlight-tutorial/ic805843.png "Administracja systemu")

1. W sekcji konfiguracji SAML2 wykonaj następujące czynności:
   
    ![SAML logowania jednokrotnego](./media/thirdlight-tutorial/ic805844.png "SAML logowania jednokrotnego")   

     a. Wybierz **Włącz SAML2 logowania jednokrotnego**.
 
     b. Jako **źródło metadanych tożsamości**, wybierz opcję **Load Metadata dostawcy tożsamości z pliku XML**.
 
     c. Otwórz plik metadanych pobrany, skopiuj zawartość, a następnie wklej go do **XML metadanych dostawcy tożsamości** pola tekstowego. 
     
     d. Kliknij przycisk **ustawień zapisywanie SAML2**.

> [!TIP]
> Teraz możesz korzystać ze zwięzłej wersji tych instrukcji w witrynie [Azure Portal](https://portal.azure.com) podczas konfigurowania aplikacji.  Po dodaniu tej aplikacji z sekcji **Active Directory > Aplikacje dla przedsiębiorstw** wystarczy kliknąć kartę **Logowanie jednokrotne** i uzyskać dostęp do osadzonej dokumentacji za pośrednictwem sekcji  **Konfiguracja** w dolnej części strony. Dalsze informacje o funkcji dokumentacji osadzonej można znaleźć tutaj: [Osadzona dokumentacja usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
W tej sekcji w witrynie Azure Portal utworzysz użytkownika testowego o nazwie Britta Simon.

![Utwórz użytkownika usługi Azure AD][100]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W **witryny Azure portal**, w okienku nawigacji po lewej stronie kliknij **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/thirdlight-tutorial/create_aaduser_01.png) 

1. Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/thirdlight-tutorial/create_aaduser_02.png) 

1. Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/thirdlight-tutorial/create_aaduser_03.png) 

1. Na **użytkownika** okna dialogowego strony, wykonaj następujące czynności:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/thirdlight-tutorial/create_aaduser_04.png) 

    a. W **nazwa** polu tekstowym wpisz **BrittaSimon**.

    b. W **nazwa_użytkownika** polu tekstowym wpisz **adres e-mail** obiektu Britta Simon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.

    d. Kliknij pozycję **Utwórz**.
 
### <a name="creating-a-thirdlight-test-user"></a>Tworzenie użytkownika testowego ThirdLight

Aby umożliwić użytkownikom usługi Azure AD, zaloguj się do ThirdLight, musi być obsługiwana w ThirdLight.  
W przypadku ThirdLight Inicjowanie obsługi administracyjnej jest zadanie ręczne.

**Aby aprowizować konto użytkownika, wykonaj następujące kroki:**

1. Zaloguj się do Twojej **ThirdLight** witryny firmy jako administrator.

1. Przejdź do **użytkowników** kartę.

1. Wybierz **użytkowników i grup**.

1. Kliknij przycisk **Dodaj nowego użytkownika** przycisku.

1. Wprowadź **nazwy użytkownika, nazwa lub opis, adres E-mail, wybierz ustawienie wstępne lub grupy nowych członków** poprawnego konta usługi AAD do aprowizowania.

1. Kliknij pozycję **Utwórz**.

>[!NOTE]
>Można użyć jakichkolwiek innych Thirdlight użytkownika konta tworzenie narzędzi lub interfejsów API dostarczonych przez Thirdlight do aprowizacji kont użytkowników usługi AAD. 

### <a name="assigning-the-azure-ad-test-user"></a>Przypisywanie użytkownika testowego usługi Azure AD

W tej sekcji możesz włączyć Britta Simon do używania usługi Azure logowanie jednokrotne za udzielanie dostępu do ThirdLight.

![Przypisz użytkownika][200] 

**Aby przypisać Britta Simon ThirdLight, wykonaj następujące czynności:**

1. W witrynie Azure portal Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

1. Na liście aplikacji wybierz **ThirdLight**.

    ![Konfigurowanie logowania jednokrotnego](./media/thirdlight-tutorial/tutorial_thirdlight_app.png) 

1. W menu po lewej stronie kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

1. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz pozycję **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

1. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Britta Simon** na liście Użytkownicy.

1. Kliknij przycisk **wybierz** znajdujący się na **użytkowników i grup** okna dialogowego.

1. Kliknij przycisk **przypisać** znajdujący się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie logowania jednokrotnego

W tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu panelu dostępu.

Po kliknięciu kafelka ThirdLight w panelu dostępu, użytkownik powinien uzyskać automatycznie zalogowanych do aplikacji ThirdLight.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md) (Wprowadzenie do panelu dostępu). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących integrowania aplikacji SaaS w usłudze Azure Active Directory](tutorial-list.md)
* [Czym jest dostęp do aplikacji i logowanie jednokrotne za pomocą usługi Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/thirdlight-tutorial/tutorial_general_01.png
[2]: ./media/thirdlight-tutorial/tutorial_general_02.png
[3]: ./media/thirdlight-tutorial/tutorial_general_03.png
[4]: ./media/thirdlight-tutorial/tutorial_general_04.png

[100]: ./media/thirdlight-tutorial/tutorial_general_100.png

[200]: ./media/thirdlight-tutorial/tutorial_general_200.png
[201]: ./media/thirdlight-tutorial/tutorial_general_201.png
[202]: ./media/thirdlight-tutorial/tutorial_general_202.png
[203]: ./media/thirdlight-tutorial/tutorial_general_203.png

