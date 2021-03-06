---
title: Uwierzytelnianie za pomocą usługi Azure Active Directory do dostępu do danych obiektów blob i kolejek, z poziomu aplikacji (wersja zapoznawcza) | Dokumentacja firmy Microsoft
description: Usługa Azure Active Directory do uwierzytelniania z poziomu aplikacji, a następnie Autoryzuj żądania do obiektów blob i kolejek (wersja zapoznawcza).
services: storage
author: tamram
ms.service: storage
ms.topic: article
ms.date: 11/21/2018
ms.author: tamram
ms.subservice: common
ms.openlocfilehash: 4c39f47169071ceb9430f419a144e11f425d65b0
ms.sourcegitcommit: 898b2936e3d6d3a8366cfcccc0fccfdb0fc781b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/30/2019
ms.locfileid: "55240730"
---
# <a name="authenticate-with-azure-active-directory-from-an-application-for-access-to-blobs-and-queues-preview"></a>Uwierzytelnianie za pomocą usługi Azure Active Directory z aplikacji do dostępu do obiektów blob i kolejek (wersja zapoznawcza)

Kluczową zaletą usługi Azure Storage przy użyciu usługi Azure Active Directory (Azure AD) to, czy poświadczenia nie są już potrzebne, mają być przechowywane w kodzie. Zamiast tego możesz zażądać token dostępu OAuth 2.0 z usługi Azure AD. Usługa Azure AD obsługuje uwierzytelnianie podmiotu zabezpieczeń (użytkownika, grupy lub jednostki usługi) uruchomiona jest aplikacja. Jeśli uwierzytelnianie zakończy się powodzeniem, usługa Azure AD zwraca token dostępu do aplikacji i aplikacji można następnie użyć tokenu dostępu do autoryzacji żądania do usługi Azure Storage.

W tym artykule przedstawiono sposób konfigurowania aplikacji na potrzeby uwierzytelniania przy użyciu usługi Azure AD. Podobne metody, z których można użyć .NET funkcji przykładowy kod, ale w innych językach.

Zanim podmiot zabezpieczeń można uwierzytelnić aplikację usługi Azure Storage, należy skonfigurować ustawienia kontroli dostępu opartej na rolach dla tego podmiotu zabezpieczeń. Usługa Azure Storage określa role RBAC, które obejmują uprawnienia do kontenerów i kolejek. Gdy rola RBAC jest przypisywana do podmiotu zabezpieczeń, tego podmiotu zabezpieczeń ma uprawnienia do tego zasobu. Aby uzyskać więcej informacji, zobacz [Zarządzaj praw dostępu do magazynu danych przy użyciu RBAC (wersja zapoznawcza)](storage-auth-aad-rbac.md).

Aby uzyskać omówienie przepływie przyznawania kodu OAuth 2.0, zobacz [Autoryzuj dostęp do aplikacji sieci web usługi Azure Active Directory przy użyciu kodu uwierzytelniania OAuth 2.0 udzielić przepływ](../../active-directory/develop/v1-protocols-oauth-code.md).

[!INCLUDE [storage-auth-aad-note-include](../../../includes/storage-auth-aad-note-include.md)]

## <a name="assign-an-rbac-role-to-an-azure-ad-security-principal"></a>Przypisz rolę RBAC do podmiotu zabezpieczeń usługi Azure AD

Na potrzeby uwierzytelniania podmiotu zabezpieczeń z poziomu aplikacji usługi Azure Storage, należy najpierw skonfigurować ustawienia kontroli (RBAC) dostępu opartej na rolach dla tego podmiotu zabezpieczeń. Usługa Azure Storage określa role RBAC, które obejmują uprawnienia do kontenerów i kolejek. Gdy rola RBAC jest przypisywana do podmiotu zabezpieczeń, tego podmiotu zabezpieczeń ma uprawnienia do tego zasobu. Aby uzyskać więcej informacji, zobacz [Zarządzaj praw dostępu do danych obiektów Blob platformy Azure i kolejek przy użyciu RBAC (wersja zapoznawcza)](storage-auth-aad-rbac.md).

## <a name="register-your-application-with-an-azure-ad-tenant"></a>Zarejestruj swoją aplikację z dzierżawy usługi Azure AD

