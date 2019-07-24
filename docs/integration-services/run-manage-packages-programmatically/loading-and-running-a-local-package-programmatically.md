---
title: Caricamento ed esecuzione di un pacchetto locale a livello di programmazione | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Integration Services packages, running
- events [Integration Services], capturing
- packages [Integration Services], running
- loading packages programmatically
- Visual Basic [Integration Services]
- running packages [Integration Services]
- programmatically load and run packages [SSIS]
ms.assetid: 2f9fc1a8-a001-4c54-8c64-63b443725422
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 3f127aeb7d9e86e70460190d11ea7c61b57c1d24
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028579"
---
# <a name="loading-and-running-a-local-package-programmatically"></a>Caricamento ed esecuzione di un pacchetto locale a livello di codice

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  È possibile eseguire i pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in base alle necessità o a orari predeterminati utilizzando i metodi descritti in [Esecuzione di pacchetti](../packages/run-integration-services-ssis-packages.md). Tuttavia, con poche righe di codice, è anche possibile eseguire un pacchetto da un'applicazione personalizzata, ad esempio un'applicazione Windows Form, un'applicazione console, un Web Form o un servizio Web ASP.NET oppure un servizio Windows.  
  
 In questo argomento viene illustrato quanto segue:  
  
-   Caricamento di un pacchetto a livello di codice  
  
-   Esecuzione di un pacchetto a livello di codice  
  
 Tutti i metodi usati in questo argomento per caricare ed eseguire pacchetti richiedono un riferimento all'assembly **Microsoft.SqlServer.ManagedDTS**. Dopo aver aggiunto il riferimento in un nuovo progetto, importare lo spazio dei nomi <xref:Microsoft.SqlServer.Dts.Runtime> con un'istruzione **using** o **Imports**.  
  
## <a name="loading-a-package-programmatically"></a>Caricamento di un pacchetto a livello di codice  
 Per caricare un pacchetto a livello di codice nel computer locale, indipendentemente dal fatto che il pacchetto sia archiviato in modalità locale o remota, chiamare uno dei metodi seguenti:  
  
|Percorso di archiviazione|Metodo da chiamare|  
|----------------------|--------------------|  
|File|<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadPackage%2A>|  
|Archivio pacchetti SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromSqlServer%2A>|  
  
> [!IMPORTANT]  
>  I metodi della classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> per l'utilizzo dell'archivio pacchetti SSIS supportano solo ".", localhost o il nome del server locale. Non è possibile utilizzare "(local)".  
  
## <a name="running-a-package-programmatically"></a>Esecuzione di un pacchetto a livello di codice  
 Lo sviluppo di un'applicazione personalizzata in codice gestito che esegue un pacchetto nel computer locale richiede l'approccio seguente. I passaggi riepilogati in questa sezione sono illustrati nell'applicazione console di esempio seguente.  
  
#### <a name="to-run-a-package-on-the-local-computer-programmatically"></a>Per eseguire un pacchetto a livello di codice nel computer locale  
  
1.  Avviare l'ambiente di sviluppo di Visual Studio e creare una nuova applicazione nel linguaggio di sviluppo preferito. In questo esempio viene utilizzata un'applicazione console. Tuttavia, è anche possibile eseguire un pacchetto da un'applicazione Windows Form, da un Web Form o servizio Web ASP.NET oppure da un servizio Windows.  
  
2.  Scegliere **Aggiungi riferimento** dal menu **Progetto**, quindi aggiungere un riferimento a **Microsoft.SqlServer.ManagedDTS.dll**. Fare clic su **OK**.  
  
3.  Usare l'istruzione **Imports** di Visual Basic o l'istruzione C# **using** per importare lo spazio dei nomi **Microsoft.SqlServer.Dts.Runtime**.  
  
4.  Aggiungere il codice seguente nella routine principale. L'applicazione console completata dovrebbe essere simile all'esempio seguente.  
  
    > [!NOTE]  
    >  Nel codice di esempio è illustrato il caricamento del pacchetto dal file system tramite il metodo <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadPackage%2A>. Tuttavia, è anche possibile caricare il pacchetto dal database MSDB chiamando il metodo <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromSqlServer%2A> o dall'archivio pacchetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] chiamando il metodo <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromDtsServer%2A>.  
  
5.  Eseguire il progetto. Nel codice di esempio viene eseguito il pacchetto di esempio CalculatedColumns, installato con gli esempi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il risultato dell'esecuzione del pacchetto è visualizzato nella finestra della console.  
  
