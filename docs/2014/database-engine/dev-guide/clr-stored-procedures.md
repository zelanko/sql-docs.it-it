---
title: Stored procedure CLR | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- database objects [CLR integration], stored procedures
- stored procedures [CLR integration]
- common language runtime [SQL Server], stored procedures
- building database objects [CLR integration], stored procedures
- output parameters [CLR integration]
- tabular results
ms.assetid: bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9f509b2a2544c67c9113bc700b7d98bfd4a24024
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62753819"
---
# <a name="clr-stored-procedures"></a>Stored procedure CLR
  Le stored procedure sono routine che non possono essere utilizzate in espressioni scalari. Diversamente dalle funzioni scalari, possono restituire risultati tabulari e messaggi al client, richiamare istruzioni DDL (Data Definition Language) e DML (Data Manipulation Language) e restituire parametri di output. Per informazioni sui vantaggi dell'integrazione con CLR e sulla scelta tra codice gestito [!INCLUDE[tsql](../../includes/tsql-md.md)]e, vedere [Cenni preliminari sull'integrazione con CLR](../../relational-databases/clr-integration/clr-integration-overview.md).  
  
## <a name="requirements-for-clr-stored-procedures"></a>Requisiti per le stored procedure CLR  
 Nel Common Language Runtime (CLR), le stored procedure vengono implementate come metodi statici pubblici su una classe in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] un assembly. Il metodo statico può essere dichiarato come void o restituisce un valore integer. Se restituisce un valore integer, il numero intero restituito viene considerato come codice restituito dalla procedura. Ad esempio:  
  
 `EXECUTE @return_status = procedure_name`  
  
 La @return_status variabile conterrà il valore restituito dal metodo. Se il metodo viene dichiarato come void, il codice restituito è 0.  
  
 Se il metodo accetta parametri, il numero di parametri nell'implementazione di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] deve coincidere con il numero di parametri utilizzato nella dichiarazione [!INCLUDE[tsql](../../includes/tsql-md.md)] della stored procedure.  
  
 I parametri passati a una stored procedure possono essere di uno dei tipi nativi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per cui è presente un equivalente nel codice gestito. Affinché la sintassi [!INCLUDE[tsql](../../includes/tsql-md.md)] crei la procedura, questi tipi devono essere specificati con l'equivalente più appropriato del tipo nativo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per ulteriori informazioni sulle conversioni di tipi, vedere [mapping dei dati dei parametri CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).  
  
### <a name="table-valued-parameters"></a>Parametri con valori di tabella  
 I parametri con valori di tabella, ovvero tipi di tabella definiti dall'utente passati in una procedura o in una funzione, consentono di passare in modo efficiente più righe di dati al server. Pur essendo caratterizzati da funzionalità simili alle matrici di parametri, i parametri con valori di tabella offrono più flessibilità e una maggiore integrazione con [!INCLUDE[tsql](../../includes/tsql-md.md)] Consentono inoltre di ottenere prestazioni potenzialmente migliori. I parametri con valori di tabella consentono inoltre di ridurre il numero di round trip al server. Anziché inviare più richieste al server, ad esempio con un elenco di parametri scalari, è possibile inviare i dati al server sotto forma di parametro con valori di tabella. Un tipo di tabella definito dall'utente non può essere passato come parametro con valori di tabella a una stored procedure gestita o a una funzione in esecuzione nel processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], né può essere restituito dalle stesse. Per altre informazioni su TVP, vedere [usare i parametri con valori di tabella &#40;motore di database&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
## <a name="returning-results-from-clr-stored-procedures"></a>Restituzione di risultati da stored procedure CLR  
 Le informazioni possono essere restituite in diversi modi dalle stored procedure [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], ad esempio come parametri di output, risultati tabulari e messaggi.  
  
### <a name="output-parameters-and-clr-stored-procedures"></a>Parametri di output e stored procedure CLR  
 Analogamente alle stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)], le informazioni possono essere restituite dalle stored procedure [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] utilizzando parametri OUTPUT. La sintassi DML di [!INCLUDE[tsql](../../includes/tsql-md.md)] utilizzata per la creazione di stored procedure [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] è la stessa utilizzata per la creazione di stored procedure scritte in [!INCLUDE[tsql](../../includes/tsql-md.md)]. Il parametro corrispondente nel codice di implementazione nella classe [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] deve utilizzare un parametro di passaggio per riferimento come argomento. Si noti che Visual Basic non supporta parametri di output nello stesso modo in cui tali parametri sono supportati in Visual C#. È necessario specificare il parametro per riferimento e applicare l' \<attributo out () > per rappresentare un parametro di output, come nell'esempio seguente:  
  
```  
Imports System.Runtime.InteropServices  
...  
Public Shared Sub PriceSum ( <Out()> ByRef value As SqlInt32)  
```  
  
 Nell'esempio seguente viene illustrata una stored procedure che restituisce informazioni tramite un parametro OUTPUT:  
  
 C#  
  
```  
using System;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void PriceSum(out SqlInt32 value)  
   {  
      using(SqlConnection connection = new SqlConnection("context connection=true"))   
      {  
         value = 0;  
         connection.Open();  
         SqlCommand command = new SqlCommand("SELECT Price FROM Products", connection);  
         SqlDataReader reader = command.ExecuteReader();  
  
         using (reader)  
         {  
            while( reader.Read() )  
            {  
               value += reader.GetSqlInt32(0);  
            }  
         }           
      }  
   }  
}  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
Imports System.Runtime.InteropServices  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Executes a query and iterates over the results to perform a summation.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub PriceSum( <Out()> ByRef value As SqlInt32)  
  
        Using connection As New SqlConnection("context connection=true")  
           value = 0  
           Connection.Open()  
           Dim command As New SqlCommand("SELECT Price FROM Products", connection)  
           Dim reader As SqlDataReader  
           reader = command.ExecuteReader()  
  
           Using reader  
              While reader.Read()  
                 value += reader.GetSqlInt32(0)  
              End While  
           End Using  
        End Using          
    End Sub  
End Class  
```  
  
 Dopo che l'assembly contenente il stored procedure CLR precedente è stato compilato e creato nel server, per creare [!INCLUDE[tsql](../../includes/tsql-md.md)] la stored procedure nel database viene utilizzato il codice seguente e viene specificato *Sum* come parametro di output.  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
-- if StoredProcedures class was inside a namespace, called MyNS,  
-- you would use:  
-- AS EXTERNAL NAME TestStoredProc.[MyNS.StoredProcedures].PriceSum  
```  
  
 Si noti *che Sum* viene dichiarato come `int` tipo di dati SQL Server e che il parametro *value* definito nel stored procedure CLR viene specificato come tipo di `SqlInt32` dati CLR. Quando un programma chiamante esegue la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stored procedure CLR, converte automaticamente il `SqlInt32` tipo di dati CLR in un `int` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati.  Per ulteriori informazioni sui tipi di dati CLR che possono e non possono essere convertiti, vedere [mapping dei dati dei parametri CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).  
  
### <a name="returning-tabular-results-and-messages"></a>Restituzione di risultati tabulari e messaggi  
 La restituzione di risultati tabulari e messaggi al client viene eseguita tramite l'oggetto `SqlPipe`, ottenuto tramite la proprietà `Pipe` della classe `SqlContext`. L'oggetto `SqlPipe` include un metodo `Send`. Chiamando il metodo `Send`, è possibile trasmettere dati tramite la pipe all'applicazione chiamante.  
  
 Sono disponibili diversi overload del metodo `SqlPipe.Send`, incluso uno che invia un oggetto `SqlDataReader` e un altro che invia semplicemente una stringa di testo.  
  
###### <a name="returning-messages"></a>Restituzione di messaggi  
 Utilizzare `SqlPipe.Send(string)` per inviare messaggi all'applicazione client. Il testo del messaggio ha un limite di 8000 caratteri. Se il messaggio supera 8000 caratteri, verrà troncato.  
  
###### <a name="returning-tabular-results"></a>Restituzione di risultati tabulari  
 Per inviare i risultati di una query direttamente al client, utilizzare uno degli overload del metodo `Execute` sull'oggetto `SqlPipe`. Si tratta della soluzione più efficiente per restituire risultati al client, in quanto i dati vengono trasferiti ai buffer di rete senza essere copiati nella memoria gestita. Ad esempio:  
  
 [C#]  
  
```  
using System;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   /// <summary>  
   /// Execute a command and send the results to the client directly.  
   /// </summary>  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void ExecuteToClient()  
   {  
   using(SqlConnection connection = new SqlConnection("context connection=true"))   
   {  
      connection.Open();  
      SqlCommand command = new SqlCommand("select @@version", connection);  
      SqlContext.Pipe.ExecuteAndSend(command);  
      }  
   }  
}  
```  
  
 [Visual Basic]  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Execute a command and send the results to the client directly.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub ExecuteToClient()  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT @@VERSION", connection)  
            SqlContext.Pipe.ExecuteAndSend(command)  
        End Using  
    End Sub  
End Class  
```  
  
 Per inviare i risultati di una query eseguita in precedenza tramite il provider in-process, o per pre-elaborare i dati utilizzando un'implementazione personalizzata di `SqlDataReader`, utilizzare l'overload del metodo `Send` che accetta un oggetto `SqlDataReader`. Questo metodo è leggermente più lento del metodo diretto descritto in precedenza, ma offre una maggiore flessibilità per modificare i dati prima di inviarli al client.  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   /// <summary>  
   /// Execute a command and send the resulting reader to the client  
   /// </summary>  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void SendReaderToClient()  
   {  
      using(SqlConnection connection = new SqlConnection("context connection=true"))   
      {  
         connection.Open();  
         SqlCommand command = new SqlCommand("select @@version", connection);  
         SqlDataReader r = command.ExecuteReader();  
         SqlContext.Pipe.Send(r);  
      }  
   }  
}  
```  
  
 [Visual Basic]  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Execute a command and send the results to the client directly.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub SendReaderToClient()  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT @@VERSION", connection)  
            Dim reader As SqlDataReader  
            reader = command.ExecuteReader()  
            SqlContext.Pipe.Send(reader)  
        End Using  
    End Sub  
End Class  
```  
  
 Per creare un set di risultati dinamico, popolarlo e inviarlo al client, è possibile creare record dalla connessione corrente e inviarli tramite `SqlPipe.Send`.  
  
```csharp  
using System.Data;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
using System.Data.SqlTypes;  
  
public class StoredProcedures   
{  
   /// <summary>  
   /// Create a result set on the fly and send it to the client.  
   /// </summary>  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void SendTransientResultSet()  
   {  
      // Create a record object that represents an individual row, including it's metadata.  
      SqlDataRecord record = new SqlDataRecord(new SqlMetaData("stringcol", SqlDbType.NVarChar, 128));  
  
      // Populate the record.  
      record.SetSqlString(0, "Hello World!");  
  
      // Send the record to the client.  
      SqlContext.Pipe.Send(record);  
   }  
}  
```  
  
 [Visual Basic]  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Create a result set on the fly and send it to the client.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub SendTransientResultSet()  
        ' Create a record object that represents an individual row, including it's metadata.  
        Dim record As New SqlDataRecord(New SqlMetaData("stringcol", SqlDbType.NVarChar, 128) )  
  
        ' Populate the record.  
        record.SetSqlString(0, "Hello World!")  
  
        ' Send the record to the client.  
        SqlContext.Pipe.Send(record)          
    End Sub  
End Class   
```  
  
 Di seguito viene fornito un esempio di invio di un risultato tabulare e di un messaggio tramite `SqlPipe`.  
  
```csharp  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void HelloWorld()  
   {  
      SqlContext.Pipe.Send("Hello world! It's now " + System.DateTime.Now.ToString()+"\n");  
      using(SqlConnection connection = new SqlConnection("context connection=true"))   
      {  
         connection.Open();  
         SqlCommand command = new SqlCommand("SELECT ProductNumber FROM ProductMaster", connection);  
         SqlDataReader reader = command.ExecuteReader();  
         SqlContext.Pipe.Send(reader);  
      }  
   }  
}  
```  
  
 [Visual Basic]  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Execute a command and send the results to the client directly.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub HelloWorld()  
        SqlContext.Pipe.Send("Hello world! It's now " & System.DateTime.Now.ToString() & "\n")  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT ProductNumber FROM ProductMaster", connection)  
            Dim reader As SqlDataReader  
            reader = command.ExecuteReader()  
            SqlContext.Pipe.Send(reader)  
        End Using  
    End Sub  
End Class   
```  
  
 Il primo metodo `Send` invia un messaggio al client, mentre il secondo invia un risultato tabulare tramite `SqlDataReader`.  
  
 Si noti che questi esempi vengono forniti esclusivamente a scopo illustrativo. Le funzioni CLR sono più appropriate rispetto alle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] semplici per le applicazioni che richiedono un elevato carico di elaborazione. Una stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] quasi equivalente all'esempio precedente è la seguente:  
  
```  
CREATE PROCEDURE HelloWorld() AS  
BEGIN  
PRINT('Hello world!')  
SELECT ProductNumber FROM ProductMaster  
END;  
```  
  
> [!NOTE]  
>  Messaggi e set di risultati vengono recuperati in modo diverso nell'applicazione client. I set di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] risultati, ad esempio, vengono visualizzati nella visualizzazione **risultati** e i messaggi vengono visualizzati nel riquadro **messaggi** .  
  
 Se il codice di Visual C# precedente viene salvato in un file MyFirstUdp.cs e compilato con:  
  
```  
csc /t:library /out:MyFirstUdp.dll MyFirstUdp.cs   
```  
  
 O se il codice di Visual Basic precedente viene salvato in un file MyFirstUdp.cs e compilato con:  
  
```  
vbc /t:library /out:MyFirstUdp.dll MyFirstUdp.vb   
```  
  
> [!NOTE]  
>  A partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], l'esecuzione di oggetti di database Visual C++, ad esempio le stored procedure, compilati con `/clr:pure` non è più supportata.  
  
 L'assembly risultante può essere registrato e il punto di ingresso richiamato utilizzando l'istruzione DDL seguente:  
  
```  
CREATE ASSEMBLY MyFirstUdp FROM 'C:\Programming\MyFirstUdp.dll';  
CREATE PROCEDURE HelloWorld  
AS EXTERNAL NAME MyFirstUdp.StoredProcedures.HelloWorld;  
EXEC HelloWorld;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni CLR definite dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [Tipi CLR definiti dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Trigger CLR](../../../2014/database-engine/dev-guide/clr-triggers.md)  
  
  
