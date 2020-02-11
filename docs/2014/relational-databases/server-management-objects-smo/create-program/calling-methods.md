---
title: Metodi di chiamata | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- methods [SMO]
- calling methods
- SQL Server Management Objects, method calling
- SMO [SQL Server], method calling
ms.assetid: c88d5c5f-9ff0-4f84-b2b6-24c6b90fa15e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5c3a004d30a5edb20da77e6f93bf51a94472419b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63192165"
---
# <a name="calling-methods"></a>Chiamata di metodi
  I metodi eseguono attività specifiche correlate all'oggetto, ad esempio l'emissione di `Checkpoint` un oggetto in un database o la richiesta di un elenco enumerato di accessi per [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]l'istanza di.  
  
 I metodi eseguono un'operazione su un oggetto. I metodi possono accettare parametri e spesso restituiscono un valore. Il valore restituito può essere un tipo di dati semplice, un oggetto complesso o una struttura che contiene molti membri.  
  
 Utilizzare la gestione delle eccezioni per determinare se il metodo è stato eseguito correttamente. Per altre informazioni, vedere [Handling SMO Exceptions](handling-smo-exceptions.md).  
  
## <a name="examples"></a>Esempi  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="using-a-simple-smo-method-in-visual-basic"></a>Utilizzo di un metodo SMO semplice in Visual Basic  
 In questo esempio il metodo <xref:Microsoft.SqlServer.Management.Smo.Database.Create%2A> non accetta parametri e non restituisce alcun valore.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBMethods1](SMO How to#SMO_VBMethods1)]  -->  
  
## <a name="using-a-simple-smo-method-in-visual-c"></a>Utilizzo di un metodo SMO semplice in Visual C#  
 In questo esempio il metodo <xref:Microsoft.SqlServer.Management.Smo.Database.Create%2A> non accetta parametri e non restituisce alcun valore.  
  
```  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Define a Database object variable by supplying the parent server and the database name arguments in the constructor.   
Database db;   
db = new Database(srv, "Test_SMO_Database");   
//Call the Create method to create the database on the instance of SQL Server.   
db.Create();   
```  
  
 }  
  
## <a name="using-an-smo-method-with-a-parameter-in-visual-basic"></a>Utilizzo di un metodo SMO con un parametro in Visual Basic  
 L'oggetto <xref:Microsoft.SqlServer.Management.Smo.Table> include un metodo denominato <xref:Microsoft.SqlServer.Management.Smo.Table.RebuildIndexes%2A>. Questo metodo richiede un parametro numerico che specifica `FillFactor`.  
  
```  
Dim srv As Server  
srv = New Server  
Dim tb As Table  
tb = srv.Databases("AdventureWorks2012").Tables("Employee", "HumanResources")  
tb.RebuildIndexes(70)  
```  
  
## <a name="using-an-smo-method-with-a-parameter-in-visual-c"></a>Utilizzo di un metodo SMO con un parametro in Visual C#  
 L'oggetto <xref:Microsoft.SqlServer.Management.Smo.Table> include un metodo denominato <xref:Microsoft.SqlServer.Management.Smo.Table.RebuildIndexes%2A>. Questo metodo richiede un parametro numerico che specifica `FillFactor`.  
  
```  
{   
Server srv = default(Server);   
srv = new Server();   
Table tb = default(Table);   
tb = srv.Databases("AdventureWorks2012").Tables("Employee", "HumanResources");   
tb.RebuildIndexes(70);   
}   
```  
  
## <a name="using-an-enumeration-method-that-returns-a-datatable-object-in-visual-basic"></a>Utilizzo di un metodo di enumerazione che restituisce un oggetto DataTable in Visual Basic  
 In questa sezione viene descritto come chiamare un metodo di enumerazione e come gestire i dati nell'oggetto <xref:System.Data.DataTable> restituito.  
  
 Il metodo <xref:Microsoft.SqlServer.Management.Smo.Server.EnumCollations%2A> restituisce un oggetto <xref:System.Data.DataTable>, che richiede ulteriore navigazione per accedere a tutte le informazioni sulle regole di confronto disponibili relative all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```  
'Connect to the local, default instance of SQL Server.  
Dim srv As Server  
srv = New Server  
'Call the EnumCollations method and return collation information to DataTable variable.  
Dim d As DataTable  
'Select the returned data into an array of DataRow.  
d = srv.EnumCollations  
'Iterate through the rows and display collation details for the instance of SQL Server.  
Dim r As DataRow  
Dim c As DataColumn  
For Each r In d.Rows  
    Console.WriteLine("==")  
    For Each c In r.Table.Columns  
        Console.WriteLine(c.ColumnName + " = " + r(c).ToString)  
    Next  
Next  
```  
  
## <a name="using-an-enumeration-method-that-returns-a-datatable-object-in-visual-c"></a>Utilizzo di un metodo di enumerazione che restituisce un oggetto DataTable in Visual C#  
 In questa sezione viene descritto come chiamare un metodo di enumerazione e come gestire i dati nell'oggetto <xref:System.Data.DataTable> restituito.  
  
 Il metodo <xref:Microsoft.SqlServer.Management.Smo.Server.EnumCollations%2A> restituisce un oggetto <xref:System.Data.DataTable> di sistema. L'oggetto <xref:System.Data.DataTable> richiede ulteriore navigazione per accedere a tutte le informazioni sulle regole di confronto disponibili relative all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```  
//Connect to the local, default instance of SQL Server.   
{   
Server srv = default(Server);   
srv = new Server();   
//Call the EnumCollations method and return collation information to DataTable variable.   
DataTable d = default(DataTable);   
//Select the returned data into an array of DataRow.   
d = srv.EnumCollations;   
//Iterate through the rows and display collation details for the instance of SQL Server.   
DataRow r = default(DataRow);   
DataColumn c = default(DataColumn);   
foreach ( r in d.Rows) {   
  Console.WriteLine("=========");   
  foreach ( c in r.Table.Columns) {   
    Console.WriteLine(c.ColumnName + " = " + r(c).ToString);   
  }   
}   
}   
```  
  
## <a name="constructing-an-object-in-visual-basic"></a>Costruzione di un oggetto in Visual Basic  
 È possibile chiamare il costruttore di qualsiasi oggetto utilizzando l'operatore `New`. Viene eseguito l'overload del costruttore dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Database> e la versione del costruttore dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Database> usata nell'esempio accetta due parametri: l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server> padre cui appartiene il database e una stringa che rappresenta il nome del nuovo database.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBMethods4](SMO How to#SMO_VBMethods4)]  -->  
  
## <a name="constructing-an-object-in-visual-c"></a>Costruzione di un oggetto in Visual C#  
 È possibile chiamare il costruttore di qualsiasi oggetto utilizzando l'operatore `New`. Viene eseguito l'overload del costruttore dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Database> e la versione del costruttore dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Database> usata nell'esempio accetta due parametri: l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server> padre cui appartiene il database e una stringa che rappresenta il nome del nuovo database.  
  
```  
{   
Server srv;   
srv = new Server();   
Table tb;   
tb = srv.Databases("AdventureWorks2012").Tables("Employee", "HumanResources");   
tb.RebuildIndexes(70);   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Declare and define a Database object by supplying the parent server and the database name arguments in the constructor.   
Database d;   
d = new Database(srv, "Test_SMO_Database");   
//Create the database on the instance of SQL Server.   
d.Create();   
Console.WriteLine(d.Name);   
}  
```  
  
## <a name="copying-an-smo-object-in-visual-basic"></a>Copia di un oggetto SMO in Visual Basic  
 In questo esempio di codice viene utilizzato il metodo <xref:Microsoft.SqlServer.Management.Common.ServerConnection.Copy%2A> per creare una copia dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server>. L'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server> rappresenta una connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VCMethods6](SMO How to#SMO_VCMethods6)]  -->  
  
## <a name="copying-an-smo-object-in-visual-c"></a>Copia di un oggetto SMO in Visual C#  
 In questo esempio di codice viene utilizzato il metodo <xref:Microsoft.SqlServer.Management.Common.ServerConnection.Copy%2A> per creare una copia dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server>. L'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server> rappresenta una connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```  
{   
//Connect to the local, default instance of SQL Server.   
Server srv1;   
srv1 = new Server();   
//Modify the default database and the timeout period for the connection.   
srv1.ConnectionContext.DatabaseName = "AdventureWorks2012";   
srv1.ConnectionContext.ConnectTimeout = 30;   
//Make a second connection using a copy of the ConnectionContext property and verify settings.   
Server srv2;   
srv2 = new Server(srv1.ConnectionContext.Copy);   
Console.WriteLine(srv2.ConnectionContext.ConnectTimeout.ToString);   
}  
```  
  
## <a name="monitoring-server-processes-in-visual-basic"></a>Monitoraggio di processi server in Visual Basic  
 È possibile ottenere le informazioni sul tipo di stato corrente relative all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzando metodi di enumerazione. Nell'esempio di codice viene utilizzato il metodo <xref:Microsoft.SqlServer.Management.Smo.Server.EnumProcesses%2A> per individuare informazioni sui processi correnti. Viene inoltre illustrato come utilizzare le colonne e le righe nell'oggetto <xref:System.Data.DataTable> restituito.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBMethods5](SMO How to#SMO_VBMethods5)]  -->  
  
## <a name="monitoring-server-processes-in-visual-c"></a>Monitoraggio di processi server in Visual C#  
 È possibile ottenere le informazioni sul tipo di stato corrente relative all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzando metodi di enumerazione. Nell'esempio di codice viene utilizzato il metodo <xref:Microsoft.SqlServer.Management.Smo.Server.EnumProcesses%2A> per individuare informazioni sui processi correnti. Viene inoltre illustrato come utilizzare le colonne e le righe nell'oggetto <xref:System.Data.DataTable> restituito.  
  
```  
//Connect to the local, default instance of SQL Server.   
{   
Server srv = default(Server);   
srv = new Server();   
//Call the EnumCollations method and return collation information to DataTable variable.   
DataTable d = default(DataTable);   
//Select the returned data into an array of DataRow.   
d = srv.EnumProcesses;   
//Iterate through the rows and display collation details for the instance of SQL Server.   
DataRow r = default(DataRow);   
DataColumn c = default(DataColumn);   
foreach ( r in d.Rows) {   
  Console.WriteLine("=====");   
  foreach ( c in r.Table.Columns) {   
    Console.WriteLine(c.ColumnName + " = " + r(c).ToString);   
  }   
}   
}   
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
  