Pierwszym krokiem przy użyciu usługi Azure AD do autoryzowania dostępu do zasobów magazynu jest zarejestrowanie aplikacji klienckiej w dzierżawę usługi Azure AD. Rejestrowanie aplikacji umożliwia wywoływanie Azure [Active Directory Authentication Library](../../active-directory/active-directory-authentication-libraries.md) (ADAL) w kodzie. Biblioteki ADAL zapewnia interfejs API do uwierzytelniania za pomocą usługi Azure AD z poziomu aplikacji. Rejestrowanie aplikacji również pozwala na autoryzowanie wywołania z tej aplikacji do interfejsów API usługi Azure Storage przy użyciu tokenu dostępu.

Możesz zarejestrować swoją aplikację, należy podać informacje o aplikacji do usługi Azure AD. Następnie usługa Azure AD zawiera identyfikator klienta (nazywanych również *identyfikator aplikacji*) umożliwia kojarzenie aplikacji z usługą Azure AD w czasie wykonywania. Aby dowiedzieć się więcej o identyfikatorze klienta, zobacz [aplikacji i obiektów nazw głównych usług w usłudze Azure Active Directory](../../active-directory/develop/app-objects-and-service-principals.md).

Aby zarejestrować swoją aplikację usługi Azure Storage, wykonaj kroki opisane w [dodawania aplikacji](../../active-directory/develop/quickstart-v1-add-azure-ad-app.md) sekcji [Integrowanie aplikacji z usługą Azure Active Directory](../../active-directory/active-directory-integrating-applications.md). Jeśli zarejestrujesz aplikację jako natywną aplikację, można określić dowolny prawidłowy identyfikator URI dla **identyfikator URI przekierowania**. Wartość nie musi odpowiadać rzeczywistemu punktowi końcowemu.

![Zrzut ekranu przedstawiający, jak zarejestrować aplikację magazynu z usługą Azure AD](./media/storage-auth-aad-app/app-registration.png)

Po zarejestrowaniu aplikacji zobaczysz identyfikator aplikacji (lub identyfikator klienta) w obszarze **ustawienia**:

![Zrzut ekranu: identyfikator klienta](./media/storage-auth-aad-app/app-registration-client-id.png)

Aby uzyskać więcej informacji na temat rejestrowania aplikacji w usłudze Azure AD, zobacz [Integrowanie aplikacji z usługą Azure Active Directory](../../active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad.md). 

## <a name="grant-your-registered-app-permissions-to-azure-storage"></a>Udzielanie uprawnień zarejestrowana aplikacja do usługi Azure Storage

Następnie należy udzielić aplikacji uprawnień do wywoływania interfejsów API usługi Azure Storage. Ten krok powoduje włączenie aplikacji do autoryzowania wywołań do usługi Azure Storage z usługą Azure AD.

1. W okienku nawigacji po lewej stronie w witrynie Azure portal wybierz **wszystkich usług**i wyszukaj **rejestracje aplikacji**.
2. Wyszukaj nazwę zarejestrowanej aplikacji, utworzonej w poprzednim kroku.
3. Wybierz aplikację zarejestrowane, a następnie kliknij przycisk **ustawienia**. W **dostęp do interfejsu API** zaznacz **wymagane uprawnienia**.
4. W **wymagane uprawnienia** bloku kliknij **Dodaj** przycisku.
5. W obszarze **wybierz interfejs API**, wyszukaj frazę "Usługi Azure Storage" i wybierz **usługi Azure Storage** z listy wyników.

    ![Zrzut ekranu przedstawiający uprawnienia do magazynu](media/storage-auth-aad-app/registered-app-permissions-1.png)

6. W obszarze **wybierz uprawnienia**, zaznacz pole wyboru obok pozycji **dostępu do usługi Azure Storage**i kliknij przycisk **wybierz**.
7. Kliknij przycisk **Gotowe**.

**Wymagane uprawnienia** systemu windows zawiera obecnie, że aplikacja usługi Azure AD ma dostęp do usługi Azure Active Directory i usługi Azure Storage. Uprawnienia są przydzielane do usługi Azure AD automatycznie po użytkownik najpierw zarejestrować aplikację z usługą Azure AD.

![Zrzut ekranu przedstawiający zarejestrować uprawnień aplikacji](media/storage-auth-aad-app/registered-app-permissions-2.png)

## <a name="net-code-example-create-a-block-blob"></a>Przykładowy kod platformy .NET: Utwórz blokowy obiekt blob

Przykład kodu pokazuje, jak uzyskiwanie dostępu do tokenu z usługi Azure AD. Token dostępu jest używany do uwierzytelniania określonego użytkownika, a następnie Autoryzuj żądanie, aby utworzyć blokowego obiektu blob. Aby to działało próbki, najpierw wykonaj kroki opisane w poprzednich sekcjach.

