---
title: Korzystanie z programu Visual Studio oraz platformy .NET i języka C# w celu wykonywania zapytań w bazie danych Azure SQL Database |Microsoft Docs
description: Użycie programu Visual Studio do tworzenia aplikacji w języku C# łączącej się z bazą danych Azure SQL Database i wykonującej w niej zapytania za pomocą instrukcji w języku Transact-SQL.
services: sql-database
ms.service: sql-database
ms.subservice: development
ms.custom: ''
ms.devlang: dotnet
ms.topic: quickstart
author: CarlRabeler
ms.author: carlrab
ms.reviewer: ''
manager: craigg
ms.date: 12/11/2018
ms.openlocfilehash: 93249b7d274ce9d7928dfa46eb339da68c92b785
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/29/2019
ms.locfileid: "55163300"
---
# <a name="quickstart-use-net-and-c-in-visual-studio-to-connect-to-and-query-an-azure-sql-database"></a>Szybki start: Korzystanie z platformy .NET i języka C# w programie Visual Studio w celu nawiązywania połączenia i wykonywania zapytań w bazie danych Azure SQL Database

Ten przewodnik Szybki Start przedstawia sposób użycia [platformy .NET ](https://www.microsoft.com/net/) i kodu w języku C# w programie Visual Studio do wykonywania zapytań do bazy danych Azure SQL za pomocą instrukcji w języku Transact-SQL.

## <a name="prerequisites"></a>Wymagania wstępne

Aby ukończyć ten przewodnik Szybki Start, musisz spełnić następujące warunki:

[!INCLUDE [prerequisites-create-db](../../includes/sql-database-connect-query-prerequisites-create-db-includes.md)]
  
- [Program Visual Studio 2017](https://www.visualstudio.com/downloads/), wersja Community, Professional lub Enterprise.

## <a name="get-sql-server-connection-information"></a>Uzyskiwanie informacji o połączeniu z serwerem SQL

[!INCLUDE [prerequisites-server-connection-info](../../includes/sql-database-connect-query-prerequisites-server-connection-info-includes.md)]

## <a name="create-code-to-query-the-sql-database"></a>Tworzenie kodu zapytania do bazy danych SQL

1. W programie Visual Studio wybierz pozycje **Plik** > **Nowy** > **Projekt**. 
   
1. W oknie dialogowym **Nowy projekt** wybierz pozycję **Visual C#** i wybierz opcję **Aplikacja konsolowa (.NET Framework)**.
   
1. Wprowadź *sqltest* jako nazwę projektu i wybierz **OK**. Zostanie utworzony nowy projekt. 
   
1. Wybierz **Projekt** > **Zarządzaj pakietami NuGet**. 
   
1. W **Menedżerze pakietów NuGet** wybierz kartę **Przeglądaj**, a następnie wyszukaj i wybierz pozycję **System.Data.SqlClient**.
   
1. Na stronie **System.Data.SqlClient** wybierz przycisk **Instaluj**. 
   - W odpowiedzi na monit wybierz **OK**, aby kontynuować instalację. 
   - W przypadku wyświetlenia okna **Akceptacja licencji** wybierz przycisk **Akceptuję**.
   
1. Po zakończeniu instalacji można zamknąć **Menedżera pakietów NuGet**. 
   
1. W edytorze kodu zastąp zawartość **Program.cs** następującym kodem. Podstaw wartości `<server>`, `<username>`, `<password>`, i `<database>`.
   
   >[!IMPORTANT]
   >Kod w tym przykładzie używa przykładowych danych AdventureWorksLT, które można wybrać jako źródło podczas tworzenia bazy danych. Jeśli baza danych zawiera różne dane, w zapytaniu SELECT należy użyć tabel z własnej bazy danych. 
   
   ```csharp
   using System;
   using System.Data.SqlClient;
   using System.Text;
   
   namespace sqltest
   {
       class Program
       {
           static void Main(string[] args)
           {
               try 
               { 
                   SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                   builder.DataSource = "<server>.database.windows.net"; 
                   builder.UserID = "<username>";            
                   builder.Password = "<password>";     
                   builder.InitialCatalog = "<database>";
   
                   using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                   {
                       Console.WriteLine("\nQuery data example:");
                       Console.WriteLine("=========================================\n");
                       
                       connection.Open();       
                       StringBuilder sb = new StringBuilder();
                       sb.Append("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName ");
                       sb.Append("FROM [SalesLT].[ProductCategory] pc ");
                       sb.Append("JOIN [SalesLT].[Product] p ");
                       sb.Append("ON pc.productcategoryid = p.productcategoryid;");
                       String sql = sb.ToString();
   
                       using (SqlCommand command = new SqlCommand(sql, connection))
                       {
                           using (SqlDataReader reader = command.ExecuteReader())
                           {
                               while (reader.Read())
                               {
                                   Console.WriteLine("{0} {1}", reader.GetString(0), reader.GetString(1));
                               }
                           }
                       }                    
                   }
               }
               catch (SqlException e)
               {
                   Console.WriteLine(e.ToString());
               }
               Console.ReadLine();
           }
       }
   }
   ```

## <a name="run-the-code"></a>Uruchamianie kodu

1. Aby uruchomić aplikację, wybierz pozycję **Debugowanie** > **Rozpocznij debugowanie** lub na pasku narzędzi wybierz **Start**, lub naciśnij klawisz **F5**.
1. Sprawdź, czy jest zwracanych 20 pierwszych wierszy kategorii/produktu z bazy danych, a następnie zamknij okno aplikacji.

## <a name="next-steps"></a>Następne kroki

- Dowiedz się, jak [uzyskać połączenie i wykonywać zapytania do bazy danych Azure SQL przy użyciu platformy .NET Core](sql-database-connect-query-dotnet-core.md) w systemach operacyjnych Windows/Linux/macOS.  
- Dowiedz się więcej o [rozpoczynaniu pracy z platformą .NET Core w systemie Windows/Linux/macOS przy użyciu wiersza polecenia](/dotnet/core/tutorials/using-with-xplat-cli).
- Dowiedz się, jak [zaprojektować pierwszą bazę danych Azure SQL przy użyciu narzędzia SSMS](sql-database-design-first-database.md) lub [zaprojektować pierwszą bazę danych Azure SQL przy użyciu platformy .NET](sql-database-design-first-database-csharp.md).
- Aby uzyskać więcej informacji na temat platformy .NET, zobacz [.NET documentation](https://docs.microsoft.com/dotnet/) (Dokumentacja platformy .NET).
- Przykład logiki ponowień: [nawiązywanie połączeń odpornych na błędy z bazą danych SQL za pomocą środowiska ADO.NET][step-4-connect-resiliently-to-sql-with-ado-net-a78n].


<!-- Link references. -->

[step-4-connect-resiliently-to-sql-with-ado-net-a78n]: https://docs.microsoft.com/sql/connect/ado-net/step-4-connect-resiliently-to-sql-with-ado-net

