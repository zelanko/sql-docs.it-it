---
description: Utilizzo di tabelle definite dall'utente
title: Utilizzo di tabelle definite dall'utente | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- user-defined tables [SQL Server]
ms.assetid: 620a4e1f-9678-4711-ae09-bcf7c9cae724
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 58f244f5216a016633b2f186d04ef9789267b6e2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448024"
---
# <a name="using-user-defined-tables"></a>Utilizzo di tabelle definite dall'utente
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  Le tabelle definite dall'utente rappresentano informazioni tabulari. Vengono utilizzate come parametri quando si passano dati tabulari in stored procedure o funzioni definite dall'utente. Non è possibile utilizzare le tabelle definite dall'utente per rappresentare le colonne di una tabella di database.  
  
 L'oggetto <xref:Microsoft.SqlServer.Management.Smo.Database> dispone di una proprietà <xref:Microsoft.SqlServer.Management.Smo.Database.UserDefinedTableTypes%2A> che fa riferimento a un oggetto <xref:Microsoft.SqlServer.Management.Smo.UserDefinedTableTypeCollection>. Ogni <xref:Microsoft.SqlServer.Management.Smo.UserDefinedTableType> oggetto nella raccolta dispone di una proprietà **Columns** che fa riferimento a una raccolta di <xref:Microsoft.SqlServer.Management.Smo.Column> oggetti in cui sono elencate le colonne della tabella definita dall'utente. Utilizzare il metodo Add per aggiungere colonne alla tabella definita dall'utente.  
  
 Quando si definisce una nuova tabella definita dall'utente tramite l'oggetto <xref:Microsoft.SqlServer.Management.Smo.UserDefinedTableType>, è necessario fornire colonne e una chiave primaria basata su una delle colonne.  
  
 Dopo averli creati, non è più possibile modificare i tipi di tabella definita dall'utente. <xref:Microsoft.SqlServer.Management.Smo.UserDefinedTableType> non supporta il metodo Alter. I tipi di tabella definita dall'utente possono disporre di vincoli CHECK, ma alcune operazioni di controllo genereranno un'eccezione perché il tipo non è modificabile.  
  
 La classe <xref:Microsoft.SqlServer.Management.Smo.DataType> consente di specificare il tipo di dati associato a colonne e parametri. Utilizzare questo tipo per specificare il tipo di tabella definita dall'utente come parametro per stored procedure e funzioni definite dall'utente.  
  
