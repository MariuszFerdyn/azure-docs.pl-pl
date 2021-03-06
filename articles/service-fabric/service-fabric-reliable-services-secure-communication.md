---
title: Bezpieczna komunikacja komunikacji zdalnej usługi w języku C# w sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft
description: Informacje o sposobie zabezpieczania komunikacji między usługami zdalnymi, na podstawie usługi C# niezawodnych usług uruchomionych w klastrze usługi sieć szkieletowa usług Azure.
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: vturecek
ms.assetid: fc129c1a-fbe4-4339-83ae-0e69a41654e0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: be5dab7b9714f13a4bd30e6ab33a5a0e2016212d
ms.sourcegitcommit: 0fa8b4622322b3d3003e760f364992f7f7e5d6a9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/27/2018
ms.locfileid: "37020023"
---
# <a name="secure-service-remoting-communications-in-a-c-service"></a>Bezpieczna komunikacja komunikacji zdalnej usługi w usłudze C#
> [!div class="op_single_selector"]
> * [C# w systemie Windows](service-fabric-reliable-services-secure-communication.md)
> * [Java w systemie Linux](service-fabric-reliable-services-secure-communication-java.md)
>
>

Zabezpieczeń jest jednym z najważniejszych aspektów komunikacji. Struktura aplikacji niezawodne usługi zapewnia kilka stosy wbudowane komunikacji i narzędzi, których można użyć w celu poprawy bezpieczeństwa. W tym artykule omówiono sposób poprawiania zabezpieczeń podczas korzystania z usługi komunikacji zdalnej w usłudze C#. Opiera się na istniejącą [przykład](service-fabric-reliable-services-communication-remoting.md) który wyjaśnia, jak skonfigurować komunikację zdalną dla niezawodne usługi napisane w języku C#. 

Aby ułatwić zabezpieczanie usługi podczas korzystania z komunikacji zdalnej usługi z usługami C#, wykonaj następujące kroki:

1. Tworzenie interfejsu `IHelloWorldStateful`, który definiuje metody, które będą dostępne dla zdalnego wywołania procedury w usłudze. Usługa będzie używać `FabricTransportServiceRemotingListener`, która jest zadeklarowana w `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` przestrzeni nazw. Jest to `ICommunicationListener` implementację, która zapewnia możliwości komunikacji zdalnej.

    ```csharp
    public interface IHelloWorldStateful : IService
    {
        Task<string> GetHelloWorld();
    }

    internal class HelloWorldStateful : StatefulService, IHelloWorldStateful
    {
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]{
                    new ServiceReplicaListener(
                        (context) => new FabricTransportServiceRemotingListener(context,this))};
        }

        public Task<string> GetHelloWorld()
        {
            return Task.FromResult("Hello World!");
        }
    }
    ```
2. Dodaj ustawienia odbiornika i poświadczeń zabezpieczeń.

    Upewnij się, że certyfikat, który ma być używany do zabezpieczania komunikacji usługi jest zainstalowany na wszystkich węzłach w klastrze. 
    
    > [!NOTE]
    > W węzłach Linux, certyfikat musi być obecny jako pliki w formacie PEM w */var/lib/sfcerts* katalogu. Aby dowiedzieć się więcej, zobacz [lokalizacji i format certyfikatów X.509 w węzłach Linux](./service-fabric-configure-certificates-linux.md#location-and-format-of-x509-certificates-on-linux-nodes). 

    Istnieją dwa sposoby, które można udostępniać ustawienia odbiornika i poświadczenia zabezpieczeń:

   1. Podaj je bezpośrednio w kodzie usługi:

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           FabricTransportRemotingListenerSettings  listenerSettings = new FabricTransportRemotingListenerSettings
           {
               MaxMessageSize = 10000000,
               SecurityCredentials = GetSecurityCredentials()
           };
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(context,this,listenerSettings))
           };
       }

       private static SecurityCredentials GetSecurityCredentials()
       {
           // Provide certificate details.
           var x509Credentials = new X509Credentials
           {
               FindType = X509FindType.FindByThumbprint,
               FindValue = "4FEF3950642138446CC364A396E1E881DB76B48C",
               StoreLocation = StoreLocation.LocalMachine,
               StoreName = "My",
               ProtectionLevel = ProtectionLevel.EncryptAndSign
           };
           x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
           x509Credentials.RemoteCertThumbprints.Add("9FEF3950642138446CC364A396E1E881DB76B483");
           return x509Credentials;
       }
       ```
   2. Podaj je za pomocą [pakietu konfiguracji](service-fabric-application-and-service-manifests.md):

       Dodaj nazwane `TransportSettings` sekcji w pliku settings.xml.

       ```xml
       <Section Name="HelloWorldStatefulTransportSettings">
           <Parameter Name="MaxMessageSize" Value="10000000" />
           <Parameter Name="SecurityCredentialsType" Value="X509" />
           <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
           <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
           <Parameter Name="CertificateRemoteThumbprints" Value="9FEF3950642138446CC364A396E1E881DB76B483" />
           <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
           <Parameter Name="CertificateStoreName" Value="My" />
           <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
           <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
       </Section>
       ```

       W takim przypadku `CreateServiceReplicaListeners` metoda będzie wyglądać następująco:

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(
                       context,this,FabricTransportRemotingListenerSettings .LoadFrom("HelloWorldStatefulTransportSettings")))
           };
       }
       ```

        Jeśli dodasz `TransportSettings` sekcji w pliku settings.xml `FabricTransportRemotingListenerSettings ` załaduje wszystkie ustawienia w tej sekcji ma domyślnie.

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        W takim przypadku `CreateServiceReplicaListeners` metoda będzie wyglądać następująco:

        ```csharp
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]
            {
                return new[]{
                        new ServiceReplicaListener(
                            (context) => new FabricTransportServiceRemotingListener(context,this))};
            };
        }
        ```
