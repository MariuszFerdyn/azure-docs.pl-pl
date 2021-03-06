---
title: Omówienie aplikacji Microsoft Authenticator — Azure Active Directory | Microsoft Docs
description: Informacje o aplikacji Microsoft Authenticator, w tym wyjaśnienie czym ona jest oraz jak działa, a także jakie informacje zawarto w tej sekcji zawartości.
services: active-directory
author: eross-msft
manager: daveba
ms.reviewer: sahenry
ms.service: active-directory
ms.subservice: user-help
ms.workload: identity
ms.topic: overview
ms.date: 01/24/2019
ms.author: lizross
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3e1724454ff67f6cfe3646b59e8302a3dd099081
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56217449"
---
# <a name="what-is-the-microsoft-authenticator-app"></a>Czym jest aplikacja Microsoft Authenticator?
Aplikacja Microsoft Authenticator pomaga w logowaniu się do kont, jeśli używana jest weryfikacja dwuskładnikowa. Weryfikacja dwuskładnikowa zapewnia bezpieczniejszy dostęp do kont, szczególnie podczas wyświetlania informacji poufnych. Ponieważ hasła mogą zostać zapomniane, skradzione lub ujawnione, weryfikacja dwuskładnikowa zapewnia dodatkowy poziom zabezpieczeń, który pomaga chronić konto, utrudniając włamanie się na nie innym osobom.

Aplikacji Microsoft Authenticator można używać na wiele sposobów, na przykład:

- Udostępnienie monitu dla drugiej metody weryfikacji po zalogowaniu się przy użyciu nazwy użytkownika i hasła.

- Udostępnienie możliwości logowania się bez wymagania hasła, ale za to przy użyciu nazwy użytkownika i jego twarzy, odcisku palca lub numeru PIN dostarczanych przez urządzenie przenośne.

>[!Important]
>Aplikacja Microsoft Authenticator współdziała z dowolną aplikacją używającą weryfikacji dwuetapowej i dowolnym kontem obsługującym standardy TOTP (Time-based One-time Password).

>Ta zawartość jest przeznaczona dla użytkowników. Jeśli jesteś administratorem, więcej informacji na temat konfigurowania i zarządzania środowiskiem usługi Azure Active Directory (Azure AD) możesz znaleźć w [dokumentacji usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory).

