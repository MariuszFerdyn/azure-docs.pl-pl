---
title: Porównywanie punktu końcowego v2.0 usługi Azure AD z punktem końcowym v1.0 | Dokumentacja firmy Microsoft
description: Znasz różnice między punktu końcowego v2.0 usługi Azure AD i punktu końcowego w wersji 1.0
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: 5060da46-b091-4e25-9fa8-af4ae4359b6c
ms.service: active-directory
ms.subservice: develop
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2018
ms.author: celested
ms.reviewer: hirsin, andret, jmprieur, sureshja, jesakowi, lenalepa, kkrishna, dadobali, negoe
ms.custom: aaddev
ms.collection: M365-identity-device-management
ms.openlocfilehash: 075df3d0834d70b8deb7c224c3f6b1cceb46fd7a
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56185965"
---
# <a name="comparing-the-azure-ad-v20-endpoint-with-the-v10-endpoint"></a>Porównywanie punktu końcowego v2.0 usługi Azure AD przy użyciu punktu końcowego w wersji 1.0

Podczas tworzenia nowej aplikacji, należy znać różnice między punktami końcowymi w wersji 1.0 i 2.0 usługi Azure Active Directory (Azure AD). W tym artykule opisano główne różnice między punktami końcowymi, a niektóre istniejące ograniczenia dla punktu końcowego v2.0.

