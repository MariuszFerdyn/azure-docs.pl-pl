---
title: Problemy z logowaniem do aplikacji galerii skonfigurowanego pod kątem federacyjnego logowania jednokrotnego | Dokumentacja firmy Microsoft
description: Wskazówki dotyczące konkretnego błędu podczas logowania się do aplikacji, które zostały skonfigurowane dla opartej na SAML federacyjne logowanie jednokrotne z usługą Azure AD
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/11/2017
ms.author: celested
ms.reviewer: asteen
ms.collection: M365-identity-device-management
ms.openlocfilehash: 45c6c217da21ff0d1b1168f61c7920328295c5d1
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56217976"
---
# <a name="problems-signing-in-to-a-gallery-application-configured-for-federated-single-sign-on"></a>Problemy z logowaniem do aplikacji galerii, skonfigurowanej do obsługi federacyjnego logowania jednokrotnego

Aby rozwiązać problem, należy sprawdzić konfigurację aplikacji w usłudze Azure AD następujące czynności:

-   Zostały wykonane wszystkie kroki konfiguracji dla aplikacji z galerii usługi Azure AD.

-   Identyfikator i adres URL odpowiedzi skonfigurowane w usłudze AAD dopasowania są oczekiwane wartości w aplikacji

-   Przypisano użytkowników do aplikacji

## <a name="application-not-found-in-directory"></a>Nie można odnaleźć w katalogu aplikacji

*Błąd AADSTS70001: Aplikacja z identyfikatorem "https://contoso.com" nie został znaleziony w katalogu*.

**Możliwa przyczyna**

Wystawcę, którego atrybut wysyła z aplikacji do usługi Azure AD w żądaniu języka SAML nie jest zgodna wartość identyfikatora skonfigurowaną w aplikacji usługi Azure AD.

**Rozdzielczość**

Upewnij się, że atrybut wystawcy żądania języka SAML jest zgodny, identyfikator wartości ustawionej w usłudze Azure AD:

1.  Otwórz [ **witryny Azure portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **Współadministratora.**

2.  Otwórz **rozszerzenia usługi Azure Active Directory** , klikając **wszystkich usług** w górnej części menu główne menu nawigacji po lewej stronie.

3.  Wpisz **"Azure Active Directory**" w polu wyszukiwania filtru i wybierz pozycję **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** menu nawigacji po lewej stronie usługi Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.

  * Jeśli nie widzisz aplikacji, chcesz, aby wyświetlić tutaj użyć **filtru** formant w górnej części **listę wszystkich aplikacji** i ustaw **Pokaż** opcję **wszystkie Aplikacje.**

6.  Wybierz aplikację, którą chcesz skonfigurować logowanie jednokrotne

7.  Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** menu nawigacji po lewej stronie aplikacji.

8.  Przejdź do **domena i adresy URL** sekcji. Upewnij się, że wartość w polu tekstowym identyfikatora jest zgodny wartość identyfikatora wyświetlane w błędzie.

Po zaktualizowaniu wartość identyfikatora w usłudze Azure AD i jest on zgodny wysyła wartość przez aplikację w żądaniu języka SAML, należy zalogować się do aplikacji.

## <a name="the-reply-address-does-not-match-the-reply-addresses-configured-for-the-application"></a>Adres, który jest niezgodny z adresy zwrotne skonfigurowane dla aplikacji.

*Błąd AADSTS50011: Jako adres zwrotny https://contoso.com"jest niezgodny z adresy zwrotne skonfigurowane dla aplikacji*

**Możliwa przyczyna**

Wartość AssertionConsumerServiceURL w żądaniu języka SAML nie jest zgodna wartość adresu URL odpowiedzi lub wzorzec skonfigurowane w usłudze Azure AD. Wartość AssertionConsumerServiceURL w żądaniu języka SAML jest adres URL, zostanie wyświetlony w błędzie.

**Rozdzielczość**

Upewnij się, że wartość AssertionConsumerServiceURL w żądaniu języka SAML jest zgodny, adres URL odpowiedzi wartości ustawionej w usłudze Azure AD.

1.  Otwórz [ **witryny Azure portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **Współadministratora.**

2.  Otwórz **rozszerzenia usługi Azure Active Directory** , klikając **wszystkich usług** w górnej części menu główne menu nawigacji po lewej stronie.

3.  Wpisz **"Azure Active Directory**" w polu wyszukiwania filtru i wybierz pozycję **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** menu nawigacji po lewej stronie usługi Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.

  * Jeśli nie widzisz aplikacji, chcesz, aby wyświetlić tutaj użyć **filtru** formant w górnej części **listę wszystkich aplikacji** i ustaw **Pokaż** opcję **wszystkie Aplikacje.**

6.  Wybierz aplikację, którą chcesz skonfigurować logowanie jednokrotne

7.  Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** menu nawigacji po lewej stronie aplikacji.

8.  Przejdź do **domena i adresy URL** sekcji. Sprawdź lub zaktualizuj tę wartość w polu tekstowym adres URL odpowiedzi być zgodna z wartością AssertionConsumerServiceURL żądania języka SAML.  
    * Jeśli w polu tekstowym adres URL odpowiedzi nie jest widoczny, wybierz opcję **Pokaż zaawansowane ustawienia adresu URL** pola wyboru.

Po zaktualizowaniu wartość adresu URL odpowiedzi w usłudze Azure AD i jest on zgodny wysyła wartość przez aplikację w żądaniu języka SAML, należy zalogować się do aplikacji.

## <a name="user-not-assigned-a-role"></a>Nie przypisaną rolę użytkownika

*Błąd AADSTS50105: Zalogowany użytkownik "brian@contoso.com" nie jest przypisany do roli aplikacji*.

**Możliwa przyczyna**

Użytkownikowi nie udzielono dostępu do aplikacji w usłudze Azure AD.

**Rozdzielczość**

Aby przypisać co najmniej jednego użytkownika do aplikacji bezpośrednio, wykonaj następujące czynności:

1.  Otwórz [ **witryny Azure portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz **rozszerzenia usługi Azure Active Directory** , klikając **wszystkich usług** w górnej części menu główne menu nawigacji po lewej stronie.

3.  Wpisz **"Azure Active Directory**" w polu wyszukiwania filtru i wybierz pozycję **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** menu nawigacji po lewej stronie usługi Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.

  * Jeśli nie widzisz aplikacji, chcesz, aby wyświetlić tutaj użyć **filtru** formant w górnej części **listę wszystkich aplikacji** i ustaw **Pokaż** opcję **wszystkie Aplikacje.**

6.  Wybierz aplikację, którą chcesz przypisać do użytkownika z listy.

7.  Po załadowaniu aplikacji, kliknij przycisk **użytkowników i grup** menu nawigacji po lewej stronie aplikacji.

8.  Kliknij przycisk **Dodaj** przycisk w górnej części **użytkowników i grup** liście, aby otworzyć **Dodaj przydziału** okienka.

9.  Kliknij przycisk **użytkowników i grup** selektor z **Dodaj przydziału** okienka.

10. Wpisz **Pełna nazwa** lub **adres e-mail** użytkownika, jesteś zainteresowany przypisywania do **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.

11. Umieść kursor nad **użytkownika** na liście, aby wyświetlić **wyboru**. Kliknij pole wyboru obok logo, aby dodać użytkownika, aby lub zdjęcie w profilu użytkownika **wybrane** listy.

12. **Opcjonalnie:** Jeśli chcesz **dodać więcej niż jednego użytkownika**, typ w innym **Pełna nazwa** lub **adres e-mail** do **wyszukiwanie według nazwy lub adresu e-mail** pole wyszukiwania, a następnie kliknij pole wyboru, aby dodać użytkownika do **wybrane** listy.

13. Gdy to zrobisz, Wybieranie użytkowników, kliknij przycisk **wybierz** przycisk, aby dodać je do listy użytkowników i grup do przypisania do aplikacji.

14. **Opcjonalnie:** kliknij **wybierz rolę** selektorze **Dodaj przydziału** okienku wybierz rolę, aby przypisać użytkownikom wybrania.

15. Kliknij przycisk **przypisać** przycisk, aby przypisać aplikację do wybranych użytkowników.

Po krótkim czasie użytkowników, dla których wybrano mogli uruchamiać te aplikacje za pomocą metod opisanych w sekcji Opis rozwiązania.

## <a name="not-a-valid-saml-request"></a>Nie prawidłowe żądania języka SAML

*Błąd AADSTS75005: Żądanie nie jest prawidłowy komunikat protokołu Saml2.*

**Możliwa przyczyna**

Usługa Azure AD nie obsługuje żądania SAML wysłanego przez aplikację na potrzeby logowania jednokrotnego. Niektóre typowe problemy to:

-   Brak wymaganych pól w żądaniu języka SAML

-   SAML zakodowana metoda żądania

**Rozdzielczość**

1.  Przechwyć żądanie języka SAML. Postępuj zgodnie z samouczkiem [sposób debugowania opartej na SAML logowania jednokrotnego do aplikacji w usłudze Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) Aby dowiedzieć się, jak przechwytywać żądania języka SAML.

2.  Skontaktuj się z dostawcą aplikacji i udziału:

   -   Żądanie języka SAML

   -   [Wymagania protokołu usługi Azure AD pojedynczego logowania jednokrotnego SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

Należy sprawdzić poprawność ich obsługa wdrożenia usługi Azure AD SAML logowania jednokrotnego.

## <a name="no-resource-in-requiredresourceaccess-list"></a>Żaden z zasobów na liście requiredResourceAccess

*Błąd AADSTS65005: aplikacja kliencka zażądała dostępu do zasobu "00000002-0000-0000-c000-000000000000'. To żądanie nie powiodło się, ponieważ klient nie określił ten zasób na liście requiredResourceAccess*.

**Możliwa przyczyna**

Obiekt aplikacji jest uszkodzony.

**Rozwiązywania konfliktów: opcji 1**

Aby rozwiązać ten problem, Dodaj wartość Unikatowy identyfikator w konfiguracji usługi Azure AD. Aby dodać wartości identyfikatora, wykonaj następujące czynności:

1.  Otwórz [ **witryny Azure portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **Współadministratora.**

2.  Otwórz **rozszerzenia usługi Azure Active Directory** , klikając **wszystkich usług** w górnej części menu główne menu nawigacji po lewej stronie.

3.  Wpisz **"Azure Active Directory**" w polu wyszukiwania filtru i wybierz pozycję **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** menu nawigacji po lewej stronie usługi Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.

  * Jeśli nie widzisz aplikacji, chcesz, aby wyświetlić tutaj użyć **filtru** formant w górnej części **listę wszystkich aplikacji** i ustaw **Pokaż** opcję **wszystkie Aplikacje.**

6.  Wybierz aplikację, zostały skonfigurowane logowanie jednokrotne.

7.  Po załadowaniu aplikacji, kliknij pozycję **logowanie jednokrotne** menu nawigacji po lewej stronie aplikacji

8.  W obszarze **domeny i adres URL** sekcji, sprawdź na **Pokaż zaawansowane ustawienia adresu URL**.

9.  w **identyfikator** pola tekstowego wpisz unikatowy identyfikator dla aplikacji.

10. **Zapisz** konfiguracji.


**Opcja rozpoznawania 2**

Jeśli opcja 1 powyżej zakończyło się niepowodzeniem dla Ciebie, spróbuj usunięcie aplikacji z katalogu. Następnie należy dodać i zmiany konfiguracji aplikacji, wykonaj następujące czynności:

1.  Otwórz [ **witryny Azure portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **Współadministratora.**

2.  Otwórz **rozszerzenia usługi Azure Active Directory** , klikając **wszystkich usług** w górnej części menu główne menu nawigacji po lewej stronie.

3.  Wpisz **"Azure Active Directory**" w polu wyszukiwania filtru i wybierz pozycję **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** menu nawigacji po lewej stronie usługi Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.

  * Jeśli nie widzisz aplikacji, chcesz, aby wyświetlić tutaj użyć **filtru** formant w górnej części **listę wszystkich aplikacji** i ustaw **Pokaż** opcję **wszystkie Aplikacje.**

6.  Wybierz aplikację, którą chcesz skonfigurować logowanie jednokrotne

7.  Kliknij przycisk **Usuń** w lewym górnym aplikacji **Przegląd** okienka.

8.  Odświeżenie usługi Azure AD, a następnie dodać tę aplikację z galerii usługi Azure AD. Następnie należy skonfigurować aplikację

<span id="_Hlk477190176" class="anchor"></span>Po ponownej konfiguracji aplikacji, można zalogować się do aplikacji.

## <a name="certificate-or-key-not-configured"></a>Certyfikatu lub klucza nieskonfigurowane

*Błąd AADSTS50003: Nie skonfigurowano klucza podpisywania.*

**Możliwa przyczyna**

Obiekt aplikacji jest uszkodzony, i usługi Azure AD nie rozpoznaje certyfikatu skonfigurowanego dla aplikacji.

**Rozdzielczość**

Aby usunąć i utworzyć nowy certyfikat, wykonaj następujące czynności:

1.  Otwórz [ **witryny Azure portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **Współadministratora.**

2.  Otwórz **rozszerzenia usługi Azure Active Directory** , klikając **wszystkich usług** w górnej części menu główne menu nawigacji po lewej stronie.

3.  Wpisz **"Azure Active Directory**" w polu wyszukiwania filtru i wybierz pozycję **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** menu nawigacji po lewej stronie usługi Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.

 * Jeśli nie widzisz aplikacji, chcesz, aby wyświetlić tutaj użyć **filtru** formant w górnej części **listę wszystkich aplikacji** i ustaw **Pokaż** opcję **wszystkie Aplikacje.**

6.  Wybierz aplikację, którą chcesz skonfigurować logowanie jednokrotne

7.  Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** menu nawigacji po lewej stronie aplikacji.

8.  Kliknij przycisk **Utwórz nowy certyfikat** w obszarze **certyfikat podpisywania SAML** sekcji.

9.  Wybierz datę wygaśnięcia. Następnie kliknij przycisk **Zapisz.**

10. Sprawdź **Ustaw nowy certyfikat jako aktywny** przesłonić aktywny certyfikat. Następnie kliknij przycisk **Zapisz** u góry okienka i zaakceptuj, aby uaktywnić certyfikat przerzucania.

11. W obszarze **certyfikat podpisywania SAML** kliknij **Usuń** do usunięcia **nieużywane** certyfikatu.

## <a name="saml-request-not-present-in-the-request"></a>Żądanie języka SAML nie znajduje się w żądaniu

*Błąd AADSTS750054: SAMLRequest lub SAMLResponse musi być obecny, ponieważ parametry ciągu w żądaniu HTTP do przekierowania protokołu SAML powiązania zapytania.*

**Możliwa przyczyna**

Usługa Azure AD nie był w stanie zidentyfikować żądanie języka SAML, w ramach parametrów adresu URL w żądaniu HTTP. Może to nastąpić, jeśli aplikacja nie używa przekierować powiązanie HTTP do wysłania żądania języka SAML do usługi Azure AD.

**Rozdzielczość**

Aplikacja musi wysyłać żądania języka SAML, kodowane do Nagłówek lokalizacji przy użyciu protokołu HTTP, przekierowanie powiązania. Aby dowiedzieć się więcej o sposobie implementacji, zapoznaj się z sekcją przekierować powiązanie HTTP w [dokument specyfikacji protokołu SAML](https://docs.oasis-open.org/security/saml/v2.0/saml-bindings-2.0-os.pdf).


## <a name="problem-when-customizing-the-saml-claims-sent-to-an-application"></a>Problem podczas dostosowywania oświadczenia języka SAML wysyłane do aplikacji

Aby dowiedzieć się, jak dostosować oświadczeń atrybutów SAML, które są wysyłane do aplikacji, zobacz [Mapowanie oświadczeń w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) Aby uzyskać więcej informacji.

## <a name="next-steps"></a>Kolejne kroki
[Jak debugować opartej na SAML logowania jednokrotnego do aplikacji w usłudze Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)
