---
title: Accesso alla transazione corrente | Microsoft Docs
description: In SQL Server integrazione con CLR, la proprietà Current della classe System. Transactions. Transaction consente di accedere alla transazione corrente.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- current transaction access
- Current property
- Transaction class
ms.assetid: 1a4e2ce5-f627-4c81-8960-6a9968cefda2
author: rothja
ms.author: jroth
ms.openlocfilehash: b9220519a926ca75a00843dba54dfad797064aee
ms.sourcegitcommit: 52252e8b4c9b50d3915aecd3135e8901d345e7e2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/16/2020
ms.locfileid: "97599848"
---
# <a name="accessing-the-current-transaction"></a>Accesso alla transazione corrente
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Se una transazione è attiva nel momento in cui viene immesso il codice Common Language Runtime (CLR) in esecuzione in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , la transazione viene esposta tramite la classe **System. Transactions. Transaction** . La proprietà **Transaction. Current** viene utilizzata per accedere alla transazione corrente. Nella maggior parte dei casi non è necessario accedere in modo esplicito alla transazione. Per le connessioni di database, ADO.NET controlla automaticamente **Transaction. Current** quando viene chiamato il metodo **Connection. Open** e integra in modo trasparente la connessione nella transazione, a meno che la parola chiave **integra** non sia impostata su false nella stringa di connessione.  
  
 Potrebbe essere necessario utilizzare l'oggetto **transazione** direttamente negli scenari seguenti:  
  
-   Se si desidera integrare una risorsa che non esegue l'integrazione automatica o che per qualche motivo non è stata integrata durante l'inizializzazione.  
  
-   Se si desidera integrare in modo esplicito una risorsa nella transazione.  
  
-   Se si desidera terminare la transazione esterna dalla stored procedure o dalla funzione. In questo caso, utilizzare <xref:System.Transactions.TransactionScope>. Nel codice seguente, ad esempio, viene eseguito il rollback della transazione corrente:  
  
    ```  
    using(TransactionScope transactionScope = new TransactionScope(TransactionScopeOptions.Required)) { }  
    ```  
  
 Nella parte restante di questo argomento vengono descritte altre modalità di annullamento di una transazione esterna.  
  
## <a name="canceling-an-external-transaction"></a>Annullamento di una transazione esterna  
 È possibile annullare le transazioni esterne da una funzione o procedura gestita nelle modalità seguenti:  
  
-   La funzione o procedura gestita può restituire un valore utilizzando un parametro di output. La [!INCLUDE[tsql](../../includes/tsql-md.md)] procedura chiamante può controllare il valore restituito e, se necessario, eseguire **Rollback Transaction**.  
  
-   La funzione o procedura gestita può generare un'eccezione personalizzata. La [!INCLUDE[tsql](../../includes/tsql-md.md)] procedura chiamante può intercettare l'eccezione generata dalla procedura o dalla funzione gestita in un blocco try/catch ed eseguire **Rollback Transaction**.  
  
-   La procedura o funzione gestita può annullare la transazione corrente chiamando il metodo **Transaction. rollback** se viene soddisfatta una determinata condizione.  
  
 Quando viene chiamato all'interno di una routine o di una funzione gestita, il metodo **Transaction. rollback** genera un'eccezione con un messaggio di errore ambiguo e può essere incluso in un blocco try/catch. Il messaggio di errore è simile al seguente:  
  
```  
Msg 3994, Level 16, State 1, Procedure uspRollbackFromProc, Line 0  
Transaction is not allowed to roll back inside a user defined routine, trigger or aggregate because the transaction is not started in that CLR level. Change application logic to enforce strict transaction nesting.  
```  
  
 Questa eccezione è prevista e il blocco try/catch è necessario per continuare a eseguire il codice. Senza il blocco try/catch, l'eccezione verrà generata immediatamente per la procedura [!INCLUDE[tsql](../../includes/tsql-md.md)] chiamante e l'esecuzione del codice gestito verrà terminata. Al termine dell'esecuzione del codice gestito, viene generata un'altra eccezione:  
  