> [!NOTE]
> Jako właściciel konta usługi Azure Storage możesz nie są automatycznie przypisywane uprawnienia dostępu do danych. Należy jawnie przypisać sobie rolę RBAC dla usługi Azure Storage. Można ją przypisać na poziomie subskrypcji, grupy zasobów, konto magazynu lub kontenera lub kolejki. 
>
> Na przykład aby uruchomić przykładowy kod na koncie magazynu, których jesteś właścicielem, a w obszarze tożsamość użytkownika, musisz przypisać rolę RBAC dla Współautor danych obiektu Blob do siebie. W przeciwnym razie wywołanie w celu utworzenia obiektu blob zakończy się niepowodzeniem z kodem stanu HTTP 403 (zabronione). Aby uzyskać więcej informacji, zobacz [Zarządzaj praw dostępu do magazynu danych przy użyciu RBAC (wersja zapoznawcza)](storage-auth-aad-rbac.md).

### <a name="well-known-values-for-authentication-with-azure-ad"></a>Dobrze znane wartości do uwierzytelniania przy użyciu usługi Azure AD

Na potrzeby uwierzytelniania podmiotu zabezpieczeń w usłudze Azure AD, należy niektóre znane wartości mają zostać uwzględnione w kodzie.

#### <a name="azure-ad-authority"></a>Urząd usługi Azure AD

Dla chmury publicznej firmy Microsoft, Azure podstawowy urząd usługi AD jest następująca, gdzie *identyfikator dzierżawy* jest identyfikator dzierżawy usługi Active Directory (lub identyfikator katalogu):

`https://login.microsoftonline.com/<tenant-id>/`

Identyfikator dzierżawy określa dzierżawy usługi Azure AD do uwierzytelniania. Aby pobrać identyfikator dzierżawy, wykonaj czynności opisane w temacie **uzyskanie Identyfikatora dzierżawy usługi Azure Active Directory**.

#### <a name="storage-resource-id"></a>Identyfikator zasobu magazynu

Identyfikator zasobu usługi Azure Storage umożliwia uzyskanie tokenu do uwierzytelniania żądań do usługi Azure Storage:

`https://storage.azure.com/`

### <a name="get-the-tenant-id-for-your-azure-active-directory"></a>Pobieranie Identyfikatora dzierżawy usługi Azure Active Directory

Aby uzyskać identyfikator dzierżawy, wykonaj następujące kroki:

1. W witrynie Azure portal wybierz usługi Active Directory.
2. Kliknij pozycję **Właściwości**.
3. Skopiuj wartość identyfikatora GUID **identyfikator katalogu**. Ta wartość jest również określany jako identyfikator dzierżawy.

![Zrzut ekranu przedstawiający sposób kopiowania Identyfikatora dzierżawy](./media/storage-auth-aad-app/aad-tenant-id.png)

### <a name="add-references-and-using-statements"></a>Dodaj odwołania i przy użyciu instrukcji  

W programie Visual Studio należy zainstalować wersję zapoznawczą biblioteki klienta usługi Azure Storage. Z **narzędzia** menu, wybierz opcję **Menedżera pakietów Nuget**, następnie **Konsola Menedżera pakietów**. Wpisz następujące polecenie w konsoli, aby zainstalować najnowszą wersję biblioteki klienta dla platformy .NET:

```
Install-Package WindowsAzure.Storage
```

Również zainstalować najnowszą wersję bibliotek ADAL:

```
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

Następnie dodaj następujące instrukcje using do kodu:

```dotnet
using System.Globalization;
using Microsoft.IdentityModel.Clients.ActiveDirectory; //ADAL client library for getting the access token
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
```

### <a name="get-an-oauth-token-from-azure-ad"></a>Pobierz OAuth token z usługi Azure AD

Następnie dodaj metodę, która żąda tokenu z usługi Azure AD. Do żądania tokenu, należy wywołać [AuthenticationContext.AcquireTokenAsync](https://docs.microsoft.com/dotnet/api/microsoft.identitymodel.clients.activedirectory.authenticationcontext.acquiretokenasync) metody. Upewnij się, że masz następujące wartości z czynności, które zostały wykonane wcześniej:

- Identyfikator dzierżawy (katalog)
- Identyfikator klienta (aplikacja)
- Identyfikator URI przekierowania klienta

```dotnet
static string GetUserOAuthToken()
{
    const string ResourceId = "https://storage.azure.com/";
    const string AuthInstance = "https://login.microsoftonline.com/{0}/";
    const string TenantId = "<tenant-id>"; // Tenant or directory ID

    // Construct the authority string from the Azure AD OAuth endpoint and the tenant ID. 
    string authority = string.Format(CultureInfo.InvariantCulture, AuthInstance, TenantId);
    AuthenticationContext authContext = new AuthenticationContext(authority);

    // Acquire an access token from Azure AD. 
    AuthenticationResult result = authContext.AcquireTokenAsync(ResourceId, 
                                                                "<client-id>", 
                                                                new Uri(@"<client-redirect-uri>"), 
                                                                new PlatformParameters(PromptBehavior.Auto)).Result;

    return result.AccessToken;
}
```

### <a name="create-the-block-blob"></a>Utwórz blokowy obiekt blob

Na koniec Użyj tokenu dostępu, aby utworzyć nowe poświadczenia magazynu i utworzenie obiektu blob przy użyciu tych poświadczeń:

```dotnet
// Get the access token.
string accessToken = GetUserOAuthToken();

// Use the access token to create the storage credentials.
TokenCredential tokenCredential = new TokenCredential(accessToken);
StorageCredentials storageCredentials = new StorageCredentials(tokenCredential);

// Create a block blob using those credentials
CloudBlockBlob blob = new CloudBlockBlob(new Uri("https://storagesamples.blob.core.windows.net/sample-container/Blob1.txt"), storageCredentials);

blob.UploadTextAsync("Blob created by Azure AD authenticated user.");
```

> [!NOTE]
> Integracja usługi Azure AD z usługą Azure Storage wymaga używania protokołu HTTPS dla operacji usługi Azure Storage.

W powyższym przykładzie biblioteki klienta .NET obsługuje autoryzacji żądania, aby utworzyć blokowego obiektu blob. Inne biblioteki klienta magazynu również obsługiwać autoryzacji żądania dla Ciebie. Jednak w przypadku wywołania operacji usługi Azure Storage przy użyciu tokenu OAuth za pomocą interfejsu API REST, następnie należy autoryzować żądania przy użyciu tokenu OAuth.   

Aby wywoływać operacje usługi obiektów Blob i kolejek, przy użyciu tokenów dostępu protokołu OAuth, należy przekazać token dostępu w **autoryzacji** przy użyciu nagłówka **elementu nośnego** schemat, a następnie określ usługę w wersji 2017-11-09 wyższa, jako pokazano w poniższym przykładzie:

```
GET /container/file.txt HTTP/1.1
Host: mystorageaccount.blob.core.windows.net
x-ms-version: 2017-11-09
Authorization: Bearer eyJ0eXAiOnJKV1...Xd6j
```

Aby uzyskać więcej informacji na temat autoryzowanie operacje usługi Azure Storage z resztą zobacz [uwierzytelnianie w usłudze Azure Active Directory (wersja zapoznawcza)](https://docs.microsoft.com/rest/api/storageservices/authenticate-with-azure-active-directory).

## <a name="next-steps"></a>Kolejne kroki

- Aby dowiedzieć się więcej na temat ról RBAC dla usługi Azure storage, zobacz [Zarządzaj praw dostępu do magazynu danych przy użyciu RBAC (wersja zapoznawcza)](storage-auth-aad-rbac.md).
- Aby dowiedzieć się więcej o korzystaniu z zarządzanych tożsamości dla zasobów platformy Azure z usługą Azure Storage, zobacz [uwierzytelnienia dostępu do obiektów blob i kolejki przy użyciu platformy Azure zarządzanych tożsamości dla zasobów platformy Azure (wersja zapoznawcza)](storage-auth-aad-msi.md).
- Aby dowiedzieć się, jak zalogować się do wiersza polecenia platformy Azure i programu PowerShell przy użyciu tożsamości usługi Azure AD, zobacz [tożsamości usługi Azure AD umożliwia dostęp do usługi Azure Storage przy użyciu interfejsu wiersza polecenia lub programu PowerShell (wersja zapoznawcza)](storage-auth-aad-script.md).
- Aby uzyskać dodatkowe informacje na temat integracji z usługą Azure AD dla kolejek i obiektów blob platformy Azure, zobacz blog zespołu usługi Azure Storage, publikowania, [ogłoszenie uwierzytelniania w wersji zapoznawczej programu Azure AD dla usługi Azure Storage](https://azure.microsoft.com/blog/announcing-the-preview-of-aad-authentication-for-storage/).



