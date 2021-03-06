---
title: Analizowanie danych czujnika przy użyciu Apache Hive i Apache Hadoop — Azure HDInsight
description: Dowiedz się, jak analizować dane czujników przy użyciu konsoli Apache do zapytań Hive z HDInsight (Hadoop), a następnie wizualizować te dane w programie Microsoft Excel za pomocą PowerView.
services: hdinsight
ms.service: hdinsight
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.topic: conceptual
ms.date: 04/14/2017
ROBOTS: NOINDEX
ms.openlocfilehash: b9c8f1af612c220534e45c5c66651f0ad8600826
ms.sourcegitcommit: c94cf3840db42f099b4dc858cd0c77c4e3e4c436
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/19/2018
ms.locfileid: "53628190"
---
# <a name="analyze-sensor-data-using-the-apache-hive-query-console-on-apache-hadoop-in-hdinsight"></a>Analizowanie danych czujników na technologii Apache Hadoop w HDInsight przy użyciu konsoli Apache Hive zapytań

Dowiedz się, jak analizować dane czujników przy użyciu konsoli Apache do zapytań Hive z HDInsight (Apache Hadoop), a następnie wizualizować te dane w programie Microsoft Excel za pomocą Power View.

> [!IMPORTANT]  
> Kroki opisane w tym dokumencie działają tylko z klastrami HDInsight z systemem Windows. HDInsight jest dostępna tylko na Windows dla wersji starszej niż HDInsight 3.4. Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).


W tym przykładzie użyjesz Hive do przetwarzania danych historycznych i zidentyfikować problemy z systemami ogrzewania i klimatyzacji. W szczególności możesz zidentyfikować systemy nie będą mogli w sposób niezawodny utrzymać stałej temperatury, wykonując następujące czynności:

* Tworzenie tabel programu HIVE do zapytania o dane przechowywane w plikach rozdzielanymi przecinkami (CSV).
* Tworzenie zapytań programu HIVE do analizowania danych.
* Aby pobrać analizowanych danych, należy użyć programu Microsoft Excel połączyć się z HDInsight.
* Aby zwizualizować dane, należy użyć Power View.

![Diagram architektury rozwiązania](./media/apache-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a>Wymagania wstępne

* Klaster usługi HDInsight (Hadoop): Zobacz [klastrów utworzyć Apache Hadoop w HDInsight](../hdinsight-hadoop-provision-linux-clusters.md) informacji dotyczących tworzenia klastra.
* Microsoft Excel 2013

  > [!NOTE]  
  > Program Microsoft Excel jest używany do wizualizacji danych z [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).

* [Sterownika Microsoft Hive ODBC](https://www.microsoft.com/download/details.aspx?id=40886)

## <a name="to-run-the-sample"></a>Aby uruchomić przykład

1. W przeglądarce sieci web przejdź do następującego adresu URL: 

         https://<clustername>.azurehdinsight.net

    Element `<clustername>` należy zastąpić nazwą klastra usługi HDInsight.

    Po wyświetleniu monitu uwierzytelniania przy użyciu nazwy użytkownika administratora i hasła, które zostały użyte podczas udostępniania tego klastra.

2. Ze strony internetowej, która zostanie otwarta, kliknij przycisk **Getting Started galerii** kartę, a następnie w obszarze **rozwiązania z przykładowymi danymi** kategorię, kliknij przycisk **analizowanie danych z czujników** próbki.

    ![Pobieranie obrazu z galerii wprowadzenie](./media/apache-hive-analyze-sensor-data/getting-started-gallery.png)

3. Postępuj zgodnie z instrukcjami na stronie sieci web zakończenie próbki.
