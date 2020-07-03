---
title: Creazione, modifica e rimozione delle funzioni definite dall'utente
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- user-defined functions [SMO]
ms.assetid: 0ebebd3b-0775-41c2-989d-aa4cf81af12a
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7eee04fd4d3ad5b56f72c1bf13b5a2c27c7741ff
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85894091"
---
# <a name="creating-altering-and-removing-user-defined-functions"></a>Creazione, modifica e rimozione delle funzioni definite dall'utente
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw.md)]
  L' <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> oggetto fornisce funzionalità che consentono agli utenti di gestire a livello di codice le funzioni definite dall'utente in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Le funzioni definite dall'utente supportano parametri di input e di output e riferimenti diretti alle colonne delle tabelle.  
  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è necessario registrare gli assembly all'interno di un database prima di poterli utilizzare in stored procedure, funzioni definite dall'utente, trigger e tipi di dati definiti dall'utente. In SMO questa funzionalità è supportata con l'oggetto <xref:Microsoft.SqlServer.Management.Smo.SqlAssembly>.  
  
 L'oggetto <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> fa riferimento all'assembly .NET con le proprietà <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.AssemblyName%2A>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.ClassName%2A> e <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.MethodName%2A>.  
  
 Quando l'oggetto <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> fa riferimento a un assembly .NET, è necessario registrare l'assembly creando un oggetto <xref:Microsoft.SqlServer.Management.Smo.SqlAssembly> e aggiungendolo all'oggetto <xref:Microsoft.SqlServer.Management.Smo.SqlAssemblyCollection> che appartiene all'oggetto <xref:Microsoft.SqlServer.Management.Smo.Database>.  
  