3. Gdy wywoływać metod w usług zabezpieczonych przy użyciu stosu usług zdalnych, zamiast `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` klasę, aby utworzyć serwer proxy usługi, użyj `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`. Przekazywanie `FabricTransportRemotingSettings`, który zawiera `SecurityCredentials`.

    ```csharp

    var x509Credentials = new X509Credentials
    {
        FindType = X509FindType.FindByThumbprint,
        FindValue = "9FEF3950642138446CC364A396E1E881DB76B483",
        StoreLocation = StoreLocation.LocalMachine,
        StoreName = "My",
        ProtectionLevel = ProtectionLevel.EncryptAndSign
    };
    x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
    x509Credentials.RemoteCertThumbprints.Add("4FEF3950642138446CC364A396E1E881DB76B48C");

    FabricTransportRemotingSettings transportSettings = new FabricTransportRemotingSettings
    {
        SecurityCredentials = x509Credentials,
    };

    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(transportSettings));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    Jeśli kod klienta działa w ramach usługi, można załadować `FabricTransportRemotingSettings` z pliku settings.xml. Utwórz sekcję HelloWorldClientTransportSettings, która jest podobna do kodu usługi, jak pokazano wcześniej. Wprowadź następujące zmiany w kodzie klienta:

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    Jeśli klient nie jest uruchomiony jako część usługi, można utworzyć plik client_name.settings.xml w tej samej lokalizacji, gdzie jest client_name.exe. Następnie można utworzyć sekcji TransportSettings w tym pliku.

    Podobnie jak usługa, jeśli dodasz `TransportSettings` części settings.xml/client_name.settings.xml klienta `FabricTransportRemotingSettings` ładuje wszystkie ustawienia w tej sekcji ma domyślnie.

    W takim przypadku jeszcze bardziej jest uproszczone wcześniejszych kodu:  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```


Jako kolejny krok, przeczytaj [interfejsu API sieci Web z oprogramowaniem OWIN w usługach niezawodnej](service-fabric-reliable-services-communication-webapi.md).
