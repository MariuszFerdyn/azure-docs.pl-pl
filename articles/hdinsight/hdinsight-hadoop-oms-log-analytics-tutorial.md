---
title: Używanie programu Log Analytics do monitorowania klastrów Azure HDInsight
description: Dowiedz się, jak używać usługi Azure Log Analytics do monitorowania zadań uruchamianych w klastrze usługi HDInsight.
services: hdinsight
author: hrasheed-msft
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 11/05/2018
ms.author: hrasheed
ms.openlocfilehash: cd129ea68315223516ac1cd3e7577b5ee4bf92e5
ms.sourcegitcommit: e69fc381852ce8615ee318b5f77ae7c6123a744c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/11/2019
ms.locfileid: "56005118"
---
# <a name="use-azure-log-analytics-to-monitor-hdinsight-clusters"></a>Umożliwia monitorowanie klastrów HDInsight w usłudze Azure Log Analytics

Dowiedz się, jak włączyć usługi Azure Log Analytics monitorować działania klastra usługi Hadoop w HDInsight oraz sposób dodawania HDInisght rozwiązanie do monitorowania.

[Log Analytics](../log-analytics/log-analytics-overview.md) to usługa w usłudze Azure Monitor, który monitoruje środowiska chmurowe lokalnych i w celu zachowania ich dostępności i wydajności. Zbiera ona dane generowane przez zasoby w środowiskach chmurowych i lokalnych oraz inne narzędzia do monitorowania, aby przeprowadzać analizę na podstawie wielu źródeł.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem [utwórz bezpłatne konto](https://azure.microsoft.com/free/).

## <a name="prerequisites"></a>Wymagania wstępne

* **Obszar roboczy usługi Log Analytics**. Ten obszar roboczy można traktować jako unikatowe środowisko usługi Log Analytics z własnym repozytorium danych, źródłami danych i rozwiązań. Aby uzyskać instrukcje, zobacz [Utwórz obszar roboczy usługi Log Analytics](../azure-monitor/learn/quick-collect-azurevm.md#create-a-workspace).

* **Klaster usługi Azure HDInsight**. Obecnie za pomocą usługi Log Analytics są następujące typy klastrów HDInsight:

  * Hadoop
  * HBase
  * Zapytanie interakcyjne
  * Kafka
  * platforma Spark
  * Storm

  Aby uzyskać instrukcje dotyczące sposobu tworzenia klastra usługi HDInsight, zobacz [Rozpoczynanie pracy z usługą Azure HDInsight](hadoop/apache-hadoop-linux-tutorial-get-started.md).

> [!NOTE]  
> Zaleca się umieszczenie klastra HDInsight i obszar roboczy usługi Log Analytics, w tym samym regionie, w celu zapewnienia lepszej wydajności. Usługa Azure Log Analytics nie jest dostępna we wszystkich regionach platformy Azure.

## <a name="enable-log-analytics-by-using-the-portal"></a>Włączanie usługi Log Analytics przy użyciu portalu

W tej sekcji skonfigurujesz istniejącego klastra usługi HDInsight Hadoop używać obszaru roboczego usługi Azure Log Analytics do monitorowania zadań, dzienniki debugowania itd.

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).

2. Z menu po lewej stronie wybierz **wszystkich usług**.

3. W obszarze **ANALYTICS**, wybierz opcję **klastry HDInsight**.

4. Z lewej strony w obszarze **monitorowanie**, wybierz opcję **pakietu Operations Management Suite**.

5. W widoku głównego w obszarze **monitorowania pakietu OMS**, wybierz opcję **Włącz**.

6. Z **wybierz obszar roboczy** listy rozwijanej wybierz istniejący obszar roboczy usługi Log Analytics.

7. Wybierz pozycję **Zapisz**.

    ![Aby włączyć monitorowanie klastrów HDInsight](./media/hdinsight-hadoop-oms-log-analytics-tutorial/hdinsight-enable-monitoring.png "Włącz monitorowanie dla klastrów HDInsight")

    Może potrwać kilka minut, aby zapisać ustawienia.

## <a name="enable-log-analytics-by-using-azure-powershell"></a>Włączanie usługi Log Analytics przy użyciu programu Azure PowerShell

Można włączyć za pomocą programu Azure PowerShell w usłudze Log Analytics. To polecenie cmdlet:

```powershell
Enable-AzureRmHDInsightOperationsManagementSuite
      [-Name] <CLUSTER NAME>
      [-WorkspaceId] <LOG ANALYTICS WORKSPACE NAME>
      [-PrimaryKey] <LOG ANALYTICS WORKSPACE PRIMARY KEY>
      [-ResourceGroupName] <RESOURCE GROUIP NAME>
```

Zobacz [AzureRmHDInsightOperationsManagementSuite Włącz](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/Enable-AzureRmHDInsightOperationsManagementSuite?view=azurermps-5.0.0).

Aby wyłączyć, to polecenie cmdlet:

```powershell
Disable-AzureRmHDInsightOperationsManagementSuite
       [-Name] <CLUSTER NAME>
       [-ResourceGroupName] <RESOURCE GROUP NAME>
```

Zobacz [AzureRmHDInsightOperationsManagementSuite Wyłącz](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/disable-azurermhdinsightoperationsmanagementsuite?view=azurermps-5.0.0).

## <a name="install-hdinsight-cluster-management-solutions"></a>Instalowanie rozwiązania do zarządzania klastrem HDInsight

HDInsight oferuje rozwiązania specyficzne dla klastra zarządzania, które można dodać do usługi Azure Log Analytics. [Rozwiązania do zarządzania](../log-analytics/log-analytics-add-solutions.md) Dodawanie funkcji do usługi Log Analytics oraz podanie dodatkowych danych i narzędzia do analizy. Te rozwiązania zbieranie metryk istotną poprawę wydajności ze klastry usługi HDInsight i zapewniają narzędzia do wyszukiwania metryk. Rozwiązania te udostępniają wizualizacje i pulpity nawigacyjne dla większości typów klastrów obsługuje HDInsight. Za pomocą metryk, które są zbierane za pomocą rozwiązania, można utworzyć niestandardowe reguły monitorowania i alertów.

Poniżej przedstawiono dostępne rozwiązania HDInsight:

* Monitorowanie usługi HDInsight Hadoop
* Monitorowanie bazy danych HBase usługi HDInsight
* Monitorowanie usługi HDInsight interakcyjnych zapytań
* Monitorowanie systemu Kafka usługi HDInsight
* Monitorowanie platformy Spark usługi HDInsight
* Monitorowanie usługi HDInsight Storm

Aby uzyskać instrukcje zainstalować rozwiązanie do zarządzania, zobacz [rozwiązań do zarządzania na platformie Azure](../azure-monitor/insights/solutions.md#install-a-monitoring-solution). Aby poeksperymentować, należy zainstalować rozwiązanie HDInsight Hadoop Monotiring. Gdy wszystko będzie gotowe, zostanie wyświetlony **HDInsightHadoop** kafelka na liście **Podsumowanie**. Wybierz **HDInsightHadoop** kafelka. Rozwiązanie HDInsightHadoop wygląda następująco:

![Widok rozwiązania monitorowania HDInsight](media/hdinsight-hadoop-oms-log-analytics-tutorial/hdinsight-oms-hdinsight-hadoop-monitoring-solution.png)

Ponieważ klaster jest całkiem nowego klastra, raport nie wyświetla żadnych działań.

## <a name="next-steps"></a>Kolejne kroki

* [Zapytanie usługi Azure Log Analytics do monitorowania klastrów HDInsight](hdinsight-hadoop-oms-log-analytics-use-queries.md)
