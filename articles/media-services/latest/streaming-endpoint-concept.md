---
title: Przesyłanie strumieniowe punktów końcowych w usłudze Azure Media Services | Dokumentacja firmy Microsoft
description: Ten artykuł zawiera wyjaśnienie, co to są punkty końcowe przesyłania strumieniowego i jak są one używane przez usługi Azure Media Services.
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.date: 01/16/2019
ms.author: juliako
ms.openlocfilehash: 18c5e48b5f7dbf664b607b8b83473a914256590b
ms.sourcegitcommit: eecd816953c55df1671ffcf716cf975ba1b12e6b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2019
ms.locfileid: "55104573"
---
# <a name="streaming-endpoints"></a>Punkty końcowe przesyłania strumieniowego

W programie Microsoft Azure Media Services (AMS), [punkty końcowe przesyłania strumieniowego](https://docs.microsoft.com/rest/api/media/streamingendpoints) jednostki reprezentuje usługę przesyłania strumieniowego, który może dostarczać zawartość bezpośrednio do aplikacji odtwarzacza klienta lub dalsze do Content Delivery Network (CDN) dla Dystrybucja. Strumień wychodzący, z **punkt końcowy przesyłania strumieniowego** usługa może być strumień na żywo lub element zawartości wideo na żądanie w ramach konta usługi Media Services. Po utworzeniu konta usługi Media Services, **domyślne** punkt końcowy przesyłania strumieniowego zostanie utworzony w stanie zatrzymania. Nie można usunąć **domyślne** punkt końcowy przesyłania strumieniowego. Dodatkowe punkty końcowe przesyłania strumieniowego mogą być tworzone w ramach konta. 

> [!NOTE]
> Aby rozpocząć przesyłanie strumieniowe filmów wideo, wówczas musisz uruchomić **punkt końcowy przesyłania strumieniowego** z którego chcesz strumieniowo przesyłać wideo. 

## <a name="naming-convention"></a>Konwencje nazewnictwa

Dla domyślnego punktu końcowego: `{AccountName}-{DatacenterAbbreviation}.streaming.media.azure.net`

Aby uzyskać wszystkie dodatkowe punkty końcowe: `{EndpointName}-{AccountName}-{DatacenterAbbreviation}.streaming.media.azure.net`

## <a name="types"></a>Typy  

Istnieją dwa **StreamingEndpoint** typów: **Standardowa** i **Premium**. Typ jest zdefiniowany przez liczbę jednostek skalowania (`scaleUnits`) możesz przydzielić dla punktu końcowego przesyłania strumieniowego. 

W tabeli opisano typy:  

|Type|Jednostki skalowania|Opis|
|--------|--------|--------|  
|**Standardowy punkt końcowy przesyłania strumieniowego** (zalecane)|0|**Standardowa** typu jest to zalecana opcja, do niemal wszystkich scenariuszy przesyłania strumieniowego i publiczność każdej wielkości. **Standardowa** typu automatycznie skaluje przepustowość wychodzącą. <br/>Dla klientów korzystających z bardzo wymagających wymagania dotyczące usługi Media Services oferuje **Premium** punkty końcowe, które mogą być używane przesyłania strumieniowego umożliwiają skalowanie pojemności dla największych odbiorców internet. Jeśli spodziewasz się dużej liczby odbiorców i osoby przeglądające współbieżnych, skontaktuj się z nami pod adresem amsstreaming@microsoft.com wskazówki dotyczące tego, czy należy przenieść do **Premium** typu. |
|**Punkt końcowy przesyłania strumieniowego Premium**|>0|Punkty końcowe przesyłania strumieniowego **Premium** są odpowiednie w przypadku zaawansowanych obciążeń, ponieważ zapewniają dedykowaną i skalowalną pojemność przepustowości. Przenieś do **Premium** typu, dostosowując `scaleUnits`. `scaleUnits` umożliwiają pojemności dedykowanej ruch wychodzący, który można zakupić według przyrostów 200 MB/s. Korzystając z **Premium** typ, każda włączona jednostka zapewnia dodatkową przepustowość do aplikacji. |

## <a name="working-with-cdn"></a>Praca z usługą CDN

W większości przypadków należy włączono usługę CDN. Jednak jeśli są przewidywania współbieżności maksymalną mniejszy niż 500 osoby przeglądające następnie zalecane jest można wyłączyć usługi CDN, ponieważ sieć CDN jest skalowana najlepsze ze współbieżnością.

> [!NOTE]
> Punkt końcowy przesyłania strumieniowego `hostname` i adres URL przesyłania strumieniowego pozostaje taki sam, czy włączyć sieć CDN.

### <a name="detailed-explanation-of-how-caching-works"></a>Szczegółowe wyjaśnienie, jak działa buforowanie

Podczas dodawania sieci CDN, ponieważ ilość przepustowości, który jest wymagany w przypadku sieci CDN włączony punkt końcowy przesyłania strumieniowego zmienia nie istnieje wartość określonej przepustowości. Wiele zależy od typu zawartości, jak popularna jest, szybkości transmisji i protokołów. Sieć CDN jest tylko pamięci podręcznej, co to jest wymagana. Oznacza to, że popularnej zawartości będą udostępnianie bezpośrednio z sieci CDN — tak długo, jak wideo fragment jest buforowany. Zawartości na żywo jest prawdopodobnie można buforować, ponieważ zwykle mają wiele osób oglądanie dokładnie tak samo. Zawartość na żądanie może być nieco trudniejszy, ponieważ może mieć zawartości, niektóre popularne i niektóre nie jest. Jeśli masz milionów zasobów wideo, gdy żaden z nich są popularne (tylko 1 lub 2 osób przeglądających w tygodniu), ale masz tysiące osób obserwujących różnych plików wideo, usługi CDN staje się znacznie mniej skuteczne. Z tą pamięcią podręczną Chybienia, zwiększasz obciążenie na punkt końcowy przesyłania strumieniowego.
 
Należy również wziąć pod uwagę sposób adaptacyjnego przesyłania strumieniowego działa. Poszczególne fragmenty w poszczególnych wideo są buforowane, ponieważ jest własne jednostki. Na przykład jeśli po raz pierwszy niektórych wideo jest monitorowana, osoba pomija wokół oglądania tylko kilka sekund tu i tam tylko fragmentów wideo skojarzonych z obserwowane osoby Pobierz buforowane w usłudze CDN. Za pomocą adaptacyjnego przesyłania strumieniowego, zazwyczaj mają różne szybkości transmisji 5 do 7 wideo. Jeśli jedna osoba obserwuje o jednej szybkości transmisji bitów i innej osobie obserwuje różne szybkości transmisji bitów, następnie one są każdego buforowane osobno w usłudze CDN. Nawet wtedy, gdy dwie osoby obserwujesz tego samego szybkości transmisji bitów można przesyłanie strumieniowe za pośrednictwem różnych protokołów. Dla każdego protokołu (HLS, MPEG-DASH, Smooth Streaming) są buforowane osobno. Dlatego każdego szybkość transmisji bitów i protokół są buforowane osobno, a tylko tych fragmentów wideo, które zażądano są buforowane.
 
## <a name="properties"></a>Właściwości 

Ta sekcja zawiera szczegółowe informacje o niektórych właściwości StreamingEndpoint. Aby zapoznać się z przykładami sposobu tworzenia nowego punktu końcowego przesyłania strumieniowego i opisy wszystkich właściwości, zobacz [punkt końcowy przesyłania strumieniowego](https://docs.microsoft.com/rest/api/media/streamingendpoints/create). 

|Właściwość|Opis|  
|--------------|----------|
|`accessControl`|Umożliwiają skonfigurowanie następujących ustawień zabezpieczeń dla tego punktu końcowego przesyłania strumieniowego: Akamai podpis nagłówka uwierzytelniania klucze i adresy IP, które mogą połączyć się z tym punktem końcowym.<br />Tę właściwość można ustawić podczas `cdnEnabled`"" jest ustawiona na wartość false.|  
|`cdnEnabled`|Wskazuje, czy integracji usługi Azure CDN dla tego punktu końcowego przesyłania strumieniowego jest włączone (domyślnie wyłączony.)<br /><br /> Jeśli ustawisz `cdnEnabled` na wartość true, następujące konfiguracje wyłączone: `customHostNames` i `accessControl`.<br /><br />Nie wszystkie centra danych obsługują integracji usługi Azure CDN. Aby sprawdzić, czy centrum danych ma usługa Azure CDN Integracja jest dostępna, wykonaj następujące czynności:<br /><br /> -Próbuje ustawić `cdnEnabled` na wartość true.<br /><br /> — Sprawdź zwrócony wynik `HTTP Error Code 412` (PreconditionFailed) z komunikatem "Właściwości CdnEnabled punktu końcowego strumienia nie można ustawić wartość true, ponieważ funkcje sieci CDN nie jest dostępna w bieżącym regionie."<br /><br /> Jeśli ten błąd w centrum danych nie obsługuje. Należy spróbować innego centrum danych.|  
|`cdnProfile`|Gdy `cdnEnabled` jest ustawiona na wartość true, można również przekazać `cdnProfile` wartości. `cdnProfile` jest nazwa profilu CDN, w której zostanie utworzony punkt końcowy usługi CDN. Można podać istniejące cdnProfile lub użyć nowej. Jeśli wartość jest równa NULL i `cdnEnabled` jest true, wartość domyślna "AzureMediaStreamingPlatformCdnProfile" jest używana. Jeśli podane `cdnProfile` już istnieje, punkt końcowy został utworzony w nim. Jeśli profil nie istnieje, nowy profil pobiera tworzone automatycznie.|
|`cdnProvider`|Po włączeniu usługi CDN, można również przekazać `cdnProvider` wartości. `cdnProvider` Określa, który dostawca, który będzie używany. Obecnie obsługiwane są trzy wartości: "StandardVerizon", "PremiumVerizon" and "StandardAkamai". Jeśli podano żadnej wartości i `cdnEnabled` ma wartość true, "StandardVerizon" jest używana (która jest wartością domyślną).|
|`crossSiteAccessPolicies`|Służy do określania zasad dostępu cross-site dla różnych klientów. Aby uzyskać więcej informacji, zobacz [określenie pliku zasad między domenami](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html) i [wprowadzania Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955\(v=vs.95\).aspx).|  
|`customHostNames`|Używany do konfigurowania punktu końcowego przesyłania strumieniowego, aby akceptować ruch skierowany do niestandardową nazwą hosta. Dzięki temu łatwiej konfiguracji zarządzania ruchu za pośrednictwem globalnej Traffic Manager GTM (wprowadzenie), a także dla nazw domen marki ma być używany jako nazwa punktu końcowego przesyłania strumieniowego.<br /><br /> Własność nazwy domeny musi zostać potwierdzone przy usługi Azure Media Services. Usługa Azure Media Services sprawdza własność nazwy domeny, wymagając `CName` rekord zawierający identyfikator konta usługi Azure Media Services jako składnik, który ma zostać dodany do domeny w użyciu. Na przykład dla "sports.contoso.com", który ma być używany jako niestandardową nazwą hosta punktu końcowego przesyłania strumieniowego, rekord `<accountId>.contoso.com` należy skonfigurować, aby wskazywały na jeden z nazw hostów weryfikacji usługi Media Services. Nazwa hosta Weryfikacja składa się z verifydns. \<mediaservices dns strefy >. Poniższa tabela zawiera oczekiwane stref DNS ma być używany w rekordzie Sprawdź, czy dla różnych regionów platformy Azure.<br /><br /> Ameryka Północna, Europa, Singapur, SRA Hongkong, Japonia, część:<br /><br /> - mediaservices.windows.net<br /><br /> -verifydns.mediaservices.windows.net<br /><br /> Chińska wersja:<br /><br /> - mediaservices.chinacloudapi.cn<br /><br /> - verifydns.mediaservices.chinacloudapi.cn<br /><br /> Na przykład `CName` rekord, który mapuje "945a4c4e-28ea-45 cd-8ccb-a519f6b700ad.contoso.com" do "verifydns.mediaservices.windows.net" okazuje się, że 945a4c4e-28ea-45cd-8ccb-a519f6b700ad usługi Azure Media Services identyfikator ma własności domeny contoso.com, umożliwiając w ten sposób dowolną nazwę w domenie contoso.com, ma być używany jako niestandardową nazwą hosta dla punktu końcowego przesyłania strumieniowego w ramach tego konta.<br /><br /> Aby znaleźć wartość Identyfikatora usługi multimediów, przejdź do [witryny Azure portal](https://portal.azure.com/) i wybierz swoje konto usługi multimediów. Identyfikator elementu MULTIMEDIALNEGO usługi pojawia się po prawej stronie pulpitu NAWIGACYJNEGO.<br /><br /> **Ostrzeżenie**: Jeśli podjęto próbę ustawienia niestandardową nazwą hosta bez prawidłowego weryfikacji `CName` rekordu, to odpowiedź DNS zakończy się niepowodzeniem i wówczas buforowana przez pewien czas. Po właściwego rekordu znajduje się w miejscu, może potrwać chwilę, aż ponownie sprawdzić poprawności nazwy odpowiedzi z pamięci podręcznej. W zależności od dostawcy DNS dla domeny niestandardowej jego może dopiero po pewnym czasie od kilku minut do godziny można przechowywać w rekordzie.<br /><br /> Oprócz `CName` mapujący `<accountId>.<parent domain>` do `verifydns.<mediaservices-dns-zone>`, należy utworzyć inny `CName` mapujący niestandardową nazwą hosta (na przykład `sports.contoso.com`) do nazwy hosta StreamingEndpont usług Media (na przykład `amstest.streaming.mediaservices.windows.net`).<br /><br /> **Uwaga**: W tym samym centrum danych, punkty końcowe przesyłania strumieniowego nie mają taką samą nazwę niestandardowego hosta.<br /> Ta właściwość jest prawidłowy w przypadku wersji Standard i premium, punkty końcowe przesyłania strumieniowego i mogą być ustawiane podczas "cdnEnabled": false<br/><br/> Obecnie usługa AMS nie obsługuje protokołu SSL z zastosowaniem domen niestandardowych.  |  
|`maxCacheAge`|Zastępuje domyślny maksymalny wiek pamięci podręcznej kontrolki nagłówka HTTP ustawione przez punkt końcowy przesyłania strumieniowego multimediów fragmentów i manifesty na żądanie. Wartość jest ustawiona w ciągu kilku sekund.|
|`resourceState`|Wartości dla właściwości:<br /><br /> -Zatrzymane. Początkowy stan punktu końcowego przesyłania strumieniowego po utworzeniu.<br /><br /> — Uruchamianie. Punkt końcowy przesyłania strumieniowego są przenoszone do stanu uruchomienia.<br /><br /> — Uruchamianie. Punkt końcowy przesyłania strumieniowego jest w stanie przesyłanie strumieniowe zawartości do klientów.<br /><br /> -Skalowania. Jednostki skalowania są zwiększanie lub zmniejszanie.<br /><br /> -Jest zatrzymywany. Punkt końcowy przesyłania strumieniowego są przenoszone do stanu zatrzymania.<br/><br/> — Usuwanie. Trwa usuwanie punktu końcowego przesyłania strumieniowego.|
|`scaleUnits `|scaleUnits zapewniają pojemności dedykowanej ruch wychodzący, który można zakupić według przyrostów 200 MB/s. Jeśli musisz przenieść **Premium** wpisz, dostosować `scaleUnits`. |

## <a name="next-steps"></a>Kolejne kroki

Przykład [w tym repozytorium](https://github.com/Azure-Samples/media-services-v3-dotnet-quickstarts/blob/master/AMSV3Quickstarts/EncodeAndStreamFiles/Program.cs) pokazuje, jak uruchomić domyślny punkt końcowy przy użyciu platformy .NET przesyłania strumieniowego.

