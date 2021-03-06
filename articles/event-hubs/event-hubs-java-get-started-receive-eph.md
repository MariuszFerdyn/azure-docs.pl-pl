---
title: Odbieranie zdarzeń za pomocą języka Java — Azure Event Hubs | Dokumentacja firmy Microsoft
description: Ten artykuł zawiera wskazówki dotyczące tworzenia aplikacji w języku Java, która odbiera zdarzenia z usługi Azure Event Hubs.
services: event-hubs
author: ShubhaVijayasarathy
manager: timlt
ms.service: event-hubs
ms.workload: core
ms.topic: article
ms.custom: seodec18
ms.date: 12/06/2018
ms.author: shvija
ms.openlocfilehash: 0fc9b8b6a8bcd62aafda7c04697ab8b9c096b17e
ms.sourcegitcommit: a7331d0cc53805a7d3170c4368862cad0d4f3144
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/30/2019
ms.locfileid: "55296583"
---
# <a name="receive-events-from-azure-event-hubs-using-java"></a>Odbieranie zdarzeń z usługi Azure Event Hubs przy użyciu języka Java

Event Hubs to wysoce skalowalny system przyjmowania danych może obsługiwać miliony zdarzeń na sekundę, umożliwiając aplikacji przetwarzanie i analizowanie olbrzymich ilości danych wytworzonych przez podłączone urządzenia i aplikacje. Po zebraniu danych do usługi Event Hubs można przekształcać dane za pomocą dowolnego dostawcy analiz w czasie rzeczywistym lub przechowywać je przy użyciu klastra magazynu.

Aby uzyskać więcej informacji, zobacz [Przegląd usługi Event Hubs][Event Hubs overview].

W tym samouczku pokazano, jak odbierać zdarzenia do Centrum zdarzeń za pomocą aplikacji konsolowej napisanej w języku Java.

## <a name="prerequisites"></a>Wymagania wstępne

W celu ukończenia tego samouczka potrzebne są następujące wymagania wstępne:

* Środowisko projektowe Java. W tym samouczku przyjęto założenie, że [Eclipse](https://www.eclipse.org/).
* Aktywne konto platformy Azure. Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto][].

Kod w ramach tego samouczka jest oparta na [EventProcessorSample kod w serwisie GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/Java/Basic/EventProcessorSample), który można sprawdzić, aby wyświetlić pełną działającą aplikację.

## <a name="receive-messages-with-eventprocessorhost-in-java"></a>Odbieranie komunikatów EventProcessorHost w języku Java

**EventProcessorHost** jest klasą języka Java, która upraszcza odbieranie zdarzeń z usługi Event Hubs przez zarządzanie trwałymi punktami kontrolnymi i równoległymi odbiorami z tych centrów zdarzeń. Za pomocą klasy EventProcessorHost, można podzielić zdarzenia między wieloma odbiornikami, nawet w przypadku hostowania w różnych węzłach. W tym przykładzie przedstawiono, jak używać klasy EventProcessorHost dla jednego odbiornika.

### <a name="create-a-storage-account"></a>Tworzenie konta magazynu

Aby używać klasy EventProcessorHost, musisz mieć [konta usługi Azure Storage][Azure Storage account]:

