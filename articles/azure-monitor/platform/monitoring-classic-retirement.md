---
title: Ujednolicone alerty i monitorowanie w usłudze Azure Monitor zastępuje klasycznego alerty i monitorowanie
description: Omówienie wycofanie klasycznych usług monitorowania i funkcjonalności, wcześniej wyświetlane w witrynie Azure portal w obszarze alerty (klasyczne). Klasyczne, alerty i monitorowanie obejmuje alertów klasycznych metryki dla zasobów platformy Azure, klasyczne alertów dotyczących metryk usługi Application Insights alertów klasycznych testu internetowego usługi Application Insights klasycznego metryk niestandardowych na podstawie alertów dla usługi Application Insights i Model Klasyczny alerty dotyczące SmartDetection Insights aplikacji w wersji 1
author: msvijayn
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 2/7/2019
ms.author: vinagara
ms.subservice: alerts
ms.openlocfilehash: 7cca9d9c91f35c30bbd71ae82b9f02447051078d
ms.sourcegitcommit: 943af92555ba640288464c11d84e01da948db5c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/09/2019
ms.locfileid: "55983172"
---
# <a name="unified-alerting--monitoring-in-azure-monitor-replaces-classic-alerting--monitoring"></a>Ujednolicone alerty i monitorowanie w usłudze Azure Monitor zastępuje klasycznego alerty i monitorowanie

