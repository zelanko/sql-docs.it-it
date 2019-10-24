---
title: Creazione, modifica e rimozione di funzioni definite dall'utente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- user-defined functions [SMO]
ms.assetid: 0ebebd3b-0775-41c2-989d-aa4cf81af12a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: edde17b3339a6a78f81ddf92da95afb2f8ba851c
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782346"
---
# <a name="creating-altering-and-removing-user-defined-functions"></a>Creazione, modifica e rimozione delle funzioni definite dall'utente
  L'oggetto <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> fornisce funzionalità che consentono agli utenti di gestire a livello di codice le funzioni definite dall'utente nei [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. Le funzioni definite dall'utente supportano parametri di input e di output e riferimenti diretti alle colonne delle tabelle.  
  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è necessario registrare gli assembly all'interno di un database prima di poterli utilizzare in stored procedure, funzioni definite dall'utente, trigger e tipi di dati definiti dall'utente. In SMO questa funzionalità è supportata con l'oggetto <xref:Microsoft.SqlServer.Management.Smo.SqlAssembly>.  
  
 L'oggetto <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> fa riferimento all'assembly .NET con le proprietà <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.AssemblyName%2A>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.ClassName%2A> e <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.MethodName%2A>.  
  
 Quando l'oggetto <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> fa riferimento a un assembly .NET, è necessario registrare l'assembly creando un oggetto <xref:Microsoft.SqlServer.Management.Smo.SqlAssembly> e aggiungendolo all'oggetto <xref:Microsoft.SqlServer.Management.Smo.SqlAssemblyCollection> che appartiene all'oggetto <xref:Microsoft.SqlServer.Management.Smo.Database>.  
  
## <a name="example"></a>Esempio  
 Per usare qualsiasi esempio di codice fornito, è necessario scegliere l'ambiente di programmazione, il modello di programmazione e il linguaggio di programmazione per la creazione dell'applicazione. Per ulteriori informazioni, vedere [creare un Visual Basic progetto SMO in Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) o [creare un progetto Visual&#35; C SMO in Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-scalar-user-defined-function-in-visual-basic"></a>Creazione di una funzione scalare definita dall'utente in Visual Basic  
 In questo esempio di codice viene illustrato come creare e rimuovere una funzione scalare definita dall'utente con un parametro dell'oggetto <xref:System.DateTime> di input e un tipo restituito integer in [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]. La funzione definita dall'utente viene creata nel database [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . Nell'esempio viene creata una funzione definita dall'utente, ISOweek, che accetta un argomento data per calcolare il numero di settimana ISO. Affinché il calcolo venga eseguito correttamente, è necessario impostare l'opzione DATEFIRST del database su 1 prima di chiamare la funzione.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBUserDefFuncs1](SMO How to#SMO_VBUserDefFuncs1)]  -->  
  
## <a name="creating-a-scalar-user-defined-function-in-visual-c"></a>Creazione di una funzione scalare definita dall'utente in Visual C#  
 In questo esempio di codice viene illustrato come creare e rimuovere una funzione scalare definita dall'utente con un parametro dell'oggetto <xref:System.DateTime> di input e un tipo restituito integer in [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]. La funzione definita dall'utente viene creata nel database [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . Nell'esempio viene creata la funzione definita dall'utente. `ISOweek`(Indici per tabelle con ottimizzazione per la memoria). Questa funzione calcola il numero di settimana ISO in base a un argomento di data specificato. Affinché il calcolo venga eseguito correttamente, è necessario impostare l'opzione `DATEFIRST` del database su `1` prima di chiamare la funzione.  
  
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
 In questo esempio di codice viene illustrato come creare e rimuovere una funzione scalare definita dall'utente con un parametro dell'oggetto <xref:System.DateTime> di input e un tipo restituito integer in [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]. La funzione definita dall'utente viene creata nel database [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . Nell'esempio viene creata la funzione definita dall'utente. `ISOweek`(Indici per tabelle con ottimizzazione per la memoria). Questa funzione calcola il numero di settimana ISO in base a un argomento di data specificato. Affinché il calcolo venga eseguito correttamente, è necessario impostare l'opzione `DATEFIRST` del database su `1` prima di chiamare la funzione.  
  
```powershell
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = Get-Item Adventureworks2012  
  
# Define a user defined function object variable by supplying the parent database and name arguments in the constructor.
$udf  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunction -argumentlist $db, "IsOWeek"  
  
# Set the TextMode property to false and then set the other properties.
$udf.TextMode = $false  
$udf.DataType = [Microsoft.SqlServer.Management.SMO.DataType]::Int
$udf.ExecutionContext = [Microsoft.SqlServer.Management.SMO.ExecutionContext]::Caller  
$udf.FunctionType = [Microsoft.SqlServer.Management.SMO.UserDefinedFunctionType]::Scalar  
$udf.ImplementationType = [Microsoft.SqlServer.Management.SMO.ImplementationType]::TransactSql  
  
# Define a Parameter object variable by supplying the parent function, name and type arguments in the constructor.  
$type = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$par  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunctionParameter -argumentlist $udf, "@DATE",$type  
  
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
