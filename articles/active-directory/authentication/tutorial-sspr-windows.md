---
title: Samoobsługowe resetowanie hasła usługi Azure AD z ekranu logowania systemu Windows 10
description: W tym samouczku włączysz resetowanie hasła z ekranu logowania systemu Windows 10, aby zmniejszyć liczbę zgłoszeń do działu pomocy technicznej.
services: active-directory
ms.service: active-directory
ms.subservice: authentication
ms.topic: tutorial
ms.date: 02/01/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: sahenry
ms.collection: M365-identity-device-management
ms.openlocfilehash: a0463a2ad3fa74f33a52e15a246dfd4ffd63107a
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56200874"
---
# <a name="tutorial-azure-ad-password-reset-from-the-login-screen"></a>Samouczek: Resetowanie hasła usługi Azure AD z ekranu logowania

W tym samouczku umożliwisz użytkownikom resetowanie swoich haseł z ekranu logowania systemu Windows 10. Dzięki nowej aktualizacji systemu Windows 10 z kwietnia 2018 r. użytkownicy z urządzeniami **dołączonymi do usługi Azure AD** lub urządzeniami **hybrydowymi dołączonymi do usługi Azure AD** mogą skorzystać z linku „Resetuj hasło” znajdującego się na ich ekranach logowania. Kliknięcie tego linku powoduje przejście do znanego użytkownikom środowiska samoobsługowego resetowania hasła.

> [!div class="checklist"]
> * Konfigurowanie linku resetowania hasła przy użyciu usługi Intune
> * Opcjonalne konfigurowanie przy użyciu rejestru Windows
> * Interpretacja tego, co będą widzieli użytkownicy

## <a name="prerequisites"></a>Wymagania wstępne

* Musisz mieć co najmniej system Windows 10 z aktualizacją z kwietnia 2018 r., a urządzenie musi być:
   * [dołączone do usługi Azure AD](../device-management-azure-portal.md) lub
   * [dołączone do hybrydowej usługi Azure AD](../device-management-hybrid-azuread-joined-devices-setup.md) z łącznością sieciową z kontrolerem domeny.
* Musisz włączyć funkcję samoobsługowego resetowania haseł w usłudze Azure AD.
* Jeśli urządzenia z systemem Windows 10 są za serwerem proxy lub zaporą, musisz dodać adresy URL `passwordreset.microsoftonline.com` oraz `ajax.aspnetcdn.com` do listy Dozwolone adresy URL ruchu protokołu HTTPS (port 443).
* Przejrzyj ograniczenia poniżej przed wypróbowaniem tej funkcji w danym środowisku.

## <a name="configure-reset-password-link-using-intune"></a>Konfigurowanie linku resetowania hasła przy użyciu usługi Intune

Wdrażanie zmiany konfiguracji w celu włączenia możliwości resetowania hasła z poziomu ekranu logowania przy użyciu usługi Intune jest metodą najbardziej elastyczną. Usługa Intune umożliwia wdrażanie zmiany konfiguracji dla określonej zdefiniowanej grupy maszyn. Ta metoda wymaga rejestracji urządzenia w usłudze Intune.

### <a name="create-a-device-configuration-policy-in-intune"></a>Tworzenie zasad konfiguracji urządzenia w usłudze Intune

