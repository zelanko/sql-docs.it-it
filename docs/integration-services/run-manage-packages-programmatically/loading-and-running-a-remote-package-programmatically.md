---
description: Caricamento ed esecuzione di un pacchetto remoto a livello di programmazione
title: Caricamento ed esecuzione di un pacchetto remoto a livello di programmazione | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Integration Services packages, running
- packages [Integration Services], running
- remote packages [Integration Services]
ms.assetid: 9f6ef376-3408-46bf-b5fa-fc7b18c689c9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6db12047bd1a8228f6576989e8331b9611bb0742
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495560"
---
# <a name="loading-and-running-a-remote-package-programmatically"></a>Caricamento ed esecuzione di un pacchetto remoto a livello di programmazione

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Per eseguire pacchetti remoti da un computer locale in cui non è installato [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], avviare i pacchetti in modo che vengano eseguiti nel computer remoto in cui è installato [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. A tale scopo, configurare il computer locale per l'utilizzo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, un servizio Web o un componente remoto per avviare i pacchetti nel computer remoto. Se si tenta di avviare i pacchetti remoti direttamente dal computer locale, i pacchetti verranno caricati e ne verrà effettuato il tentativo di esecuzione dal computer locale. Se nel computer locale non è installato [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], i pacchetti non verranno eseguiti.  
  
> [!NOTE]  
>  Non è possibile eseguire i pacchetti all'esterno di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] in un computer client in cui [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non è installato e le condizioni di licenza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potrebbero non consentire l'installazione di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in computer aggiuntivi. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è un componente server e non è ridistribuibile a computer client.  
  
 In alternativa, è possibile eseguire un pacchetto remoto da un computer locale in cui è installato [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Per altre informazioni, vedere [Caricamento ed esecuzione di un pacchetto locale a livello di programmazione](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md).  
  
##  <a name="running-a-remote-package-on-the-remote-computer"></a><a name="top"></a> Esecuzione di un pacchetto remoto nel computer remoto  
 Come accennato in precedenza, è possibile eseguire un pacchetto remoto in un server remoto in vari modi:  
  
-   [Usare SQL Server Agent per eseguire il pacchetto remoto a livello di programmazione](#agent)  
  
-   [Usare un servizio Web o un componente remoto per eseguire il pacchetto remoto a livello di programmazione](#service)  
  
 Quasi tutti i metodi usati in questo argomento per caricare e salvare pacchetti richiedono un riferimento all'assembly **Microsoft.SqlServer.ManagedDTS**. Fa eccezione l'approccio ADO.NET illustrato in questo argomento per l'esecuzione della stored procedure **sp_start_job**, che richiede solo un riferimento a **System.Data**. Dopo aver aggiunto il riferimento all'assembly **Microsoft.SqlServer.ManagedDTS** in un nuovo progetto, importare lo spazio dei nomi <xref:Microsoft.SqlServer.Dts.Runtime> con un'istruzione **using** o **Imports**.  
  
###  <a name="using-sql-server-agent-to-run-a-remote-package-programmatically-on-the-server"></a><a name="agent"></a> Uso di SQL Server Agent per eseguire un pacchetto remoto a livello di programmazione nel server  
 Nell'esempio di codice seguente è illustrato come utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a livello di programmazione per eseguire un pacchetto remoto nel server. Il codice di esempio chiama la stored procedure di sistema **sp_start_job**, che avvia un processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Il processo avviato dalla stored procedure è denominato `RunSSISPackage` e si trova nel computer remoto. Il processo `RunSSISPackage` esegue quindi il pacchetto nel computer remoto.  
  
> [!NOTE]  
>  Il valore restituito della stored procedure **sp_start_job** indica se la stored procedure è stata in grado di avviare correttamente il processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. ma non indica se il pacchetto è stato o meno eseguito correttamente.  
  
 Per informazioni su come risolvere i problemi legati all'esecuzione di pacchetti dai processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, vedere l'articolo Microsoft [relativo a un pacchetto SSIS che non viene eseguito quando si chiama il pacchetto SSIS da un passaggio di processo di SQL Server Agent](https://support.microsoft.com/kb/918760).  
  
### <a name="sample-code"></a>Codice di esempio  
  
```vb  
Imports System.Data  
Imports System.Data.SqlClient  
  
Module Module1  
  
  Sub Main()  
  
    Dim jobConnection As SqlConnection  
    Dim jobCommand As SqlCommand  
    Dim jobReturnValue As SqlParameter  
    Dim jobParameter As SqlParameter  
    Dim jobResult As Integer  
  
    jobConnection = New SqlConnection("Data Source=(local);Initial Catalog=msdb;Integrated Security=SSPI")  
    jobCommand = New SqlCommand("sp_start_job", jobConnection)  
    jobCommand.CommandType = CommandType.StoredProcedure  
  
    jobReturnValue = New SqlParameter("@RETURN_VALUE", SqlDbType.Int)  
    jobReturnValue.Direction = ParameterDirection.ReturnValue  
    jobCommand.Parameters.Add(jobReturnValue)  
  
    jobParameter = New SqlParameter("@job_name", SqlDbType.VarChar)  
    jobParameter.Direction = ParameterDirection.Input  
    jobCommand.Parameters.Add(jobParameter)  
    jobParameter.Value = "RunSSISPackage"  
  
    jobConnection.Open()  
    jobCommand.ExecuteNonQuery()  
    jobResult = DirectCast(jobCommand.Parameters("@RETURN_VALUE").Value, Integer)  
    jobConnection.Close()  
  
    Select Case jobResult  
      Case 0  
        Console.WriteLine("SQL Server Agent job, RunSISSPackage, started successfully.")  
      Case Else  
        Console.WriteLine("SQL Server Agent job, RunSISSPackage, failed to start.")  
    End Select  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlClient;  
  
namespace LaunchSSISPackageAgent_CS  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      SqlConnection jobConnection;  
      SqlCommand jobCommand;  
      SqlParameter jobReturnValue;  
      SqlParameter jobParameter;  
      int jobResult;  
  
      jobConnection = new SqlConnection("Data Source=(local);Initial Catalog=msdb;Integrated Security=SSPI");  
      jobCommand = new SqlCommand("sp_start_job", jobConnection);  
      jobCommand.CommandType = CommandType.StoredProcedure;  
  
      jobReturnValue = new SqlParameter("@RETURN_VALUE", SqlDbType.Int);  
      jobReturnValue.Direction = ParameterDirection.ReturnValue;  
      jobCommand.Parameters.Add(jobReturnValue);  
  
      jobParameter = new SqlParameter("@job_name", SqlDbType.VarChar);  
      jobParameter.Direction = ParameterDirection.Input;  
      jobCommand.Parameters.Add(jobParameter);  
      jobParameter.Value = "RunSSISPackage";  
  
      jobConnection.Open();  
      jobCommand.ExecuteNonQuery();  
      jobResult = (Int32)jobCommand.Parameters["@RETURN_VALUE"].Value;  
      jobConnection.Close();  
  
      switch (jobResult)  
      {  
        case 0:  
          Console.WriteLine("SQL Server Agent job, RunSISSPackage, started successfully.");  
          break;  
        default:  
          Console.WriteLine("SQL Server Agent job, RunSISSPackage, failed to start.");  
          break;  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
###  <a name="using-a-web-service-or-remote-component-to-run-a-remote-package-programmatically"></a><a name="service"></a> Uso di un servizio Web o un componente remoto per eseguire un pacchetto remoto a livello di programmazione  
 La soluzione precedente per l'esecuzione dei pacchetti a livello di programmazione nel server non richiede codice personalizzato nel server. Tuttavia, può essere preferibile una soluzione che non si basa su SQL Server Agent per l'esecuzione dei pacchetti. Nell'esempio seguente sono illustrati un servizio Web che è possibile creare nel server per avviare i pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in locale e un'applicazione di test che è possibile utilizzare per chiamare il servizio Web da un computer client. Se si preferisce creare un componente remoto anziché un servizio Web, è possibile usare lo stesso codice con poche modifiche in un computer remoto. Tuttavia, un componente remoto può richiedere una configurazione più estesa rispetto a un servizio Web.  
  
> [!IMPORTANT]  
>  Con le impostazioni predefinite relative ad autenticazione e autorizzazione, un servizio Web in genere non dispone di autorizzazioni sufficienti per accedere a SQL Server o al file system per caricare ed eseguire pacchetti. Può essere necessario assegnare le autorizzazioni appropriate al servizio Web configurando le relative impostazioni di autenticazione e autorizzazione nel file **web.config** e assegnando le autorizzazioni appropriate per database e file system. Una descrizione completa delle autorizzazioni per Web, database e file system esula dall'ambito di questo argomento.  
  
> [!IMPORTANT]  
>  I metodi della classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> per l'utilizzo dell'archivio pacchetti SSIS supportano solo ".", localhost o il nome del server locale. Non è possibile utilizzare "(local)".  
  
### <a name="sample-code"></a>Codice di esempio  
 Negli esempi di codice seguenti è illustrato come creare e testare il servizio Web.  
  
#### <a name="creating-the-web-service"></a>Creazione del servizio Web  
 Un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] può essere caricato direttamente da un file, direttamente da SQL Server o dall'archivio pacchetti SSIS, che gestisce l'archiviazione di pacchetti in SQL Server e in cartelle speciali del file system. Questo esempio supporta tutte le opzioni disponibili usando un costrutto **Select Case** o **switch** per selezionare la sintassi appropriata per l'avvio del pacchetto e per concatenare gli argomenti di input in modo appropriato. Il metodo LaunchPackage del servizio Web restituisce il risultato dell'esecuzione del pacchetto come numero intero anziché come valore <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult>, per cui i computer client non richiedono un riferimento agli assembly di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
###### <a name="to-create-a-web-service-to-run-packages-on-the-server-programmatically"></a>Per creare un servizio Web per eseguire i pacchetti nel server a livello di programmazione  
  
1.  Aprire Visual Studio e creare un progetto di servizio Web nel linguaggio di programmazione preferito. Nel codice di esempio viene utilizzato il nome LaunchSSISPackageService per il progetto.  
  
2.  Aggiungere un riferimento a **Microsoft.SqlServer.ManagedDTS** e un'istruzione **Imports** o **using** al file codice per lo spazio dei nomi **Microsoft.SqlServer.Dts.Runtime**.  
  
3.  Incollare il codice di esempio per il metodo LaunchPackage del servizio Web nella classe. In questo esempio viene visualizzato l'intero contenuto della finestra del codice.  
  
4.  Compilare e testare il servizio Web fornendo un set di valori validi per gli argomenti di input del metodo LaunchPackage che puntano a un pacchetto esistente. Ad esempio, se package1.dtsx è archiviato nel server in C:\My Packages, passare "file" come valore di sourceType, "C:\My Packages" come valore di sourceLocation e "package1" (senza l'estensione) come valore di packageName.  
  
```vb  
Imports System.Web  
Imports System.Web.Services  
Imports System.Web.Services.Protocols  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports System.IO  
  
<WebService(Namespace:="https://dtsue/")> _  
<WebServiceBinding(ConformsTo:=WsiProfiles.BasicProfile1_1)> _  
<Global.Microsoft.VisualBasic.CompilerServices.DesignerGenerated()> _  
Public Class LaunchSSISPackageService  
  Inherits System.Web.Services.WebService  
  
  ' LaunchPackage Method Parameters:  
  ' 1. sourceType: file, sql, dts  
  ' 2. sourceLocation: file system folder, (none), logical folder  
  ' 3. packageName: for file system, ".dtsx" extension is appended  
  
  <WebMethod()> _  
  Public Function LaunchPackage( _  
    ByVal sourceType As String, _  
    ByVal sourceLocation As String, _  
    ByVal packageName As String) As Integer 'DTSExecResult  
  
    Dim packagePath As String  
    Dim myPackage As Package  
    Dim integrationServices As New Application  
  
    ' Combine path and file name.  
    packagePath = Path.Combine(sourceLocation, packageName)  
  
    Select Case sourceType  
      Case "file"  
        ' Package is stored as a file.  
        ' Add extension if not present.  
        If String.IsNullOrEmpty(Path.GetExtension(packagePath)) Then  
          packagePath = String.Concat(packagePath, ".dtsx")  
        End If  
        If File.Exists(packagePath) Then  
          myPackage = integrationServices.LoadPackage(packagePath, Nothing)  
        Else  
          Throw New ApplicationException( _  
            "Invalid file location: " & packagePath)  
        End If  
      Case "sql"  
        ' Package is stored in MSDB.  
        ' Combine logical path and package name.  
        If integrationServices.ExistsOnSqlServer(packagePath, ".", String.Empty, String.Empty) Then  
          myPackage = integrationServices.LoadFromSqlServer( _  
            packageName, "(local)", String.Empty, String.Empty, Nothing)  
        Else  
          Throw New ApplicationException( _  
            "Invalid package name or location: " & packagePath)  
        End If  
      Case "dts"  
        ' Package is managed by SSIS Package Store.  
        ' Default logical paths are File System and MSDB.  
        If integrationServices.ExistsOnDtsServer(packagePath, ".") Then  
          myPackage = integrationServices.LoadFromDtsServer(packagePath, "localhost", Nothing)  
        Else  
          Throw New ApplicationException( _  
            "Invalid package name or location: " & packagePath)  
        End If  
      Case Else  
        Throw New ApplicationException( _  
          "Invalid sourceType argument: valid values are 'file', 'sql', and 'dts'.")  
    End Select  
  
    Return myPackage.Execute()  
  
  End Function  
  
End Class  
```  
  
```csharp  
using System;  
using System.Web;  
using System.Web.Services;  
using System.Web.Services.Protocols;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.IO;  
  
[WebService(Namespace = "https://dtsue/")]  
[WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]  
public class LaunchSSISPackageServiceCS : System.Web.Services.WebService  
{  
  public LaunchSSISPackageServiceCS()  
  {  
    }  
  
  // LaunchPackage Method Parameters:  
  // 1. sourceType: file, sql, dts  
  // 2. sourceLocation: file system folder, (none), logical folder  
  // 3. packageName: for file system, ".dtsx" extension is appended  
  
  [WebMethod]  
  public int LaunchPackage(string sourceType, string sourceLocation, string packageName)  
  {   
  
    string packagePath;  
    Package myPackage;  
    Application integrationServices = new Application();  
  
    // Combine path and file name.  
    packagePath = Path.Combine(sourceLocation, packageName);  
  
    switch(sourceType)  
    {  
      case "file":  
        // Package is stored as a file.  
        // Add extension if not present.  
        if (String.IsNullOrEmpty(Path.GetExtension(packagePath)))  
        {  
          packagePath = String.Concat(packagePath, ".dtsx");  
        }  
        if (File.Exists(packagePath))  
        {  
          myPackage = integrationServices.LoadPackage(packagePath, null);  
        }  
        else  
        {  
          throw new ApplicationException("Invalid file location: "+packagePath);  
        }  
        break;  
      case "sql":  
        // Package is stored in MSDB.  
        // Combine logical path and package name.  
        if (integrationServices.ExistsOnSqlServer(packagePath, ".", String.Empty, String.Empty))  
        {  
          myPackage = integrationServices.LoadFromSqlServer(packageName, "(local)", String.Empty, String.Empty, null);  
        }  
        else  
        {  
          throw new ApplicationException("Invalid package name or location: "+packagePath);  
        }  
        break;  
      case "dts":  
        // Package is managed by SSIS Package Store.  
        // Default logical paths are File System and MSDB.  
        if (integrationServices.ExistsOnDtsServer(packagePath, "."))  
        {  
          myPackage = integrationServices.LoadFromDtsServer(packagePath, "localhost", null);  
        }  
        else  
        {  
          throw new ApplicationException("Invalid package name or location: "+packagePath);  
        }  
        break;  
      default:  
        throw new ApplicationException("Invalid sourceType argument: valid values are 'file', 'sql', and 'dts'.");  
    }  
  
    return (Int32)myPackage.Execute();  
  
  }  
  
}  
```  
  
#### <a name="testing-the-web-service"></a>Test del servizio Web  
 Nell'applicazione console di esempio seguente viene utilizzato il servizio Web per eseguire un pacchetto. Il metodo LaunchPackage del servizio Web restituisce il risultato dell'esecuzione del pacchetto come numero intero anziché come valore <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult>, per cui i computer client non richiedono un riferimento agli assembly di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Nell'esempio viene creata un'enumerazione privata i cui valori rispecchiano i valori <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> per riportare i risultati dell'esecuzione.  
  
###### <a name="to-create-a-console-application-to-test-the-web-service"></a>Per creare un'applicazione console per testare il servizio Web  
  
1.  In Visual Studio aggiungere una nuova applicazione console, utilizzando il linguaggio di programmazione preferito, nella stessa soluzione che contiene il progetto di servizio Web. Nell'esempio di codice viene utilizzato il nome LaunchSSISPackageTest per il progetto.  
  
2.  Impostare la nuova applicazione console come progetto di avvio nella soluzione.  
  
3.  Aggiungere un riferimento Web per il progetto di servizio Web. Se necessario, modificare la dichiarazione di variabili nell'esempio di codice per il nome assegnato all'oggetto proxy del servizio Web.  
  
4.  Incollare l'esempio di codice per la routine principale e l'enumerazione privata nel codice. In questo esempio viene visualizzato l'intero contenuto della finestra del codice.  
  
5.  Modificare la riga di codice che chiama il metodo LaunchPackage per fornire un set di valori validi per gli argomenti di input che puntano a un pacchetto esistente. Ad esempio, se package1.dtsx è archiviato nel server in C:\My Packages, passare "file" come valore di `sourceType`, "C:\My Packages" come valore di `sourceLocation` e "package1" (senza l'estensione) come valore di `packageName`.  
  
```vb  
Module LaunchSSISPackageTest  
  
  Sub Main()  
  
    Dim launchPackageService As New LaunchSSISPackageService.LaunchSSISPackageService  
    Dim packageResult As Integer  
  
    Try  
      packageResult = launchPackageService.LaunchPackage("sql", String.Empty, "SimpleTestPackage")  
    Catch ex As Exception  
      ' The type of exception returned by a Web service is:  
      '  System.Web.Services.Protocols.SoapException  
      Console.WriteLine("The following exception occurred: " & ex.Message)  
    End Try  
  
    Console.WriteLine(CType(packageResult, PackageExecutionResult).ToString)  
    Console.ReadKey()  
  
  End Sub  
  
  Private Enum PackageExecutionResult  
    PackageSucceeded  
    PackageFailed  
    PackageCompleted  
    PackageWasCancelled  
  End Enum  
  
End Module  
```  
  
```csharp  
using System;  
  
namespace LaunchSSISPackageSvcTestCS  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      LaunchSSISPackageServiceCS.LaunchSSISPackageServiceCS launchPackageService = new LaunchSSISPackageServiceCS.LaunchSSISPackageServiceCS();  
      int packageResult = 0;  
  
      try  
      {  
        packageResult = launchPackageService.LaunchPackage("sql", String.Empty, "SimpleTestPackage");  
      }  
      catch (Exception ex)  
      {  
        // The type of exception returned by a Web service is:  
        //  System.Web.Services.Protocols.SoapException  
        Console.WriteLine("The following exception occurred: " + ex.Message);  
      }  
  
      Console.WriteLine(((PackageExecutionResult)packageResult).ToString());  
      Console.ReadKey();  
  
    }  
  
    private enum PackageExecutionResult  
    {  
      PackageSucceeded,  
      PackageFailed,  
      PackageCompleted,  
      PackageWasCancelled  
    };  
  
  }  
}  
```  
  
## <a name="external-resources"></a>Risorse esterne  
  
-   Video relativo alla [procedura sull'automazione dell'esecuzione di un pacchetto SSIS usando SQL Server Agent (video di SQL Server)](https://technet.microsoft.com/sqlserver/ff686764.aspx) nel sito technet.microsoft.com  
  
## <a name="see-also"></a>Vedere anche  
 [Differenze tra l'esecuzione locale e remota](../../integration-services/run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [Caricamento ed esecuzione di un pacchetto locale a livello di programmazione](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [Caricamento dell'output di un pacchetto locale](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