## <a name="examples"></a>Esempi  
Per usare qualsiasi esempio di codice fornito, è necessario scegliere l'ambiente di programmazione, il modello di programmazione e il linguaggio di programmazione per la creazione dell'applicazione. Per altre informazioni, vedere [creare un progetto Visual C&#35; SMO in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  

  
## <a name="creating-a-user-defined-table-in-visual-basic"></a>Creazione di una tabella definita dall'utente in Visual Basic  
 Per questo esempio, sarà necessario includere un'istruzione Imports per la libreria di classi che contiene il tipo **StringCollection** .  
  
 `Imports System.Collections.Specialized`  
  
 Nell'esempio viene illustrato come creare una tabella definita dall'utente e successivamente come utilizzarla come parametro in una funzione definita dall'utente.  
  
```VBNET  
'Connect to the local, default instance of SQL Server  
        Dim srv As Server  
        srv = New Server  
        'Reference the AdventureWorks2012 database.  
        Dim db As Database  
        db = srv.Databases("AdventureWorks2012")  
        'Define a UserDefinedTableType object variable by supplying the 'database and name in the constructor.  
        Dim udtt As UserDefinedTableType  
        udtt = New UserDefinedTableType(db, "My_User_Defined_Table")  
        'Add three columns of different types to the  
        'UserDefinedTableType object.  
        udtt.Columns.Add(New Column(udtt, "Col1", DataType.Int))  
        udtt.Columns.Add(New Column(udtt, "Col2", DataType.VarCharMax))  
        udtt.Columns.Add(New Column(udtt, "Col3", DataType.Money))  
        'Define an Index object variable by supplying the user-defined  
        'table variable and name in the constructor.  
        Dim idx As Index  
        idx = New Index(udtt, "PK_UddtTable")  
        'Add the first column in the user-defined table as  
        'the indexed column.  
        idx.IndexedColumns.Add(New IndexedColumn(idx, "Col1"))  
        'Specify that the index is a clustered, unique, primary key.  
        idx.IsClustered = True  
        idx.IsUnique = True  
        idx.IndexKeyType = IndexKeyType.DriPrimaryKey  
        udtt.Indexes.Add(idx)  
        'Add the index and create the user-defined table.  
        udtt.Create()  
        'Display the Transact-SQL creation script for the  
        'user-defined table.  
        Dim sc As StringCollection  
        sc = udtt.Script()  
        For Each c As String In sc  
            Console.WriteLine(c)  
        Next  
  
        'Define a new user-defined function with a single parameter.  
        Dim udf As UserDefinedFunction  
        udf = New UserDefinedFunction(db, "My_User_Defined_Function")  
        udf.TextMode = False  
        udf.FunctionType = UserDefinedFunctionType.Scalar  
        udf.ImplementationType = ImplementationType.TransactSql  
        udf.DataType = DataType.DateTime  
        'Specify the parameter as a UserDefinedTableTable object.  
        Dim udfp As UserDefinedFunctionParameter  
        udfp = New UserDefinedFunctionParameter(udf, "@param")  
        udfp.DataType = New DataType(udtt)  
        udfp.IsReadOnly = True  
        udf.Parameters.Add(udfp)  
        'Specify the TextBody property to the Transact-SQL definition of the  
        'user-defined function.  
        udf.TextBody = "BEGIN RETURN (GETDATE());end"  
        'Create the user-defined function.  
        udf.Create()  
```  
  
## <a name="creating-a-user-defined-table-in-visual-c"></a>Creazione di una tabella definita dall'utente in Visual C#  
 Per questo esempio, sarà necessario includere un'istruzione Imports per la libreria di classi che contiene il tipo **StringCollection** .  
  
 `using System.Collections.Specialized;`  
  
 Nell'esempio viene illustrato come creare una tabella definita dall'utente e come utilizzarla quindi come parametro in una funzione definita dall'utente.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server   
               Server srv = new Server();  
  
            //Reference the AdventureWorks2012 database.   
            Database db = srv.Databases["AdventureWorks2012"];  
            //Define a UserDefinedTableType object variable by supplying the  
            //database and name in the constructor.   
         UserDefinedTableType udtt = new UserDefinedTableType(db, "My_User_Defined_Table");  
  
            //Add three columns of different types to the   
            //UserDefinedTableType object.   
         udtt.Columns.Add(new Column(udtt, "Col1", DataType.Int));  
         udtt.Columns.Add(new Column(udtt, "Col2", DataType.VarCharMax));  
         udtt.Columns.Add(new Column(udtt, "Col3", DataType.Money));  
  
            //Define an Index object variable by supplying the user-defined   
            //table variable and name in the constructor.   
  
            Index idx = new Index(udtt, "PK_UddtTable");  
  
            //Add the first column in the user-defined table as   
            //the indexed column.   
            idx.IndexedColumns.Add(new IndexedColumn(idx, "Col1"));  
            //Specify that the index is a clustered, unique, primary key.   
            idx.IsClustered = true;  
            idx.IsUnique = true;  
            idx.IndexKeyType = IndexKeyType.DriPrimaryKey;  
            udtt.Indexes.Add(idx);  
            //Add the index and create the user-defined table.   
            udtt.Create();  
  
            //Display the Transact-SQL creation script for the   
            //user-defined table.   
            System.Collections.Specialized.StringCollection sc;  
            sc = udtt.Script();  
            foreach (string s in sc)  
            {  
                Console.WriteLine(s);  
            }  
  
            //Define a new user-defined function with a single parameter.  
            UserDefinedFunction udf = new UserDefinedFunction(db, "My_User_Defined_Function");  
            udf.TextMode = false;  
            udf.FunctionType = UserDefinedFunctionType.Scalar;  
            udf.ImplementationType = ImplementationType.TransactSql;  
            udf.DataType = DataType.DateTime;  
  
            //Specify the parameter as a UserDefinedTableTable object.  
             UserDefinedFunctionParameter udfp = new UserDefinedFunctionParameter(udf, "@param");  
            udfp.DataType = new DataType(udtt);  
            udfp.IsReadOnly = true;  
            udf.Parameters.Add(udfp);  
  
            //Specify the TextBody property to the Transact-SQL definition of the   
            //user-defined function.   
            udf.TextBody = "BEGIN RETURN (GETDATE());end";  
            //Create the user-defined function.   
            udf.Create();  
        }  