### <a name="sample-code"></a>Codice di esempio  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim pkgLocation As String  
    Dim pkg As New Package  
    Dim app As New Application  
    Dim pkgResults As DTSExecResult  
  
    pkgLocation = _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx"  
    pkg = app.LoadPackage(pkgLocation, Nothing)  
    pkgResults = pkg.Execute()  
  
    Console.WriteLine(pkgResults.ToString())  
    Console.ReadKey()  
  
  End Sub  
  
End Module  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace RunFromClientAppCS  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string pkgLocation;  
      Package pkg;  
      Application app;  
      DTSExecResult pkgResults;  
  
      pkgLocation =  
        @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx";  
      app = new Application();  
      pkg = app.LoadPackage(pkgLocation, null);  
      pkgResults = pkg.Execute();  
  
      Console.WriteLine(pkgResults.ToString());  
      Console.ReadKey();  
    }  
  }  
}  
```  
  
## <a name="capturing-events-from-a-running-package"></a>Acquisizione di eventi da un pacchetto in esecuzione  
 Quando si esegue un pacchetto a livello di codice, come illustrato nell'esempio precedente, è anche possibile acquisire errori e altri eventi che si verificano durante l'esecuzione del pacchetto. A tale scopo, aggiungere una classe che eredita dalla classe <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> e passare un riferimento a tale classe quando si carica il pacchetto. Anche se nell'esempio seguente viene acquisito solo l'evento <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents.OnError%2A>, la classe <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> consente di acquisire molti altri eventi.  
  
#### <a name="to-run-a-package-on-the-local-computer-programmatically-and-capture-package-events"></a>Per eseguire un pacchetto a livello di codice nel computer locale e acquisire gli eventi del pacchetto  
  
1.  Attenersi alla procedura descritta nell'esempio precedente per creare un progetto.  
  
2.  Aggiungere il codice seguente nella routine principale. L'applicazione console completata dovrebbe essere simile all'esempio seguente.  
  
3.  Eseguire il progetto. Nel codice di esempio viene eseguito il pacchetto di esempio CalculatedColumns, installato con gli esempi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il risultato dell'esecuzione del pacchetto è visualizzato nella finestra della console, insieme agli eventuali errori che si verificano.  
  
### <a name="sample-code"></a>Codice di esempio  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim pkgLocation As String  
    Dim pkg As New Package  
    Dim app As New Application  
    Dim pkgResults As DTSExecResult  
  
    Dim eventListener As New EventListener()  
  
    pkgLocation = _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx"  
    pkg = app.LoadPackage(pkgLocation, eventListener)  
    pkgResults = pkg.Execute(Nothing, Nothing, eventListener, Nothing, Nothing)  
  
    Console.WriteLine(pkgResults.ToString())  
    Console.ReadKey()  
  
  End Sub  
  
End Module  
  
Class EventListener  
  Inherits DefaultEvents  
  
  Public Overrides Function OnError(ByVal source As Microsoft.SqlServer.Dts.Runtime.DtsObject, _  
    ByVal errorCode As Integer, ByVal subComponent As String, ByVal description As String, _  
    ByVal helpFile As String, ByVal helpContext As Integer, _  
    ByVal idofInterfaceWithError As String) As Boolean  
  
    ' Add application-specific diagnostics here.  
    Console.WriteLine("Error in {0}/{1} : {2}", source, subComponent, description)  
    Return False  
  
  End Function  
  
End Class  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace RunFromClientAppWithEventsCS  
{  
  class MyEventListener : DefaultEvents  
  {  
    public override bool OnError(DtsObject source, int errorCode, string subComponent,   
      string description, string helpFile, int helpContext, string idofInterfaceWithError)  
    {  
      // Add application-specific diagnostics here.  
      Console.WriteLine("Error in {0}/{1} : {2}", source, subComponent, description);  
      return false;  
    }  
  }  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string pkgLocation;  
      Package pkg;  
      Application app;  
      DTSExecResult pkgResults;  
  
      MyEventListener eventListener = new MyEventListener();  
  
      pkgLocation =  
        @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx";  
      app = new Application();  
      pkg = app.LoadPackage(pkgLocation, eventListener);  
      pkgResults = pkg.Execute(null, null, eventListener, null, null);  
  
      Console.WriteLine(pkgResults.ToString());  
      Console.ReadKey();  
    }  
  }  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Differenze tra l'esecuzione locale e remota](../../integration-services/run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [Caricamento ed esecuzione di un pacchetto remoto a livello di programmazione](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)   
 [Caricamento dell'output di un pacchetto locale](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