> [!NOTE]
> Punkt końcowy v2.0 nie obsługuje wszystkich scenariuszy usługi Azure AD i funkcji. Aby ustalić, należy użyć punktu końcowego v2.0, przeczytaj temat [ograniczenia v2.0](#limitations).

## <a name="who-can-sign-in"></a>Kto może się zarejestrować

![Kto może zalogować się przy użyciu punktów końcowych w wersji 1.0 i 2.0](media/azure-ad-endpoint-comparison/who-can-sign-in.png)

* Punkt końcowy v1.0 pozwala tylko kont służbowych zalogować się do aplikacji (Azure AD)
* Punkt końcowy v2.0 umożliwia roboczych i kont służbowych z usługi Azure AD i osobistych kont Microsoft (MSA), np. hotmail.com, outlook.com i msn.com, aby zalogować się.
* Punkty końcowe w wersji 1.0 i 2.0 także zaakceptować logowania z *[użytkowników-gości](https://docs.microsoft.com/azure/active-directory/b2b/what-is-b2b)* katalogu usługi Azure AD dla aplikacji skonfigurowanych jako *[pojedynczej dzierżawy](single-and-multi-tenant-apps.md)* lub *wielodostępnych* aplikacji skonfigurowanych do punktu z punktem końcowym specyficznym dla dzierżawy (`https://login.microsoftonline.com/{TenantId_or_Name}`).

Punkt końcowy v2.0 umożliwia pisanie aplikacji, które akceptują logowania z osobistych kont Microsoft i kont służbowych. Zapewnia możliwość pisania całkowicie konta niezależny od aplikacji. Na przykład, jeśli aplikacja odwołuje się [programu Microsoft Graph](https://graph.microsoft.io), niektóre dodatkowe funkcje i dane będą dostępne dla konta, takie jak ich witryny programu SharePoint lub dane katalogu. Jednak wiele akcji takich jak [czytanie poczty użytkownika](https://developer.microsoft.com/graph/docs/api-reference/v1.0/api/user_list_messages), ten sam kod mogą uzyskiwać dostęp do poczty e-mail dla zarówno osobistych i kont służbowych.

Dla punktu końcowego v2.0 Biblioteka Microsoft Authentication Library (MSAL) służy do uzyskania dostępu do konsumentów, edukacji i środowiska przedsiębiorstwa. Punkt końcowy usługi Azure AD w wersji 1.0 akceptuje logowania z tylko kont służbowych.

## <a name="incremental-and-dynamic-consent"></a>Przyrostowe i dynamiczne zgody

Aplikacji przy użyciu punktu końcowego usługi Azure AD w wersji 1.0 są wymagane, aby określić ich wymaganych uprawnień OAuth 2.0 z wyprzedzeniem, na przykład:

![Uprawnienia rejestracji interfejsu użytkownika](./media/azure-ad-endpoint-comparison/app_reg_permissions.png)

Uprawnienia ustawione bezpośrednio na rejestrowanie aplikacji są **statyczne**. Podczas statycznej uprawnienia aplikacji zdefiniowane w witrynie Azure portal zachować zgodność kodu nieuprzywilejowany i proste, przedstawia niektóre potencjalne problemy dla deweloperów:

* Aplikacja musi zażądać uprawnień, które nigdy nie będą potrzebne po użytkownik pierwsze logowanie. Może to prowadzić do długą listę uprawnień, które zniechęcać użytkowników końcowych do zatwierdzania aplikacji dostęp do początkowego logowania.

* Aplikacja musi wiedzieć, wszystkie zasoby, które nigdy nie dostęp do wcześniej. Trudno było je tworzyć aplikacje, które można uzyskać dostępu dowolną liczbę zasobów.

Z punktem końcowym v2.0 możesz zignorować statyczne uprawnienia zdefiniowane w informacje o rejestracji aplikacji w portalu i żądania uprawnień platformy Azure przyrostowo zamiast tego, co oznacza pytaniem, czy są dostępne bez minimalny zestaw uprawnień z wyprzedzeniem i bardziej przypadający wraz z upływem czasu jak długo klient używa funkcji dodatkowych aplikacji. Aby to zrobić, można określić zakresy, Twoja aplikacja wymaga w dowolnym momencie przez nowe zakresy, w tym `scope` parametru podczas żądania tokenu dostępu — bez konieczności wstępnego definiowania ich informacji o rejestracji aplikacji. Jeśli użytkownik jeszcze nie wyrażono zgodę nowe zakresy dodawana do żądania, monitowani będzie zgody tylko do nowych uprawnień. Aby dowiedzieć się więcej, zobacz [uprawnienia, wyrażania zgody i zakresy](v2-permissions-and-consent.md).

Zezwolenie aplikacji, aby zażądać uprawnień dynamicznie za pomocą `scope` parametru daje deweloperom pełną kontrolę nad środowiskiem użytkownika. Można również frontonu obciążenia swoją zgodę środowisko i poproś o wszystkie uprawnienia w jednym żądaniu początkowej autoryzacji. Jeśli aplikacja wymaga dużej liczby uprawnień, można gromadzić te uprawnienia od użytkownika przyrostowo kiedy będą próbowali określonych funkcji aplikacji wraz z upływem czasu.

Zgoda administratora wykonywane w imieniu organizacji nadal wymaga statycznego uprawnień zarejestrowany dla aplikacji, więc należy ustawić te uprawnienia dla aplikacji w portalu rejestracji aplikacji, jeśli administrator musisz wyrazić zgodę w imieniu całej organizacji. Zmniejsza to cykle wymaganego przez administratora organizacji, aby skonfigurować aplikację.

## <a name="scopes-not-resources"></a>Zakresy, nie zasobów

W przypadku aplikacji przy użyciu punktu końcowego v1.0 aplikacji mogą zachowywać się jak **zasobów**, lub odbiorcy tokenów. Zasób można zdefiniować wiele **zakresy** lub **oAuth2Permissions** siebie, dzięki czemu klienta aplikacji, aby żądać tokenów z zasobu na potrzeby określone zakresy. Należy wziąć pod uwagę interfejsu API programu Graph usługi Azure AD, na przykład zasób:

* Identyfikator zasobu lub `AppID URI`: `https://graph.windows.net/`
* Zakresy, lub `oAuth2Permissions`: `Directory.Read`, `Directory.Write`i tak dalej.

Prawdziwe dla punktu końcowego v2.0. Aplikacja, nadal może zachowywać się jako zasób, Definiowanie zakresów i być identyfikowany przez identyfikator URI. Aplikacje klienckie nadal może zażądać dostępu do tych zakresów. Jednak zmienił się sposób, że klient żąda te uprawnienia. 

Dla punktu końcowego w wersji 1.0, OAuth 2.0 autoryzować żądania do usługi Azure AD może być sprawdzono, takich jak:

```text
GET https://login.microsoftonline.com/common/oauth2/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&resource=https://graph.windows.net/
...
```

W tym miejscu **zasobów** parametru wskazane zasobu, który aplikacja kliencka żąda autoryzacji. Usługa Azure AD obliczane uprawnień wymaganych przez aplikację na podstawie konfiguracji statycznej w witrynie Azure portal i w związku z tym wystawionych tokenów. 

W przypadku aplikacji przy użyciu punktu końcowego v2.0 tego samego protokołu OAuth 2.0 zezwalają na żądanie wygląda:

```text
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&scope=https://graph.windows.net/directory.read%20https://graph.windows.net/directory.write
...
```

W tym miejscu **zakres** parametr wskazuje, które zasobu i uprawnień aplikacja żąda autoryzacji. Żądany zasób jest nadal znajdują się na żądanie — on ujęty w każdej wartości parametru zakresu. Za pomocą parametru zakresu w ten sposób umożliwia punktem końcowym v2.0 za bardziej zgodny ze specyfikacją protokołu OAuth 2.0 i lepiej wyrównane typowe rozwiązania w branży. Umożliwia aplikacji przeprowadzenie [przyrostowe zgody](#incremental-and-dynamic-consent) — tylko żądające uprawnień, gdy aplikacja wymaga ich w przeciwieństwie do góry.

## <a name="well-known-scopes"></a>Dobrze znane zakresów

### <a name="offline-access"></a>Dostęp w trybie offline

Aplikacje korzystające z punktem końcowym v2.0 może wymagać korzystanie z nowego uprawnienia dobrze znanych dla aplikacji — `offline_access` zakresu. Wszystkie aplikacje, należy zażądać tego uprawnienia, gdy potrzebują dostępu do zasobów w imieniu użytkownika przez dłuższy okres czasu, nawet wtedy, gdy użytkownik może nie być aktywnie przy użyciu aplikacji. `offline_access` Użytkownikowi w oknach dialogowych wyrażania zgody, jak będzie wyglądać zakres **uzyskiwać dostęp do danych w dowolnym momencie**, które użytkownik musi wyrazić zgodę na. Żądanie `offline_access` uprawnień spowoduje włączenie aplikacji sieci web do odbierania refresh_tokens OAuth 2.0 z punktem końcowym v2.0. Odśwież tokeny są długotrwałe i mogły być wymieniane przez dłuższy czas dostępu dla nowych tokenów dostępu protokołu OAuth 2.0.

Jeśli aplikacja nie żądania `offline_access` zakresu, nie będzie ona otrzymywać tokenów odświeżania. Oznacza to, że po wprowadzeniu kodu autoryzacji w przepływ kodu autoryzacji OAuth 2.0, tylko otrzymasz ponownie tokenu dostępu z `/token` punktu końcowego. Który dostęp do tokenu pozostaje prawidłowy krótki czas (zazwyczaj jedna godzina), ale wygaśnie po pewnym czasie. W tym punktu w czasie Twojej aplikacji będą musieli przekieruje użytkownika z powrotem do `/authorize` punktu końcowego, aby pobrać nowy kod autoryzacji. Podczas tego przekierowania użytkownik może lub nie trzeba ponownie wprowadzić swoje poświadczenia lub reconsent uprawnień, w zależności od typu aplikacji.

Aby dowiedzieć się więcej na temat protokołu OAuth 2.0 `refresh_tokens`, i `access_tokens`, zapoznaj się z [referencyjne protokołu v2.0](active-directory-v2-protocols.md).

### <a name="openid-profile-and-email"></a>OpenID, profilu i wiadomości e-mail

W przeszłości, najbardziej podstawowa przepływ protokołu OpenID Connect logowania w usłudze Azure AD będzie dostarczali mnóstwa informacji o użytkowniku w wynikowym *id_token*. Oświadczenia w id_token mogą obejmować nazwy, preferowany nazwy użytkownika, adres e-mail, identyfikator obiektu i więcej.

Informacje, `openid` zakresu daje aplikacji dostęp do jest teraz ograniczone. `openid` Zakresu zezwala tylko Twojej aplikacji logują użytkownika i odbieranie identyfikator specyficzny dla aplikacji dla użytkownika. Jeśli chcesz pobrać dane osobowe o użytkowniku w swojej aplikacji, Twoja aplikacja powinna uzyskać dodatkowe uprawnienia od użytkownika. Dwa nowe zakresy, `email` i `profile`, będzie można uzyskać dodatkowe uprawnienia.

* `email` Zakresu umożliwia aplikacji dostęp do adres podstawowy adres e-mail użytkownika za pośrednictwem `email` oświadczenia w id_token, zakładając, że użytkownik ma adres adresy e-mail. 
* `profile` Zakresu daje aplikacji dostęp do wszystkich innych podstawowe informacje o użytkowniku, takie jak nazwy username preferowaną, identyfikator obiektu, i tak dalej w id_token.

Te zakresy umożliwiają kodu aplikacji w sposób minimalny ujawnienie, dzięki czemu można tylko prosisz użytkownika o zestaw informacji, że aplikacja potrzebuje do wykonywania swojej pracy. Aby uzyskać więcej informacji na temat tych zakresów, zobacz [dokumentacja zakresu v2.0](v2-permissions-and-consent.md).

## <a name="token-claims"></a>Token oświadczeń

Punkt końcowy v2.0 wystawia mniejszy zestaw oświadczenia w tokenach jego domyślnie zachowywanie małych ładunków. Jeśli masz aplikacje i usługi, które mają zależności na określoną oświadczenia w tokenie 1.0, który nie jest już oferowana domyślnie w tokenie w wersji 2.0, należy wziąć pod uwagę przy użyciu [opcjonalnych oświadczeń](active-directory-optional-claims.md) funkcję, aby uwzględnić to roszczenie.

## <a name="limitations"></a>Ograniczenia

Istnieje kilka ograniczeń pod uwagę podczas korzystania z wersji 2.0.

Podczas tworzenia aplikacji, które integrują się z platformą Microsoft identity należy zdecydować, czy punkt końcowy i uwierzytelniania protokoły w wersji 2.0 własnych potrzeb. Punkt końcowy w wersji 1.0 i platformy jest nadal w pełni obsługiwana i pod pewnymi względami jest więcej wyposażonym niż w wersji 2.0. Jednak w wersji 2.0 [wprowadzono znaczące korzyści związane](azure-ad-endpoint-comparison.md) dla deweloperów.

Oto uproszczony zalecenia dla deweloperów, w tym momencie:

* Jeśli lub chcesz obsługiwać osobistych kont Microsoft do aplikacji lub pisania nowych aplikacji, należy użyć w wersji 2.0. Jednak zanim to zrobisz, upewnij się, że rozumiesz ograniczenia omówionych w tym artykule.
* Jeśli jesteś migracji lub aktualizowanie aplikacji korzystającej z protokołu SAML, nie można używać w wersji 2.0. Zamiast tego należy odwoływać się do [przewodnik v1.0](v1-overview.md).

Aby wyeliminować ograniczenia wymienione w tym miejscu, tak aby tylko nigdy nie należy używać punktu końcowego v2.0 ewoluuje wraz z punktem końcowym v2.0. W międzyczasie Użyj w tym artykule, aby określić, czy punktem końcowym v2.0 jest odpowiedni dla Ciebie. Będziemy zaktualizować ten artykuł, aby odzwierciedlić bieżący stan punktu końcowego v2.0. Sprawdź ponownie oceń wymagań względem możliwości w wersji 2.0.

### <a name="restrictions-on-app-registrations"></a>Ograniczenia dotyczące rejestracje aplikacji

Dla każdej aplikacji, którą chcesz zintegrować z punktem końcowym v2.0, można utworzyć rejestracji aplikacji w [portalu rejestracji aplikacji Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList). Alternatywnie, można zarejestrować aplikacji za pomocą [ **rejestracje aplikacji (wersja zapoznawcza)** środowisko](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview) w witrynie Azure portal. Istniejących aplikacji konta Microsoft nie są zgodne z portalu w wersji zapoznawczej, ale są wszystkie aplikacje usługi AAD, niezależnie od tego, gdzie i kiedy zostały one zarejestrowane. 

Rejestracje aplikacji, które obsługują służbowych i kont służbowych i osobistych kont mają następujące zastrzeżenia:

* Tylko dwa wpisy tajne aplikacji są dozwolone na identyfikator aplikacji.
* Aplikacja, która nie została zarejestrowana w dzierżawie mogą zarządzać tylko konta, na którym jest on zarejestrowany. Nie może być współużytkowane z innymi deweloperami. Jest to w przypadku większości aplikacji, które zostały zarejestrowane przy użyciu osobistego konta Microsoft, w portalu rejestracji aplikacji. Jeśli chcesz udostępnić swoją rejestrację aplikacji za pomocą wielu deweloperów, należy zarejestrować aplikację w dzierżawie za pomocą **rejestracje aplikacji (wersja zapoznawcza)** części witryny Azure portal.
* Istnieje kilka ograniczeń dotyczących formatu adres URL przekierowania, który jest dozwolony. Aby uzyskać więcej informacji na temat adres URL przekierowania zobacz następną sekcję.

### <a name="restrictions-on-redirect-urls"></a>Ograniczenia dotyczące przekierowania adresów URL

Aplikacje, które są zarejestrowane dla wersji 2.0 są ograniczone do ograniczonego zestawu wartości adresu URL przekierowania. Przekierowywanie adresu URL dla aplikacji i usług internetowych musi zaczynać się od systemu `https`, a wszystkie wartości adresu URL przekierowania muszą współużytkować jedną domenę DNS.  System rejestracji porównuje całą nazwę DNS istniejącego adresu URL przekierowania na nazwę DNS adresu URL przekierowania, który dodajesz. `http://localhost` obsługiwane jest również jako adres URL przekierowania.  

Żądanie dodania nazwy DNS zakończy się niepowodzeniem, jeśli będzie spełniony jeden z następujących warunków:  

* Cała nazwa DNS nowego adresu URL przekierowania nie odpowiada nazwę DNS istniejącego adresu URL przekierowania.
* Cała nazwa DNS nowego adresu URL przekierowania nie jest poddomeną istniejącego adresu URL przekierowania.

#### <a name="example-1"></a>Przykład 1

Jeśli aplikacja ma adres URL przekierowania `https://login.contoso.com`, można dodać adresu URL przekierowania, w którym nazwa DNS jest dopasowuje dokładnie tak, jak pokazano w poniższym przykładzie:

`https://login.contoso.com/new`

Lub możesz zapoznać się z przywoływana jest poddomena DNS domeny Login.contoso.com, jak pokazano w poniższym przykładzie:

`https://new.login.contoso.com`

#### <a name="example-2"></a>Przykład 2

Jeśli chcesz mieć aplikację, która ma `login-east.contoso.com` i `login-west.contoso.com` jako przekierowania adresów URL, należy dodać te przekierowania adresów URL w następującej kolejności:

`https://contoso.com`  
`https://login-east.contoso.com`  
`https://login-west.contoso.com`  

Dwa ostatnie adresy można dodać, ponieważ są poddomenami pierwszego adresu URL przekierowania contoso.com. To ograniczenie zostanie usunięte w kolejnej wersji.

Należy również zauważyć, może mieć tylko 20 adresów URL odpowiedzi dla określonej aplikacji — ten limit ma zastosowanie w przypadku wszystkich typów aplikacji, że rejestracji obsługuje (SPA, klient natywny, aplikacji sieci web i usługi).  

Aby dowiedzieć się, jak zarejestrować aplikację do użytku z wersji 2.0, zobacz te przewodniki Szybki Start:

* [Rejestrowanie aplikacji przy użyciu portalu rejestracji aplikacji](quickstart-v2-register-an-app.md)
* [Rejestrowanie aplikacji za pomocą aplikacji środowiska rejestracji (wersja zapoznawcza)](quickstart-register-app.md)

### <a name="restrictions-on-libraries-and-sdks"></a>Ograniczenia dotyczące bibliotek i zestawów SDK

Obecnie Obsługa bibliotek dla punktu końcowego v2.0 jest ograniczona. Jeśli chcesz używać punktu końcowego v2.0 w aplikacji produkcyjnej, masz następujące opcje:

* Jeśli tworzysz aplikację sieci web bezpiecznie służy ogólnie dostępne oprogramowanie pośredniczące po stronie serwera do wykonywania sprawdzania poprawności logowania i tokenu. Obejmują one oprogramowania pośredniczącego OWIN OpenID Connect dla platformy ASP.NET i Node.js Passport wtyczki. Aby uzyskać przykłady kodu, które używają oprogramowania pośredniczącego Microsoft, zobacz [v2.0 wprowadzenie](v2-overview.md#getting-started) sekcji.
* Jeśli tworzysz aplikację na komputerze lub urządzeniu przenośnym, można użyć jednej z bibliotek uwierzytelniania firmy Microsoft (MSAL) w wersji zapoznawczej. Tych bibliotek znajdują się w obsługiwane w środowisku produkcyjnym wersji zapoznawczej, więc bezpiecznie z nich korzystać w aplikacjach produkcyjnych. Możesz dowiedzieć się więcej o warunkach korzystania z wersji zapoznawczej i dostępnych bibliotek w [dokumentacja bibliotek uwierzytelniania](reference-v2-libraries.md).
* W przypadku platform nie są objęte biblioteki Microsoft można zintegrować z punktem końcowym v2.0 przez bezpośrednie wysyłanie i odbieranie wiadomości protokołu w kodzie aplikacji. Protokoły OpenID Connect i OAuth 2.0 [są udokumentowane](active-directory-v2-protocols.md) ułatwiające wykonanie takiej integracji.
* Na koniec można użyć bibliotek typu open-source OpenID Connect i OAuth do integracji z punktem końcowym v2.0. Punkt końcowy v2.0 powinien być zgodny z wielu bibliotek typu open-source protokołu bez zmian. Dostępność tych rodzajów bibliotek zależy od języka i platformy. [OpenID Connect](https://openid.net/connect/) i [OAuth 2.0](https://oauth.net/2/) witryn sieci Web utrzymywać listę popularnych implementacji. Aby uzyskać więcej informacji, zobacz [biblioteki Azure Active Directory w wersji 2.0 i uwierzytelniania](reference-v2-libraries.md)i listy, biblioteki klienckie typu open source i przykładów, które zostały przetestowane z punktem końcowym v2.0.
* Odwołanie `.well-known` endpoint wspólnego punktu końcowego v2.0 jest `https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration`. Zastąp `common` identyfikatorem dzierżawy można pobrać danych określonego dla Twojej dzierżawy.  

### <a name="protocol-changes"></a>Protokół zmian

Nie obsługuje punktu końcowego v2.0, SAML lub WS-Federation; obsługuje tylko OpenID Connect i OAuth 2.0.  Istotne zmiany w protokoły OAuth 2.0 z punktu końcowego w wersji 1.0 są: 

* `email` Oświadczeń jest zwracany, jeśli skonfigurowano opcjonalnego roszczenia **lub** zakres = wiadomość e-mail została określona w żądaniu. 
* `scope` Parametr jest teraz obsługiwany zamiast `resource` parametru.  
* Wiele odpowiedzi zostały zmodyfikowane w celu były bardziej zgodny ze specyfikacją protokołu OAuth 2.0, na przykład poprawnie zwracanie `expires_in` jako int zamiast ciągu.  

Aby lepiej zrozumieć zakres protokołu funkcje obsługiwane w punkcie końcowym v2.0, zobacz [referencyjne protokołu OpenID Connect i OAuth 2.0](active-directory-v2-protocols.md).

#### <a name="saml-restrictions"></a>Ograniczenia dotyczące języka SAML

Jeśli używano Active Directory Authentication Library (ADAL) w aplikacjach Windows, należy wprowadzić jakieś zalet zintegrowanego uwierzytelniania Windows, które używa grant asercji zabezpieczeń Assertion Markup Language (SAML). Z tym przydziałem użytkowników federacyjnych usługi Azure AD mogą dyskretnie uwierzytelnianie dzierżaw za pomocą swojego wystąpienia usługi Active Directory w środowisku lokalnym bez konieczności wprowadzania poświadczeń. Udziel potwierdzenie SAML nie jest obsługiwana w punkcie końcowym v2.0.
