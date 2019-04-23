---
title: Trigger CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- inserted tables
- database objects [CLR integration], triggers
- common language runtime [SQL Server], triggers
- updated columns
- building database objects [CLR integration], triggers
- triggers [CLR integration]
- deleted tables
- EventData property
- SqlTriggerContext class
- transactions [CLR integration]
ms.assetid: 302a4e4a-3172-42b6-9cc0-4a971ab49c1c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 87d822e97a75bbd08375980fe6a6f0341d8f9c60
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158537"
---
# <a name="clr-triggers"></a>Trigger CLR
  Grazie all'integrazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con CLR (Common Language Runtime) di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], è possibile utilizzare qualsiasi linguaggio [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] per creare trigger CLR. In questa sezione vengono fornite informazioni specifiche relative ai trigger implementati utilizzando l'integrazione con CLR. Per una descrizione completa dei trigger, vedere [trigger DDL](../../relational-databases/triggers/ddl-triggers.md).  
  
## <a name="what-are-triggers"></a>Definizione dei trigger  
 Un trigger è un tipo speciale di stored procedure che viene eseguita automaticamente quando viene eseguito un evento del linguaggio. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] include due tipi generali di trigger: Data Manipulation Language (DML) e Data Definition Language (DDL). I trigger DML possono essere utilizzati quando l'istruzione `INSERT`, `UPDATE` o `DELETE` modifica i dati in una tabella o in una vista specificata. I trigger DDL attivano stored procedure in risposta a diverse istruzioni DDL, che corrispondono principalmente a istruzioni che iniziano con `CREATE`, `ALTER` e `DROP`. Possono essere utilizzati per attività di amministrazione quali il controllo e la regolazione delle operazioni sul database.  
  
## <a name="unique-capabilities-of-clr-triggers"></a>Funzionalità univoche dei trigger CLR  
 I trigger scritti in [!INCLUDE[tsql](../../includes/tsql-md.md)] consentono di determinare quali colonne della tabella o della vista di attivazione sono state aggiornate mediante le funzioni `UPDATE(column)` e `COLUMNS_UPDATED()`.  
  
 Esistono notevoli differenze tra i trigger scritti in un linguaggio CLR e gli altri oggetti di integrazione con CLR. I trigger CLR possono:  
  
-   Fare riferimento ai dati delle tabelle `INSERTED` e `DELETED`  
  
-   Determinare quali colonne sono state modificate in seguito a un'operazione `UPDATE`  
  
-   Accedere alle informazioni sugli oggetti di database interessati dall'esecuzione di istruzioni DDL.  
  
 Queste funzionalità vengono fornite implicitamente nel linguaggio di query o dalla classe `SqlTriggerContext`. Per informazioni sui vantaggi dell'integrazione con CLR e sulla scelta tra codice gestito e [!INCLUDE[tsql](../../includes/tsql-md.md)], vedere [panoramica dell'integrazione con CLR](../../relational-databases/clr-integration/clr-integration-overview.md).  
  
## <a name="using-the-sqltriggercontext-class"></a>Utilizzo della classe SqlTriggerContext  
 La classe `SqlTriggerContext` non può essere costruita pubblicamente e può essere ottenuta solo accedendo alla proprietà `SqlContext.TriggerContext` all'interno del corpo di un trigger CLR. È possibile ottenere la classe `SqlTriggerContext` dall'oggetto `SqlContext` attivo chiamando la proprietà `SqlContext.TriggerContext`:  
  
 `SqlTriggerContext myTriggerContext = SqlContext.TriggerContext;`  
  
 La classe `SqlTriggerContext` fornisce informazioni sul contesto per il trigger. Tali informazioni includono il tipo di azione che ha provocato l'attivazione del trigger, le colonne modificate in un'operazione UPDATE e, nel caso di un trigger DDL, una struttura XML `EventData` che descrive l'operazione di attivazione del trigger. Per altre informazioni, vedere [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql).  
  
