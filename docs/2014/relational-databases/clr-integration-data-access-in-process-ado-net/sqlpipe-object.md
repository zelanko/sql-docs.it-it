---
title: Oggetto SqlPipe | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: bcf462f82d7455f83bb0bee8a3b0af991ec2e7db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62920058"
---
# <a name="sqlpipe-object"></a>Oggetto SqlPipe
  Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è molto comune scrivere una stored procedure (o una stored procedure estesa) per l'invio di risultati o parametri di output al client chiamante.  
  
 In una stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] qualsiasi istruzione `SELECT` che restituisce zero o più righe invia i risultati alla "pipe" del chiamante connesso.  
  
 Per gli oggetti di database CLR (Common Language Runtime) in esecuzione in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è possibile inviare i risultati alla pipe connessa utilizzando i metodi `Send` dell'oggetto `SqlPipe`. Accedere alla proprietà `Pipe` dell'oggetto `SqlContext` per ottenere l'oggetto `SqlPipe`. Concettualmente la classe `SqlPipe` è simile alla classe `Response` di ASP.NET. Per ulteriori informazioni, vedere documentazione di riferimento per la classe SqlPipe in .NET Framework SDK (Software Development Kit).  
  
## <a name="returning-tabular-results-and-messages"></a>Restituzione di risultati tabulari e messaggi  
 L'oggetto `SqlPipe` dispone di un metodo `Send` che presenta tre overload, Sono:  
  
-   `void Send(string message)`  
  
-   `void Send(SqlDataReader reader)`  
  
-   `void Send(SqlDataRecord record)`  
  
 Il metodo `Send` invia dati direttamente al client o al chiamante. In genere è il client che utilizza l'output proveniente dal metodo `SqlPipe`, ma nel caso di stored procedure CLR nidificate il consumer dell'output può anche essere una stored procedure. Procedure1 chiama ad esempio SqlCommand.ExecuteReader() con il testo del comando "EXEC Procedure2". Procedure2 è anche una stored procedure gestita. Se Procedure2 chiama il metodo SqlPipe.Send(SqlDataRecord), la riga verrà inviata al lettore di Procedure1, non al client.  
  
 Il metodo `Send` invia un messaggio stringa che viene visualizzato sul client come messaggio informativo, equivalente a PRINT in [!INCLUDE[tsql](../../includes/tsql-md.md)]. Può inoltre inviare un set di risultati a riga singola utilizzando `SqlDataRecord` o un set di risultati a più righe utilizzando `SqlDataReader`.  
  
 L'oggetto `SqlPipe` include inoltre un metodo `ExecuteAndSend`. Questo metodo può essere utilizzato per eseguire un comando (passato come oggetto `SqlCommand`) e per restituire i risultati direttamente al chiamante. Se sono presenti errori nel comando inviato, le eccezioni vengono inviate alla pipe, ma una copia viene inviata anche al codice gestito chiamante. Se il codice chiamante non rileva l'eccezione, lo stack verrà propagato al codice [!INCLUDE[tsql](../../includes/tsql-md.md)] e verrà visualizzato due volte nell'output. Se il codice chiamante rileva l'eccezione, il consumer della pipe visualizzerà l'errore, ma questo non verrà duplicato.  
  
 Il metodo può utilizzare solo un comando `SqlCommand` associato alla connessione con contesto e non un comando associato alla connessione senza contesto.  
  
## <a name="returning-custom-result-sets"></a>Restituzione di set di risultati personalizzati  
 Le stored procedure gestite possono inviare set di risultati che non provengono da un oggetto `SqlDataReader`. Il metodo `SendResultsStart`, insieme ai metodi `SendResultsRow` e `SendResultsEnd`, consente alle stored procedure di inviare set di risultati personalizzati al client.  
  
 
  `SendResultsStart` utilizza un oggetto `SqlDataRecord` come input. Indica l'inizio di un set di risultati e utilizza i metadati del record per costruire i metadati che descrivono il set in questione. Non invia il valore del record con `SendResultsStart`. Tutte le righe successive, inviate mediante il metodo `SendResultsRow`, dovranno corrispondere alla specifica definizione dei metadati.  
  
> [!NOTE]  
>  Dopo la chiamata al metodo `SendResultsStart`, è possibile chiamare solo `SendResultsRow` e `SendResultsEnd`. La chiamata di qualsiasi altro metodo nella stessa istanza di `SqlPipe` provoca una `InvalidOperationException`. 
  `SendResultsEnd` imposta `SqlPipe` di nuovo nello stato iniziale nel quale possono essere chiamati gli altri metodi.  
  
### <a name="example"></a>Esempio  
 La stored procedure `uspGetProductLine` restituisce il nome, il numero di prodotto, il colore e il prezzo di listino di tutti i prodotti di una linea dei prodotti specificata. Questo stored procedure accetta corrispondenze esatte per *prodLine*.  
  
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
  
 Nell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente viene eseguita la procedura `uspGetProduct` che restituisce un elenco di biciclette da passeggio.  
  
```  
EXEC uspGetProductLineVB 'T';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto SqlDataRecord](sqldatarecord-object.md)   
 [Stored procedure CLR](../../database-engine/dev-guide/clr-stored-procedures.md)   
 [Estensioni specifiche in-process di SQL Server ad ADO.NET](sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