>Jeśli masz problemy z zalogowaniem się do swojego konta, zobacz temat [Kiedy nie możesz zalogować się na swoje konto Microsoft](https://support.microsoft.com/help/12429). Uzyskaj więcej informacji o tym, co zrobić, gdy podczas próby zalogowania się do konta Microsoft pojawia się komunikat [„To konto Microsoft nie istnieje”](https://support.microsoft.com/help/13811).

## <a name="terminology"></a>Terminologia
|Termin|Opis|
|----|-----------|
|Weryfikacja dwuskładnikowa |Proces weryfikacji, który wymaga specjalnego użycia tylko dwóch rodzajów informacji o weryfikacji, takich jak hasło i numer PIN. Aplikacja Microsoft Authenticator obsługuje zarówno standardową weryfikację dwuskładnikową, jak i logowanie bez hasła.|
|Multi-Factor Authentication (MFA)|Wszystkie weryfikacje dwuskładnikowe są odmianami uwierzytelniania wieloskładnikowego, które wymaga użycia *co najmniej* dwóch rodzajów informacji o weryfikacji, w zależności od wymagań organizacji.|
|Konto Microsoft (nazywane też kontem MSA)|Tworzone własnoręcznie konta osobiste zapewniają dostęp do produktów i usług w chmurze firmy Microsoft przeznaczonych dla konsumentów, takich jak Outlook, OneDrive, Xbox LIVE i Office 365. Konto Microsoft jest tworzone i przechowywane w systemie kont tożsamości konsumentów firmy Microsoft.|
|Konto służbowe|Twoja organizacja tworzy konto służbowe (takie jak alain@contoso.com), aby umożliwić Ci dostęp do wewnętrznych i potencjalnie ograniczonych zasobów, takich jak platforma Microsoft Azure, usługa Windows Intune i Office 365.|
|Kod weryfikacyjny|Sześciocyfrowy kod, który jest wyświetlany w aplikacji wystawcy uwierzytelnienia, w obszarze każdego dodanego konta. Kod weryfikacyjny zmienia się co 30 sekund, uniemożliwiając wielokrotne użycie kodu. Jest to również nazywany jednorazowym kodem dostępu (OTP).|

## <a name="how-two-factor-verification-works-with-the-app"></a>W jaki sposób weryfikacja dwuskładnikowa współdziała z aplikacją
Weryfikacja dwuskładnikowa współdziała z aplikacją Microsoft Authenticator w następujący sposób:

- **Powiadomienie.** Wpisz nazwę użytkownika i hasło na urządzeniu, za pomocą którego logujesz się do swojego służbowego lub osobistego konta Microsoft, a aplikacja Microsoft Authenticator wyśle powiadomienie z prośbą o **zatwierdzenie logowania**. Wybierz pozycję **Zatwierdź**, jeśli rozpoznajesz próbę logowania. W przeciwnym razie wybierz pozycję **Odmów**. Jeśli wybierzesz pozycję **Odmów**, możesz również oznaczyć żądanie jako fałszywe.

- **Kod weryfikacyjny.** Wpisz nazwę użytkownika i hasło na urządzeniu, za pomocą którego logujesz się do swojego służbowego lub osobistego konta Microsoft, a następnie skopiuj powiązany kod weryfikacyjny z ekranu **Konta** aplikacji Microsoft Authenticator. Kod weryfikacyjny jest również nazywany uwierzytelnianiem jednorazowym kodem dostępu (OTP).

- **Logowanie bez hasła.** Wpisz nazwę użytkownika na urządzeniu, za pomocą którego logujesz się do swojego służbowego lub osobistego konta Microsoft, a następnie użyj urządzenia przenośnego do potwierdzenia swojej tożsamości za pomocą odcisku palca, twarzy lub numeru PIN. W przypadku tej metody nie musisz wprowadzać hasła.

### <a name="whether-to-use-your-devices-biometric-capabilities"></a>Zdecydowanie o użyciu możliwości biometrycznych swojego urządzenia
Jeśli do zakończenia procesu uwierzytelniania używasz numeru PIN, możesz skonfigurować aplikację Microsoft Authenticator, aby zamiast tego używała możliwości biometrycznych (rozpoznawania odcisku palca lub twarzy) urządzenia. Możesz to skonfigurować podczas pierwszego użycia aplikacji Authenticator do zweryfikowania swojego konta. Wystarczy jako metodę identyfikacji wybrać opcję użycia możliwości biometrycznych urządzenia zamiast numeru PIN.

## <a name="who-decides-if-you-use-this-feature"></a>Kto decyduje o możliwości użycia tej funkcji?
W zależności od typu konta o konieczności korzystania z weryfikacji dwuskładnikowej może zdecydować Twoja organizacja lub ta decyzja może zostać przeniesiona na użytkownika.

- **Konto służbowe.** Jeśli używasz konta służbowego (na przykład alain@contoso.com), to Twoja organizacja decyduje, czy musisz korzystać z weryfikacji dwuskładnikowej i konkretnych metod weryfikacji. Aby uzyskać więcej informacji o dodawaniu konta służbowego do aplikacji Microsoft Authenticator, zobacz [Dodawanie konta służbowego](microsoft-authenticator-app-add-work-account.md).

- **Osobiste konto Microsoft.** Weryfikację dwuskładnikowa można skonfigurować dla osobistych kont Microsoft (na przykład alain@outlook.com). Aby uzyskać więcej informacji na temat dodawania Twojego osobistego konta Microsoft, zobacz 

- **Konto inne niż Microsoft.** Weryfikację dwuskładnikowa można skonfigurować dla kont innych niż Microsoft (na przykład alain@gmail.com). Konta nienależące do firmy Microsoft mogą używać innego terminu na oznaczenia weryfikacji dwuskładnikowej. Funkcja ta powinna znajdować się w ustawieniach zabezpieczeń (**Security**) lub ustawieniach logowania (**Sign-in**). Aplikacja Microsoft Authenticator działa przy użyciu dowolnego konta, które obsługuje standardy TOTP.

## <a name="in-this-section"></a>W tej sekcji

|Artykuł |Opis |
|------|------------|
|[Pobieranie i instalowanie aplikacji](user-help-auth-app-download-install.md)|W tym artykule opisano lokalizację oraz sposób pobierania i instalowania aplikacji Microsoft Authenticator dla urządzeń z systemami Android i iOS.|
|[Dodawanie kont służbowych](user-help-auth-app-add-work-school-account.md)|W tym artykule opisano sposób dodawania różnych służbowych i osobistych kont do aplikacji Microsoft Authenticator.|
|[Dodawanie kont osobistych](user-help-auth-app-add-personal-ms-account.md)|W tym artykule opisano sposób dodawania do aplikacji Microsoft Authenticator kont osobistych należących i nienależących do firmy Microsoft.|
|[Ręczne dodawanie kont](user-help-auth-app-add-account-manual.md)|W tym artykule opisano ręczne dodawanie kont do aplikacji Microsoft Authenticator, jeśli nie można zeskanować udostępnionego kodu QR.|
|[Logowanie się za pomocą aplikacji](user-help-auth-app-sign-in.md)|W tym artykule opisano sposób logowania się do różnych kont przy użyciu aplikacji Microsoft Authenticator.|
|[Wykonywanie kopii zapasowych i odzyskiwanie poświadczeń konta](user-help-auth-app-backup-recovery.md)| Zawiera informacje dotyczące tworzenia kopii zapasowej i odzyskiwania poświadczeń konta za pomocą aplikacji Microsoft Authenticator.|
|[Microsoft Authenticator app FAQ (Aplikacja Microsoft Authenticator — często zadawane pytania)](user-help-auth-app-faq.md)|Zawiera odpowiedzi na często zadawane pytania dotyczące aplikacji.|
