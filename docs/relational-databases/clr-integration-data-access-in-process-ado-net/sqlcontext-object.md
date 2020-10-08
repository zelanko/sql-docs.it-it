---
title: Oggetto SqlContext | Microsoft Docs
description: Quando si richiama codice gestito in SQL Server in una connessione utente, l'accesso al contesto del chiamante viene astratto in un oggetto SqlContext.
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
ms.openlocfilehash: c423b4d2b6296da5ce95e62bfc51a160beb956a5
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810727"
---
# <a name="sqlcontext-object"></a>Oggetto SqlContext
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  È possibile richiamare il codice gestito nel server quando si chiama una routine o una funzione, quando si chiama un metodo su un tipo CLR definito dall'utente o quando l'azione genera un trigger definito in uno dei linguaggi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework. Dal momento che l'esecuzione di questo codice viene richiesta come parte di una connessione utente, è necessario l'accesso al contesto del chiamante dal codice in esecuzione sul server. Determinate operazioni di accesso ai dati potrebbero inoltre essere valide solo se eseguite nel contesto del chiamante. L'accesso alle pseudotabelle inserite ed eliminate utilizzate nelle operazioni del trigger, ad esempio, è valido solo nel contesto del chiamante.  
  
 Il contesto del chiamante viene astratto in un oggetto **SqlContext** . Per ulteriori informazioni sui metodi e le proprietà di **SqlTriggerContext** , vedere la documentazione di riferimento della classe **Microsoft. SqlServer. Server. SqlTriggerContext** in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
 **SqlContext** consente di accedere ai componenti seguenti:  
  
-   **SqlPipe**: l'oggetto **SqlPipe** rappresenta il "pipe" tramite il quale i risultati passano al client. Per ulteriori informazioni sull'oggetto **SqlPipe** , vedere [SqlPipe Object](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md).  
  
-   **SqlTriggerContext**: l'oggetto **SqlTriggerContext** può essere recuperato solo dall'interno di un trigger CLR. Fornisce informazioni sull'operazione che ha attivato il trigger e una mappa delle colonne che sono state aggiornate. Per ulteriori informazioni sull'oggetto **SqlTriggerContext** , vedere [oggetto SqlTriggerContext](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md).  
  
-   **Disavailable** **: la proprietà** IsSynchronized viene utilizzata per determinare la disponibilità del contesto.  
  
-   **WindowsIdentity**: la proprietà **WindowsIdentity** viene utilizzata per recuperare l'identità di Windows del chiamante.  
  
## <a name="determining-context-availability"></a>Determinazione della disponibilità del contesto  
 Eseguire una query sulla classe **SqlContext** per verificare se il codice attualmente in esecuzione è in esecuzione in-process. A tale scopo, controllare la proprietà di **disponibilità** dell'oggetto **SqlContext** . La proprietà **disavailable** è di sola lettura e restituisce **true** se il codice chiamante viene eseguito all'interno [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di e se è possibile accedere ad altri membri **SqlContext** . Se la **Proprietà** IsSynchronized restituisce **false**, tutti gli altri membri **SqlContext** generano un' **eccezione InvalidOperationException**, se utilizzata. Se **viene** restituito **false**, qualsiasi tentativo di aprire un oggetto connessione con "context connection = true" nella stringa di connessione ha esito negativo.  
  
## <a name="retrieving-windows-identity"></a>Recupero dell'identità di Windows  
 Il codice CLR in esecuzione all'interno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene sempre richiamato nel contesto dell'account del processo. Se il codice deve eseguire determinate azioni utilizzando l'identità dell'utente chiamante, anziché l'identità del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processo, è necessario ottenere un token di rappresentazione tramite la proprietà **WindowsIdentity** dell'oggetto **SqlContext** . La proprietà **WindowsIdentity** restituisce un'istanza **WindowsIdentity** che rappresenta l' [!INCLUDE[msCoName](../../includes/msconame-md.md)] identità Windows del chiamante o null se il client è stato autenticato tramite l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Solo gli assembly contrassegnati con **EXTERNAL_ACCESS** o le autorizzazioni **unsafe** possono accedere a questa proprietà.  
  
 Una volta ottenuto l'oggetto **WindowsIdentity** , i chiamanti possono rappresentare l'account client ed eseguire azioni per loro conto.  
  
 L'identità del chiamante è disponibile solo tramite **SqlContext. WindowsIdentity** se il client che ha avviato l'esecuzione della stored procedure o della funzione è connessa al server utilizzando l'autenticazione di Windows. Se invece è stata utilizzata l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questa proprietà è Null e il codice non è in grado di rappresentare il chiamante.  
  
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
 [SqlPipe (oggetto)](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)   
 [Oggetto SqlTriggerContext](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)   
 [Trigger CLR](/dotnet/framework/data/adonet/sql/clr-triggers)   
 [Estensioni specifiche in-process di SQL Server ad ADO.NET](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