Usługa Azure Monitor stał się teraz ujednolicony pełnego stosu monitorowania usługi, która obsługuje teraz "Jedną metrykę" i "Alerty jednego" między zasobami; Aby uzyskać więcej informacji, zobacz nasze [wpis w blogu na nowej usługi Azure Monitor](https://azure.microsoft.com/blog/new-full-stack-monitoring-capabilities-in-azure-monitor/). Nowa platforma monitorowania i zgłaszania alertów platformy Azure została opracowana jako szybciej i MĄDRZEJ i rozszerzalny — przechowywanie tempa z rosnącą expanse chmury obliczeniowej i wiersz z filozofią inteligentnej chmury firmy Microsoft. 

Nowe monitorowania platformy Azure i zgłaszania alertów platformy w miejscu, firma Microsoft będzie wycofywana "klasyczny", monitorowania i zgłaszania alertów platformy — hostowanych na platformie *wyświetlanie alertów klasycznych* sekcji alertów platformy Azure, **zostaną wycofane w czerwcu 2019 w chmurach publicznych Azure**. [Chmura platformy Azure dla instytucji rządowych](../../azure-government/documentation-government-welcome.md) nie zostaną zmienione.

 ![Klasyczny alert w witrynie Azure portal](media/monitoring-classic-retirement/monitor-alert-screen2.png) 

Zachęcamy do rozpoczęcia pracy i ponownie utworzyć alerty na nowej platformie. W przypadku klientów, którzy mają dużą liczbę alertów będziemy działają w celu zapewnienia zautomatyzowany sposób, aby przenieść istniejące alertów klasycznych do nowego systemu alerty bez przerw w działaniu lub dodane koszty.

> [!IMPORTANT]
> Klasyczne reguły alertów utworzone w dzienniku aktywności nie będzie przestarzały lub migracji. Wszystkie klasyczne reguły alertów utworzone w dzienniku aktywności można uzyskać dostęp i używany jako-pochodzi z usługi Azure Monitor nowe — alerty. Aby uzyskać więcej informacji, zobacz [tworzenie, wyświetlanie i zarządzanie nimi za pomocą usługi Azure Monitor alertów dziennika aktywności](../../azure-monitor/platform/alerts-activity-log.md). Podobnie, można uzyskać dostęp i używany jako alerty dotyczące kondycji usługi-pochodzi z nową sekcję Service Health. Aby uzyskać więcej informacji, zobacz [alertów dla powiadomień dotyczących kondycji usług](../../azure-monitor/platform/alerts-activity-log-service-notifications.md).

## <a name="unified-metrics-and-alerts-in-application-insights"></a>Ujednolicone metryk i alertów w usłudze Application Insights

Nowsze platformy metryk usługi Azure Monitor będzie teraz power monitorowania pochodzących z usługi Application Insights. To przeniesienie oznacza, że usługi Application Insights będzie dołączyć do grupy akcji, co znacznie więcej opcji niż po prostu poprzedniego wywołania poczty e-mail i elementy webhook. Teraz możesz wyzwolić alerty, połączenia głosowe, usługi Azure Functions, Logic Apps, wiadomości SMS i narzędziami ITSM, takich jak usługi ServiceNow i elementów Runbook usługi Automation. Przy użyciu niemal w czasie rzeczywistym, monitorowania i alertów, nowa platforma umożliwia użytkownikom usługi Application Insights używają tej samej technologii, zapewniająca monitorowanie z przekraczaniem innych zasobów platformy Azure i wspieranie monitorowania produktów firmy Microsoft.

Nowe ujednolicone monitorowanie i alerty dla usługi Application Insights będzie obejmować:

- **Application Insights platformy metryki** — która generuje dane pomiarowe popularnych wstępnie utworzone z produktu usługi Application Insights. Aby uzyskać więcej informacji znajduje się w artykule na temat korzystania z [platformy metryki dla usługi Application Insights na nowej usługi Azure Monitor](../../azure-monitor/app/pre-aggregated-metrics-log-metrics.md#pre-aggregated-metrics).
- **Test sieci Web i Application Insights dostępności** — które zapewnia możliwość oceny czasu odpowiedzi i dostępność aplikacji sieci web lub serwera. Aby uzyskać więcej informacji znajduje się w artykule na temat korzystania z [testy dostępności oraz alerty dotyczące usługi Application Insights na nowej usługi Azure Monitor](../../azure-monitor/app/monitor-web-app-availability.md).
- **Metryki niestandardowe Insights aplikacji** — które pozwala określić i wyemituj własnych metryk monitorowania i alertów. Aby uzyskać więcej informacji znajduje się w artykule na temat korzystania z [metryki niestandardowe dla usługi Application Insights na nowej usługi Azure Monitor](../../azure-monitor/app/pre-aggregated-metrics-log-metrics.md#custom-metrics-dimensions-and-pre-aggregation).
- **Application Insights anomalie w zakresie błędów (część wykrywania inteligentnego)** — które automatycznie powiadamia, w czasie zbliżonym do rzeczywistego Jeśli nietypowy wzrost liczba nieudanych żądań HTTP lub wywołania zależności aplikacji sieci web. Application Insights anomalie w zakresie błędów (część wykrywania inteligentnego) jako część nowej usługi Azure Monitor będzie wkrótce dostępna, a następnie zaktualizujemy ten dokument wraz z łączami w następnej iteracji zgodnie z jego jest przedstawiana w poziomie w najbliższych miesiącach.

## <a name="unified-metrics-and-alerts-for-other-azure-resources"></a>Ujednolicone metryki i alerty dotyczące innych zasobów platformy Azure

Od marca 2018 r. następna generacja wielowymiarowych monitorowania zasobów platformy Azure i generowania alertów zostały w dostępności. Nowsze platformy metryk i alertów jest teraz szybciej dzięki możliwości niemal w czasie rzeczywistym. Co ważniejsze nowszych alertów metryk platformy zapewnić większą szczegółowość, jak platforma nowszej obejmuje opcję wymiarów, które umożliwiają wycinka i Filtruj operację kombinacji określonej wartości lub warunek. Podobnie jak wszystkie alerty w nowej usłudze Azure Monitor nowszych alertów metryk są bardziej extensible przy użyciu ActionGroups — dzięki czemu powiadomienia rozwinąć poza wiadomości e-mail lub element webhook programu SMS, głos, funkcji platformy Azure, element Runbook usługi Automation i nie tylko. Aby uzyskać więcej informacji, zobacz [tworzenie, wyświetlanie i zarządzanie nimi za pomocą usługi Azure Monitor alertów dotyczących metryk](../../azure-monitor/platform/alerts-metric.md).
Nowsze metryki dla zasobów platformy Azure są dostępne jako:

- **Usługa Azure Monitor standardowych metryk platformy** — która generuje dane pomiarowe popularnych wstępnie wypełnione z różnych usług platformy Azure i produktów. Aby uzyskać więcej informacji znajduje się w artykule na [metryki są obsługiwane w usłudze Azure Monitor](../../azure-monitor/platform/alerts-metric-near-real-time.md#metrics-and-dimensions-supported) i [obsługuje alertów dotyczących metryk w usłudze Azure Monitor](../../azure-monitor/platform/alerts-metric-overview.md#supported-resource-types-for-metric-alerts).
- **Metryki usługi Azure Monitor niestandardowe** — która generuje dane pomiarowe ze źródeł takich jak agenta funkcji Diagnostyka Azure przez użytkownika. Aby uzyskać więcej informacji znajduje się w artykule na [metryki niestandardowe w usłudze Azure Monitor](../../azure-monitor/platform/metrics-custom-overview.md). Za pomocą metryk niestandardowych, można również opublikować metryki zebrane przez [agenta funkcji Diagnostyka Azure Windows](../../azure-monitor/platform/collect-custom-metrics-guestos-resource-manager-vm.md) i [agenta InfluxData Telegraf](../../azure-monitor/platform/collect-custom-metrics-linux-telegraf.md).

## <a name="retirement-of-classic-monitoring-and-alerting-platform"></a>Wycofanie klasyczne, monitorowania i zgłaszania alertów platformy

Jak wspomniano wcześniej, klasyczne, monitorowania i zgłaszania alertów platformy obecnie można używać z [alerty (klasyczne) sekcji](../../azure-monitor/platform/alerts-classic.overview.md) Azure portal zostaną wycofane w przychodzących miesiące podane one zostały zastąpione przez nowszy system.
Starsza wersja klasyczna monitorowania i alertów zostanie wycofana 30 czerwca 2019; w tym zamknięcia powiązanych interfejsów API, interfejs portalu platformy Azure i usług w nim. W szczególności te funkcje staną się przestarzałe:

- Starsze (model klasyczny) alerty i metryki dla zasobów platformy Azure jako obecnie dostępna za pośrednictwem [alerty (klasyczne) sekcji](../../azure-monitor/platform/alerts-classic.overview.md) Azure portal; dostępne jako [microsoft.insights/alertrules](https://docs.microsoft.com/rest/api/monitor/alertrules) zasobów
- Starsze platformy (model klasyczny) i metryki niestandardowe dla usługi Application Insights, a także alerty na nich jako obecnie dostępna za pośrednictwem [alerty (klasyczne) sekcji](../../azure-monitor/platform/alerts-classic.overview.md) o witrynie Azure portal i dostępne jako [microsoft.insights/ alertrules](https://docs.microsoft.com/rest/api/monitor/alertrules) zasobów
- Starsze (model klasyczny) alert anomalie obecnie dostępna jako [wykrywania inteligentnego w usłudze Application Insights](../../azure-monitor/app/proactive-diagnostics.md) w witrynie Azure portal; alertów skonfigurowanych objętego [alerty (klasyczne) sekcji](../../azure-monitor/platform/alerts-classic.overview.md) platformy Azure Portal

Wszystkie klasyczne monitorowania i zgłaszania alertów systemy w tym odpowiadającego [interfejsu API](https://msdn.microsoft.com/library/azure/dn931945.aspx), [PowerShell](../../azure-monitor/platform/alerts-classic-portal.md), [interfejsu wiersza polecenia](../../azure-monitor/platform/alerts-classic-portal.md), [stronę witryny Azure portal](../../azure-monitor/platform/alerts-classic-portal.md)i [ Szablon zasobu](../../azure-monitor/platform/alerts-enable-template.md) będą nadal można używać do końca czerwca 2019 r. 

Na koniec czerwca 2019 r, w usłudze Azure Monitor:

- Klasyczne usługi monitorowania i alerty zostaną wycofane i nie są już dostępne na potrzeby tworzenia nowych reguł alertów
- Reguły alertów, które nadal istnieją w alerty (klasyczne) poza 2019 czerwca w dalszym ciągu wykonywania i wyzwalać powiadomienia, ale nie są dostępne do modyfikacji.
- Począwszy od lipca 2019 r, wszystkie reguły alertów w klasycznym monitorowanie i alerty zostaną automatycznie przeniesione przez firmę Microsoft na ich odpowiedniki w nowej platformie usługi Azure monitor. Ten proces będzie bezproblemowe bez żadnych przestojów, a klienci będą mogli korzystać bez utraty monitorowania pokrycia.
- Alert reguły migracji do nowego alerty platformy zapewni monitorowania pokrycia, tak jak poprzednio, ale uruchomienie nastąpi powiadomienia o nowych ładunków. Dowolnego adresu e-mail, punktem końcowym elementu webhook lub link do aplikacji logiki skojarzone z klasycznej reguły alertu zostanie przekazane dalej podczas migracji, ale może nie działać poprawnie jako ładunek alert będzie się różnił w nowej platformie

> [!IMPORTANT]
> Microsoft Azure Monitor zapewnia narzędzia, klienci będą mogli automatycznie migrować ich klasyczne reguły alertów na nową platformę wkrótce. I uruchom go w życie dla wszystkich reguł alertów klasycznych, które nadal istnieją, od lipca 2019 r. Klienci będą musieli upewnić się, automatyzacji konsumencki ładunku klasycznej reguły alertu jest przystosowany do obsługi nowych ładunku z [Unified metryk i alertów w usłudze Application Insights](#unified-metrics-and-alerts-in-application-insights) lub [Unified metryk i alertów dla innych platformy Azure zasoby](#unified-metrics-and-alerts-for-other-azure-resources), po migracji z klasycznej reguły alertu. 

Wkrótce udostępnimy narzędzia, aby możliwe było dobrowolnie migracji alerty z [alerty (klasyczne) sekcji](../../azure-monitor/platform/alerts-classic.overview.md) z witryny Azure portal do nowych alertów platformy Azure. Wszystkie reguły skonfigurowanych w alertach (model klasyczny), które są migrowane do nowej usługi Azure Monitor pozostaną bezpłatne ale nie opłatami. Zmigrowane z klasycznego reguł alertów będzie mieć nie opłatami wypychanie powiadomień pocztą e-mail, element webhook lub aplikacji LogicApp. Jednak użycie nowszej typów powiadomień lub akcję (np. wiadomości SMS, połączenie głosowe, integracji z rozwiązaniami ITSM itd.) będą naliczane czy dodane do migracji lub nowego alertu. Aby uzyskać więcej informacji, zobacz [cennik usługi Azure Monitor](https://azure.microsoft.com/pricing/details/monitor/).

Ponadto następujące będą naliczane w ramach mieszczący [cennik usługi Azure Monitor](https://azure.microsoft.com/pricing/details/monitor/):

- Wszelkie nowe (nieprzeniesione) reguły alertu przekraczające bezpłatny limit jednostek na nowej platformie usługi Azure Monitor
- Wszystkie dane pozyskiwane i przechowywane dłużej niż bezpłatny limit jednostek usługi Azure Monitor
- Wszystkie testy wielu testów w sieci web, wykonywane przez usługę Application Insights
- Wszystkie metryki niestandardowe przechowywany dłużej niż bezpłatny limit jednostek w usłudze Azure Monitor

Ten artykuł będzie stale aktualizowana przy użyciu łącza i szczegóły dotyczące nowa platforma Azure monitorowanie i alerty, funkcje, jak również dostępność narzędzia do świadczenia użytkownikom pomocy w przyjmowaniu na nową platformę Azure Monitor.


## <a name="next-steps"></a>Kolejne kroki

* Dowiedz się więcej o [nowe, ujednolicone usługi Azure Monitor](../../azure-monitor/overview.md).
* Dowiedz się więcej o nowym [Azure Alerts](../../azure-monitor/platform/alerts-overview.md).

