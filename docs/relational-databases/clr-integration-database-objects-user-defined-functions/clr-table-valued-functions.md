---
title: Le funzioni con valori di tabella CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- Transact-SQL table-valued functions
- table-valued functions [CLR integration]
- TVFs [CLR integration]
ms.assetid: 9a6133ea-36e9-45bf-b572-1c0df3d6c194
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 97ad8e64260d337135a1b0d5cda739d8c81b1799
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62707139"
---
# <a name="clr-table-valued-functions"></a>Funzioni CLR con valori di tabella
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Una funzione con valori di tabella è una funzione definita dall'utente che restituisce una tabella.  
  
 A partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estende la funzionalità delle funzioni con valori di tabella consentendo la definizione di una funzione di questo tipo in qualsiasi linguaggio gestito. Vengono restituiti dati da una funzione con valori di tabella tramite un **IEnumerable** oppure **IEnumerator** oggetto.  
  
> [!NOTE]  
>  Per le funzioni con valori di tabella, le colonne del tipo di tabella restituito non possono includere colonne timestamp o colonne di tipo di dati stringa non Unicode (ad esempio **char**, **varchar**, e **testo**). Il vincolo NOT NULL non è supportato.  
  
 Per altre informazioni sulle funzioni con valori di tabella CLR, vedere 'MSSQLTips [Introduzione a CLR di SQL Server funzioni con valori di tabella.](https://www.mssqltips.com/sqlservertip/2582/introduction-to-sql-server-clr-table-valued-functions/)  
  
## <a name="differences-between-transact-sql-and-clr-table-valued-functions"></a>Differenze tra funzioni con valori di tabella CLR e Transact-SQL  
 Le funzioni con valori di tabella [!INCLUDE[tsql](../../includes/tsql-md.md)] materializzano i risultati della chiamata alla funzione in una tabella intermedia. Poiché utilizzano una tabella intermedia, possono supportare vincoli e indici univoci sui risultati. Queste caratteristiche possono rivelarsi estremamente utili quando vengono restituiti risultati di grandi dimensioni.  
  
 Le funzioni con valori di tabella CLR rappresentano invece un modello di flusso alternativo. Non è necessario che l'intero set di risultati venga materializzato in una singola tabella. Il **IEnumerable** oggetto restituito dalla funzione gestita viene chiamato direttamente dal piano di esecuzione della query che chiama la funzione con valori di tabella e i risultati vengono utilizzati in modo incrementale. Questo modello di flusso consente di utilizzare i risultati non appena è disponibile la prima riga invece di dover attendere il popolamento dell'intera tabella. Rappresenta inoltre un'alternativa migliore in presenza di grandi quantità di righe restituite, in quanto non devono essere materializzate interamente in memoria. Una funzione con valori di tabella gestita, ad esempio, può essere utilizzata per analizzare un file di testo e restituire ogni riga del file come riga di tabella.  
  
## <a name="implementing-table-valued-functions"></a>Implementazione di funzioni con valori di tabella  
 È possibile implementare funzioni con valori di tabella come metodi di una classe in un assembly [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework. Il codice della funzione con valori di tabella deve implementare il **IEnumerable** interfaccia. Il **IEnumerable** interfaccia sia definita in .NET Framework. Tipi che rappresentano matrici e raccolte in .NET Framework già implementa il **IEnumerable** interfaccia. Questo semplifica la scrittura di funzioni con valori di tabella che convertono una raccolta o una matrice in un set di risultati.  
  
## <a name="table-valued-parameters"></a>Parametri con valori di tabella  
 I parametri con valori di tabella sono tipi di tabella definiti dall'utente passati in una procedura o in una funzione che consentono di passare in modo efficiente più righe di dati al server. I parametri con valori di tabella offrono funzionalità simili a quelle delle matrici di parametri, ma garantiscono più flessibilità e una maggiore integrazione con [!INCLUDE[tsql](../../includes/tsql-md.md)]. Consentono inoltre di ottenere prestazioni potenzialmente migliori. I parametri con valori di tabella aiutano anche a ridurre il numero di round trip al server. Anziché inviare più richieste al server, ad esempio con un elenco di parametri scalari, è possibile inviare i dati al server sotto forma di parametro con valori di tabella. Un tipo di tabella definito dall'utente non può essere passato come parametro con valori di tabella a una stored procedure gestita o a una funzione in esecuzione nel processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], né può essere restituito dalle stesse. Per altre informazioni sui parametri con valori di tabella, vedere [Usare parametri con valori di tabella &#40;motore di database&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
## <a name="output-parameters-and-table-valued-functions"></a>Parametri di output e funzioni con valori di tabella  
 Le funzioni con valori di tabella possono restituire le informazioni tramite parametri di output. Il parametro corrispondente nella funzione con valori di tabella nel codice di implementazione deve utilizzare un parametro di passaggio per riferimento come argomento. Si noti che Visual Basic non supporta parametri di output nello stesso modo in cui tali parametri sono supportati in Visual C#. È necessario specificare il parametro per riferimento e applicare il \<out () > attributo per rappresentare un parametro di output, come illustrato di seguito:  
  
```vb  
Imports System.Runtime.InteropServices  
...  
Public Shared Sub FillRow ( <Out()> ByRef value As SqlInt32)  
```  
  
### <a name="defining-a-table-valued-function-in-transact-sql"></a>Definizione di una funzione con valori di tabella in Transact-SQL  
 La sintassi per la definizione di una funzione con valori di tabella CLR è simile a quella di un [!INCLUDE[tsql](../../includes/tsql-md.md)] funzione con valori di tabella, con l'aggiunta del **EXTERNAL NAME** clausola. Ad esempio:   
  
```  
CREATE FUNCTION GetEmpFirstLastNames()  
RETURNS TABLE (FirstName NVARCHAR(4000), LastName NVARCHAR(4000))  
EXTERNAL NAME MyDotNETAssembly.[MyNamespace.MyClassname]. GetEmpFirstLastNames;  
```  
  
 Le funzioni con valori di tabella vengono utilizzate per rappresentare i dati in formato relazionale per un'ulteriore elaborazione nelle query, come nell'esempio seguente:  
  
```  
select * from function();  
select * from tbl join function() f on tbl.col = f.col;  
select * from table t cross apply function(t.column);  
```  
  
 Le funzioni con valori di tabella possono restituire una tabella nei casi seguenti:  
  
-   Vengono create da argomenti di input scalari. Una funzione con valori di tabella che utilizza, ad esempio, una stringa di numeri delimitati da virgole e trasforma i numeri in tabella tramite Pivot.  
  
-   Vengono generate da dati esterni. Una funzione con valori di tabella che legge, ad esempio, il log eventi e lo espone come tabella.  
  
 **Nota** una funzione con valori di tabella può eseguire solo l'accesso ai dati tramite un [!INCLUDE[tsql](../../includes/tsql-md.md)] eseguire una query nella **InitMethod** metodo e non nel **FillRow** (metodo). Il **InitMethod** devono essere contrassegnati con la **SqlFunction.DataAccess.Read** proprietà dell'attributo se un [!INCLUDE[tsql](../../includes/tsql-md.md)] query viene eseguita.  
  
## <a name="a-sample-table-valued-function"></a>Funzione con valori di tabella di esempio  
 La funzione con valori di tabella seguente restituisce informazioni dal registro eventi di sistema. La funzione accetta un singolo argomento stringa contenente il nome del registro eventi da leggere.  
  
###### <a name="sample-code"></a>Codice di esempio  
  
```csharp  
using System;  
using System.Data.Sql;  
using Microsoft.SqlServer.Server;  
using System.Collections;  
using System.Data.SqlTypes;  
using System.Diagnostics;  
  
public class TabularEventLog  
{  
    [SqlFunction(FillRowMethodName = "FillRow")]  
    public static IEnumerable InitMethod(String logname)  
    {  
        return new EventLog(logname).Entries;    }  
  
    public static void FillRow(Object obj, out SqlDateTime timeWritten, out SqlChars message, out SqlChars category, out long instanceId)  
    {  
        EventLogEntry eventLogEntry = (EventLogEntry)obj;  
        timeWritten = new SqlDateTime(eventLogEntry.TimeWritten);  
        message = new SqlChars(eventLogEntry.Message);  
        category = new SqlChars(eventLogEntry.Category);  
        instanceId = eventLogEntry.InstanceId;  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data.Sql  
Imports Microsoft.SqlServer.Server  
Imports System.Collections  
Imports System.Data.SqlTypes  
Imports System.Diagnostics  
Imports System.Runtime.InteropServices  
  
Public Class TabularEventLog  
    <SqlFunction(FillRowMethodName:="FillRow")> _  
    Public Shared Function InitMethod(ByVal logname As String) As IEnumerable  
        Return New EventLog(logname).Entries  
    End Function  
  
    Public Shared Sub FillRow(ByVal obj As Object, <Out()> ByRef timeWritten As SqlDateTime, <Out()> ByRef message As SqlChars, <Out()> ByRef category As SqlChars, <Out()> ByRef instanceId As Long)  
        Dim eventLogEnTry As EventLogEntry = CType(obj, EventLogEntry)  
        timeWritten = New SqlDateTime(eventLogEnTry.TimeWritten)  
        message = New SqlChars(eventLogEnTry.Message)  
        category = New SqlChars(eventLogEnTry.Category)  
        instanceId = eventLogEnTry.InstanceId  
    End Sub  
End Class  
```  
  
###### <a name="declaring-and-using-the-sample-table-valued-function"></a>Dichiarazione e utilizzo della funzione con valori di tabella di esempio  
 Dopo che la funzione con valori di tabella è stata compilata, può essere dichiarata in [!INCLUDE[tsql](../../includes/tsql-md.md)] nel modo seguente:  
  
```  
use master;  
-- Replace SQL_Server_logon with your SQL Server user credentials.  
GRANT EXTERNAL ACCESS ASSEMBLY TO [SQL_Server_logon];   
-- Modify the following line to specify a different database.  
ALTER DATABASE master SET TRUSTWORTHY ON;  
  
-- Modify the next line to use the appropriate database.  
CREATE ASSEMBLY tvfEventLog   
FROM 'D:\assemblies\tvfEventLog\tvfeventlog.dll'   
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
GO  
CREATE FUNCTION ReadEventLog(@logname nvarchar(100))  
RETURNS TABLE   
(logTime datetime,Message nvarchar(4000),Category nvarchar(4000),InstanceId bigint)  
AS   
EXTERNAL NAME tvfEventLog.TabularEventLog.InitMethod;  
GO  
```  
  
 L'esecuzione degli oggetti di database Visual C++ compilati con /clr:pure non è più supportata in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Tali oggetti di database, ad esempio, includono funzioni con valori di tabella.  
  
 Per testare l'esempio, provare a utilizzare il codice [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente:  
  
```  
-- Select the top 100 events,  
SELECT TOP 100 *  
FROM dbo.ReadEventLog(N'Security') as T;  
go  
  
-- Select the last 10 login events.  
SELECT TOP 10 T.logTime, T.Message, T.InstanceId   
FROM dbo.ReadEventLog(N'Security') as T  
WHERE T.Category = N'Logon/Logoff';  
go  
```  
  
## <a name="sample-returning-the-results-of-a-sql-server-query"></a>Esempio: Restituzione dei risultati di una Query di SQL Server  
 Nell'esempio seguente viene illustrata una funzione con valori di tabella che esegue una query su un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In questo esempio viene utilizzato il database AdventureWorks Light di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Visualizzare [ https://www.codeplex.com/sqlserversamples ](https://go.microsoft.com/fwlink/?LinkId=87843) per altre informazioni sul download di AdventureWorks.  
  
 Assegnare al file di codice sorgente il nome FindInvalidEmails.cs o FindInvalidEmails.vb.  
  
```csharp  
using System;  
using System.Collections;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
  
using Microsoft.SqlServer.Server;  
  
public partial class UserDefinedFunctions {  
   private class EmailResult {  
      public SqlInt32 CustomerId;  
      public SqlString EmailAdress;  
  
      public EmailResult(SqlInt32 customerId, SqlString emailAdress) {  
         CustomerId = customerId;  
         EmailAdress = emailAdress;  
      }  
   }  
  
   public static bool ValidateEmail(SqlString emailAddress) {  
      if (emailAddress.IsNull)  
         return false;  
  
      if (!emailAddress.Value.EndsWith("@adventure-works.com"))  
         return false;  
  
      // Validate the address. Put any more rules here.  
      return true;  
   }  
  
   [SqlFunction(  
       DataAccess = DataAccessKind.Read,  
       FillRowMethodName = "FindInvalidEmails_FillRow",  
       TableDefinition="CustomerId int, EmailAddress nvarchar(4000)")]  
   public static IEnumerable FindInvalidEmails(SqlDateTime modifiedSince) {  
      ArrayList resultCollection = new ArrayList();  
  
      using (SqlConnection connection = new SqlConnection("context connection=true")) {  
         connection.Open();  
  
         using (SqlCommand selectEmails = new SqlCommand(  
             "SELECT " +  
             "[CustomerID], [EmailAddress] " +  
             "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " +  
             "WHERE [ModifiedDate] >= @modifiedSince",  
             connection)) {  
            SqlParameter modifiedSinceParam = selectEmails.Parameters.Add(  
                "@modifiedSince",  
                SqlDbType.DateTime);  
            modifiedSinceParam.Value = modifiedSince;  
  
            using (SqlDataReader emailsReader = selectEmails.ExecuteReader()) {  
               while (emailsReader.Read()) {  
                  SqlString emailAddress = emailsReader.GetSqlString(1);  
                  if (ValidateEmail(emailAddress)) {  
                     resultCollection.Add(new EmailResult(  
                         emailsReader.GetSqlInt32(0),  
                         emailAddress));  
                  }  
               }  
            }  
         }  
      }  
  
      return resultCollection;  
   }  
  
   public static void FindInvalidEmails_FillRow(  
       object emailResultObj,  
       out SqlInt32 customerId,  
       out SqlString emailAdress) {  
      EmailResult emailResult = (EmailResult)emailResultObj;  
  
      customerId = emailResult.CustomerId;  
      emailAdress = emailResult.EmailAdress;  
   }  
};  
```  
  
```vb  
Imports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Public Partial Class UserDefinedFunctions  
   Private Class EmailResult  
      Public CustomerId As SqlInt32  
      Public EmailAdress As SqlString  
  
      Public Sub New(customerId__1 As SqlInt32, emailAdress__2 As SqlString)  
         CustomerId = customerId__1  
         EmailAdress = emailAdress__2  
      End Sub  
   End Class  
  
   Public Shared Function ValidateEmail(emailAddress As SqlString) As Boolean  
      If emailAddress.IsNull Then  
         Return False  
      End If  
  
      If Not emailAddress.Value.EndsWith("@adventure-works.com") Then  
         Return False  
      End If  
  
      ' Validate the address. Put any more rules here.  
      Return True  
   End Function  
  
   <SqlFunction(DataAccess := DataAccessKind.Read, FillRowMethodName := "FindInvalidEmails_FillRow", TableDefinition := "CustomerId int, EmailAddress nvarchar(4000)")> _  
   Public Shared Function FindInvalidEmails(modifiedSince As SqlDateTime) As IEnumerable  
      Dim resultCollection As New ArrayList()  
  
      Using connection As New SqlConnection("context connection=true")  
         connection.Open()  
  
         Using selectEmails As New SqlCommand("SELECT " & "[CustomerID], [EmailAddress] " & "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " & "WHERE [ModifiedDate] >= @modifiedSince", connection)  
            Dim modifiedSinceParam As SqlParameter = selectEmails.Parameters.Add("@modifiedSince", SqlDbType.DateTime)  
            modifiedSinceParam.Value = modifiedSince  
  
            Using emailsReader As SqlDataReader = selectEmails.ExecuteReader()  
               While emailsReader.Read()  
                  Dim emailAddress As SqlString = emailsReader.GetSqlString(1)  
                  If ValidateEmail(emailAddress) Then  
                     resultCollection.Add(New EmailResult(emailsReader.GetSqlInt32(0), emailAddress))  
                  End If  
               End While  
            End Using  
         End Using  
      End Using  
  
      Return resultCollection  
   End Function  
  
   Public Shared Sub FindInvalidEmails_FillRow(emailResultObj As Object, ByRef customerId As SqlInt32, ByRef emailAdress As SqlString)  
      Dim emailResult As EmailResult = DirectCast(emailResultObj, EmailResult)  
  
      customerId = emailResult.CustomerId  
      emailAdress = emailResult.EmailAdress  
   End Sub  
End ClassImports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Public Partial Class UserDefinedFunctions  
   Private Class EmailResult  
      Public CustomerId As SqlInt32  
      Public EmailAdress As SqlString  
  
      Public Sub New(customerId__1 As SqlInt32, emailAdress__2 As SqlString)  
         CustomerId = customerId__1  
         EmailAdress = emailAdress__2  
      End Sub  
   End Class  
  
   Public Shared Function ValidateEmail(emailAddress As SqlString) As Boolean  
      If emailAddress.IsNull Then  
         Return False  
      End If  
  
      If Not emailAddress.Value.EndsWith("@adventure-works.com") Then  
         Return False  
      End If  
  
      ' Validate the address. Put any more rules here.  
      Return True  
   End Function  
  
   <SqlFunction(DataAccess := DataAccessKind.Read, FillRowMethodName := "FindInvalidEmails_FillRow", TableDefinition := "CustomerId int, EmailAddress nvarchar(4000)")> _  
   Public Shared Function FindInvalidEmails(modifiedSince As SqlDateTime) As IEnumerable  
      Dim resultCollection As New ArrayList()  
  
      Using connection As New SqlConnection("context connection=true")  
         connection.Open()  
  
         Using selectEmails As New SqlCommand("SELECT " & "[CustomerID], [EmailAddress] " & "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " & "WHERE [ModifiedDate] >= @modifiedSince", connection)  
            Dim modifiedSinceParam As SqlParameter = selectEmails.Parameters.Add("@modifiedSince", SqlDbType.DateTime)  
            modifiedSinceParam.Value = modifiedSince  
  
            Using emailsReader As SqlDataReader = selectEmails.ExecuteReader()  
               While emailsReader.Read()  
                  Dim emailAddress As SqlString = emailsReader.GetSqlString(1)  
                  If ValidateEmail(emailAddress) Then  
                     resultCollection.Add(New EmailResult(emailsReader.GetSqlInt32(0), emailAddress))  
                  End If  
               End While  
            End Using  
         End Using  
      End Using  
  
      Return resultCollection  
   End Function  
  
   Public Shared Sub FindInvalidEmails_FillRow(emailResultObj As Object, customerId As SqlInt32, emailAdress As SqlString)  
      Dim emailResult As EmailResult = DirectCast(emailResultObj, EmailResult)  
  
      customerId = emailResult.CustomerId  
      emailAdress = emailResult.EmailAdress  
   End Sub  
End Class  
```  
  
 Compilare il codice sorgente in una DLL e copiare la DLL nella directory radice dell'unità C.  Eseguire quindi la query [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente.  
  
```  
use AdventureWorksLT2008;  
go  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'FindInvalidEmails')  
   DROP FUNCTION FindInvalidEmails;  
go  
  
IF EXISTS (SELECT name FROM sys.assemblies WHERE name = 'MyClrCode')  
   DROP ASSEMBLY MyClrCode;  
go  
  
CREATE ASSEMBLY MyClrCode FROM 'C:\FindInvalidEmails.dll'  
WITH PERMISSION_SET = SAFE -- EXTERNAL_ACCESS;  
GO  
  
CREATE FUNCTION FindInvalidEmails(@ModifiedSince datetime)   
RETURNS TABLE (  
   CustomerId int,  
   EmailAddress nvarchar(4000)  
)  
AS EXTERNAL NAME MyClrCode.UserDefinedFunctions.[FindInvalidEmails];  
go  
  
SELECT * FROM FindInvalidEmails('2000-01-01');  
go  
```  
  
  
