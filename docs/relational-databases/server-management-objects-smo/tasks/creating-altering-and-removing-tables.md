---
title: Creazione, modifica e rimozione di tabelle
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- tables [SMO]
ms.assetid: ff0bcfff-812f-4999-b0c7-736a97804c2b
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3f98b77fd740b31cbc3f9334f58d4a48586031e0
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85900784"
---
# <a name="creating-altering-and-removing-tables"></a>Creazione, modifica e rimozione di tabelle
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw.md)]
  In SMO ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects) le tabelle sono rappresentate dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.Table>. Nella gerarchia degli oggetti di SMO, l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Table> si trova sotto l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Database>.  
  
## <a name="example"></a>Esempio  
 Per utilizzare qualsiasi esempio di codice fornito, è necessario scegliere l'ambiente, il modello e il linguaggio di programmazione per la creazione dell'applicazione. Per altre informazioni, vedere [creare un progetto Visual C&#35; SMO in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-table-in-visual-basic"></a>Creazione, modifica e rimozione di una tabella in Visual Basic  
 In questo esempio di codice viene creata una tabella che dispone di diverse colonne con tipi e scopi diversi. Nel codice vengono inoltre forniti esempi di come creare un campo di identità e una chiave primaria e di come modificare le proprietà delle tabelle.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 2008R2 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define a Table object variable by supplying the parent database and table name in the constructor. 
Dim tb As Table
tb = New Table(db, "Test_Table")
'Add various columns to the table.
Dim col1 As Column
col1 = New Column(tb, "Name", DataType.NChar(50))
col1.Collation = "Latin1_General_CI_AS"
col1.Nullable = True
tb.Columns.Add(col1)
Dim col2 As Column
col2 = New Column(tb, "ID", DataType.Int)
col2.Identity = True
col2.IdentitySeed = 1
col2.IdentityIncrement = 1
tb.Columns.Add(col2)
Dim col3 As Column
col3 = New Column(tb, "Value", DataType.Real)
tb.Columns.Add(col3)
Dim col4 As Column
col4 = New Column(tb, "Date", DataType.DateTime)
col4.Nullable = False
tb.Columns.Add(col4)
'Create the table on the instance of SQL Server.
tb.Create()
'Add another column.
Dim col5 As Column
col5 = New Column(tb, "ExpiryDate", DataType.DateTime)
col5.Nullable = False
tb.Columns.Add(col5)
'Run the Alter method to make the change on the instance of SQL Server.
tb.Alter()
'Remove the table from the database.

tb.Drop()
``` 
  
## <a name="creating-altering-and-removing-a-table-in-visual-c"></a>Creazione, modifica e rimozione di una tabella in Visual C#  
 In questo esempio di codice viene creata una tabella che dispone di diverse colonne con tipi e scopi diversi. Nel codice vengono inoltre forniti esempi di come creare un campo di identità e una chiave primaria e di come modificare le proprietà delle tabelle.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
        Server srv;   
        srv = new Server();   
        //Reference the AdventureWorks2012 database.   
        Database db;   
        db = srv.Databases["AdventureWorks2012"];   
        //Define a Table object variable by supplying the parent database and table name in the constructor.   
        Table tb;   
        tb = new Table(db, "Test_Table");   
        //Add various columns to the table.   
        Column col1;   
        col1 = new Column(tb, "Name", DataType.NChar(50));   
        col1.Collation = "Latin1_General_CI_AS";   
        col1.Nullable = true;   
        tb.Columns.Add(col1);   
        Column col2;   
        col2 = new Column(tb, "ID", DataType.Int);   
        col2.Identity = true;   
        col2.IdentitySeed = 1;   
        col2.IdentityIncrement = 1;   
        tb.Columns.Add(col2);   
        Column col3;   
        col3 = new Column(tb, "Value", DataType.Real);   
        tb.Columns.Add(col3);   
        Column col4;   
        col4 = new Column(tb, "Date", DataType.DateTime);   
        col4.Nullable = false;   
        tb.Columns.Add(col4);   
        //Create the table on the instance of SQL Server.   
        tb.Create();   
        //Add another column.   
        Column col5;   
        col5 = new Column(tb, "ExpiryDate", DataType.DateTime);   
        col5.Nullable = false;   
        tb.Columns.Add(col5);   
        //Run the Alter method to make the change on the instance of SQL Server.   
        tb.Alter();   
        //Remove the table from the database.   
        tb.Drop();   
        }  
```  
  
## <a name="creating-altering-and-removing-a-table-in-powershell"></a>Creazione, modifica e rimozione di una tabella in PowerShell  
 In questo esempio di codice viene creata una tabella che dispone di diverse colonne con tipi e scopi diversi. Nel codice vengono inoltre forniti esempi di come creare un campo di identità e una chiave primaria e di come modificare le proprietà delle tabelle.  
  
```powershell  
#Load the assembly containing the objects used in this example  
[reflection.assembly]::LoadWithPartialName("Microsoft.SqlServer.Types")  
  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012.  
$db = get-item AdventureWorks2012  
  
#Create a SMO Table  
$tb = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Table -argumentlist $db, "Test_Table"  
  
#Add various columns to the table.   
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::NChar(50)  
$col1 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"Name", $Type  
$col1.Collation = "Latin1_General_CI_AS"  
$col1.Nullable = $true  
$tb.Columns.Add($col1)  
  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::Int  
$col2 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"ID", $Type  
$col2.Identity = $true  
$col2.IdentitySeed = 1  
$col2.IdentityIncrement = 1  
$tb.Columns.Add($col2)   
  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::Real  
$col3 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"Value", $Type  
$tb.Columns.Add($col3)   
  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$col4 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"Date", $Type  
$col4.Nullable = $false  
$tb.Columns.Add($col4)   
  
#Create the table  
$tb.Create()  
  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$col5 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"ExpiryDate", $Type  
$col5.Nullable = $false  
$tb.Columns.Add($col5)   
  
#Run the Alter method to make the change on the instance of SQL Server.   
$tb.Alter()  
  
#Remove the table from the database.   
$tb.Drop()  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.SqlServer.Management.Smo.Table>  
  
  