1. Zaloguj się do [witryny Azure portal][Azure portal]i kliknij przycisk **+ Utwórz zasób** po lewej stronie ekranu.
2. Kliknij pozycję **Magazyn**, a następnie pozycję **Konto magazynu**. W **Tworzenie konta magazynu** okna i wpisz nazwę konta magazynu. Wykonaj pozostałe pola, wybierz odpowiedni region, a następnie kliknij **Utwórz**.
   
    ![Tworzenie konta magazynu](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. Kliknij nowo utworzone konto magazynu, a następnie kliknij przycisk **klucze dostępu**:
   
    ![Uzyskiwanie dostępu do kluczy](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    Skopiuj wartość klucz 1 do lokalizacji tymczasowej. Będziesz jej używać w dalszej części tego samouczka.

### <a name="create-a-java-project-using-the-eventprocessor-host"></a>Tworzenie projektu języka Java za pomocą hosta EventProcessor

Biblioteki klienta Java dla usługi Event Hubs jest dostępna do użytku w projektach narzędzia Maven z [Maven Central Repository][Maven Package]i można się odwoływać przy użyciu poniższej deklaracji zależności wewnątrz usługi Maven plik projektu: 

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>2.2.0</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs-eph</artifactId>
    <version>2.4.0</version>
</dependency>
```

Dla różnych typów środowisk kompilacji można jawnie uzyskać najnowsze plików JAR, korzystając z [Maven Central Repository][Maven Package].  

1. Na potrzeby poniższego przykładu należy w ulubionym środowisku programowania Java utworzyć nowy projekt Maven dla aplikacji konsoli lub powłoki. Nosi nazwę klasy `ErrorNotificationHandler`.     
   
    ```java
    import java.util.function.Consumer;
    import com.microsoft.azure.eventprocessorhost.ExceptionReceivedEventArgs;
   
    public class ErrorNotificationHandler implements Consumer<ExceptionReceivedEventArgs>
    {
        @Override
        public void accept(ExceptionReceivedEventArgs t)
        {
            System.out.println("SAMPLE: Host " + t.getHostname() + " received general error notification during " + t.getAction() + ": " + t.getException().toString());
        }
    }
    ```
2. Użyj następującego kodu, aby utworzyć nową klasę o nazwie `EventProcessorSample`. Zastąp symbole zastępcze wartości użyte do utworzenia event hub i konto magazynu:
   
   ```java
   package com.microsoft.azure.eventhubs.samples.eventprocessorsample;

   import com.microsoft.azure.eventhubs.ConnectionStringBuilder;
   import com.microsoft.azure.eventhubs.EventData;
   import com.microsoft.azure.eventprocessorhost.CloseReason;
   import com.microsoft.azure.eventprocessorhost.EventProcessorHost;
   import com.microsoft.azure.eventprocessorhost.EventProcessorOptions;
   import com.microsoft.azure.eventprocessorhost.ExceptionReceivedEventArgs;
   import com.microsoft.azure.eventprocessorhost.IEventProcessor;
   import com.microsoft.azure.eventprocessorhost.PartitionContext;

   import java.util.concurrent.ExecutionException;
   import java.util.function.Consumer;

   public class EventProcessorSample
   {
       public static void main(String args[]) throws InterruptedException, ExecutionException
       {
           String consumerGroupName = "$Default";
           String namespaceName = "----NamespaceName----";
           String eventHubName = "----EventHubName----";
           String sasKeyName = "----SharedAccessSignatureKeyName----";
           String sasKey = "----SharedAccessSignatureKey----";
           String storageConnectionString = "----AzureStorageConnectionString----";
           String storageContainerName = "----StorageContainerName----";
           String hostNamePrefix = "----HostNamePrefix----";
        
           ConnectionStringBuilder eventHubConnectionString = new ConnectionStringBuilder()
                .setNamespaceName(namespaceName)
                .setEventHubName(eventHubName)
                .setSasKeyName(sasKeyName)
                .setSasKey(sasKey);
        
           EventProcessorHost host = new EventProcessorHost(
                EventProcessorHost.createHostName(hostNamePrefix),
                eventHubName,
                consumerGroupName,
                eventHubConnectionString.toString(),
                storageConnectionString,
                storageContainerName);
        
           System.out.println("Registering host named " + host.getHostName());
           EventProcessorOptions options = new EventProcessorOptions();
           options.setExceptionNotification(new ErrorNotificationHandler());

           host.registerEventProcessor(EventProcessor.class, options)
           .whenComplete((unused, e) ->
           {
               if (e != null)
               {
                   System.out.println("Failure while registering: " + e.toString());
                   if (e.getCause() != null)
                   {
                       System.out.println("Inner exception: " + e.getCause().toString());
                   }
               }
           })
           .thenAccept((unused) ->
           {
               System.out.println("Press enter to stop.");
               try 
               {
                   System.in.read();
               }
               catch (Exception e)
               {
                   System.out.println("Keyboard read failed: " + e.toString());
               }
           })
           .thenCompose((unused) ->
           {
               return host.unregisterEventProcessor();
           })
           .exceptionally((e) ->
           {
               System.out.println("Failure while unregistering: " + e.toString());
               if (e.getCause() != null)
               {
                   System.out.println("Inner exception: " + e.getCause().toString());
               }
               return null;
           })
           .get(); // Wait for everything to finish before exiting main!
        
           System.out.println("End of sample");
       }
    ```
3. Utwórz jeden więcej klasę o nazwie `EventProcessor`, używając następującego kodu:
   
    ```java
    public static class EventProcessor implements IEventProcessor
    {
        private int checkpointBatchingCount = 0;

        // OnOpen is called when a new event processor instance is created by the host. 
        @Override
        public void onOpen(PartitionContext context) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is opening");
        }

        // OnClose is called when an event processor instance is being shut down. 
        @Override
        public void onClose(PartitionContext context, CloseReason reason) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is closing for reason " + reason.toString());
        }
        
        // onError is called when an error occurs in EventProcessorHost code that is tied to this partition, such as a receiver failure.
        @Override
        public void onError(PartitionContext context, Throwable error)
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " onError: " + error.toString());
        }

        // onEvents is called when events are received on this partition of the Event Hub. 
        @Override
        public void onEvents(PartitionContext context, Iterable<EventData> events) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " got event batch");
            int eventCount = 0;
            for (EventData data : events)
            {
                try
                {
                    System.out.println("SAMPLE (" + context.getPartitionId() + "," + data.getSystemProperties().getOffset() + "," +
                            data.getSystemProperties().getSequenceNumber() + "): " + new String(data.getBytes(), "UTF8"));
                    eventCount++;
                    
                    // Checkpointing persists the current position in the event stream for this partition and means that the next
                    // time any host opens an event processor on this event hub+consumer group+partition combination, it will start
                    // receiving at the event after this one. 
                    this.checkpointBatchingCount++;
                    if ((checkpointBatchingCount % 5) == 0)
                    {
                        System.out.println("SAMPLE: Partition " + context.getPartitionId() + " checkpointing at " +
                            data.getSystemProperties().getOffset() + "," + data.getSystemProperties().getSequenceNumber());
                        // Checkpoints are created asynchronously. It is important to wait for the result of checkpointing
                        // before exiting onEvents or before creating the next checkpoint, to detect errors and to ensure proper ordering.
                        context.checkpoint(data).get();
                    }
                }
                catch (Exception e)
                {
                    System.out.println("Processing failed for an event: " + e.toString());
                }
            }
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " batch size was " + eventCount + " for host " + context.getOwner());
        }
    }
    ```

Instrukcje w tym samouczku obejmują użycie pojedynczego wystąpienia hosta EventProcessorHost. Aby zwiększyć przepływność, zaleca się uruchomienie wielu wystąpień klasy EventProcessorHost, najlepiej na oddzielnych komputerach.  Zapewnia także nadmiarowości. W tych przypadkach różne wystąpienia automatycznie koordynują się ze sobą w celu równoważenia obciążenia odebranych zdarzeń. Jeśli chcesz, aby wiele odbiorników przetwarzało *wszystkie* zdarzenia, musisz użyć koncepcji **ConsumerGroup**. W przypadku odbierania zdarzeń z różnych komputerów dobrym rozwiązaniem może być określenie nazw wystąpień hosta EventProcessorHost w oparciu o komputery (lub role), w których są one wdrażane.

## <a name="publishing-messages-to-eventhub"></a>Publikowanie komunikatów do Centrum zdarzeń

Przed pobraniem wiadomości przez konsumentów, mają do opublikowania partycji najpierw przez wydawców. Warto zauważyć, że po opublikowaniu wiadomości do Centrum zdarzeń, które synchronicznie przy użyciu metody sendSync() obiektu com.microsoft.azure.eventhubs.EventHubClient, wiadomości mogą zostać wysłane do określonej partycji lub dystrybuowane do wszystkich dostępnych partycji w sposób okrężny w zależności od tego, czy określono klucza partycji, czy nie.

Gdy określona jest ciąg reprezentujący klucz partycji, klucz jest przekazywane do określenia partycji do wysłania zdarzenia do.

Jeśli nie ustawiono klucza partycji, następnie wiadomości są round robined do wszystkich dostępnych partycji

```java
// Serialize the event into bytes
byte[] payloadBytes = gson.toJson(messagePayload).getBytes(Charset.defaultCharset());

