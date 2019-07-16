---
title: Oggetto SqlContext | Microsoft Docs
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
ms.openlocfilehash: 746ce8cec228b6fe9a9d36c4e0287ad7c2f3c517
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67951670"
---
# <a name="sqlcontext-object"></a>Oggetto SqlContext
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  È possibile richiamare il codice gestito nel server quando si chiama una routine o una funzione, quando si chiama un metodo su un tipo CLR definito dall'utente o quando l'azione genera un trigger definito in uno dei linguaggi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework. Dal momento che l'esecuzione di questo codice viene richiesta come parte di una connessione utente, è necessario l'accesso al contesto del chiamante dal codice in esecuzione sul server. Determinate operazioni di accesso ai dati potrebbero inoltre essere valide solo se eseguite nel contesto del chiamante. L'accesso alle pseudotabelle inserite ed eliminate utilizzate nelle operazioni del trigger, ad esempio, è valido solo nel contesto del chiamante.  
  
 Il contesto del chiamante viene astratto in un **SqlContext** oggetto. Per ulteriori informazioni sul **SqlTriggerContext** metodi e proprietà, vedere la **Microsoft.SqlServer.Server.SqlTriggerContext** documentazione di riferimento nella classe di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
 **SqlContext** fornisce l'accesso per i componenti seguenti:  
  
-   **Oggetto SqlPipe**: Il **SqlPipe** oggetto rappresenta "pipe" tramite il quale i risultati giungono al client. Per altre informazioni sul **SqlPipe** oggetti, vedere [oggetto SqlPipe](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md).  
  
-   **SqlTriggerContext**: Il **SqlTriggerContext** oggetto può essere recuperato solo dall'interno di un trigger CLR. Fornisce informazioni sull'operazione che ha attivato il trigger e una mappa delle colonne che sono state aggiornate. Per altre informazioni sul **SqlTriggerContext** oggetti, vedere [oggetto SqlTriggerContext](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md).  
  
-   **IsAvailable**: Il **IsAvailable** proprietà viene utilizzata per determinare la disponibilità di contesto.  
  
-   **WindowsIdentity**: Il **WindowsIdentity** proprietà viene utilizzata per recuperare l'identità Windows del chiamante.  
  
## <a name="determining-context-availability"></a>Determinazione della disponibilità del contesto  
 Query di **SqlContext** classe verificare se il codice attualmente in esecuzione è in esecuzione in-process. A questo scopo, verificare i **IsAvailable** proprietà delle **SqlContext** oggetto. Il **IsAvailable** proprietà è di sola lettura e restituisce **True** se il codice chiamante è in esecuzione all'interno [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, se altri **SqlContext** membri sono accessibili. Se il **IsAvailable** restituisce proprietà **False**, tutti gli altri **SqlContext** membri, viene generata un' **InvalidOperationException**, se usata . Se **IsAvailable** restituisce **False**, qualsiasi tentativo di aprire un oggetto connessione contenente "connessione di contesto = true" nella stringa di connessione ha esito negativo.  
  
## <a name="retrieving-windows-identity"></a>Recupero dell'identità di Windows  
 Il codice CLR in esecuzione all'interno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene sempre richiamato nel contesto dell'account del processo. Se il codice deve eseguire determinate azioni utilizzando l'identità dell'utente chiamante, anziché il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identità processo, quindi un token di rappresentazione deve essere ottenuto tramite il **WindowsIdentity** proprietà il  **SqlContext** oggetto. Il **WindowsIdentity** restituisce un **WindowsIdentity** che rappresenta l'istanza il [!INCLUDE[msCoName](../../includes/msconame-md.md)] identità Windows del chiamante oppure null se il client è stato autenticato tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Autenticazione. Solo gli assembly contrassegnati con **EXTERNAL_ACCESS** oppure **UNSAFE** autorizzazioni possono accedere a questa proprietà.  
  
 Dopo aver ottenuto il **WindowsIdentity** dell'oggetto, i chiamanti possono rappresentare l'account del client ed eseguire azioni per loro conto.  
  
 L'identità del chiamante è disponibile solo tramite **SqlContext.WindowsIdentity** se il client che ha avviato l'esecuzione della stored procedure o della funzione connesso al server usando l'autenticazione di Windows. Se invece è stata utilizzata l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questa proprietà è Null e il codice non è in grado di rappresentare il chiamante.  
  
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
 [Trigger CLR](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [Estensioni specifiche In-Process di SQL Server ad ADO.NET](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
