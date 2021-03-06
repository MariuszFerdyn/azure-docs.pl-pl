---
title: Wrażenia użytkowników końcowych w aplikacji — Azure Active Directory | Dokumentacja firmy Microsoft
description: Azure Active Directory (Azure AD) oferuje kilka sposobów dostosowania do wdrażania aplikacji dla użytkowników końcowych w organizacji.
services: active-directory
author: CelesteDG
manager: mtillman
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.topic: conceptual
ms.date: 11/09/2018
ms.author: celested
ms.reviewer: arvindh
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2488cb085c3be68265a787bd062028598c9243b8
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56190028"
---
# <a name="end-user-experiences-for-applications-in-azure-active-directory"></a>Środowiska użytkownika końcowego dla aplikacji w usłudze Azure Active Directory
Azure Active Directory (Azure AD) oferuje kilka sposobów dostosowania do wdrażania aplikacji dla użytkowników końcowych w organizacji:

* Panel dostępu usługi Azure AD
* Uruchamianie aplikacji usługi Office 365
* Bezpośrednie logowanie do aplikacji federacyjnych
* Linki bezpośrednie do federacyjnych, opartych na hasłach lub istniejących aplikacjach

Metody, które chcesz wdrożyć w organizacji jest uznania.

## <a name="azure-ad-access-panel"></a>Panel dostępu usługi Azure AD
Panel dostępu w https://myapps.microsoft.com jest oparte na sieci web portalu, który umożliwia użytkownikowi końcowemu za pomocą konta organizacyjnego usługi Azure Active Directory, aby wyświetlić i uruchamiania aplikacji opartych na chmurze do których zostały one udzielony dostęp administrator usługi Azure AD. Jeśli użytkownik końcowy za pomocą [usługi Azure Active Directory — wersja Premium](https://azure.microsoft.com/pricing/details/active-directory/), możesz również korzystać z funkcji zarządzania grupami samoobsługi za pomocą panelu dostępu.

![Panel dostępu usługi Azure AD](media/what-is-single-sign-on/azure-ad-access-panel.png)

Panel dostępu różni się w witrynie Azure portal i nie wymaga, aby użytkownicy mieli subskrypcję platformy Azure lub usługi Office 365.