### <a name="determining-the-trigger-action"></a>Determinazione dell'azione trigger  
 Dopo aver ottenuto un `SqlTriggerContext`, è possibile utilizzarlo per determinare il tipo di azione che ha causato l'attivazione del trigger. Queste informazioni sono disponibili mediante la proprietà `TriggerAction` della classe `SqlTriggerContext`.  
  
 Per i trigger DML, la proprietà `TriggerAction` può essere uno dei valori seguenti:  
  
-   TriggerAction.Update (0x1)  
  
-   TriggerAction.Insert (0x2)  
  
-   TriggerAction.Delete (0x3)  
  
-   Per i trigger DDL, l'elenco dei valori TriggerAction possibili è molto più lungo. Per ulteriori informazioni, vedere "Enumerazione TriggerAction" in .NET Framework SDK.  
  
### <a name="using-the-inserted-and-deleted-tables"></a>Utilizzo delle tabelle Inserted e Deleted  
 Nelle istruzioni di trigger DML vengono utilizzate due tabelle speciali: il **inserito** tabella e il **eliminato** tabella. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea e gestisce queste tabelle automaticamente. È possibile utilizzare queste tabelle temporanee per verificare gli effetti di determinate modifiche apportate ai dati e impostare le condizioni per le azioni dei trigger DML. Non è tuttavia possibile modificare direttamente i dati nelle tabelle.  
  
 Trigger CLR possono accedere le **inserito** e **eliminato** tabelle tramite il provider in-process CLR. A tale scopo è necessario ottenere un oggetto `SqlCommand` dall'oggetto SqlContext. Ad esempio:   
  
 C#  
  
```  
SqlConnection connection = new SqlConnection ("context connection = true");  
connection.Open();  
SqlCommand command = connection.CreateCommand();  
command.CommandText = "SELECT * from " + "inserted";  
```  
  
 Visual Basic  
  
```  
Dim connection As New SqlConnection("context connection=true")  
Dim command As SqlCommand  
connection.Open()  
command = connection.CreateCommand()  
command.CommandText = "SELECT * FROM " + "inserted"  
```  
  
### <a name="determining-updated-columns"></a>Determinazione delle colonne aggiornate  
 È possibile determinare il numero di colonne modificate da un'operazione UPDATE tramite la proprietà `ColumnCount` dell'oggetto `SqlTriggerContext`. Il metodo `IsUpdatedColumn`, che accetta il numero ordinale di colonna come parametro di input, consente di determinare se la colonna è stata aggiornata. Il valore `True` indica che la colonna è stata aggiornata.  
  
 Nel frammento di codice seguente, estratto dal trigger EmailAudit riportato più avanti in questo argomento, sono ad esempio elencate tutte le colonne aggiornate:  
  
 C#  
  
```  
reader = command.ExecuteReader();  
reader.Read();  
for (int columnNumber = 0; columnNumber < triggContext.ColumnCount; columnNumber++)  
{  
   pipe.Send("Updated column "  
      + reader.GetName(columnNumber) + "? "  
   + triggContext.IsUpdatedColumn(columnNumber).ToString());  
 }  
  
 reader.Close();  
```  
  
 Visual Basic  
  
```  
reader = command.ExecuteReader()  
reader.Read()  
Dim columnNumber As Integer  
  
For columnNumber=0 To triggContext.ColumnCount-1  
  
   pipe.Send("Updated column " & reader.GetName(columnNumber) & _  
   "? " & triggContext.IsUpdatedColumn(columnNumber).ToString() )  
  
Next  
  
reader.Close()  
```  
  