## <a name="example"></a>Esempio  
 Per usare qualsiasi esempio di codice fornito, è necessario scegliere l'ambiente di programmazione, il modello di programmazione e il linguaggio di programmazione per la creazione dell'applicazione. Per altre informazioni, vedere [creare un progetto Visual C&#35; SMO in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-scalar-user-defined-function-in-visual-basic"></a>Creazione di una funzione scalare definita dall'utente in Visual Basic  
 In questo esempio di codice viene illustrato come creare e rimuovere una funzione scalare definita dall'utente con un parametro dell'oggetto <xref:System.DateTime> di input e un tipo restituito integer in [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]. La funzione definita dall'utente viene creata nel database [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . Nell'esempio viene creata una funzione definita dall'utente, ISOweek, che accetta un argomento data per calcolare il numero di settimana ISO. Affinché il calcolo venga eseguito correttamente, è necessario impostare l'opzione DATEFIRST del database su 1 prima di chiamare la funzione.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 2008R2 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define a UserDefinedFunction object variable by supplying the parent database and the name arguments in the constructor.
Dim udf As UserDefinedFunction
udf = New UserDefinedFunction(db, "IsOWeek")
'Set the TextMode property to false and then set the other properties.
udf.TextMode = False
udf.DataType = DataType.Int
udf.ExecutionContext = ExecutionContext.Caller
udf.FunctionType = UserDefinedFunctionType.Scalar
udf.ImplementationType = ImplementationType.TransactSql
'Add a parameter.
Dim par As UserDefinedFunctionParameter
par = New UserDefinedFunctionParameter(udf, "@DATE", DataType.DateTime)
udf.Parameters.Add(par)
'Set the TextBody property to define the user defined function.
udf.TextBody = "BEGIN  DECLARE @ISOweek int SET @ISOweek= DATEPART(wk,@DATE)+1 -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104') IF (@ISOweek=0) SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1 AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1 IF ((DATEPART(mm,@DATE)=12) AND ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28)) SET @ISOweek=1 RETURN(@ISOweek) END;"
'Create the user defined function on the instance of SQL Server.
udf.Create()
'Remove the user defined function.
udf.Drop()
``` 
  
## <a name="creating-a-scalar-user-defined-function-in-visual-c"></a>Creazione di una funzione scalare definita dall'utente in Visual C#  
 In questo esempio di codice viene illustrato come creare e rimuovere una funzione scalare definita dall'utente con un parametro dell'oggetto <xref:System.DateTime> di input e un tipo restituito integer in [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]. La funzione definita dall'utente viene creata nel database [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . Nell'esempio viene creata la funzione definita dall'utente. `ISOweek`. Questa funzione calcola il numero di settimana ISO in base a un argomento di data specificato. Affinché il calcolo venga eseguito correttamente, è necessario impostare l'opzione `DATEFIRST` del database su `1` prima di chiamare la funzione.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
           Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
           Database db = srv.Databases["AdventureWorks2012"];  
  
            //Define a UserDefinedFunction object variable by supplying the parent database and the name arguments in the constructor.   
            UserDefinedFunction udf = new UserDefinedFunction(db, "IsOWeek");  
  
            //Set the TextMode property to false and then set the other properties.   
            udf.TextMode = false;  
            udf.DataType = DataType.Int;  
            udf.ExecutionContext = ExecutionContext.Caller;  
            udf.FunctionType = UserDefinedFunctionType.Scalar;  
            udf.ImplementationType = ImplementationType.TransactSql;  
  
            //Add a parameter.   
  
     UserDefinedFunctionParameter par = new UserDefinedFunctionParameter(udf, "@DATE", DataType.DateTime);  
            udf.Parameters.Add(par);  
  
            //Set the TextBody property to define the user-defined function.   
            udf.TextBody = "BEGIN DECLARE @ISOweek int SET @ISOweek= DATEPART(wk,@DATE)+1 -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104') IF (@ISOweek=0) SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1 AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1 IF ((DATEPART(mm,@DATE)=12) AND ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28)) SET @ISOweek=1 RETURN(@ISOweek) END;";  
  
            //Create the user-defined function on the instance of SQL Server.   
            udf.Create();  
  
            //Remove the user-defined function.   
            udf.Drop();  
        }  
```  
  
## <a name="creating-a-scalar-user-defined-function-in-powershell"></a>Creazione di una funzione scalare definita dall'utente in PowerShell  
 In questo esempio di codice viene illustrato come creare e rimuovere una funzione scalare definita dall'utente con un parametro dell'oggetto <xref:System.DateTime> di input e un tipo restituito integer in [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]. La funzione definita dall'utente viene creata nel database [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . Nell'esempio viene creata la funzione definita dall'utente. `ISOweek`. Questa funzione calcola il numero di settimana ISO in base a un argomento di data specificato. Affinché il calcolo venga eseguito correttamente, è necessario impostare l'opzione `DATEFIRST` del database su `1` prima di chiamare la funzione.  
  
```powershell   
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a user defined function object variable by supplying the parent database and name arguments in the constructor.   
$udf  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunction `  
-argumentlist $db, "IsOWeek"  
  
# Set the TextMode property to false and then set the other properties.   
$udf.TextMode = $false  
$udf.DataType = [Microsoft.SqlServer.Management.SMO.DataType]::Int   
$udf.ExecutionContext = [Microsoft.SqlServer.Management.SMO.ExecutionContext]::Caller  
$udf.FunctionType = [Microsoft.SqlServer.Management.SMO.UserDefinedFunctionType]::Scalar  
$udf.ImplementationType = [Microsoft.SqlServer.Management.SMO.ImplementationType]::TransactSql  
  
# Define a Parameter object variable by supplying the parent function, name and type arguments in the constructor.  
$type = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$par  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunctionParameter `  
-argumentlist $udf, "@DATE",$type  
  
# Add the parameter to the function  
$udf.Parameters.Add($par)  
  
#Set the TextBody property to define the user-defined function.   
$udf.TextBody = "BEGIN DECLARE @ISOweek int SET @ISOweek= DATEPART(wk,@DATE)+1 -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104') IF (@ISOweek=0) SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1 AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1 IF ((DATEPART(mm,@DATE)=12) AND ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28)) SET @ISOweek=1 RETURN(@ISOweek) END;"  
  
# Create the user-defined function on the instance of SQL Server.   
$udf.Create()  
  
# Remove the user-defined function.   
$udf.Drop()  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction>  
  
  
