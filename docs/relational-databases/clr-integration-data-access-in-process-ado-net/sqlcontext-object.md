---
title: 'Oggetto SqlContext : Documenti Microsoft'
description: Quando si richiama codice gestito in SQL ServerSQL Server in una connessione utente, l'accesso al contesto del chiamante viene astratto in un oggetto SqlContext.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: cd6d3091b155ae829e368bdd182b3da8286c7194
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487538"
---
# <a name="sqlcontext-object"></a>Oggetto SqlContext
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  È possibile richiamare il codice gestito nel server quando si chiama una routine o una funzione, quando si chiama un metodo su un tipo CLR definito dall'utente o quando l'azione genera un trigger definito in uno dei linguaggi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework. Dal momento che l'esecuzione di questo codice viene richiesta come parte di una connessione utente, è necessario l'accesso al contesto del chiamante dal codice in esecuzione sul server. Determinate operazioni di accesso ai dati potrebbero inoltre essere valide solo se eseguite nel contesto del chiamante. L'accesso alle pseudotabelle inserite ed eliminate utilizzate nelle operazioni del trigger, ad esempio, è valido solo nel contesto del chiamante.  
  
 Il contesto del chiamante è astratto in un oggetto **SqlContext.** Per ulteriori informazioni sui metodi e le proprietà **Di SqlTriggerContext,** vedere la documentazione [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] di riferimento della classe **Microsoft.SqlServer.Server.SqlTriggerContext** nell'SDK.  
  
 **SqlContext** fornisce l'accesso ai componenti seguenti:SqlContext provides access to the following components:  
  
-   **SqlPipe**: L'oggetto **SqlPipe** rappresenta la "pipe" attraverso la quale i risultati scorrono al client. Per ulteriori informazioni sull'oggetto **SqlPipe** , vedere [Oggetto SqlPipe](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md).  
  
-   **SqlTriggerContext:** l'oggetto **SqlTriggerContext** può essere recuperato solo dall'interno di un trigger CLR. Fornisce informazioni sull'operazione che ha attivato il trigger e una mappa delle colonne che sono state aggiornate. Per ulteriori informazioni sull'oggetto **SqlTriggerContext** , vedere [Oggetto SqlTriggerContext](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md).  
  
-   **IsAvailable:** la proprietà **IsAvailable** viene utilizzata per determinare la disponibilità del contesto.  
  
-   **WindowsIdentity**: la proprietà **WindowsIdentity** viene utilizzata per recuperare l'identità Di Windows del chiamante.  
  
## <a name="determining-context-availability"></a>Determinazione della disponibilità del contesto  
 Eseguire una query sulla classe **SqlContext** per verificare se il codice attualmente in esecuzione è in esecuzione in-process. A tale scopo, controllare il **IsAvailable** proprietà del **SqlContext** oggetto. Il **IsAvailable** proprietà è di sola lettura e restituisce [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **True** se il codice chiamante è in esecuzione all'interno e se è possibile accedere ad altri **membri SqlContext.** Se la proprietà **IsAvailable** restituisce **False**, tutti gli altri membri **SqlContext** generano un'eccezione **InvalidOperationException**, se utilizzata. Se **IsAvailable** restituisce **False**, qualsiasi tentativo di aprire un oggetto connessione che contiene "context connection -true" nella stringa di connessione ha esito negativo.  
  
## <a name="retrieving-windows-identity"></a>Recupero dell'identità di Windows  
 Il codice CLR in esecuzione all'interno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene sempre richiamato nel contesto dell'account del processo. Se il codice deve eseguire determinate azioni usando l'identità dell'utente chiamante, anziché l'identità del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processo, è necessario ottenere un token di rappresentazione tramite la proprietà **WindowsIdentity** dell'oggetto **SqlContext.** La proprietà **WindowsIdentity** restituisce un'istanza di **WindowsIdentity** che rappresenta [!INCLUDE[msCoName](../../includes/msconame-md.md)] l'identità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows del chiamante oppure null se il client è stato autenticato tramite autenticazione. Solo gli assembly contrassegnati con autorizzazioni **EXTERNAL_ACCESS** o **UNSAFE** possono accedere a questa proprietà.  
  
 Dopo aver ottenuto l'oggetto **WindowsIdentity,** i chiamanti possono rappresentare l'account client ed eseguire azioni per loro conto.  
  
 L'identità del chiamante è disponibile solo tramite **SqlContext.WindowsIdentity** se il client che ha avviato l'esecuzione della stored procedure o della funzione si è connesso al server tramite l'autenticazione di Windows. Se invece è stata utilizzata l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questa proprietà è Null e il codice non è in grado di rappresentare il chiamante.  
  
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
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto SqlPipe](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)   
 [Oggetto SqlTriggerContext](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)   
 [Trigger CLRCLR Triggers](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [Estensioni specifiche in-process di SQL Server ad ADO.NET](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
