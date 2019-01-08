---
title: Il trasferimento dei dati | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 49754be9b412f9cf6e7d660402527aed954a09fa
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53377673"
---
# <a name="transferring-data"></a>Trasferimento di dati
  La classe <xref:Microsoft.SqlServer.Management.Smo.Transfer> è una classe di utilità che fornisce gli strumenti per trasferire oggetti e dati.  
  
 Gli oggetti nello schema del database vengono trasferiti eseguendo uno script generato sul server di destinazione. I dati <xref:Microsoft.SqlServer.Management.Smo.Table> vengono trasferiti con un pacchetto DTS creato dinamicamente.  
  
 L'oggetto <xref:Microsoft.SqlServer.Management.Smo.Transfer> contiene tutte le funzionalità degli oggetti <xref:Microsoft.SqlServer.Management.Smo.Transfer> in DMO e altre funzionalità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Tuttavia, in SMO [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], il <xref:Microsoft.SqlServer.Management.Smo.Transfer> dell'oggetto viene utilizzato il [SQLBulkCopy](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy\(v=VS.90\).aspx) API per trasferire i dati. Inoltre, i metodi e le proprietà utilizzati per eseguire trasferimenti di dati si trovano nell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Transfer> anziché nell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Database>. Lo spostamento delle funzionalità dalle classi di istanze alle classi di utilità è coerente con un modello a oggetti semplificato poiché il codice per le attività specifiche viene caricato solo quando è richiesto.  
  
 L'oggetto <xref:Microsoft.SqlServer.Management.Smo.Transfer> non supporta trasferimenti di dati in un database di destinazione con una proprietà <xref:Microsoft.SqlServer.Management.Smo.Database.CompatibilityLevel%2A> inferiore alla versione dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Esempio  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="transferring-schema-and-data-from-one-database-to-another-in-visual-basic"></a>Trasferimento di schemi e dati da un database a un altro in Visual Basic  
 In questo esempio di codice viene illustrato come trasferire schemi e dati da un database all'altro utilizzando l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.  
  
```VBNET
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
  
```  
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
  
```  
#Connect to the local, default instance of SQL Server.  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Reference the AdventureWorks2012 database.  
$db = $srv.Databases["AdventureWorks2012"]  
  
#Create a database to hold the copy of AdventureWorks  
$dbCopy = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Database -argumentlist $srv, "AdventureWorksCopy"  
$dbCopy.Create()  
  
#Define a Transfer object and set the required options and properties.  
$xfr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Transfer -argumentlist $db  
  
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
  
  