Aby uzyskać więcej informacji na panelu dostępu do usługi Azure AD, zobacz [wprowadzenie do panelu dostępu](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="office-365-application-launcher"></a>Uruchamianie aplikacji usługi Office 365
W przypadku organizacji, które zostały wdrożone usługi Office 365, aplikacje przypisane do użytkowników za pomocą usługi Azure AD pojawiają się w portalu usługi Office 365 w https://portal.office.com/myapps. To sprawia, że można łatwo i wygodnie dla użytkowników w organizacji można uruchomić aplikacji bez konieczności używania drugiej portalu i jest zalecaną aplikację uruchamiania rozwiązania dla organizacji przy użyciu usługi Office 365.

![](./media/what-is-single-sign-on/officeapphub.png)

Aby uzyskać więcej informacji na temat uruchamiania aplikacji usługi Office 365, zobacz [aplikacji są wyświetlane w obszarze uruchamiania aplikacji usługi Office 365](https://msdn.microsoft.com/office/office365/howto/connect-your-app-to-o365-app-launcher).

## <a name="direct-sign-on-to-federated-apps"></a>Bezpośrednie logowanie do aplikacji federacyjnych
Większość aplikacji federacyjnych obsługuje SAML 2.0, WS-Federation i OpenID connect również pomocy technicznej przez użytkowników na poziomie aplikacji, a następnie Pobierz zalogowany za pomocą usługi Azure AD przez automatyczne przekierowanie lub klikając łącze do logowania. Jest to określane jako dostawca usług-zainicjowania logowania jednokrotnego, a większość aplikacji federacyjnych w galerii aplikacji usługi Azure AD obsługuje tego (znajduje się dokumentacja połączone za pomocą Kreatora konfiguracji rejestracji logowania jednokrotnego aplikacji w witrynie Azure portal, aby uzyskać szczegółowe informacje).

![](./media/what-is-single-sign-on/workdaymobile.png)

## <a name="direct-sign-on-links"></a>Łącza bezpośrednie logowanie jednokrotne
Usługa Azure AD obsługuje również pojedynczego logowania jednokrotnego łączy bezpośrednich dla poszczególnych aplikacji, które obsługują opartego na hasłach logowanie jednokrotne połączonej logowania jednokrotnego i jakiejkolwiek formy federacyjnego logowania jednokrotnego.

Te łącza są specjalnie przygotowane adresów URL, które wysyłają użytkownika przez proces logowania w usłudze Azure AD dla określonej aplikacji bez konieczności uruchamiania użytkownik je z usługi Azure AD dostęp do panelu lub usługi Office 365. Te pojedynczego logowania jednokrotnego adresy URL można znaleźć w obszarze karty Pulpit nawigacyjny wstępnie zintegrowanych aplikacji w sekcji usługi Active Directory w witrynie Azure Portal, jak pokazano na poniższym zrzucie ekranu.

![](./media/what-is-single-sign-on/deeplink.png)

Te linki można kopiować i wkleić z dowolnego miejsca, chcesz udostępnić Link umożliwiający zalogowanie się do wybranej aplikacji. Może to być w wiadomości e-mail lub w dowolnym opartych na sieci web portalu niestandardowym skonfigurowanej dla dostępu aplikacji użytkownika. Oto przykład z usługi Azure AD bezpośrednie pojedynczy adres URL logowania do usługi Twitter:

`https://myapps.microsoft.com/signin/Twitter/230848d52c8745d4b05a60d29a40fced`

Podobnie jak adresów URL specyficznych dla organizacji do obsługi panelu dostępu, można dostosować ten adres URL, dodając jeden aktywny lub zweryfikowanych domen dla katalogu po nazwie domeny myapps.microsoft.com. Gwarantuje to, że wszelkie znakowanie organizacji jest ładowany bezpośrednio na stronie logowania bez użytkownik nie musi najpierw wprowadź swój identyfikator użytkownika:

`https://myapps.microsoft.com/contosobuild.com/signin/Twitter/230848d52c8745d4b05a60d29a40fced`

Po kliknięciu autoryzowanym użytkownikiem na jednym z poniższych linków, specyficzne dla aplikacji, są najpierw Zobacz ich organizacji strony logowania (przy założeniu, że ich nie jest już zalogowany), a po zalogowaniu nastąpi przekierowanie do swoich aplikacji bez konieczności zatrzymywania w panelu dostępu, najpierw. Jeśli użytkownik nie ma dostępu do aplikacji, takich jak rozszerzenie przeglądarki logowania jednokrotnego opartego na hasłach, wymagania wstępne łącze będzie monitował użytkownika można zainstalować brakujące rozszerzenia. Adres URL linku również pozostaje na stałym, jeśli zmiany jednej konfiguracji logowania jednokrotnego dla aplikacji.

Te linki pełnić te same mechanizmy kontroli dostępu do panelu dostępu i usługi Office 365, a tylko tych użytkowników lub grupy, którzy zostali przypisani do aplikacji w witrynie Azure portal będzie mógł pomyślnie wykonać uwierzytelnienia. Jednak każdy użytkownik, który nie jest autoryzowany, zostanie wyświetlony komunikat wyjaśniający, że nie przyznano dostęp i podano łącza do załadowania panelu dostępu, aby wyświetlić dostępne aplikacje, dla których mają dostęp.

## <a name="next-steps"></a>Kolejne kroki
W przypadku planów wdrożenia zobacz [planów wdrożenia usługi Azure Active Directory](../fundamentals/active-directory-deployment-plans.md)
