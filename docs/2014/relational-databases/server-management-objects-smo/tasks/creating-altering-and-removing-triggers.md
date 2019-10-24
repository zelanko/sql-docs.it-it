---
title: Creazione, modifica e rimozione di trigger | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- triggers [SMO]
ms.assetid: 8ddbe23b-6e31-4f8e-8a70-17bd5072413e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 31430674d88d8aa5b820823a16dc18d110b9dd9a
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782306"
---
# <a name="creating-altering-and-removing-triggers"></a>Creazione, modifica e rimozione di trigger
  In SMO i trigger sono rappresentati tramite l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Trigger>. Il codice [!INCLUDE[tsql](../../../includes/tsql-md.md)] eseguito quando il trigger attivato viene impostato dalla proprietà <xref:Microsoft.SqlServer.Management.Smo.Trigger.TextBody%2A> dell'oggetto trigger. Il tipo di trigger viene impostato tramite altre proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Trigger>, ad esempio la proprietà <xref:Microsoft.SqlServer.Management.Smo.Trigger.Update%2A>. Si tratta di una proprietà booleana che specifica se il trigger viene attivato da una parola chiave `UPDATE` di record nella tabella padre.  
  
 L'oggetto <xref:Microsoft.SqlServer.Management.Smo.Trigger> rappresenta trigger DML (Data Manipulation Language) tradizionali. In [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e versioni successive sono supportati anche i trigger DDL (Data Definition Language). I trigger DDL sono rappresentati dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.DatabaseDdlTrigger> e dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.ServerDdlTrigger>.  
  
## <a name="example"></a>Esempio  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-basic"></a>Creazione, modifica e rimozione di un trigger in Visual Basic  
 In questo esempio di codice viene illustrato come creare e inserire un trigger di aggiornamento in una tabella esistente, denominata `Sales`, nel database di [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]. Il trigger invia un messaggio di promemoria quando la tabella viene aggiornata o quando viene inserito un nuovo record.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBTriggers1](SMO How to#SMO_VBTriggers1)]  -->  
  
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
$mytab = Get-Item Sales.Customer  
  
# Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.  
$tr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Trigger -argumentlist $mytab, "Sales"  
  
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