1. Zaloguj się do witryny [Azure Portal](https://portal.azure.com) i kliknij pozycję **Intune**.
2. Utwórz nowy profil konfiguracji urządzenia, przechodząc kolejno do pozycji **Konfiguracja urządzenia** > **Profil** > **Utwórz profil**
   * Podaj znaczącą nazwę profilu
   * Opcjonalnie podaj znaczący opis profilu
   * Platforma: **Windows 10 lub nowsza**
   * Typ profilu: **Niestandardowy**

3. Skonfiguruj obszar **Ustawienia**
   * **Dodaj** następujące ustawienie OMA-URI, aby włączyć link resetowania hasła
      * Podaj znaczącą nazwę, aby ułatwić zrozumienie działania ustawienia
      * Opcjonalnie podaj znaczący opis ustawienia
      * Ustaw pozycję **OMA-URI** na wartość `./Vendor/MSFT/Policy/Config/Authentication/AllowAadPasswordReset`
      * Ustaw pozycję **Typ danych** na **Liczba całkowita**
      * Ustaw pozycję **Wartość**  na **1**
      * Kliknij przycisk **OK**.
   * Kliknij przycisk **OK**.
4. Kliknij przycisk **Utwórz**

### <a name="assign-a-device-configuration-policy-in-intune"></a>Przypisywanie zasad konfiguracji urządzenia w usłudze Intune

#### <a name="create-a-group-to-apply-device-configuration-policy-to"></a>Tworzenie grupy do zastosowania zasad konfiguracji urządzeń

1. Zaloguj się do witryny [Azure Portal](https://portal.azure.com) i kliknij pozycję **Azure Active Directory**.
2. Przejdź kolejno do pozycji **Użytkownicy i grupy** > **Wszystkie grupy** > **Nowa grupa**
3. Podaj nazwę grupy i w obszarze **Typ członkostwa** wybierz pozycję **Przypisane**
   * W obszarze **Członkowie** wybierz urządzenia z systemem Windows 10 dołączone do usługi Azure AD, do których chcesz zastosować zasady.
   * Kliknij pozycję **Wybierz**
4. Kliknij przycisk **Utwórz**

Więcej informacji na temat tworzenia grup można znaleźć w artykule [Zarządzanie dostępem do zasobów za pomocą grup usługi Azure Active Directory](../fundamentals/active-directory-manage-groups.md).

#### <a name="assign-device-configuration-policy-to-device-group"></a>Przypisywanie zasad konfiguracji urządzeń do grupy urządzeń

1. Zaloguj się do witryny [Azure Portal](https://portal.azure.com) i kliknij pozycję **Intune**.
2. Znajdź utworzony wcześniej profil konfiguracji urządzenia, przechodząc kolejno do pozycji **Konfiguracja urządzenia** > **Profile** > kliknij utworzony wcześniej profil
3. Przypisz profil do grupy urządzeń 
   * Kliknij kolejno pozycje **Przypisania** > w obszarze **Uwzględnianie** > **Wybierz grupy do uwzględnienia**
   * Wybierz utworzoną wcześniej grupę, a następnie kliknij pozycję **Wybierz**
   * Kliknij pozycję **Zapisz**

   ![Przypisanie][Assignment]

Zasady konfiguracji urządzenia zostały teraz utworzone i przypisane w celu włączenia linku resetowania hasła na ekranie logowania przy użyciu usługi Intune.

## <a name="configure-reset-password-link-using-the-registry"></a>Konfigurowanie linku resetowania hasła przy użyciu rejestru

1. Zaloguj się do komputera PC z systemem Windows przy użyciu poświadczeń administracyjnych
2. Uruchom **regedit** jako administrator
3. Ustaw poniższy klucz rejestru
   * `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\AzureADAccount`
      * `"AllowPasswordReset"=dword:00000001`

## <a name="what-do-users-see"></a>Co widzą użytkownicy

Teraz, gdy zasady zostały skonfigurowane i przypisane, co zmienia się dla użytkownika? Skąd użytkownicy będą wiedzieć, że mogą zresetować swoje hasło na ekranie logowania?

![LoginScreen][LoginScreen]

Gdy użytkownicy próbują się zalogować, widzą teraz link resetowania, który otwiera środowisko samoobsługowego resetowania hasła na ekranie logowania. Ta funkcja umożliwia użytkownikom zresetowanie hasła bez konieczności uzyskiwania dostępu do przeglądarki internetowej przy użyciu innego urządzenia.

Wskazówki dotyczące używania tej funkcji będzie można znaleźć w artykule [Reset your work or school password (Resetowanie hasła służbowego)](../user-help/active-directory-passwords-update-your-own-password.md#reset-password-at-sign-in)

Dziennik inspekcji usługi Azure AD zawiera informacje dotyczące adresu IP i typu klienta, które są powiązane z żądaniem resetowania hasła.

![Przykład resetowania hasła na ekranie logowania w dzienniku inspekcji usługi Azure AD](media/tutorial-sspr-windows/windows-sspr-azure-ad-audit-log.png)

Gdy użytkownik resetuje swoje hasło na ekranie logowania urządzenia z systemem Windows 10, tworzone jest tymczasowe konto o niskim poziomie uprawnień i nazwie „defaultuser1”. To konto jest używane, aby zapewnić bezpieczeństwo procesu resetowania hasła. Samo konto ma losowo wygenerowane hasło, nie jest widoczne dla logowania urządzenia i zostanie automatycznie usunięte po zresetowaniu hasła użytkownika. Może istnieć wiele profilów „defaultuser”, ale można je bezpiecznie zignorować.

## <a name="limitations"></a>Ograniczenia

Podczas testowania tej funkcjonalności za pomocą funkcji Hyper-V link „Resetuj hasło” nie jest wyświetlany.

* Przejdź do maszyny wirtualnej używanej do testowania, kliknij pozycję **Widok**, a następnie usuń zaznaczenie pola wyboru **Sesja rozszerzona**.

Podczas testowania tej funkcjonalności za pomocą pulpitu zdalnego lub rozszerzonej sesji maszyny wirtualnej link „Resetuj hasło” nie jest wyświetlany.

* Resetowanie hasła nie jest obecnie obsługiwane z poziomu pulpitu zdalnego.

Jeśli zasady w wersjach systemu Windows 10 wcześniejszych niż 1809 wymagają naciśnięcia klawiszy Ctrl+Alt+Del, pozycja **Resetuj hasło** nie będzie działać.

Jeśli powiadomienia na ekranie blokady są wyłączone, pozycja **Resetuj hasło** nie będzie działać.

Wiadomo, że następujące ustawienia zasad zakłócają możliwość resetowania haseł

   * Ustawienie HideFastUserSwitching jest włączone lub ustawione na wartość 1
   * Ustawienie DontDisplayLastUserName jest włączone lub ustawione na wartość 1
   * Ustawienie NoLockScreen jest włączone lub ustawione na wartość 1
   * Ustawienie EnableLostMode jest określone na urządzeniu
   * Plik Explorer.exe został zastąpiony niestandardową powłoką

Ta funkcja nie działa w przypadku sieci z wdrożonym uwierzytelnianiem sieci 802.1x oraz opcji „Wykonaj bezpośrednio przed logowaniem użytkownika”. W sieciach z wdrożonym uwierzytelnianiem sieci 802.1x zalecane jest używanie uwierzytelniania maszynowego w celu włączenia tej funkcji.

W przypadku scenariuszy z hybrydowym dołączeniem do domeny przepływ pracy samoobsługowego resetowania hasła zakończy się pomyślnie bez konieczności używania kontrolera domeny usługi Active Directory. Jeśli użytkownik wykona proces resetowania hasła w czasie, gdy komunikacja z kontrolerem domeny usługi Active Directory jest niedostępna, na przykład podczas pracy zdalnej, nie będzie mógł zalogować się do urządzenia, dopóki urządzenie nie nawiąże połączenia z kontrolerem domeny i nie zaktualizuje poświadczeń w pamięci podręcznej. **Łączność z kontrolerem domeny jest wymagana do użycia nowego hasła po raz pierwszy**.

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Jeśli zdecydujesz, że nie chcesz już korzystać z funkcji, które zostały skonfigurowane w ramach tego samouczka, usuń utworzony profil konfiguracji urządzenia usługi Intune lub klucz rejestru.

## <a name="next-steps"></a>Następne kroki

W tym samouczku umożliwiono użytkownikom resetowanie swoich haseł z ekranu logowania systemu Windows 10. Przejdź do następnego samouczka, aby zobaczyć, jak można zintegrować usługę Azure Identity Protection ze środowiskami samoobsługowego resetowania haseł i uwierzytelniania wieloskładnikowego.

> [!div class="nextstepaction"]
> [Ocena ryzyka podczas logowania](tutorial-risk-based-sspr-mfa.md)

[Assignment]: ./media/tutorial-sspr-windows/profile-assignment.png "Przypisywanie zasad konfiguracji urządzenia usługi Intune do grupy urządzeń z systemem Windows 10"
[LoginScreen]: ./media/tutorial-sspr-windows/logon-reset-password.png "Link resetowania hasła na ekranie logowania systemu Windows 10"
