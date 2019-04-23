---
title: Gestire SQL Server in Linux con PowerShell | Microsoft Docs
description: Questo articolo offre una panoramica dell'uso di PowerShell in Windows con SQL Server in Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: a3492ce1-5d55-4505-983c-d6da8d1a94ad
ms.openlocfilehash: 903d2d89ca0d551cbb78cfb69dd305f852f62313
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158767"
---
# <a name="use-powershell-on-windows-to-manage-sql-server-on-linux"></a>Usare PowerShell in Windows per gestire SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo introduce [SQL Server PowerShell](../powershell/sql-server-powershell.md) e illustra alcuni esempi su come usare questa funzionalità con SQL Server in Linux. Supporto di PowerShell per SQL Server è attualmente disponibile in Windows, quindi è possibile usare quando si dispone di un computer Windows che può connettersi a un'istanza remota di SQL Server in Linux.

## <a name="install-the-newest-version-of-sql-powershell-on-windows"></a>Installare la versione più recente di PowerShell per SQL in Windows

[PowerShell per SQL](../powershell/download-sql-server-ps-module.md) in Windows viene mantenuta in PowerShell Gallery. Quando si lavora con SQL Server, è consigliabile usare sempre la versione più recente del modulo SqlServer PowerShell.

## <a name="before-you-begin"></a>Operazioni preliminari

Leggere il [problemi noti](sql-server-linux-release-notes.md) per SQL Server in Linux.

## <a name="launch-powershell-and-import-the-sqlserver-module"></a>Avviare PowerShell e importare il *sqlserver* modulo

Per iniziare, avviare PowerShell su Windows. Aprire una *prompt dei comandi* nel computer Windows e digitare **PowerShell** per avviare una nuova sessione di Windows PowerShell.

```
PowerShell
```

SQL Server fornisce un modulo di Windows PowerShell denominato **SqlServer** che è possibile usare per importare i componenti di SQL Server (provider di SQL Server e i cmdlet) in un ambiente di PowerShell o script.

Copiare e incollare il comando seguente al prompt di PowerShell per importare i **SqlServer** modulo nella sessione corrente di PowerShell:

```powershell
Import-Module SqlServer
```

Digitare il comando seguente al prompt di PowerShell per verificare che il **SqlServer** modulo è stato importato correttamente:

```powershell
Get-Module -Name SqlServer
```

PowerShell dovrebbe riportare informazioni simili all'output seguente:

```
ModuleType Version    Name          ExportedCommands
---------- -------    ----          ----------------
Script     21.1.18102 SqlServer     {Add-SqlAvailabilityDatabase, Add-SqlAvailabilityGroupList...
```

## <a name="connect-to-sql-server-and-get-server-information"></a>Connettersi a SQL Server e ottenere informazioni sul server

È possibile usare PowerShell in Windows per connettersi all'istanza di SQL Server in Linux e visualizzare un paio di proprietà del server.

Copiare e incollare i comandi seguenti al prompt di PowerShell. Quando si eseguono questi comandi, verranno PowerShell:
- Visualizzazione di *richiesta credenziali di Windows PowerShell* finestra di dialogo in cui vengono richieste le credenziali (*nome utente SQL* e *password SQL*) per connettersi a SQL Server istanza in Linux
- Creare un'istanza di [Server](https://msdn.microsoft.com/library/microsoft.sqlserver.management.smo.server.aspx) oggetto
- Connettere il **Server** e visualizzare alcune proprietà

Ricordare di sostituire **\<your_server_instance\>** con l'indirizzo IP o il nome host dell'istanza di SQL Server in Linux.

```powershell
# Prompt for credentials to login into SQL Server
$serverInstance = "<your_server_instance>"
$credential = Get-Credential

# Connect to the Server and get a few properties
Get-SqlInstance -ServerInstance $serverInstance -Credential $credential
# done
```

PowerShell dovrebbe riportare informazioni simili all'output seguente:

```
Instance Name                   Version    ProductLevel UpdateLevel  HostPlatform HostDistribution                
-------------                   -------    ------------ -----------  ------------ ----------------                
your_server_instance            14.0.3048  RTM          CU13         Linux        Ubuntu 
```
> [!NOTE]
> Se per questi valori viene visualizzato nulla, molto probabilmente la connessione all'istanza di SQL Server di destinazione non riuscita. Assicurarsi che è possibile usare le stesse informazioni di connessione per la connessione da SQL Server Management Studio. Rivedere poi i [consigli per la risoluzione dei problemi di connessione](sql-server-linux-troubleshooting-guide.md#connection).

## <a name="examine-sql-server-error-logs"></a>Esaminare i log degli errori di SQL Server

È possibile usare PowerShell in Windows per esaminare i log degli errori connettersi nell'istanza di SQL Server in Linux. Si userà anche il **Out-GridView** cmdlet per visualizzare le informazioni dall'errore log in una visualizzazione griglia.

Copiare e incollare i comandi seguenti al prompt di PowerShell. Si potrebbero richiedere alcuni minuti per l'esecuzione. Questi comandi le operazioni seguenti:
- Visualizzazione di *richiesta credenziali di Windows PowerShell* finestra di dialogo in cui vengono richieste le credenziali (*nome utente SQL* e *password SQL*) per connettersi a SQL Server istanza in Linux
- Usare il **Get-SqlErrorLog** log di cmdlet per connettersi all'istanza di SQL Server in Linux e recuperare l'errore poiché **ieri**
- Inviare tramite pipe l'output per il **Out-GridView** cmdlet

Ricordare di sostituire **\<your_server_instance\>** con l'indirizzo IP o il nome host dell'istanza di SQL Server in Linux.

```powershell
# Prompt for credentials to login into SQL Server
$serverInstance = "<your_server_instance>"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday | Out-GridView
# done
```
## <a name="see-also"></a>Vedere anche
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)
