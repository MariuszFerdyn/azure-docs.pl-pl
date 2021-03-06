---
title: Użycie infrastruktury raportowania dla dostawców usług w chmurze dla usługi Azure Stack | Dokumentacja firmy Microsoft
description: Usługa Azure Stack obejmuje infrastrukturę potrzebną do śledzenia użycia w przypadku dzierżaw obsługiwany przez dostawca usług chmury (CSP), ponieważ występuje i przekazuje je do usługi Azure.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2019
ms.author: sethm
ms.reviewer: alfredop
ms.lastreviewed: 01/05/2019
ms.openlocfilehash: 1b8b83491211ae26493a6bb41c7f0f219f47f620
ms.sourcegitcommit: 898b2936e3d6d3a8366cfcccc0fccfdb0fc781b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/30/2019
ms.locfileid: "55241308"
---
# <a name="usage-reporting-infrastructure-for-cloud-service-providers"></a>Użycie infrastruktury raportowania dla dostawców usług w chmurze

Usługa Azure Stack obejmuje infrastrukturę potrzebną do śledzenia użycia, ponieważ występuje i przekazuje je do platformy Azure. Na platformie Azure Azure Commerce przetwarza dane użycia i opłaty za użycie do odpowiedniej subskrypcji platformy Azure. Dzieje się tak samo jak, które śledzenie użycia jest monitorowany w chmurze globalnej platformy Azure.

Należy pamiętać, że niektóre pojęcia są spójne z globalnej platformy Azure i usługi Azure Stack. Usługa Azure Stack ma subskrypcje lokalne, które spełniają podobną rolę do subskrypcji platformy Azure. Subskrypcje lokalne są prawidłowe tylko lokalnie. Subskrypcje lokalne są mapowane na subskrypcje platformy Azure, w przypadku użycia jest przekazywany do platformy Azure.

Usługa Azure Stack ma mierników użycia lokalnego. Użycie lokalnego jest zamapowana na liczniki używane w informacjach handlowych platformy Azure. Jednak identyfikatory licznika są różne. Więcej liczniki są dostępne lokalnie niż wykorzystywane przez firmę Microsoft do rozliczeń.

Istnieją pewne różnice między jak usług są wyceniane w usłudze Azure Stack i platformą Azure. Na przykład w usłudze Azure Stack, opłaty za maszyny wirtualne tylko opiera się na rdzeniach wirtualnych/godziny z tej samej stawki dla wszystkich maszyn wirtualnych serii, w przeciwieństwie do usługi Azure. Przyczyną jest to, że na platformie Azure globalnego różnych ceny innego sprzętu. W usłudze Azure Stack klienta zawiera sprzętu, dzięki czemu nie ma powodu do obciążenia w różnym tempie dla różnych klas maszyny Wirtualnej.

Możesz dowiedzieć się o mierników usługi Azure Stack, używany w sprzedaży i ich ceny w Centrum partnerskim w taki sam sposób, podobnie jak w przypadku usług platformy Azure:

1. W Centrum partnerskim, przejdź do **menu pulpitu nawigacyjnego** > **ceny i oferty**.
2. W obszarze **usług opartych na użyciu**, wybierz opcję **bieżącego**.
3. Otwórz **platformy Azure w cenniku dostawców CSP globalnego** arkusza kalkulacyjnego.
4. Filtrowanie według **Region usługi Azure Stack =**.

## <a name="usage-and-billing-error-codes"></a>Użycie i rozliczenia kody błędów

Następujące komunikaty o błędach mogą być podczas dodawania dzierżawy do rejestracji.

