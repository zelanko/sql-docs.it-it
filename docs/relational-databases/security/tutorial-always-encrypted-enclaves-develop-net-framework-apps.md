---
title: "Esercitazione: Sviluppare un'applicazione .NET Framework usando Always Encrypted con enclave sicuri | Microsoft Docs"
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: b73d24edb139e36f11e05c854c9d10d885994e18
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "73595486"
---
# <a name="tutorial-develop-a-net-framework-application-using-always-encrypted-with-secure-enclaves"></a>Esercitazione: Sviluppare un'applicazione .NET Framework usando Always Encrypted con enclave sicuri
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

Questa esercitazione illustra come sviluppare una semplice applicazione che esegue query di database che usano un'enclave sicuro lato server per [Always Encrypted con enclave sicuri](encryption/always-encrypted-enclaves.md). 

## <a name="prerequisites"></a>Prerequisites
Questa esercitazione è la continuazione di [Esercitazione: Introduzione ad Always Encrypted con enclave sicuri tramite SSMS](./tutorial-getting-started-with-always-encrypted-enclaves.md). Assicurarsi di averla completata prima eseguire le procedure riportate di seguito.

È necessario anche Visual Studio (è consigliata la versione 2019), che può essere scaricato da [https://visualstudio.microsoft.com/](https://visualstudio.microsoft.com). Il computer di sviluppo dell'applicazione deve eseguire .NET Framework 4.7.2 o versione successiva.

## <a name="step-1-set-up-your-visual-studio-project"></a>Passaggio 1: Configurare il progetto di Visual Studio

Per usare Always Encrypted con enclave sicuri in un'applicazione .NET Framework, è necessario assicurarsi che l'applicazione sia sviluppata con .NET Framework 4.7.2 e integrata con il [pacchetto NuGet Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders). Inoltre, se si archivia la chiave master della colonna in Azure Key Vault, è anche necessario integrare l'applicazione con il [pacchetto NuGet Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider), versione 2.2.0 o successiva. 

1. Aprire Visual Studio.

2. Creare un nuovo progetto di app console C\# (.NET Framework).

3. Assicurarsi che il progetto sia destinato almeno a .NET Framework 4.7.2. Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni, scegliere Proprietà e impostare Framework di destinazione su .NET Framework 4.7.2.

4. Installare il pacchetto NuGet seguente passando a**Strumenti** (menu principale) > **Gestione pacchetti NuGet** > **Console di Gestione pacchetti**. Eseguire il codice seguente nella Console di Gestione pacchetti.

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders -IncludePrerelease
   ```

5. Se si usa Azure Key Vault pe l'archiviazione delle chiavi master della colonna, installare i pacchetti NuGet seguenti passando a **Strumenti** (menu principale) > **Gestione pacchetti NuGet** > **Console di Gestione pacchetti**. Eseguire il codice seguente nella Console di Gestione pacchetti.

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider -IncludePrerelease -Version 2.2.0
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```

7. Aprire il file App.config del progetto.

8. Individuare la sezione \<configuration\> e aggiungere o aggiornare le sezioni \<configSections\>.

   a. Se la sezione \<configuration\>**non** contiene la sezione \<configSections\>, aggiungere il contenuto seguente immediatamente sotto \<configuration\>.
   
      ```xml
      <configSections>
         <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
      </configSections>
      ```
   b. Se la sezione \<configuration\> contiene già la sezione \<configSections\>, aggiungere la riga seguente in \<configSections\>:

   ```xml
   <section name="SqlColumnEncryptionEnclaveProviders"  type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data,  Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" /\>
   ```

9. All'interno della sezione configuration, sotto \<configSections\>, aggiungere la sezione seguente, che specifica un provider di enclave da usare per attestare gli enclave VBS e interagire con essi:

   ```xml
   <SqlColumnEncryptionEnclaveProviders>
       <providers>
           <add name="VBS"  type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.HostGuardianServiceEnclaveProvider,  Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders,    Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91"/>
       </providers>
   </SqlColumnEncryptionEnclaveProviders>
   ```

Di seguito è riportato un esempio completo di un file app.config per una semplice applicazione console.
```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
  </configSections>
  <SqlColumnEncryptionEnclaveProviders>
    <providers>
      <add name="VBS"  type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.HostGuardianServiceEnclaveProvider,  Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders,    Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91"/>
    </providers>
  </SqlColumnEncryptionEnclaveProviders>
  <startup> 
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7.2" />
  </startup>
</configuration>
```
## <a name="step-2-implement-your-application-logic"></a>Passaggio 2: Implementare la logica dell'applicazione
L'applicazione si connetterà al database **ContosoHR** creato in [Esercitazione: Introduzione ad Always Encrypted con enclave sicuri tramite SSMS](tutorial-getting-started-with-always-encrypted-enclaves.md) ed eseguirà una query che contiene il predicato `LIKE` sulla colonna **SSN** e un confronto di intervalli sulla colonna **Salary**.

1. Sostituire il contenuto del file Program.cs (generato da Visual Studio) con il codice seguente. Aggiornare la stringa di connessione di database con il nome del server e l'URL di attestazione dell'enclave per l'ambiente. È anche possibile aggiornare le impostazioni di autenticazione del database.

    ```cs
    using System;
    using System.Data.SqlClient;
    using System.Data;

    namespace ConsoleApp1
    {
        class Program
        {
            static void Main(string[] args)
            {
    
                string connectionString = "Data Source = myserver; Initial Catalog = ContosoHR; Column Encryption Setting = Enabled;Enclave Attestation Url = http://hgs.bastion.local/Attestation; Integrated Security = true";

                using (SqlConnection connection = new SqlConnection(connectionString))
                {
                    connection.Open();

                    SqlCommand cmd = connection.CreateCommand();
                    cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [Salary] FROM [dbo].[Employees] WHERE [SSN] LIKE @SSNPattern AND [Salary] > @MinSalary;";

                    SqlParameter paramSSNPattern = cmd.CreateParameter();

                    paramSSNPattern.ParameterName = @"@SSNPattern";
                    paramSSNPattern.DbType = DbType.AnsiStringFixedLength;
                    paramSSNPattern.Direction = ParameterDirection.Input;
                    paramSSNPattern.Value = "%1111";
                    paramSSNPattern.Size = 11;

                    cmd.Parameters.Add(paramSSNPattern);

                    SqlParameter MinSalary = cmd.CreateParameter();

                    MinSalary.ParameterName = @"@MinSalary";
                    MinSalary.DbType = DbType.Currency;
                    MinSalary.Direction = ParameterDirection.Input;
                    MinSalary.Value = 900;

                    cmd.Parameters.Add(MinSalary);
                    cmd.ExecuteNonQuery();
    
                    SqlDataReader reader = cmd.ExecuteReader();
                    while (reader.Read())

                    {
                        Console.WriteLine(reader);
                        Console.WriteLine(reader[0] + ", " + reader[1] + ", " + reader[2] + ", " + reader[3]);
                    }   
                    Console.ReadKey();
                }
            }
        }
    }
    ```
2. Compilare ed eseguire l'applicazione.  

## <a name="see-also"></a>Vedere anche
- [Using Always Encrypted with .NET Framework Data Provider for SQL Server (Uso di Always Encrypted con il provider di dati .NET Framework per SQL Server)](encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)