```  
Msg 3991, Level 16, State 1, Procedure uspRollbackFromProc, Line 1   
The context transaction which was active before entering user defined routine, trigger or aggregate " uspRollbackFromProc " has been ended inside of it, which is not allowed. Change application logic to enforce strict transaction nesting. The statement has been terminated.  
```  
  
 Anche questa eccezione è prevista e, per continuare l'esecuzione è necessario un blocco try/catch intorno all'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] che esegue l'azione che attiva il trigger. Nonostante le due eccezioni generate, viene eseguito il rollback della transazione e le modifiche non vengono sottoposte a commit.  
  
### <a name="example"></a>Esempio  
 Di seguito è riportato un esempio di una transazione di cui viene eseguito il rollback da una procedura gestita tramite il metodo **Transaction. rollback** . Si noti il blocco try/catch intorno al metodo **Transaction. rollback** nel codice gestito. Lo script [!INCLUDE[tsql](../../includes/tsql-md.md)] crea un assembly e una stored procedure gestita. Tenere presente che l'istruzione **Exec uspRollbackFromProc** è racchiusa in un blocco try/catch, in modo che l'eccezione generata al termine dell'esecuzione della procedura gestita venga rilevata.  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
using System.Transactions;  
  
public partial class StoredProcedures  
{  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void uspRollbackFromProc()  
{  
   using (SqlConnection connection = new SqlConnection(@"context connection=true"))  
   {  
      // Open the connection.  
      connection.Open();  
  
      bool successCondition = true;  
  
      // Success condition is met.  
      if (successCondition)  
      {  
         SqlContext.Pipe.Send("Success condition met in procedure.");   
         // Perform other actions here.  
      }  
  
      //  Success condition is not met, the transaction will be rolled back.  
      else  
      {  
         SqlContext.Pipe.Send("Success condition not met in managed procedure. Transaction rolling back...");  
         try  
         {  
               // Get the current transaction and roll it back.  
               Transaction trans = Transaction.Current;  
               trans.Rollback();  
         }  
         catch (SqlException ex)  
         {  
            // Catch the expected exception.   
            // This allows the connection to close correctly.                      
         }    
      }  
  
      // Close the connection.  
      connection.Close();  
   }  
}  
};  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Transactions  
  
Partial Public Class StoredProcedures  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub  uspRollbackFromProc ()  
   Using connection As New SqlConnection("context connection=true")  
  
   ' Open the connection.  
   connection.Open()  
  
   Dim successCondition As Boolean  
   successCondition = False  
  
   ' Success condition is met.  
   If successCondition Then  
  
      SqlContext.Pipe.Send("Success condition met in procedure.")  
  
      ' Success condition is not met, the transaction will be rolled back.  
  
   Else  
      SqlContext.Pipe.Send("Success condition not met in managed procedure. Transaction rolling back...")  
      Try  
         ' Get the current transaction and roll it back.  
         Dim trans As Transaction  
         trans = Transaction.Current  
         trans.Rollback()  
  
      Catch ex As SqlException  
         ' Catch the exception instead of throwing it.    
         ' This allows the connection to close correctly.                      
      End Try  
  
   End If  
  
   ' Close the connection.  
   connection.Close()  
  
End Using  
End Sub  
End Class  
```  
  
 **Transact-SQL**  
  
```  
--Register assembly.  
CREATE ASSEMBLY TestProcs FROM 'C:\Programming\TestProcs.dll'   
Go  
CREATE PROCEDURE uspRollbackFromProc AS EXTERNAL NAME TestProcs.StoredProcedures.uspRollbackFromProc  
Go  
  
-- Execute procedure.  
BEGIN TRY  
BEGIN TRANSACTION   
-- Perform other actions.  
Exec uspRollbackFromProc  
-- Perform other actions.  
PRINT N'Commiting transaction...'  
COMMIT TRANSACTION  
END TRY  
  
BEGIN CATCH  
SELECT ERROR_NUMBER() AS ErrorNum, ERROR_MESSAGE() AS ErrorMessage  
PRINT N'Exception thrown, rolling back transaction.'  
ROLLBACK TRANSACTION  
PRINT N'Transaction rolled back.'   
END CATCH  
Go  
  
-- Clean up.  
DROP Procedure uspRollbackFromProc;  
Go  
DROP ASSEMBLY TestProcs;  
Go  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Integrazione con CLR e transazioni](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