### <a name="accessing-eventdata-for-clr-ddl-triggers"></a>Accesso a EventData per i trigger CLR DDL  
 I trigger DDL, analogamente ai trigger normali, attivano stored procedure in risposta a un evento. Diversamente dai trigger DML, tuttavia, questi trigger non vengono attivati in risposta a un'istruzione UPDATE, INSERT o DELETE in una tabella o una vista. Tali trigger vengono invece attivati in risposta a diverse istruzioni DDL, che corrispondono principalmente a istruzioni che iniziano con CREATE, ALTER e DROP. I trigger DDL possono essere utilizzati per attività di amministrazione quali il controllo e il monitoraggio delle operazioni sul database e le modifiche di schema.  
  
 Informazioni su un evento che attiva un trigger DDL sono disponibili nella proprietà `EventData` della classe `SqlTriggerContext`. Questa proprietà contiene un valore `xml`. L'elemento XML Schema include informazioni sugli elementi seguenti:  
  
-   Ora dell'evento.  
  
-   ID di processo di sistema (SPID) della connessione durante la quale è stato eseguito il trigger.  
  
-   Tipo di evento che ha attivato il trigger.  
  
 In base al tipo di evento, lo schema include inoltre informazioni aggiuntive quali il database nel quale è stato generato l'evento, l'oggetto per il quale è stato generato l'evento e il comando [!INCLUDE[tsql](../../includes/tsql-md.md)] dell'evento.  
  
 Nell'esempio riportato di seguito il trigger DDL restituisce la proprietà `EventData` non elaborata.  
  
> [!NOTE]  
>  L'invio di risultati e messaggi tramite l'oggetto `SqlPipe` è mostrato solo a scopo illustrativo e in genere se ne sconsiglia l'uso nel codice di produzione durante la programmazione dei trigger CLR. I dati aggiuntivi restituiti potrebbero essere imprevisti e generare errori nell'applicazione.  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.Sql;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Xml;  
using System.Text.RegularExpressions;  
  
