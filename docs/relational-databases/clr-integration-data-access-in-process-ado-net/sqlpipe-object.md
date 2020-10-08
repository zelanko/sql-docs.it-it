---
title: Oggetto SqlPipe | Microsoft Docs
description: Per gli oggetti di database CLR in esecuzione in SQL Server, è possibile inviare risultati alla pipe connessa utilizzando i metodi Send dell'oggetto SqlPipe.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- custom result sets [CLR integration]
- SqlPipe object
- tabular results
ms.assetid: 3e090faf-085f-4c01-a565-79e3f1c36e3b
author: rothja
ms.author: jroth
ms.openlocfilehash: 66b5478f23d771d9aa65f98f4bc7f29bcf885b25
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810865"
---
# <a name="sqlpipe-object"></a>Oggetto SqlPipe
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è molto comune scrivere una stored procedure (o una stored procedure estesa) per l'invio di risultati o parametri di output al client chiamante.  
  
 In una [!INCLUDE[tsql](../../includes/tsql-md.md)] stored procedure, tutte le istruzioni **SELECT** che restituiscono zero o più righe inviano i risultati alla "pipe" del chiamante connesso.  
  
 Per gli oggetti di database Common Language Runtime (CLR) in esecuzione in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è possibile inviare risultati alla pipe connessa utilizzando i metodi **Send** dell'oggetto **SqlPipe** . Accedere alla proprietà **pipe** dell'oggetto **SqlContext** per ottenere l'oggetto **SqlPipe** . La classe **SqlPipe** è concettualmente simile alla classe **Response** disponibile in ASP.NET. Per ulteriori informazioni, vedere documentazione di riferimento per la classe SqlPipe in .NET Framework SDK (Software Development Kit).  
  
## <a name="returning-tabular-results-and-messages"></a>Restituzione di risultati tabulari e messaggi  
 **SqlPipe** ha un metodo **Send** , che presenta tre overload. ovvero:  
  
-   `void Send(string message)`  
  
-   `void Send(SqlDataReader reader)`  
  
-   `void Send(SqlDataRecord record)`  
  
 Il metodo **Send** invia i dati direttamente al client o al chiamante. Si tratta in genere del client che utilizza l'output di **SqlPipe**, ma nel caso di stored procedure CLR nidificate, il consumer di output può essere anche un stored procedure. Procedure1 chiama ad esempio SqlCommand.ExecuteReader() con il testo del comando "EXEC Procedure2". Procedure2 è anche una stored procedure gestita. Se Procedure2 chiama il metodo SqlPipe.Send(SqlDataRecord), la riga verrà inviata al lettore di Procedure1, non al client.  
  
 Il metodo **Send** Invia un messaggio stringa che viene visualizzato sul client come messaggio informativo, equivalente a Print in [!INCLUDE[tsql](../../includes/tsql-md.md)] . Può inoltre inviare un set di risultati a riga singola utilizzando **SqlDataRecord**o un set di risultati con più righe utilizzando un oggetto **SqlDataReader**.  
  
 L'oggetto **SqlPipe** dispone anche di un metodo **ExecuteAndSend** . Questo metodo può essere utilizzato per eseguire un comando (passato come oggetto **SqlCommand** ) e restituire i risultati direttamente al chiamante. Se sono presenti errori nel comando inviato, le eccezioni vengono inviate alla pipe, ma una copia viene inviata anche al codice gestito chiamante. Se il codice chiamante non rileva l'eccezione, lo stack verrà propagato al codice [!INCLUDE[tsql](../../includes/tsql-md.md)] e verrà visualizzato due volte nell'output. Se il codice chiamante rileva l'eccezione, il consumer della pipe visualizzerà l'errore, ma questo non verrà duplicato.  
  
 Può solo assumere un **SqlCommand** associato alla connessione di contesto. non è possibile eseguire un comando associato alla connessione non di contesto.  
  
## <a name="returning-custom-result-sets"></a>Restituzione di set di risultati personalizzati  
 Le stored procedure gestite possono inviare set di risultati che non provengono da un oggetto **SqlDataReader**. Il metodo **SendResultsStart** , insieme a **SendResultsRow** e **SendResultsEnd**, consente alle stored procedure di inviare set di risultati personalizzati al client.  
  
 **SendResultsStart** accetta un oggetto **SqlDataRecord** come input. Indica l'inizio di un set di risultati e utilizza i metadati del record per costruire i metadati che descrivono il set in questione. Non invia il valore del record con **SendResultsStart**. Tutte le righe successive, inviate utilizzando **SendResultsRow**, devono corrispondere alla definizione dei metadati.  
  
> [!NOTE]  
>  Dopo aver chiamato il metodo **SendResultsStart** , è possibile chiamare solo **SendResultsRow** e **SendResultsEnd** . La chiamata di qualsiasi altro metodo nella stessa istanza di **SqlPipe** causa un' **eccezione InvalidOperationException**. **SendResultsEnd** imposta **SqlPipe** nuovamente sullo stato iniziale in cui è possibile chiamare altri metodi.  
  
### <a name="example"></a>Esempio  
 Il stored procedure **uspGetProductLine** restituisce il nome, il numero di prodotto, il colore e il prezzo di listino di tutti i prodotti all'interno di una linea di prodotti specificata. Questo stored procedure accetta corrispondenze esatte per *prodLine*.  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
  
public partial class StoredProcedures  
{  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void uspGetProductLine(SqlString prodLine)  
{  
    // Connect through the context connection.  
    using (SqlConnection connection = new SqlConnection("context connection=true"))  
    {  
        connection.Open();  
  
        SqlCommand command = new SqlCommand(  
            "SELECT Name, ProductNumber, Color, ListPrice " +  
            "FROM Production.Product " +   
            "WHERE ProductLine = @prodLine;", connection);  
  
        command.Parameters.AddWithValue("@prodLine", prodLine);  
  
        try  
        {  
            // Execute the command and send the results to the caller.  
            SqlContext.Pipe.ExecuteAndSend(command);  
        }  
        catch (System.Data.SqlClient.SqlException ex)  
        {  
            // An error occurred executing the SQL command.  
        }  
     }  
}  
};  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Partial Public Class StoredProcedures  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub uspGetProductLine(ByVal prodLine As SqlString)  
    Dim command As SqlCommand  
  
    ' Connect through the context connection.  
    Using connection As New SqlConnection("context connection=true")  
        connection.Open()  
  
        command = New SqlCommand( _  
        "SELECT Name, ProductNumber, Color, ListPrice " & _  
        "FROM Production.Product " & _  
        "WHERE ProductLine = @prodLine;", connection)  
        command.Parameters.AddWithValue("@prodLine", prodLine)  
  
        Try  
            ' Execute the command and send the results   
            ' directly to the caller.  
            SqlContext.Pipe.ExecuteAndSend(command)  
        Catch ex As System.Data.SqlClient.SqlException  
            ' An error occurred executing the SQL command.  
        End Try  
    End Using  
End Sub  
End Class  
```  
  
 Nell' [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione seguente viene eseguita la procedura **uspGetProduct** , che restituisce un elenco di prodotti Touring bike.  
  
```  
EXEC uspGetProductLineVB 'T';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto SqlDataRecord](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqldatarecord-object.md)   
 [Stored procedure CLR](/dotnet/framework/data/adonet/sql/clr-stored-procedures)   
 [Estensioni specifiche in-process di SQL Server ad ADO.NET](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