```  
  
## <a name="creating-a-user-defined-table-in-powershell"></a>Creazione di una tabella definita dall'utente in PowerShell  
 Per questo esempio, sarà necessario includere un'istruzione Imports per la libreria di classi che contiene il tipo **StringCollection** .  
  
 `using System.Collections.Specialized;`  
  
 Nell'esempio viene illustrato come creare una tabella definita dall'utente e come utilizzarla quindi come parametro in una funzione definita dall'utente.  
  
```powershell   
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
#Define a UserDefinedTableType object variable by supplying the  
#database and name in the constructor.   
$udtt = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedTableType `  
-argumentlist $db, "My_User_Defined_Table"  
  
#Add three columns of different types to the UserDefinedTableType object.  
  
$type = [Microsoft.SqlServer.Management.SMO.DataType]::Int  
$col = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column `  
-argumentlist $udtt, "col1",$type  
$udtt.Columns.Add($col)  
  
$type = [Microsoft.SqlServer.Management.SMO.DataType]::VarCharMax  
$col = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column `  
-argumentlist $udtt, "col2",$type  
$udtt.Columns.Add($col)  
  
 $type = [Microsoft.SqlServer.Management.SMO.DataType]::Money  
$col = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column `  
-argumentlist $udtt, "col3",$type  
$udtt.Columns.Add($col)          
  
#Define an Index object variable by supplying the user-defined   
#table variable and name in the constructor.   
$idx = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Index `  
-argumentlist $udtt, "PK_UddtTable"  
  
#Add the first column in the user-defined table as   
#the indexed column.   
$idxcol = New-Object -TypeName Microsoft.SqlServer.Management.SMO.IndexedColumn `  
-argumentlist $idx, "Col1"  
$idx.IndexedColumns.Add($idxcol)  
  
#Specify that the index is a clustered, unique, primary key.   
$idx.IsClustered = $true  
$idx.IsUnique = $true  
$idx.IndexKeyType = [Microsoft.SqlServer.Management.SMO.IndexKeyType]::DriPrimaryKey;  
  
#Add the index and create the user-defined table.   
$udtt.Indexes.Add($idx)  
$udtt.Create();  
  
# Display the Transact-SQL creation script for the   
# user-defined table.   
$sc = $udtt.Script()  
$sc  
  
# Define a new user-defined function with a single parameter.   
$udf = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunction `  
-argumentlist $db, "My_User_Defined_Function"  
$udf.TextMode = $false  
$udf.FunctionType = [Microsoft.SqlServer.Management.SMO.UserDefinedFunctionType]::Scalar  
$udf.ImplementationType = [Microsoft.SqlServer.Management.SMO.ImplementationType]::TransactSql  
$udf.DataType = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
  
# Specify the parameter as a UserDefinedTableTable object.  
$udfp = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunctionParameter `  
-argumentlist $udf, "@param"  
$type    =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.DataType `  
-argumentlist $udtt  
$udfp.DataType = $type  
$udfp.IsReadOnly = $true  
$udf.Parameters.Add($udfp)  
  
# Specify the TextBody property to the Transact-SQL definition of the   
# user-defined function.   
$udf.TextBody = "BEGIN RETURN (GETDATE());end"  
  
# Create the user-defined function.   
$udf.Create()           
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.SqlServer.Management.Smo.FileGroup>   
 [Filegroup e file di database](../../../relational-databases/databases/database-files-and-filegroups.md)   
  
  