| Błąd                           | Szczegóły                                                                                                                                                                                                                                                                                                                           | Komentarze                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|---------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **RegistrationNotFound**            | Nie znaleziono podanej rejestracji. Upewnij się, że poprawnie podano następujące informacje:<br>1. Identyfikator subskrypcji (podana wartość: _identyfikator subskrypcji_),<br>2. Grupa zasobów (podana wartość: _grupy zasobów_),<br>3. Nazwa rejestracji (podana wartość: _nazwa rejestracji_).                             | Ten błąd występuje zazwyczaj, gdy informacje wskazujące do wstępnej rejestracji jest nieprawidłowy. Jeśli musisz sprawdzić, grupy zasobów i nazwę Twojej rejestracji można znaleźć go w witrynie Azure portal, wyświetlając wszystkie zasoby. Jeśli znajdziesz więcej niż jeden zasób rejestracji, Przyjrzyj się **CloudDeploymentID** we właściwości i wybierz pozycję rejestracja którego **CloudDeploymentID** są zgodne z Twoją chmurą. Aby znaleźć **CloudDeploymentID**, można użyć tego programu PowerShell w usłudze Azure Stack:<br>`$azureStackStampInfo = Invoke-Command -Session $session -ScriptBlock { Get-AzureStackStampInformation }` |
| **BadCustomerSubscriptionId**       | Podany _identyfikatora subskrypcji klienta_ i _nazwa rejestracji_ identyfikator subskrypcji nie należą do tego samego dostawcy usług w chmurze firmy Microsoft. Sprawdź, czy identyfikator subskrypcji klienta jest poprawny. Jeśli problem będzie się powtarzać, skontaktuj się z pomocą techniczną. | Ten błąd występuje, gdy subskrypcja klienta jest subskrypcją dostawcy CSP, ale jej zbiera partner programu CSP inny niż ten, do której subskrypcji używany w wstępnej rejestracji zbiera. Aby zapobiec sytuacji, które mogłyby spowodować rozliczeniowy partnera CSP, który nie jest odpowiedzialny za używane usługi Azure Stack jest wykonywane to sprawdzenie.                                                                                                                                                                                                                                                                          |
| **InvalidCustomerSubscriptionId**   | "_Identyfikatora subskrypcji klienta_" jest nieprawidłowa. Upewnij się, że podano prawidłową subskrypcję platformy Azure.                                                                                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| **CustomerSubscriptionNotFound**    | _Identyfikator subskrypcji klienta_ nie został znaleziony w obszarze nazwy _registration. Upewnij się, ważnej subskrypcji platformy Azure jest używany i czy identyfikator subskrypcji został dodany do rejestracji przy użyciu operacji PUT.                                                   | Ten błąd występuje podczas próby AGA dzierżawy została dodana do subskrypcji, która ma być skojarzona z rejestracją nie odnaleziono subskrypcji klienta. Klient nie został dodany do rejestracji lub identyfikator subskrypcji została nieprawidłowo zapisana.                                                                                                                                                                                                                                                                                                                                |
| **UnauthorizedCspRegistration**     | Podany _nazwa rejestracji_ nie jest zatwierdzona do użycia wielu dzierżawców. Wyślij wiadomość e-mail do azstCSP@microsoft.com i zawierać nazwę rejestracji, grupy zasobów i identyfikator subskrypcji używany w rejestracji.                                                                                    | Rejestracja wymaga zatwierdzenia do obsługi wielu dzierżawców przez firmę Microsoft przed rozpoczęciem dodawania dzierżaw do niego.                                                                                                                                                                                                                                                                                                                                                                                             |
| **CustomerSubscriptionsNotAllowed** | Operacje związane z subskrypcją klienta nie są obsługiwane dla klientów odłączonych. Aby można było użyć tej funkcji, należy ponownie zarejestrować za pomocą płacić jako używasz licencjonowania.                                                                                                                                                                    | Rejestracja, do którego próbujesz dodać dzierżawcy jest rejestracji pojemności; oznacza to, kiedy utworzono rejestrację, parametr `BillingModel Capacity` był używany. Płacenie tylko w miarę używasz rejestracji mogą dodawać dzierżawy. Należy ponownie zarejestrować za pomocą parametru `BillingModel PayAsYouUse`.                                                                                                                                                                                                                                                                                          |
| **InvalidCSPSubscription**          | Podany _identyfikatora subskrypcji klienta_ nie jest prawidłową subskrypcją dostawcy CSP. Upewnij się, że podano prawidłową subskrypcję platformy Azure.                                                                                                                                                        | Jest to najbardziej prawdopodobną przyczyną było subskrypcji klienta jest błędnie wpisana.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| **MetadataResolverBadGatewayError** | Jednym z serwerów nadrzędnych zwrócił nieoczekiwany błąd. Spróbuj ponownie później. Jeśli problem będzie się powtarzać, skontaktuj się z pomocą techniczną.                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

## <a name="terms-used-for-billing-and-usage"></a>Terminy używane do rozliczenia i użycie

Poniższe terminy i pojęcia są używane do użycia i rozliczeń w usłudze Azure Stack:

| Termin | Definicja |
| --- | --- |
| Bezpośrednie partner programu CSP | Partner Cloud Solution Provider (CSP) bezpośrednie odbiera bezpośrednio faktury bezpośrednio od firmy Microsoft dla platformy Azure i usługi Azure Stack użycia i rachunków klientów. |
| Pośredniego programu CSP | Odsprzedawcy pośrednich współpracować z dostawcę pośredniego (dystrybutora). Odsprzedawców pozyskiwania klientów końcowych. pośrednie dostawca przechowuje rozliczeń relacji z firmą Microsoft, zarządza klienta rozliczeń i zapewnia dodatkowych usług, takich jak pomoc techniczna. |
| Odbiorcy końcowego | Klientów końcowych są firmom i agencje rządowe, które należą do aplikacji i innych obciążeń, które są uruchamiane w usłudze Azure Stack. |

## <a name="next-steps"></a>Kolejne kroki

- Aby dowiedzieć się więcej na temat programu CSP, zobacz [programu Cloud Solution Provider](https://partner.microsoft.com/solutions/microsoft-cloud-solutions).
- Aby dowiedzieć się więcej o tym, jak pobrać informacje o użyciu zasobów z usługi Azure Stack, zobacz [użycie i rozliczenia w usłudze Azure Stack](azure-stack-billing-and-chargeback.md).
