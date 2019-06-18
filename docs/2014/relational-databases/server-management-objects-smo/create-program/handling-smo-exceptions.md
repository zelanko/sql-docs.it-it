---
title: Gestione delle eccezioni SMO | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 595da161660b60845c02d71e22411a2a4eba009c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63192114"
---
# <a name="handling-smo-exceptions"></a>Gestione delle eccezioni SMO
  Nel codice gestito vengono generate eccezioni quando si verifica un errore. Proprietà e metodi SMO non indicano l'esito positivo o negativo nel valore restituito. Le eccezioni possono invece essere rilevate e gestite da un gestore di eccezioni.  
  
 In SMO esistono classi di eccezioni diverse. È possibile estrarre informazioni sull'eccezione dalle proprietà dell'eccezione, ad esempio la proprietà `Message` fornisce un messaggio di testo sull'eccezione.  
  
 Le istruzioni relative alla gestione delle eccezioni sono specifiche del linguaggio di programmazione. In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic, ad esempio, è l'istruzione `Catch`.  
  
## <a name="inner-exceptions"></a>Eccezioni interne  
 Le eccezioni possono essere generali o specifiche. Le eccezioni generali contengono un set di eccezioni specifiche. È possibile utilizzare diverse istruzioni `Catch` per gestire gli errori anticipati e fare in modo che gli errori rimanenti vengano passati al codice di gestione delle eccezioni generali. Le eccezioni si verificano spesso in una sequenza a cascata. Accade di frequente che un'eccezione SMO sia stata causata da un'eccezione SQL. È possibile stabilirlo utilizzando in successione la proprietà `InnerException` per determinare l'eccezione originale che ha provocato l'eccezione finale di livello superiore.  
  
> [!NOTE]  
>  Il `SQLException` eccezione viene dichiarata nel **SqlClient** dello spazio dei nomi.  
  
 ![Un diagramma che mostra i livelli da cui viene generata un'eccezione](../../../database-engine/dev-guide/media/exception-flow.gif "un diagramma che mostra i livelli da cui viene generata un'eccezione")  
  
 Nel diagramma seguente viene illustrato il flusso di eccezioni attraverso i livelli dell'applicazione.  
  
## <a name="example"></a>Esempio  
 Per usare qualsiasi esempio di codice fornito, è necessario scegliere l'ambiente di programmazione, il modello di programmazione e il linguaggio di programmazione per la creazione dell'applicazione. Per altre informazioni, vedere [creare un Visual C&#35; progetto SMO in Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md) oppure [creare un progetto Visual Basic SMO in Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md).  
  
## <a name="catching-an-exception-in-visual-basic"></a>Rilevamento di un'eccezione in Visual Basic  
 Questo esempio di codice illustra come usare l'istruzione `Try...Catch...Finally`[!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] per rilevare un'eccezione SMO. Tutte le eccezioni SMO sono di tipo SmoException e sono elencate nella documentazione di riferimento di SMO. La sequenza di eccezioni interne viene visualizzata per mostrare la radice dell'errore. Per ulteriori informazioni, vedere la documentazione di [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] .NET.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBExceptions1](SMO How to#SMO_VBExceptions1)]  -->  
  
## <a name="catching-an-exception-in-visual-c"></a>Rilevamento di un'eccezione in Visual C#  
 In questo esempio di codice viene illustrato come utilizzare l'istruzione `Try...Catch...Finally` Visual C# per rilevare un'eccezione SMO. Tutte le eccezioni SMO sono di tipo SmoException e sono elencate nella documentazione di riferimento di SMO. La sequenza di eccezioni interne viene visualizzata per mostrare la radice dell'errore. Per ulteriori informazioni, vedere la documentazione di Visual C#.  
  
```  
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
  
  