public class CLRTriggers  
{  
   public static void DropTableTrigger()  
   {  
       SqlTriggerContext triggContext = SqlContext.TriggerContext;             
  
       switch(triggContext.TriggerAction)  
       {  
           case TriggerAction.DropTable:  
           SqlContext.Pipe.Send("Table dropped! Here's the EventData:");  
           SqlContext.Pipe.Send(triggContext.EventData.Value);  
           break;  
  
           default:  
           SqlContext.Pipe.Send("Something happened! Here's the EventData:");  
           SqlContext.Pipe.Send(triggContext.EventData.Value);  
           break;  
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
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class CLRTriggers   
  
    Public Shared Sub DropTableTrigger()  
        Dim triggContext As SqlTriggerContext  
        triggContext = SqlContext.TriggerContext  
  
        Select Case triggContext.TriggerAction  
           Case TriggerAction.DropTable  
              SqlContext.Pipe.Send("Table dropped! Here's the EventData:")  
              SqlContext.Pipe.Send(triggContext.EventData.Value)  
  
           Case Else  
              SqlContext.Pipe.Send("Something else happened! Here's the EventData:")  
              SqlContext.Pipe.Send(triggContext.EventData.Value)  
  
        End Select  
    End Sub  
End Class     
```  
  
 L'output di esempio seguente è il valore della proprietà `EventData` restituito dopo un trigger DDL attivato da un evento `CREATE TABLE`  
  
 `<EVENT_INSTANCE><PostTime>2004-04-16T21:17:16.160</PostTime><SPID>58</SPID><EventType>CREATE_TABLE</EventType><ServerName>MACHINENAME</ServerName><LoginName>MYDOMAIN\myname</LoginName><UserName>MYDOMAIN\myname</UserName><DatabaseName>AdventureWorks</DatabaseName><SchemaName>dbo</SchemaName><ObjectName>UserName</ObjectName><ObjectType>TABLE</ObjectType><TSQLCommand><SetOptions ANSI_NULLS="ON" ANSI_NULL_DEFAULT="ON" ANSI_PADDING="ON" QUOTED_IDENTIFIER="ON" ENCRYPTED="FALSE" /><CommandText>create table dbo.UserName  
(  
 UserName varchar(50),  
 RealName varchar(50)  
)  
</CommandText></TSQLCommand></EVENT_INSTANCE>`  
  
 Oltre alle informazioni accessibili tramite la classe `SqlTriggerContext`, le query possono fare ancora riferimento a `COLUMNS_UPDATED` e alle tabelle Inserted/Deleted all'interno del testo di un comando eseguito in-process.  
  
## <a name="sample-clr-trigger"></a>Trigger CLR di esempio  
 Per questo esempio si consideri lo scenario in cui si lascia l'utente libero di scegliere l'ID desiderato, ma si desidera conoscere gli utenti che hanno immesso in modo specifico un indirizzo di posta elettronica come ID. Il trigger seguente consente di rilevare tali informazioni e registrarle nella tabella di controllo.  
  
> [!NOTE]  
>  L'invio di risultati e messaggi tramite l'oggetto `SqlPipe` è mostrato solo a scopo illustrativo e in genere se ne sconsiglia l'utilizzo nel codice di produzione. I dati aggiuntivi restituiti potrebbero essere imprevisti e generare errori nell'applicazione.  
  
```csharp  
using System;  
using System.Data;  
using System.Data.Sql;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Xml;  
using System.Text.RegularExpressions;  
  
public class CLRTriggers  
{  
   [SqlTrigger(Name = @"EmailAudit", Target = "[dbo].[Users]", Event = "FOR INSERT, UPDATE, DELETE")]  
   public static void EmailAudit()  
   {  
      string userName;  
      string realName;  
      SqlCommand command;  
      SqlTriggerContext triggContext = SqlContext.TriggerContext;  
      SqlPipe pipe = SqlContext.Pipe;  
      SqlDataReader reader;  
  
      switch (triggContext.TriggerAction)  
      {  
         case TriggerAction.Insert:  
         // Retrieve the connection that the trigger is using  
         using (SqlConnection connection  
            = new SqlConnection(@"context connection=true"))  
         {  
            connection.Open();  
            command = new SqlCommand(@"SELECT * FROM INSERTED;",  
               connection);  
            reader = command.ExecuteReader();  
            reader.Read();  
            userName = (string)reader[0];  
            realName = (string)reader[1];  
            reader.Close();  
  
            if (IsValidEMailAddress(userName))  
            {  
               command = new SqlCommand(  
                  @"INSERT [dbo].[UserNameAudit] VALUES ('"  
                  + userName + @"', '" + realName + @"');",  
                  connection);  
               pipe.Send(command.CommandText);  
               command.ExecuteNonQuery();  
               pipe.Send("You inserted: " + userName);  
            }  
         }  
  
         break;  
  
         case TriggerAction.Update:  
         // Retrieve the connection that the trigger is using  
         using (SqlConnection connection  
            = new SqlConnection(@"context connection=true"))  
         {  
            connection.Open();  
            command = new SqlCommand(@"SELECT * FROM INSERTED;",  
               connection);  
            reader = command.ExecuteReader();  
            reader.Read();  
  
            userName = (string)reader[0];  
            realName = (string)reader[1];  
  
            pipe.Send(@"You updated: '" + userName + @"' - '"  
               + realName + @"'");  
  
            for (int columnNumber = 0; columnNumber < triggContext.ColumnCount; columnNumber++)  
            {  
               pipe.Send("Updated column "  
                  + reader.GetName(columnNumber) + "? "  
                  + triggContext.IsUpdatedColumn(columnNumber).ToString());  
            }  
  
            reader.Close();  
         }  
  
         break;  
  
         case TriggerAction.Delete:  
            using (SqlConnection connection  
               = new SqlConnection(@"context connection=true"))  
               {  
                  connection.Open();  
                  command = new SqlCommand(@"SELECT * FROM DELETED;",  
                     connection);  
                  reader = command.ExecuteReader();  
  
                  if (reader.HasRows)  
                  {  
                     pipe.Send(@"You deleted the following rows:");  
                     while (reader.Read())  
                     {  
                        pipe.Send(@"'" + reader.GetString(0)  
                        + @"', '" + reader.GetString(1) + @"'");  
                     }  
  
                     reader.Close();  
  
                     //alternately, to just send a tabular resultset back:  
                     //pipe.ExecuteAndSend(command);  
                  }  
                  else  
                  {  
                     pipe.Send("No rows affected.");  
                  }  
               }  
  
               break;  
            }  
        }  
  
     public static bool IsValidEMailAddress(string email)  
     {  
         return Regex.IsMatch(email, @"^([\w-]+\.)*?[\w-]+@[\w-]+\.([\w-]+\.)*?[\w]+$");  
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
Imports System.Text.RegularExpressions  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class CLRTriggers   
  
    <SqlTrigger(Name:="EmailAudit", Target:="[dbo].[Users]", Event:="FOR INSERT, UPDATE, DELETE")> _  
    Public Shared Sub EmailAudit()  
        Dim userName As String  
        Dim realName As String  
        Dim command As SqlCommand  
        Dim triggContext As SqlTriggerContext  
        Dim pipe As SqlPipe  
        Dim reader As SqlDataReader    
  
        triggContext = SqlContext.TriggerContext      
        pipe = SqlContext.Pipe    
  
        Select Case triggContext.TriggerAction  
           Case TriggerAction.Insert  
              Using connection As New SqlConnection("context connection=true")  
                 connection.Open()  
                 command = new SqlCommand("SELECT * FROM INSERTED;", connection)  
  
                 reader = command.ExecuteReader()  
                 reader.Read()  
  
                 userName = CType(reader(0), String)  
                 realName = CType(reader(1), String)  
  
                 reader.Close()  
  
                 If IsValidEmailAddress(userName) Then  
                     command = New SqlCommand("INSERT [dbo].[UserNameAudit] VALUES ('" & _  
                       userName & "', '" & realName & "');", connection)  
  
                    pipe.Send(command.CommandText)  
                    command.ExecuteNonQuery()  
                    pipe.Send("You inserted: " & userName)  
  
                 End If  
              End Using  
  
           Case TriggerAction.Update  
              Using connection As New SqlConnection("context connection=true")  
                 connection.Open()  
                 command = new SqlCommand("SELECT * FROM INSERTED;", connection)  
  
                 reader = command.ExecuteReader()  
                 reader.Read()  
  
                 userName = CType(reader(0), String)  
                 realName = CType(reader(1), String)  
  
                 pipe.Send("You updated: " & userName & " - " & realName)  
  
                 Dim columnNumber As Integer  
  
                 For columnNumber=0 To triggContext.ColumnCount-1  
  
                    pipe.Send("Updated column " & reader.GetName(columnNumber) & _  
                      "? " & triggContext.IsUpdatedColumn(columnNumber).ToString() )  
  
                 Next  
  
                 reader.Close()  
              End Using  
  
           Case TriggerAction.Delete  
              Using connection As New SqlConnection("context connection=true")  
                 connection.Open()  
                 command = new SqlCommand("SELECT * FROM DELETED;", connection)  
  
                 reader = command.ExecuteReader()  
  
                 If reader.HasRows Then  
                    pipe.Send("You deleted the following rows:")  
  
                    While reader.Read()  
  
                       pipe.Send( reader.GetString(0) & ", " & reader.GetString(1) )  
  
                    End While   
  
                    reader.Close()  
  
                    ' Alternately, just send a tabular resultset back:  
                    ' pipe.ExecuteAndSend(command)  
  
                 Else  
                   pipe.Send("No rows affected.")  
                 End If  
  
              End Using   
        End Select  
    End Sub  
  
    Public Shared Function IsValidEMailAddress(emailAddress As String) As Boolean  
  
       return Regex.IsMatch(emailAddress, "^([\w-]+\.)*?[\w-]+@[\w-]+\.([\w-]+\.)*?[\w]+$")  
    End Function      
End Class  
```  
  
 Si supponga l'esistenza di due tabelle con le definizioni seguenti:  
  
```  
CREATE TABLE Users  
(  
    UserName nvarchar(200) NOT NULL,  
    RealName nvarchar(200) NOT NULL  
);  
GO CREATE TABLE UserNameAudit  
(  
    UserName nvarchar(200) NOT NULL,  
    RealName nvarchar(200) NOT NULL  
)  
```  
  
 Il [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione che crea il trigger [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è come indicato di seguito e presuppone che l'assembly **SQLCLRTest** è già registrato nell'attuale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database.  
  
```  
CREATE TRIGGER EmailAudit  
ON Users  
FOR INSERT, UPDATE, DELETE  
AS  
EXTERNAL NAME SQLCLRTest.CLRTriggers.EmailAudit  
```  
  
## <a name="validating-and-canceling-invalid-transactions"></a>Convalida e annullamento delle transazioni non valide  
 L'utilizzo dei trigger per convalidare e annullare le transazioni INSERT, UPDATE o DELETE non valide o per impedire modifiche allo schema del database è piuttosto comune. A tale scopo è necessario incorporare la logica di convalida nel trigger e quindi eseguire il rollback della transazione corrente se l'azione non soddisfa i criteri di convalida.  
  
 Quando viene chiamato all'interno di un trigger, il metodo `Transaction.Rollback` o un oggetto SqlCommand con il testo del comando "TRANSACTION ROLLBACK" genera un'eccezione con un messaggio di errore ambiguo e deve essere incluso in un blocco try/catch. Il messaggio di errore visualizzato è simile al seguente:  
  
```  
Msg 6549, Level 16, State 1, Procedure trig_InsertValidator, Line 0  
A .NET Framework error occurred during execution of user defined routine or aggregate 'trig_InsertValidator':   
System.Data.SqlClient.SqlException: Transaction is not allowed to roll back inside a user defined routine, trigger or aggregate because the transaction is not started in that CLR level. Change application logic to enforce strict transaction nesting... User transaction, if any, will be rolled back.  
```  
  
 Questa eccezione è prevista e il blocco try/catch è necessario per continuare a eseguire il codice. Al termine dell'esecuzione del codice del trigger, viene generata un'altra eccezione  
  
```  
Msg 3991, Level 16, State 1, Procedure trig_InsertValidator, Line 1   
The context transaction which was active before entering user defined routine, trigger or aggregate "trig_InsertValidator" has been ended inside of it, which is not allowed. Change application logic to enforce strict transaction nesting.  
The statement has been terminated.  
```  
  
 Anche questa eccezione è prevista e per continuare l'esecuzione è necessario un blocco try/catch intorno all'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] che esegue l'azione che attiva il trigger. Nonostante le due eccezioni generate, viene eseguito il rollback della transazione e le modifiche non vengono sottoposte a commit nella tabella. Una differenza principale tra i trigger CLR e i trigger [!INCLUDE[tsql](../../includes/tsql-md.md)] sta nel fatto che i trigger [!INCLUDE[tsql](../../includes/tsql-md.md)] possono continuare a eseguire altre operazioni in seguito al rollback della transazione.  
  
### <a name="example"></a>Esempio  
 Nel trigger seguente viene eseguita una semplice convalida delle istruzioni INSERT in una tabella. Se il valore intero inserito è uguale a uno, viene eseguito il rollback della transazione e il valore non viene inserito nella tabella. Tutti gli altri valori interi vengono inseriti nella tabella. Si noti il blocco try/catch intorno al metodo `Transaction.Rollback`. Lo script [!INCLUDE[tsql](../../includes/tsql-md.md)] crea una tabella di prova, un assembly e una stored procedure gestita. Notare che le due istruzioni INSERT vengono inserite in un blocco try/catch in modo da consentire l'intercettazione dell'eccezione generata al termine dell'esecuzione del trigger.  
  
 C#  
  
```  
using System;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;  
using System.Transactions;  
  
public partial class Triggers  
{  
    // Enter existing table or view for the target and uncomment the attribute line  
    // [Microsoft.SqlServer.Server.SqlTrigger (Name="trig_InsertValidator", Target="Table1", Event="FOR INSERT")]  
    public static void trig_InsertValidator()  
    {  
        using (SqlConnection connection = new SqlConnection(@"context connection=true"))  
        {  
            SqlCommand command;  
            SqlDataReader reader;  
            int value;  
  
            // Open the connection.  
            connection.Open();  
  
            // Get the inserted value.  
            command = new SqlCommand(@"SELECT * FROM INSERTED", connection);  
            reader = command.ExecuteReader();  
            reader.Read();  
            value = (int)reader[0];  
            reader.Close();  
  
            // Rollback the transaction if a value of 1 was inserted.  
            if (1 == value)  
            {  
                try  
                {  
                    // Get the current transaction and roll it back.  
                    Transaction trans = Transaction.Current;  
                    trans.Rollback();                      
                }  
                catch (SqlException ex)  
                {  
                    // Catch the expected exception.                      
                }  
            }  
            else  
            {  
                // Perform other actions here.  
            }  
  
            // Close the connection.  
            connection.Close();              
        }  
    }  
}  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Transactions  
  
Partial Public Class Triggers  
' Enter existing table or view for the target and uncomment the attribute line  
' <Microsoft.SqlServer.Server.SqlTrigger(Name:="trig_InsertValidator", Target:="Table1", Event:="FOR INSERT")> _  
Public Shared Sub  trig_InsertValidator ()  
    Using connection As New SqlConnection("context connection=true")  
  
        Dim command As SqlCommand  
        Dim reader As SqlDataReader  
        Dim value As Integer  
  
        ' Open the connection.  
        connection.Open()  
  
        ' Get the inserted value.  
        command = New SqlCommand("SELECT * FROM INSERTED", connection)  
        reader = command.ExecuteReader()  
        reader.Read()  
        value = CType(reader(0), Integer)  
        reader.Close()  
  
        ' Rollback the transaction if a value of 1 was inserted.  
        If value = 1 Then  
  
            Try  
                ' Get the current transaction and roll it back.  
                Dim trans As Transaction  
                trans = Transaction.Current  
                trans.Rollback()  
  
            Catch ex As SqlException  
  
                ' Catch the exception.                      
            End Try  
        Else  
  
            ' Perform other actions here.  
        End If  
  
        ' Close the connection.  
        connection.Close()  
    End Using  
End Sub  
End Class  
```  
  
 Transact-SQL  
  
```  
-- Create the test table, assembly, and trigger.  
CREATE TABLE Table1(c1 int);  
go  
  
CREATE ASSEMBLY ValidationTriggers from 'E:\programming\ ValidationTriggers.dll';  
go  
  
CREATE TRIGGER trig_InsertValidator  
ON Table1  
FOR INSERT  
AS EXTERNAL NAME ValidationTriggers.Triggers.trig_InsertValidator;  
go  
  
-- Use a Try/Catch block to catch the expected exception  
BEGIN TRY  
   INSERT INTO Table1 VALUES(42)  
   INSERT INTO Table1 VALUES(1)  
END TRY  
BEGIN CATCH  
  SELECT ERROR_NUMBER() AS ErrorNum, ERROR_MESSAGE() AS ErrorMessage  
END CATCH;  
  
-- Clean up.  
DROP TRIGGER trig_InsertValidator;  
DROP ASSEMBLY ValidationTriggers;  
DROP TABLE Table1;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)   
 [Trigger DML](../../relational-databases/triggers/dml-triggers.md)   
 [Trigger DDL](../../relational-databases/triggers/ddl-triggers.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/try-catch-transact-sql)   
 [Compilazione di oggetti di Database con Common Language Runtime &#40;CLR&#41; integrazione](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
