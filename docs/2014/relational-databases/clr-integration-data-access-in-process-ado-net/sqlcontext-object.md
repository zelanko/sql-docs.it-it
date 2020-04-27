---
title: Oggetto SqlContext | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- Windows identity [CLR integration]
- SqlContext object
- context [CLR integration]
ms.assetid: 67437853-8a55-44d9-9337-90689ebba730
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 223111874ca34ba4df4968c550e6cc47edf2b390
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62920051"
---
# <a name="sqlcontext-object"></a>Oggetto SqlContext
  È possibile richiamare il codice gestito nel server quando si chiama una routine o una funzione, quando si chiama un metodo su un tipo CLR definito dall'utente o quando l'azione genera un trigger definito in uno dei linguaggi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework. Dal momento che l'esecuzione di questo codice viene richiesta come parte di una connessione utente, è necessario l'accesso al contesto del chiamante dal codice in esecuzione sul server. Determinate operazioni di accesso ai dati potrebbero inoltre essere valide solo se eseguite nel contesto del chiamante. L'accesso alle pseudotabelle inserite ed eliminate utilizzate nelle operazioni del trigger, ad esempio, è valido solo nel contesto del chiamante.  
  
 Il contesto del chiamante può essere un'astrazione in un oggetto `SqlContext`. Per ulteriori informazioni sulle proprietà e sui metodi `SqlTriggerContext`, vedere la documentazione di riferimento della classe `Microsoft.SqlServer.Server.SqlTriggerContext` in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
 `SqlContext` fornisce l'accesso ai componenti seguenti:  
  
-   `SqlPipe`: l'oggetto `SqlPipe` rappresenta la "pipe" tramite la quale i risultati vengono propagati al client. Per ulteriori informazioni sull' `SqlPipe` oggetto, vedere [SqlPipe Object](sqlpipe-object.md).  
  
-   `SqlTriggerContext`: l'oggetto `SqlTriggerContext` può essere recuperato solo dall'interno un trigger CLR. Fornisce informazioni sull'operazione che ha attivato il trigger e una mappa delle colonne che sono state aggiornate. Per ulteriori informazioni sull' `SqlTriggerContext` oggetto, vedere [oggetto SqlTriggerContext](sqltriggercontext-object.md).  
  
-   `IsAvailable`: la proprietà `IsAvailable` viene utilizzata per stabilire la disponibilità del contesto.  
  
-   `WindowsIdentity`: la proprietà `WindowsIdentity` viene utilizzata per recuperare l'identità di Windows del chiamante.  
  
## <a name="determining-context-availability"></a>Determinazione della disponibilità del contesto  
 Eseguire una query sulla classe `SqlContext` per vedere se il codice attualmente in esecuzione viene eseguito in-process. A tale scopo, verificare la proprietà `IsAvailable` dell'oggetto `SqlContext`. La proprietà `IsAvailable` è di sola lettura e restituisce `True` se il codice chiamante viene eseguito all'interno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e se è possibile accedere ad altri membri di `SqlContext`. Se la proprietà `IsAvailable` restituisce `False`, tutti gli altri membri di `SqlContext` generano un'eccezione `InvalidOperationException` se vengono utilizzati. Se `IsAvailable` restituisce `False`, qualsiasi tentativo di aprire un oggetto connessione in cui "context connection=true" nella stringa di connessione non riesce.  
  
## <a name="retrieving-windows-identity"></a>Recupero dell'identità di Windows  
 Il codice CLR in esecuzione all'interno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene sempre richiamato nel contesto dell'account del processo. Se il codice deve eseguire determinate azioni utilizzando l'identità dell'utente chiamante, anziché l'identità di processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario ottenere un token di rappresentazione mediante la proprietà `WindowsIdentity` dell'oggetto `SqlContext`. La proprietà `WindowsIdentity` restituisce un'istanza di `WindowsIdentity` che rappresenta l'identità di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows del chiamante oppure Null se il client è stato autenticato con l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Solo gli assembly contrassegnati con le autorizzazioni `EXTERNAL_ACCESS` o `UNSAFE` possono accedere a questa proprietà.  
  
 Dopo avere ottenuto l'oggetto `WindowsIdentity`, i chiamanti possono rappresentare l'account del client ed eseguirne le azioni.  
  
 L'identità del chiamante è disponibile solo tramite `SqlContext.WindowsIdentity` se il client che ha iniziato l'esecuzione della stored procedure o della funzione ha eseguito la connessione al server utilizzando l'autenticazione di Windows. Se invece è stata utilizzata l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questa proprietà è Null e il codice non è in grado di rappresentare il chiamante.  
  
### <a name="example"></a>Esempio  
 Nell'esempio riportato di seguito viene illustrato come ottenere l'identità di Windows del client chiamante e rappresentare il client.  
  
 C#  
  
```  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void WindowsIDTestProc()  
{  
    WindowsIdentity clientId = null;  
    WindowsImpersonationContext impersonatedUser = null;  
  
    // Get the client ID.  
    clientId = SqlContext.WindowsIdentity;  
  
    // This outer try block is used to thwart exception filter   
    // attacks which would prevent the inner finally   
    // block from executing and resetting the impersonation.  
    try  
    {  
        try  
        {  
            impersonatedUser = clientId.Impersonate();  
            if (impersonatedUser != null)  
            {  
                // Perform some action using impersonation.  
            }  
        }  
        finally  
        {  
            // Undo impersonation.  
            if (impersonatedUser != null)  
                impersonatedUser.Undo();  
        }  
    }  
    catch  
    {  
        throw;  
    }  
}  
```  
  
 Visual Basic  
  
```  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub  WindowsIDTestProcVB ()  
    Dim clientId As WindowsIdentity  
    Dim impersonatedUser As WindowsImpersonationContext  
  
    ' Get the client ID.  
    clientId = SqlContext.WindowsIdentity  
  
    ' This outer try block is used to thwart exception filter   
    ' attacks which would prevent the inner finally   
    ' block from executing and resetting the impersonation.  
  
    Try  
        Try  
  
            impersonatedUser = clientId.Impersonate()  
  
            If impersonatedUser IsNot Nothing Then  
                ' Perform some action using impersonation.  
            End If  
  
        Finally  
            ' Undo impersonation.  
            If impersonatedUser IsNot Nothing Then  
                impersonatedUser.Undo()  
            End If  
        End Try  
  
    Catch e As Exception  
  
        Throw e  
  
    End Try  
End Sub  
```  
  
## <a name="see-also"></a>Vedi anche  
 [SqlPipe (oggetto)](sqlpipe-object.md)   
 [Oggetto SqlTriggerContext](sqltriggercontext-object.md)   
 [Trigger CLR](../../database-engine/dev-guide/clr-triggers.md)   
 [Estensioni specifiche in-process di SQL Server ad ADO.NET](sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
