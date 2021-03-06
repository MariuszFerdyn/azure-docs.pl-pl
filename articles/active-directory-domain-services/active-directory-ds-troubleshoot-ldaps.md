---
title: 'Azure Active Directory Domain Services: Rozwiązywania problemów z Secure konfigurację protokołu LDAP | Dokumentacja firmy Microsoft'
description: Rozwiązywanie problemów z bezpiecznego protokołu LDAP dla usług domenowych Azure AD
services: active-directory-ds
documentationcenter: ''
author: eringreenlee
manager: ''
editor: ''
ms.assetid: 81208c0b-8d41-4f65-be15-42119b1b5957
ms.service: active-directory
ms.subservice: domain-services
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 02/21/2018
ms.author: ergreenl
ms.openlocfilehash: be07579d8273ab19101aa6c475ae5d23375517ca
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/29/2019
ms.locfileid: "55177189"
---
# <a name="azure-ad-domain-services---troubleshooting-secure-ldap-configuration"></a>Azure AD Domain Services — Konfiguracja Rozwiązywanie problemów z bezpiecznego protokołu LDAP

Ten artykuł zawiera rozwiązania typowych problemów, gdy [Konfigurowanie protokołu secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md) dla usług domenowych Azure AD.

## <a name="aadds101-secure-ldap-network-security-group-configuration"></a>AADDS101: Secure LDAP konfiguracją sieciowej grupy zabezpieczeń

**Komunikat alertu:**

*Dla domeny zarządzanej włączono protokół Secure LDAP przez internet. Dostęp do portu 636 nie jest zablokowany za pomocą sieciowej grupy zabezpieczeń. Może to wystawić konta użytkowników w domenie zarządzanej na próby ataków siłowych hasła.*

### <a name="secure-ldap-port"></a>Bezpieczny port LDAP

Po włączeniu protokołu secure LDAP, zaleca się utworzenie dodatkowe zasady w celu umożliwienia dostępu przychodzącego protokołu LDAPS tylko z określonych adresów IP. Te zasady chronią domeny przed atakami, które mogą stanowić zagrożenie bezpieczeństwa. Portu 636 umożliwia dostęp do Twojej domeny zarządzanej. Oto jak można zaktualizować usługi sieciowej grupy zabezpieczeń, aby umożliwić dostęp do bezpiecznego protokołu LDAP:

1. Przejdź do [karty sieciowe grupy zabezpieczeń](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Network%2FNetworkSecurityGroups) w witrynie Azure portal
2. Wybierz grupy zabezpieczeń sieci skojarzonych z Twoją domeną z tabeli.
3. Kliknij pozycję **reguły zabezpieczeń dla ruchu przychodzącego**
4. Tworzenie reguły portu 636
   1. Kliknij przycisk **Dodaj** na górnym pasku nawigacyjnym.
   2. Wybierz **adresów IP** dla źródła.
   3. Określanie zakresów portów źródłowych dla tej reguły.
   4. Dane wejściowe "636" na potrzeby docelowe zakresy portów.
   5. Protokół jest **TCP**.
   6. Nadaj regule odpowiednią nazwę, opis i priorytet. Priorytet tej reguły powinien być większy niż priorytet reguły "Deny wszystkie", jeśli nie masz.
   7. Kliknij przycisk **OK**.
5. Sprawdź, czy reguła została utworzona.
6. Sprawdzanie kondycji domeny w ciągu dwóch godzin, aby upewnić się, że czynności zostały wykonane poprawnie.

> [!TIP]
> Portu 636 nie jest tylko reguły służące do usług domenowych Azure AD gwarantującego bezproblemowe działanie. Aby dowiedzieć się więcej, odwiedź stronę [wytyczne dotyczące sieci](active-directory-ds-networking.md) lub [konfiguracji sieciowej grupy zabezpieczeń z Rozwiązywanie problemów z](active-directory-ds-troubleshoot-nsg.md) artykułów.
>

## <a name="aadds502-secure-ldap-certificate-expiring"></a>AADDS502: Secure LDAP wygaśnięcia ważności certyfikatu

**Komunikat alertu:**

*Certyfikat secure LDAP dla domeny zarządzanej wygaśnie w dniu [date]].*

**Rozwiązanie:**

Utwórz nowy certyfikat secure LDAP, wykonując czynności opisane w temacie [Konfiguracja protokołu secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md) artykułu.

## <a name="contact-us"></a>Skontaktuj się z nami
Skontaktuj się z zespołem produktu usługi Azure Active Directory Domain Services, aby [Podziel się opinią lub pomocy technicznej](active-directory-ds-contact-us.md).