// Use the bytes to construct an {@link EventData} object
EventData sendEvent = EventData.create(payloadBytes);

// Transmits the event to event hub without a partition key
// If a partition key is not set, then we will round-robin to all topic partitions
eventHubClient.sendSync(sendEvent);

//  the partitionKey will be hash'ed to determine the partitionId to send the eventData to.
eventHubClient.sendSync(sendEvent, partitionKey);

```

## <a name="implementing-a-custom-checkpointmanager-for-eventprocessorhost-eph"></a>Implementowanie niestandardowego CheckpointManager EventProcessorHost (EPH)

Interfejs API udostępnia mechanizm do implementowania Menedżera niestandardowego punktu kontrolnego dla scenariuszy, w którym nie jest zgodny z danego przypadku użycia w implementacji domyślnej.

Menedżer punktów kontrolnych domyślne korzysta z magazynu obiektów blob, ale Jeśli zastąpisz Menedżer punktów kontrolnych, używane przez EPH z Twojej własnej implementacji, możesz użyć dowolnego magazynu, które chcesz wykonać kopię implementacji Menedżera punktu kontrolnego.

Utwórz klasę, która implementuje com.microsoft.azure.eventprocessorhost.ICheckpointManager interfejsu

Użyj niestandardowych implementacji Menedżer punktów kontrolnych (com.microsoft.azure.eventprocessorhost.ICheckpointManager)

W ramach wdrożenia można zastąpić domyślny mechanizm tworzenia punktów kontrolnych i zaimplementować własną punkty kontrolne, w oparciu o własny magazyn danych (SQL Server, bazy danych cosmos DB, pamięci podręcznej Azure redis Cache itd.). Zaleca się, że magazyn używany do wykonania kopii implementacji Menedżera punktu kontrolnego jest dostępny dla wszystkich wystąpień EPH skuteczność przetwarzania zdarzeń dla grupy odbiorców.

Możesz użyć dowolnego magazynu danych, która jest dostępna w danym środowisku.

Klasa com.microsoft.azure.eventprocessorhost.EventProcessorHost zapewnia dwa konstruktory, które pozwalają na zastąpienie Menedżera punktu kontrolnego dla swojej klasy EventProcessorHost.

## <a name="next-steps"></a>Kolejne kroki
W tym przewodniku Szybki Start utworzono aplikację Java, która Odebrano komunikaty z Centrum zdarzeń. Aby dowiedzieć się, jak do wysyłania zdarzeń do Centrum zdarzeń za pomocą języka Java, zobacz [wysyłać zdarzenia z Centrum zdarzeń — Java](event-hubs-java-get-started-send.md).

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
[bezpłatne konto]: https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio
