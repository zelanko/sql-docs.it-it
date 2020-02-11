---
title: Impostazione delle proprietà-SMO | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SMO [SQL Server], properties
- SQL Server Management Objects, properties
- properties [SMO]
ms.assetid: 342569ba-d2f7-44d2-8f3f-ae9c701c7f0f
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6ffcdda8e1c6a3c85703ad7f3d6ed94ca0ca91fe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "70148709"
---
# <a name="setting-properties---smo"></a>Impostazione delle proprietà - SMO
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Le proprietà sono valori in cui sono archiviate informazioni descrittive sull'oggetto. Le opzioni di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] configurazione, ad esempio, sono <xref:Microsoft.SqlServer.Management.Smo.Server.Configuration%2A> rappresentate dalle proprietà dell'oggetto. Alle proprietà è possibile accedere direttamente o indirettamente utilizzando la relativa raccolta. Per l'accesso diretto alle proprietà viene utilizzata la sintassi seguente:  
  
 `objInstance.PropertyName`  
  
 Un valore di proprietà può essere modificato o recuperato a seconda che la proprietà disponga di accesso in lettura/scrittura o di accesso in sola lettura. È inoltre necessario impostare determinate proprietà prima che sia possibile creare un oggetto. Per ulteriori informazioni, vedere la documentazione di riferimento di SMO per l'oggetto specifico.  
  
> [!NOTE]  
>  Le raccolte di oggetti figlio vengono visualizzate come proprietà di un oggetto. La raccolta **Tables** è ad esempio una proprietà di un oggetto **Server** . Per altre informazioni, vedere [Using Collections](../../../relational-databases/server-management-objects-smo/create-program/using-collections.md).  
  
 Le proprietà di un oggetto sono membri della raccolta Properties. Tale raccolta può essere utilizzata per scorrere tutte le proprietà di un oggetto.  
  
 Talvolta una proprietà non è disponibile per i motivi seguenti:  
  
-   La versione del server non supporta la proprietà, ad esempio se si tenta di accedere a una proprietà che rappresenta una nuova funzionalità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in una versione precedente di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Il server non fornisce dati per la proprietà, ad esempio se si tenta di accedere a una proprietà che rappresenta un componente di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non installato.  
  
 Per gestire queste situazioni è possibile individuare le eccezioni SMO <xref:Microsoft.SqlServer.Management.Smo.UnknownPropertyException> e <xref:Microsoft.SqlServer.Management.Smo.PropertyCannotBeRetrievedException>.  
  
## <a name="setting-default-initialization-fields"></a>Impostazione dei campi di inizializzazione predefiniti  
 SMO consente di eseguire un'ottimizzazione durante il recupero di oggetti. L'ottimizzazione riduce il numero di proprietà caricate mediante il passaggio automatico tra gli stati seguenti:  
  
1.  Parzialmente caricato. Quando viene fatto riferimento a un oggetto per la prima volta, esso dispone di un minimo di proprietà disponibili (ad esempio Name e Schema).  
  
2.  Completamente caricato. Quando viene fatto riferimento a una proprietà, le proprietà restanti, che sono rapide da caricare, vengono inizializzate e rese disponibili.  
  
3.  Proprietà che utilizzano grandi quantità di memoria. Le restanti proprietà non disponibili utilizzano grandi quantità di memoria e presentano un valore True per la proprietà <xref:Microsoft.SqlServer.Management.Smo.Property.Expensive%2A> (ad esempio <xref:Microsoft.SqlServer.Management.Smo.Database.DataSpaceUsage%2A>). Tali proprietà vengono caricate solo quando viene fatto loro riferimento in modo specifico.  
  
 Se l'applicazione recupera proprietà aggiuntive, oltre a quelle fornite nello stato di caricamento parziale, invia una query per recuperarle e passa allo stato di caricamento completo. Ciò può provocare traffico non necessario tra il client e server. Per una maggiore ottimizzazione, è possibile chiamare il metodo <xref:Microsoft.SqlServer.Management.Smo.Server.SetDefaultInitFields%2A>. Il metodo <xref:Microsoft.SqlServer.Management.Smo.Server.SetDefaultInitFields%2A> consente la specifica delle proprietà caricate quando viene inizializzato l'oggetto.  
  
 Il metodo <xref:Microsoft.SqlServer.Management.Smo.Server.SetDefaultInitFields%2A> imposta il comportamento di caricamento della proprietà per la parte restante dell'applicazione o fino a quando non viene reimpostato. È possibile salvare il comportamento originale utilizzando il metodo <xref:Microsoft.SqlServer.Management.Smo.Server.GetDefaultInitFields%2A> e ripristinarlo come necessario.  
  
## <a name="examples"></a>Esempi  
Per utilizzare qualsiasi esempio di codice fornito, è necessario scegliere l'ambiente di programmazione, il modello di programmazione e il linguaggio di programmazione per la creazione dell'applicazione. Per altre informazioni, vedere [creare un progetto Visual C&#35; SMO in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  

  
## <a name="getting-and-setting-a-property-in-visual-basic"></a>Ottenere e impostare una proprietà in Visual Basic  
 In questo esempio di codice viene illustrato come <xref:Microsoft.SqlServer.Management.Smo.Information.Edition%2A> ottenere la proprietà <xref:Microsoft.SqlServer.Management.Smo.Information> dell'oggetto e come impostare la <xref:Microsoft.SqlServer.Management.Common.ServerConnection.SqlExecutionModes%2A> proprietà della <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> proprietà sul membro **ExecuteSQL** del tipo <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes> enumerato.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Get a property.
Console.WriteLine(srv.Information.Version)
'Set a property.
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.ExecuteSql
```
  
## <a name="getting-and-setting-a-property-in-visual-c"></a>Ottenere e impostare una proprietà in Visual C#  
 In questo esempio di codice viene illustrato come <xref:Microsoft.SqlServer.Management.Smo.Information.Edition%2A> ottenere la proprietà <xref:Microsoft.SqlServer.Management.Smo.Information> dell'oggetto e come impostare la <xref:Microsoft.SqlServer.Management.Common.ServerConnection.SqlExecutionModes%2A> proprietà della <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> proprietà sul membro **ExecuteSQL** del tipo <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes> enumerato.  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Get a property.   
Console.WriteLine(srv.Information.Version);   
//Set a property.   
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.ExecuteSql;   
}  
```  
  
## <a name="setting-various-properties-before-an-object-is-created-in-visual-basic"></a>Impostazione di diverse proprietà prima della creazione di un oggetto in Visual Basic  
 In questo esempio di codice viene illustrato come impostare direttamente la proprietà <xref:Microsoft.SqlServer.Management.Smo.Table.AnsiNullsStatus%2A> dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Table> e come creare e aggiungere colonne prima di creare l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Table>.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Create a new table in the AdventureWorks2012 database. 
Dim db As Database
db = srv.Databases("AdventureWorks2012")
Dim tb As Table
'Specify the parent database, table schema and the table name in the constructor.
tb = New Table(db, "Test_Table", "HumanResources")
'Add columns because the table requires columns before it can be created. 
Dim c1 As Column
'Specify the parent table, the column name and data type in the constructor.
c1 = New Column(tb, "ID", DataType.Int)
tb.Columns.Add(c1)
c1.Nullable = False
c1.Identity = True
c1.IdentityIncrement = 1
c1.IdentitySeed = 0
Dim c2 As Column
c2 = New Column(tb, "Name", DataType.NVarChar(100))
c2.Nullable = False
tb.Columns.Add(c2)
tb.AnsiNullsStatus = True
'Create the table on the instance of SQL Server.
tb.Create()
```
  
## <a name="setting-various-properties-before-an-object-is-created-in-visual-c"></a>Impostazione di diverse proprietà prima della creazione di un oggetto in Visual C#  
 In questo esempio di codice viene illustrato come impostare direttamente la proprietà <xref:Microsoft.SqlServer.Management.Smo.Table.AnsiNullsStatus%2A> dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Table> e come creare e aggiungere colonne prima di creare l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Table>.  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Create a new table in the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
Table tb;   
//Specify the parent database, table schema, and the table name in the constructor.   
tb = new Table(db, "Test_Table", "HumanResources");   
//Add columns because the table requires columns before it can be created.   
Column c1;   
//Specify the parent table, the column name, and data type in the constructor.   
c1 = new Column(tb, "ID", DataType.Int);   
tb.Columns.Add(c1);   
c1.Nullable = false;   
c1.Identity = true;   
c1.IdentityIncrement = 1;   
c1.IdentitySeed = 0;   
Column c2;   
c2 = new Column(tb, "Name", DataType.NVarChar(100));   
c2.Nullable = false;   
tb.Columns.Add(c2);   
tb.AnsiNullsStatus = true;   
//Create the table on the instance of SQL Server.   
tb.Create();   
}  
```  
  
## <a name="iterating-through-all-properties-of-an-object-in-visual-basic"></a>Scorrimento di tutte le proprietà di un oggetto in Visual Basic  
 Questo esempio di codice scorre la raccolta **Properties** dell' <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> oggetto e li Visualizza nella schermata di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] output.  
  
 Nell'esempio l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Property> è stato inserito tra parentesi quadre in quanto è anche una parola chiave di [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)].  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Set properties on the uspGetEmployeeManagers stored procedure on the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
Dim sp As StoredProcedure
sp = db.StoredProcedures("uspGetEmployeeManagers")
sp.AnsiNullsStatus = False
sp.QuotedIdentifierStatus = False
'Iterate through the properties of the stored procedure and display.
'Note the Property object requires [] parentheses to distinguish it from the Visual Basic key word.
Dim p As [Property]
For Each p In sp.Properties
    Console.WriteLine(p.Name & p.Value)
Next
```
  
## <a name="iterating-through-all-properties-of-an-object-in-visual-c"></a>Scorrimento di tutte le proprietà di un oggetto in Visual C#  
 Questo esempio di codice scorre la raccolta **Properties** dell' <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> oggetto e li Visualizza nella schermata di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] output.  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Set properties on the uspGetEmployeedManagers stored procedure on the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
StoredProcedure sp;   
sp = db.StoredProcedures("uspGetEmployeeManagers");   
sp.AnsiNullsStatus = false;   
sp.QuotedIdentifierStatus = false;   
//Iterate through the properties of the stored procedure and display.   
  Property p;   
  foreach ( p in sp.Properties) {   
    Console.WriteLine(p.Name + p.Value);   
  }   
}  
```  
  
## <a name="setting-default-initialization-fields-in-visual-basic"></a>Impostazione dei campi di inizializzazione predefiniti in Visual Basic  
 In questo esempio di codice viene illustrato come ridurre il numero di proprietà dell'oggetto inizializzate in un programma SMO. È necessario includere l'istruzione `using System.Collections.Specialized` per utilizzare l'oggetto <xref:System.Collections.Specialized.StringCollection>.  
  
 
  [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] consente di confrontare il numero di istruzioni inviate all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con questa ottimizzazione.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Assign the Table object type to a System.Type object variable.
Dim tb As Table
Dim typ As Type
tb = New Table
typ = tb.GetType
'Assign the current default initialization fields for the Table object type to a 
'StringCollection object variable.
Dim sc As StringCollection
sc = srv.GetDefaultInitFields(typ)
'Set the default initialization fields for the Table object type to the CreateDate property.
srv.SetDefaultInitFields(typ, "CreateDate")
'Retrieve the Schema, Name, and CreateDate properties for every table in AdventureWorks2012.
'Note that the improvement in performance can be viewed in SQL Profiler.
For Each tb In db.Tables
    Console.WriteLine(tb.Schema + "." + tb.Name + " " + tb.CreateDate)
Next
'Set the default initialization fields for the Table object type back to the original settings.
srv.SetDefaultInitFields(typ, sc)
```
  
## <a name="setting-default-initialization-fields-in-visual-c"></a>Impostazione dei campi di inizializzazione predefiniti in Visual C#  
 In questo esempio di codice viene illustrato come ridurre il numero di proprietà dell'oggetto inizializzate in un programma SMO. È necessario includere l'istruzione `using System.Collections.Specialized` per utilizzare l'oggetto <xref:System.Collections.Specialized.StringCollection>.  
  
 
  [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] consente di confrontare il numero di istruzioni inviate all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con questa ottimizzazione.  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Reference the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
//Assign the Table object type to a System.Type object variable.   
Table tb;   
Type typ;   
tb = new Table();   
typ = tb.GetType;   
//Assign the current default initialization fields for the Table object type to a   
//StringCollection object variable.   
StringCollection sc;   
sc = srv.GetDefaultInitFields(typ);   
//Set the default initialization fields for the Table object type to the CreateDate property.   
srv.SetDefaultInitFields(typ, "CreateDate");   
//Retrieve the Schema, Name, and CreateDate properties for every table in AdventureWorks2012.   
   //Note that the improvement in performance can be viewed in SQL Server Profiler.   
foreach ( tb in db.Tables) {   
   Console.WriteLine(tb.Schema + "." + tb.Name + " " + tb.CreateDate);   
}   
//Set the default initialization fields for the Table object type back to the original settings.   
srv.SetDefaultInitFields(typ, sc);   
}  
```  
  
  
