---
title: Odbieranie zdarzeń za pomocą języka Python — Azure Event Hubs | Dokumentacja firmy Microsoft
description: Ten artykuł zawiera wskazówki dotyczące tworzenia aplikacji w języku Python, który odbiera zdarzenia z usługi Azure Event Hubs.
services: event-hubs
author: ShubhaVijayasarathy
manager: femila
ms.service: event-hubs
ms.workload: core
ms.topic: article
ms.date: 11/26/2018
ms.author: shvija
ms.openlocfilehash: bc1cf07c5a74bc4d7182eea5281e75525fd04247
ms.sourcegitcommit: 9fb6f44dbdaf9002ac4f411781bf1bd25c191e26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2018
ms.locfileid: "53103188"
---
# <a name="receive-events-from-event-hubs-using-python"></a>Odbieranie zdarzeń z usługi Event Hubs przy użyciu języka Python

Azure Event Hubs to system zarządzania zdarzeń o wysokim stopniu skalowalności, który może obsługiwać miliony zdarzeń na sekundę, dzięki czemu aplikacje mogą przetwarzać oraz analizować duże ilości danych wytworzonych przez podłączone urządzenia i innymi systemami. Po zebraniu danych do Centrum zdarzeń, może odbierać i obsługa zdarzeń z użyciem w trakcie obsługi lub funkcji przekazywania z innymi systemami analizy.

Aby dowiedzieć się więcej na temat usługi Event Hubs, zobacz [Przegląd usługi Event Hubs][Event Hubs overview].

W tym samouczku opisano, jak odbierać zdarzenia z Centrum zdarzeń z aplikacji napisanych w języku Python. Aby wysyłać zdarzenia, zobacz [do odpowiedniego artykułu wysyłania](event-hubs-python-get-started-send.md).

Kod w tym samouczku pochodzi z [tych przykładów usługi GitHub](https://github.com/Azure/azure-event-hubs-python/tree/master/examples), który można sprawdzić, aby wyświetlić pełną działającą aplikację, w tym instrukcje importowania i deklaracje zmiennych. Inne przykłady są dostępne w tym samym folderze w usłudze GitHub.

## <a name="prerequisites"></a>Wymagania wstępne

Do wykonania kroków tego samouczka niezbędne jest spełnienie następujących wymagań wstępnych:

- Subskrypcja platformy Azure. Jeśli nie masz subskrypcji, przed rozpoczęciem [utwórz bezpłatne konto](https://azure.microsoft.com/free/).
- Python 3.4 lub nowsze.
- Istniejące usługi Event Hubs przestrzeni nazw i Centrum zdarzeń. Te jednostki można utworzyć, postępując zgodnie z instrukcjami wyświetlanymi w [w tym artykule](event-hubs-create.md). 

## <a name="install-python-package"></a>Zainstaluj pakiet języka Python

Aby zainstalować pakiet języka Python dla usługi Event Hubs, Otwórz okno wiersza polecenia, którego języka Python w ścieżce, a następnie uruchom następujące polecenie: 

```bash
pip install azure-eventhub
```

## <a name="create-a-python-script-to-receive-events"></a>Utwórz skrypt w języku Python do odbierania zdarzeń

Następnie utwórz aplikację w języku Python, który odbiera zdarzenia z Centrum zdarzeń:

1. Otwórz ulubionym edytorze języka Python, takich jak [programu Visual Studio Code][Visual Studio Code].
2. Tworzenie skryptu o nazwie **recv.py**.
3. Wklej następujący kod do recv.py, zastępując wartości klucza, użytkownika i adres wartościami uzyskanymi z witryny Azure portal w poprzedniej sekcji: 

```python
import os
import sys
import logging
import time
from azure.eventhub import EventHubClient, Receiver, Offset

logger = logging.getLogger("azure")

# Address can be in either of these formats:
# "amqps://<URL-encoded-SAS-policy>:<URL-encoded-SAS-key>@<mynamespace>.servicebus.windows.net/myeventhub"
# "amqps://<mynamespace>.servicebus.windows.net/myeventhub"
# For example:
ADDRESS = "amqps://mynamespace.servicebus.windows.net/myeventhub"

# SAS policy and key are not required if they are encoded in the URL
USER = "RootManageSharedAccessKey"
KEY = "namespaceSASKey"
CONSUMER_GROUP = "$default"
OFFSET = Offset("-1")
PARTITION = "0"

total = 0
last_sn = -1
last_offset = "-1"
client = EventHubClient(ADDRESS, debug=False, username=USER, password=KEY)
try:
    receiver = client.add_receiver(CONSUMER_GROUP, PARTITION, prefetch=5000, offset=OFFSET)
    client.run()
    start_time = time.time()
    for event_data in receiver.receive(timeout=100):
        last_offset = event_data.offset
        last_sn = event_data.sequence_number
        print("Received: {}, {}".format(last_offset, last_sn))
        total += 1

    end_time = time.time()
    client.stop()
    run_time = end_time - start_time
    print("Received {} messages in {} seconds".format(total, run_time))

except KeyboardInterrupt:
    pass
finally:
    client.stop()
```

## <a name="receive-events"></a>Odbieranie zdarzeń

Aby uruchomić skrypt, Otwórz okno wiersza polecenia, którego języka Python w ścieżce, a następnie uruchom następujące polecenie:

```bash
start python recv.py
```
 
## <a name="next-steps"></a>Kolejne kroki
W tym przewodniku Szybki Start utworzono aplikację w języku Python, które odebrano komunikaty z Centrum zdarzeń. Aby dowiedzieć się, jak do wysyłania zdarzeń do Centrum zdarzeń za pomocą języka Python, zobacz [wysyłać zdarzenia z Centrum zdarzeń — Python](event-hubs-python-get-started-send.md).

<!-- Links -->
[Event Hubs overview]: event-hubs-about.md
[Visual Studio Code]: https://code.visualstudio.com/
[free account]: https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio
