---
title: Gestione delle eccezioni SMO | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SMO [SQL Server], exceptions
- exceptions [SMO]
- SQL Server Management Objects, exceptions
- inner exceptions [SMO]
ms.assetid: 4c725ff2-6588-44ca-b86a-87979e164153
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a764a077f1be87f6c846589b9a1fb1e989a8e93a
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52537328"
---
# <a name="handling-smo-exceptions"></a>Gestione delle eccezioni SMO
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Nel codice gestito vengono generate eccezioni quando si verifica un errore. Proprietà e metodi SMO non indicano l'esito positivo o negativo nel valore restituito. Le eccezioni possono invece essere rilevate e gestite da un gestore di eccezioni.  
  
 In SMO esistono classi di eccezioni diverse. È possibile estrarre informazioni sull'eccezione dalle proprietà dell'eccezione, ad esempio la proprietà **Message** fornisce un messaggio di testo sull'eccezione.  
  
 Le istruzioni relative alla gestione delle eccezioni sono specifiche del linguaggio di programmazione. In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic, ad esempio, è l'istruzione **Catch** .  
  
## <a name="inner-exceptions"></a>Eccezioni interne  
 Le eccezioni possono essere generali o specifiche. Le eccezioni generali contengono un set di eccezioni specifiche. È possibile utilizzare diverse istruzioni **Catch** per gestire gli errori anticipati e fare in modo che gli errori rimanenti vengano passati al codice di gestione delle eccezioni generali. Le eccezioni si verificano spesso in una sequenza a cascata. Accade di frequente che un'eccezione SMO sia stata causata da un'eccezione SQL. È possibile stabilirlo utilizzando in successione la proprietà **InnerException** per determinare l'eccezione originale che ha provocato l'eccezione finale di livello superiore.  
  
> [!NOTE]  
>  Il **SQLException** eccezione viene dichiarata nel **SqlClient** dello spazio dei nomi.  
  
 ![Un diagramma che mostra i livelli da cui viene generata un'eccezione](../../../relational-databases/server-management-objects-smo/create-program/media/exception-flow.gif "un diagramma che mostra i livelli da cui viene generata un'eccezione")  
  
 Nel diagramma seguente viene illustrato il flusso di eccezioni attraverso i livelli dell'applicazione.  
  
## <a name="example"></a>Esempio  
 Per usare qualsiasi esempio di codice fornito, è necessario scegliere l'ambiente di programmazione, il modello di programmazione e il linguaggio di programmazione per la creazione dell'applicazione. Per altre informazioni, vedere [creare un Visual C&#35; progetto SMO in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).
  
## <a name="catching-an-exception-in-visual-basic"></a>Rilevamento di un'eccezione in Visual Basic  
 Questo esempio di codice viene illustrato come utilizzare il **Try... Catch... Infine** [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] istruzione per rilevare un'eccezione SMO. Tutte le eccezioni SMO sono di tipo SmoException e sono elencate nella documentazione di riferimento di SMO. La sequenza di eccezioni interne viene visualizzata per mostrare la radice dell'errore. Per ulteriori informazioni, vedere la documentazione di [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] .NET.  
  
```VBNET
'This sample requires the Microsoft.SqlServer.Management.Smo.Agent namespace is included.
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Define an Operator object variable by supplying the parent SQL Agent and the name arguments in the constructor.
'Note that the Operator type requires [] parenthesis to differentiate it from a Visual Basic key word.
Dim op As [Operator]
op = New [Operator](srv.JobServer, "Test_Operator")
op.Create()
'Start exception handling.
Try
    'Create the operator again to cause an SMO exception.
    Dim opx As OperatorCategory
    opx = New OperatorCategory(srv.JobServer, "Test_Operator")
    opx.Create()
    'Catch the SMO exception
Catch smoex As SmoException
    Console.WriteLine("This is an SMO Exception")
    'Display the SMO exception message.
    Console.WriteLine(smoex.Message)
    'Display the sequence of non-SMO exceptions that caused the SMO exception.
    Dim ex As Exception
    ex = smoex.InnerException
    Do While ex.InnerException IsNot (Nothing)
        Console.WriteLine(ex.InnerException.Message)
        ex = ex.InnerException
    Loop
    'Catch other non-SMO exceptions.
Catch ex As Exception
    Console.WriteLine("This is not an SMO exception.")
End Try
``` 
  
## <a name="catching-an-exception-in-visual-c"></a>Rilevamento di un'eccezione in Visual C#  
 Questo esempio di codice viene illustrato come utilizzare il **Try... Catch... Infine** Visual C# istruzione per rilevare un'eccezione SMO. Tutte le eccezioni SMO sono di tipo SmoException e sono elencate nella documentazione di riferimento di SMO. La sequenza di eccezioni interne viene visualizzata per mostrare la radice dell'errore. Per ulteriori informazioni, vedere la documentazione di Visual C#.  
  
```csharp  
{   
//This sample requires the Microsoft.SqlServer.Management.Smo.Agent namespace to be included.   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Define an Operator object variable by supplying the parent SQL Agent and the name arguments in the constructor.   
//Note that the Operator type requires [] parenthesis to differentiate it from a Visual Basic key word.   
op = new Operator(srv.JobServer, "Test_Operator");   
op.Create();   
//Start exception handling.   
try {   
    //Create the operator again to cause an SMO exception.   
    OperatorCategory opx;   
    opx = new OperatorCategory(srv.JobServer, "Test_Operator");   
    opx.Create();   
}   
//Catch the SMO exception   
catch (SmoException smoex) {   
    Console.WriteLine("This is an SMO Exception");   
   //Display the SMO exception message.   
   Console.WriteLine(smoex.Message);   
   //Display the sequence of non-SMO exceptions that caused the SMO exception.   
   Exception ex;   
   ex = smoex.InnerException;   
   while (!object.ReferenceEquals(ex.InnerException, (null))) {   
      Console.WriteLine(ex.InnerException.Message);   
      ex = ex.InnerException;   
    }   
    }   
   //Catch other non-SMO exceptions.   
   catch (Exception ex) {   
      Console.WriteLine("This is not an SMO exception.");   
}   
}  
```  
  
  
