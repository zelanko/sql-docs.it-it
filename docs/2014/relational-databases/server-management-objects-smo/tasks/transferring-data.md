---
title: Trasferimento di dati | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- data transfers [SMO]
- transferring data
ms.assetid: eea255c3-8251-40f0-973b-fe4ef6cb5261
author: stevestein
ms.author: sstein
ms.openlocfilehash: aefe926d487a78c3ab73ac08483932e2d0a44410
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85037504"
---
# <a name="transferring-data"></a>Trasferimento di dati
  La classe <xref:Microsoft.SqlServer.Management.Smo.Transfer> è una classe di utilità che fornisce gli strumenti per trasferire oggetti e dati.  
  
 Gli oggetti nello schema del database vengono trasferiti eseguendo uno script generato sul server di destinazione. I dati <xref:Microsoft.SqlServer.Management.Smo.Table> vengono trasferiti con un pacchetto DTS creato dinamicamente.  
  
 L'oggetto <xref:Microsoft.SqlServer.Management.Smo.Transfer> contiene tutte le funzionalità degli oggetti <xref:Microsoft.SqlServer.Management.Smo.Transfer> in DMO e altre funzionalità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Tuttavia, in SMO in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] , l' <xref:Microsoft.SqlServer.Management.Smo.Transfer> oggetto usa l'API [SqlBulkCopy](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy\(v=VS.90\).aspx) per trasferire i dati. Inoltre, i metodi e le proprietà utilizzati per eseguire trasferimenti di dati si trovano nell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Transfer> anziché nell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Database>. Lo spostamento delle funzionalità dalle classi di istanze alle classi di utilità è coerente con un modello a oggetti semplificato poiché il codice per le attività specifiche viene caricato solo quando è richiesto.  
  
 L'oggetto <xref:Microsoft.SqlServer.Management.Smo.Transfer> non supporta trasferimenti di dati in un database di destinazione con una proprietà <xref:Microsoft.SqlServer.Management.Smo.Database.CompatibilityLevel%2A> inferiore alla versione dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Esempio  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="transferring-schema-and-data-from-one-database-to-another-in-visual-basic"></a>Trasferimento di schemi e dati da un database a un altro in Visual Basic  
 In questo esempio di codice viene illustrato come trasferire schemi e dati da un database all'altro utilizzando l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.  
  
```vb
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 2008R2 database
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Create a new database that is to be destination database.
Dim dbCopy As Database
dbCopy = New Database(srv, "AdventureWorks2012Copy")
dbCopy.Create()
'Define a Transfer object and set the required options and properties.
Dim xfr As Transfer
xfr = New Transfer(db)
xfr.CopyAllTables = True
xfr.Options.WithDependencies = True
xfr.Options.ContinueScriptingOnError = True
xfr.DestinationDatabase = "AdventureWorks2012Copy"
xfr.DestinationServer = srv.Name
xfr.DestinationLoginSecure = True
xfr.CopySchema = True
'Script the transfer. Alternatively perform immediate data transfer with TransferData method.
xfr.ScriptTransfer()
```
  
## <a name="transferring-schema-and-data-from-one-database-to-another-in-visual-c"></a>Trasferimento di schemi e dati da un database all'altro in Visual C#  
 In questo esempio di codice viene illustrato come trasferire schemi e dati da un database all'altro utilizzando l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.  
  
```csharp
{  
            Server srv;  
            srv = new Server();  
            //Reference the AdventureWorks2012 database   
            Database db;  
            db = srv.Databases["AdventureWorks2012"];  
            //Create a new database that is to be destination database.   
            Database dbCopy;  
            dbCopy = new Database(srv, "AdventureWorks2012Copy");  
            dbCopy.Create();  
            //Define a Transfer object and set the required options and properties.   
            Transfer xfr;  
            xfr = new Transfer(db);  
            xfr.CopyAllTables = true;  
            xfr.Options.WithDependencies = true;  
            xfr.Options.ContinueScriptingOnError = true;  
            xfr.DestinationDatabase = "AdventureWorks2012Copy";  
            xfr.DestinationServer = srv.Name;  
            xfr.DestinationLoginSecure = true;  
            xfr.CopySchema = true;  
            //Script the transfer. Alternatively perform immediate data transfer   
            // with TransferData method.   
            xfr.ScriptTransfer();  
        }   
```  
  
## <a name="transferring-schema-and-data-from-one-database-to-another-in-powershell"></a>Trasferimento di schemi e dati da un database all'altro in PowerShell  
 In questo esempio di codice viene illustrato come trasferire schemi e dati da un database all'altro utilizzando l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.  
  
```powershell
#Connect to the local, default instance of SQL Server.  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Reference the AdventureWorks2012 database.  
$db = $srv.Databases["AdventureWorks2012"]  
  
#Create a database to hold the copy of AdventureWorks  
$dbCopy = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Database -ArgumentList $srv, "AdventureWorksCopy"  
$dbCopy.Create()  
  
#Define a Transfer object and set the required options and properties.  
$xfr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Transfer -ArgumentList $db  
  
#Set this objects properties  
$xfr.CopyAllTables = $true  
$xfr.Options.WithDependencies = $true  
$xfr.Options.ContinueScriptingOnError = $true  
$xfr.DestinationDatabase = "AdventureWorksCopy"  
$xfr.DestinationServer = $srv.Name  
$xfr.DestinationLoginSecure = $true  
$xfr.CopySchema = $true  
"Scripting Data Transfer"  
#Script the transfer. Alternatively perform immediate data transfer with TransferData method.  
$xfr.ScriptTransfer()  
```  
