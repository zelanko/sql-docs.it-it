---
title: Creazione, modifica e rimozione di trigger | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- triggers [SMO]
ms.assetid: 8ddbe23b-6e31-4f8e-8a70-17bd5072413e
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bd2aa0bce55273295cfde3b15d2863d7e35f3d26
ms.sourcegitcommit: f3f83ef95399d1570851cd1360dc2f072736bef6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2019
ms.locfileid: "70911260"
---
# <a name="creating-altering-and-removing-triggers"></a>Creazione, modifica e rimozione di trigger
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]
  In SMO i trigger sono rappresentati tramite l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Trigger>. Il [!INCLUDE[tsql](../../../includes/tsql-md.md)] codice che viene eseguito quando il trigger attivato viene impostato <xref:Microsoft.SqlServer.Management.Smo.Trigger.TextBody%2A> dalla proprietà dell'oggetto trigger. Il tipo di trigger viene impostato tramite altre proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Trigger>, ad esempio la proprietà <xref:Microsoft.SqlServer.Management.Smo.Trigger.Update%2A>. Si tratta di una proprietà booleana che specifica se il trigger viene attivato da un **aggiornamento** dei record nella tabella padre.  
  
 L'oggetto <xref:Microsoft.SqlServer.Management.Smo.Trigger> rappresenta trigger DML (Data Manipulation Language) tradizionali. In [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e versioni successive sono supportati anche i trigger DDL (Data Definition Language). I trigger DDL sono rappresentati dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.DatabaseDdlTrigger> e dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.ServerDdlTrigger>.  
  
## <a name="example"></a>Esempio  
Per usare qualsiasi esempio di codice fornito, è necessario scegliere l'ambiente di programmazione, il modello di programmazione e il linguaggio di programmazione per la creazione dell'applicazione. Per altre informazioni, vedere [creare un progetto Visual&#35; C SMO in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
 
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-basic"></a>Creazione, modifica e rimozione di un trigger in Visual Basic  
 In questo esempio di codice viene illustrato come creare e inserire un trigger di aggiornamento in una tabella esistente, denominata `Sales`, nel database di [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]. Il trigger invia un messaggio di promemoria quando la tabella viene aggiornata o quando viene inserito un nuovo record.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim mysrv As Server
mysrv = New Server
'Reference the AdventureWorks2012 2008R2 database.
Dim mydb As Database
mydb = mysrv.Databases("AdventureWorks2012")
'Declare a Table object variable and reference the Customer table.
Dim mytab As Table
mytab = mydb.Tables("Customer", "Sales")
'Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.
Dim tr As Trigger
tr = New Trigger(mytab, "Sales")
'Set TextMode property to False, then set other properties to define the trigger.
tr.TextMode = False
tr.Insert = True
tr.Update = True
tr.InsertOrder = Agent.ActivationOrder.First
Dim stmt As String
stmt = " RAISERROR('Notify Customer Relations',16,10) "
tr.TextBody = stmt
tr.ImplementationType = ImplementationType.TransactSql
'Create the trigger on the instance of SQL Server.
tr.Create()
'Remove the trigger.
tr.Drop()
``` 
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-c"></a>Creazione, modifica e rimozione di un trigger in Visual C#  
 In questo esempio di codice viene illustrato come creare e inserire un trigger di aggiornamento in una tabella esistente, denominata `Sales`, nel database di [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]. Il trigger invia un messaggio di promemoria quando la tabella viene aggiornata o quando viene inserito un nuovo record.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server mysrv;  
            mysrv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database mydb;  
            mydb = mysrv.Databases["AdventureWorks2012"];  
            //Declare a Table object variable and reference the Customer table.   
            Table mytab;  
            mytab = mydb.Tables["Customer", "Sales"];  
            //Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.   
            Trigger tr;  
            tr = new Trigger(mytab, "Sales");  
            //Set TextMode property to False, then set other properties to define the trigger.   
            tr.TextMode = false;  
            tr.Insert = true;  
            tr.Update = true;  
            tr.InsertOrder = ActivationOrder.First;  
            string stmt;  
            stmt = " RAISERROR('Notify Customer Relations',16,10) ";  
            tr.TextBody = stmt;  
            tr.ImplementationType = ImplementationType.TransactSql;  
            //Create the trigger on the instance of SQL Server.   
            tr.Create();  
            //Remove the trigger.   
            tr.Drop();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-trigger-in-powershell"></a>Creazione, modifica e rimozione di un trigger in PowerShell  
 In questo esempio di codice viene illustrato come creare e inserire un trigger di aggiornamento in una tabella esistente, denominata `Sales`, nel database di [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]. Il trigger invia un messaggio di promemoria quando la tabella viene aggiornata o quando viene inserito un nuovo record.  
  
```powershell  
# Set the path context to the local, default instance of SQL Server and to the  
#database tables in Adventureworks2012  
CD \sql\localhost\default\databases\AdventureWorks2012\Tables\  
  
#Get reference to the trigger's target table  
$mytab = get-item Sales.Customer  
  
# Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.  
$tr  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Trigger `  
-argumentlist $mytab, "Sales"  
  
# Set TextMode property to False, then set other properties to define the trigger.   
$tr.TextMode = $false  
$tr.Insert = $true  
$tr.Update = $true  
$tr.InsertOrder = [Microsoft.SqlServer.Management.SMO.Agent.ActivationOrder]::First  
$tr.TextBody = " RAISERROR('Notify Customer Relations',16,10) "  
$tr.ImplementationType = [Microsoft.SqlServer.Management.SMO.ImplementationType]::TransactSql  
  
# Create the trigger on the instance of SQL Server.   
$tr.Create()  
  
#Remove the trigger.   
$tr.Drop()  
```  
  
  
