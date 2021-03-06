---
title: Zmienne środowiskowe węzła — Azure Batch COMPUTE | Dokumentacja firmy Microsoft
description: Obliczenia Odnośnik zmiennej środowiskowej węzła usługi Azure Batch Analytics.
services: batch
author: laurenhughes
manager: jeconnoc
ms.assetid: ''
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 01/03/2019
ms.author: lahugh
ms.openlocfilehash: 48c2172e02e935dde28ac323c776c8895b1d36b2
ms.sourcegitcommit: 25936232821e1e5a88843136044eb71e28911928
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/04/2019
ms.locfileid: "54017365"
---
# <a name="azure-batch-compute-node-environment-variables"></a>Zmienne środowiskowe węzła obliczeniowego usługi Azure Batch

[Usługi Azure Batch](https://azure.microsoft.com/services/batch/) ustawia następujące zmienne środowiskowe w węzłach obliczeniowych. Można odwoływać się tych zmiennych środowiskowych w wierszach polecenia zadań podrzędnych oraz w programach i skryptach uruchamianych przez wiersze polecenia.

Aby uzyskać dodatkowe informacje dotyczące używania zmiennych środowiskowych za pomocą usługi Batch, zobacz [ustawienia środowiska dla podzadań](https://docs.microsoft.com/azure/batch/batch-api-basics#environment-settings-for-tasks).

## <a name="environment-variable-visibility"></a>Widoczność zmiennych środowiskowych

Te zmienne środowiskowe są widoczne tylko w kontekście **zadania użytkownika**, konto użytkownika w węźle, w którym zadanie jest wykonywane. Będą one *niewidoczne*, jeśli [zdalnie połączysz się](https://azure.microsoft.com/documentation/articles/batch-api-basics/#connecting-to-compute-nodes) z węzłem obliczeniowym, za pomocą protokołu RDP lub SSH i wyświetlisz listę zmiennych środowiskowych. Dzieje się tak dlatego, że konto użytkownika, używane na potrzeby połączenia zdalnego jest inne niż konto używane przez zadanie podrzędne.

## <a name="command-line-expansion-of-environment-variables"></a>Wiersza polecenia rozszerzanie zmiennych środowiskowych

Wiersze polecenia wykonywane przez zadania obliczeniowe węzłów nie uruchamiaj w ramach powłoki. Dlatego te wiersze polecenia nie może natywnie korzystać z zalet funkcji powłoki, takich jak rozszerzanie zmiennych środowiskowych (dotyczy to również `PATH`). Aby móc korzystać z takich funkcji, musisz mieć **Wywołaj powłokę** w wierszu polecenia. Na przykład uruchomić `cmd.exe` Windows węzłów obliczeniowych lub `/bin/sh` w węzłach systemu Linux:

`cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

`/bin/sh -c MyTaskApplication $MY_ENV_VAR`

## <a name="environment-variables"></a>Zmienne środowiskowe

| Nazwa zmiennej                     | Opis                                                              | Dostępność | Przykład |
|-----------------------------------|--------------------------------------------------------------------------|--------------|---------|
| AZ_BATCH_ACCOUNT_NAME           | Nazwa konta usługi Batch, do którego należy zadanie.                  | Wszystkie zadania.   | mybatchaccount |
| AZ_BATCH_AUTHENTICATION_TOKEN   | Token uwierzytelniania, która udziela dostępu do ograniczonego zestawu operacji usługi Batch. Ta zmienna środowiskowa jest obecny tylko, jeśli [authenticationTokenSettings](/rest/api/batchservice/task/add#authenticationtokensettings) są ustawiane podczas [zadanie zostanie dodane](/rest/api/batchservice/task/add#request-body). Wartość tokenu jest używany w interfejsów API usługi Batch jako poświadczeń do tworzenia klienta usługi Batch, takich jak w [interfejsu API platformy .NET BatchClient.Open()](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.batchclient.open#Microsoft_Azure_Batch_BatchClient_Open_Microsoft_Azure_Batch_Auth_BatchTokenCredentials_). | Wszystkie zadania. | Token dostępu OAuth2 |
| AZ_BATCH_CERTIFICATES_DIR       | Katalogu w ramach [katalogu roboczego zadań] [ files_dirs] węzłów obliczeniowych, w którym certyfikaty są przechowywane w systemie Linux. Należy zauważyć, że ta zmienna środowiskowa nie ma zastosowania do Windows węzłów obliczeniowych.                                                  | Wszystkie zadania.   |  /mnt/batch/tasks/workitems/batchjob001/job-1/task001/certs |
| AZ_BATCH_JOB_ID                 | Identyfikator zadania, do którego należy zadanie podrzędne. | Wszystkie zadania, z wyjątkiem zadanie podrzędne uruchamiania. | batchjob001 |
| AZ_BATCH_JOB_PREP_DIR           | Pełna ścieżka zadanie podrzędne przygotowanie [katalogu zadań] [ files_dirs] w węźle. | Wszystkie zadania, z wyjątkiem zadania podrzędnego uruchamiania i zadania podrzędnego przygotowania zadania. Dostępną tylko, jeśli zadanie jest skonfigurowany przy użyciu zadania przygotowania zadania. | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation |
| AZ_BATCH_JOB_PREP_WORKING_DIR   | Pełna ścieżka zadanie podrzędne przygotowanie [katalogu roboczego zadań] [ files_dirs] w węźle. | Wszystkie zadania, z wyjątkiem zadania podrzędnego uruchamiania i zadania podrzędnego przygotowania zadania. Dostępną tylko, jeśli zadanie jest skonfigurowany przy użyciu zadania przygotowania zadania. | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation\wd |
| AZ_BATCH_NODE_ID                | Identyfikator węzła, który zadanie zostanie przypisane do. | Wszystkie zadania. | tvm-1219235766_3-20160919t172711z |
| AZ_BATCH_NODE_ROOT_DIR          | Pełna ścieżka katalogu głównego wszystkich [Batch katalogi] [ files_dirs] w węźle. | Wszystkie zadania. | C:\user\tasks |
| AZ_BATCH_NODE_SHARED_DIR        | Pełna ścieżka [udostępnionego katalogu] [ files_dirs] w węźle. Wszystkie zadania, które są wykonywane w węźle dostęp odczyt/zapis do tego katalogu. Zadania wykonywane w innych węzłach ma zdalny dostęp do tego katalogu (nie jest katalogiem "udostępniona" w sieci). | Wszystkie zadania. | C:\user\tasks\shared |
| AZ_BATCH_NODE_STARTUP_DIR       | Pełna ścieżka [start katalogu zadań] [ files_dirs] w węźle. | Wszystkie zadania. | C:\user\tasks\startup |
| AZ_BATCH_POOL_ID                | Identyfikator puli, w której jest uruchamiane zadanie podrzędne. | Wszystkie zadania. | batchpool001 |
| AZ_BATCH_TASK_DIR               | Pełna ścieżka [katalogu zadań] [ files_dirs] w węźle. Ten katalog zawiera `stdout.txt` i `stderr.txt` zadania oraz AZ_BATCH_TASK_WORKING_DIR. | Wszystkie zadania. | C:\user\tasks\workitems\batchjob001\job-1\task001 |
| AZ_BATCH_TASK_ID                | Identyfikator bieżącego zadania. | Wszystkie zadania, z wyjątkiem zadanie podrzędne uruchamiania. | task001 |
| AZ_BATCH_TASK_WORKING_DIR       | Pełna ścieżka [katalogu roboczego zadań] [ files_dirs] w węźle. Aktualnie uruchomione zadanie dostępem odczytu/zapisu do tego katalogu. | Wszystkie zadania. | C:\user\tasks\workitems\batchjob001\job-1\task001\wd |
| CCP_NODES                       | Lista węzłów i liczbę rdzeni na węzeł, który jest przydzielony do [zadanie podrzędne obejmujące wiele wystąpień][multi_instance]. Węzłów i rdzeni, które są wymienione w formacie `numNodes<space>node1IP<space>node1Cores<space>`<br/>`node2IP<space>node2Cores<space> ...`, gdzie liczba węzłów następuje co najmniej jeden adres IP węzła i liczby rdzeni dla każdego. |  Podstawowym obejmujące wiele wystąpień i podzadań. |`2 10.0.0.4 1 10.0.0.5 1` |
| AZ_BATCH_NODE_LIST              | Lista węzłów, które są przydzielane [zadanie podrzędne obejmujące wiele wystąpień] [ multi_instance] w formacie `nodeIP;nodeIP`. | Podstawowym obejmujące wiele wystąpień i podzadań. | `10.0.0.4;10.0.0.5` |
| AZ_BATCH_HOST_LIST              | Lista węzłów, które są przydzielane [zadanie podrzędne obejmujące wiele wystąpień] [ multi_instance] w formacie `nodeIP,nodeIP`. | Podstawowym obejmujące wiele wystąpień i podzadań. | `10.0.0.4,10.0.0.5` |
| AZ_BATCH_MASTER_NODE            | Adres IP i port węzła obliczeniowego, w której głównym zadaniem [zadanie podrzędne obejmujące wiele wystąpień] [ multi_instance] działa. | Podstawowym obejmujące wiele wystąpień i podzadań. | `10.0.0.4:6000`|
| AZ_BATCH_TASK_SHARED_DIR | Ścieżka katalogu, która jest taka sama dla podstawowego zadania i podzadania, każdy z [zadanie podrzędne obejmujące wiele wystąpień][multi_instance]. Ścieżka istnieje w każdym węźle, na którym zadanie działa wiele wystąpień, a jest dostępna dla polecenia zadania uruchomione w tym węźle odczytu/zapisu (zarówno [polecenia koordynacji] [ coord_cmd] i [ polecenie aplikacji][app_cmd]). Podzadania lub podstawowe zadania, które wykonywania na innych węzłach ma zdalny dostęp do tego katalogu (nie jest katalogiem "udostępniona" w sieci). | Podstawowym obejmujące wiele wystąpień i podzadań. | C:\user\tasks\workitems\multiinstancesamplejob\job-1\multiinstancesampletask |
| AZ_BATCH_IS_CURRENT_NODE_MASTER | Określa, czy bieżący węzeł jest węzłem głównym dla [zadanie podrzędne obejmujące wiele wystąpień][multi_instance]. Możliwe wartości to `true` i `false`.| Podstawowym obejmujące wiele wystąpień i podzadań. | `true` |
| AZ_BATCH_NODE_IS_DEDICATED | Jeśli `true`, bieżącego węzła jest węzłów dedykowanych. Jeśli `false`, jest [węzłów o niskim priorytecie](batch-low-pri-vms.md). | Wszystkie zadania. | `true` |

[files_dirs]: https://azure.microsoft.com/documentation/articles/batch-api-basics/#files-and-directories
[multi_instance]: https://azure.microsoft.com/documentation/articles/batch-mpi/
[coord_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#coordination-command
[app_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#application-command
