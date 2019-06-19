---
title: Gestire SQL Server in Linux con PowerShell | Microsoft Docs
description: Questo articolo offre una panoramica dell'uso di PowerShell in Windows con SQL Server in Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: a3492ce1-5d55-4505-983c-d6da8d1a94ad
ms.openlocfilehash: 8398db9e03aabf6863bd770f8be6657b58be1591
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718080"
---
# <a name="use-powershell-on-windows-to-manage-sql-server-on-linux"></a>Usare PowerShell in Windows per gestire SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo introduce [SQL Server PowerShell](../powershell/sql-server-powershell.md) e illustra alcuni esempi su come usare questa funzionalità con SQL Server in Linux. Supporto di PowerShell per SQL Server è attualmente disponibile in Windows, MacOS e Linux. Questo articolo illustra l'uso di un computer Windows per connettersi a un'istanza remota di SQL Server in Linux.

## <a name="install-the-newest-version-of-sql-powershell-on-windows"></a>Installare la versione più recente di PowerShell per SQL in Windows

[PowerShell per SQL](../powershell/download-sql-server-ps-module.md) in Windows viene mantenuta in PowerShell Gallery. Quando si lavora con SQL Server, è consigliabile usare sempre la versione più recente del modulo SqlServer PowerShell.

## <a name="before-you-begin"></a>Operazioni preliminari

Leggere il [problemi noti](sql-server-linux-release-notes.md) per SQL Server in Linux.

## <a name="launch-powershell-and-import-the-sqlserver-module"></a>Avviare PowerShell e importare il *sqlserver* modulo

Per iniziare, avviare PowerShell su Windows. Uso <kbd>vincere</kbd>+<kbd>R</kbd>, nel computer Windows e digitare **PowerShell** per avviare una nuova sessione di Windows PowerShell.

```
PowerShell
```

SQL Server fornisce un modulo di PowerShell denominato **SqlServer**. È possibile usare la **SqlServer** module per importare i componenti di SQL Server (provider di SQL Server e i cmdlet) in un ambiente di PowerShell o script.

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
- Visualizzare una finestra di dialogo che richiede il nome host o indirizzo IP dell'istanza di
- Visualizzare il *richiesta di credenziali di Windows PowerShell* finestra di dialogo che richiede le credenziali. È possibile usare il *username SQL* e *password SQL* per connettersi all'istanza di SQL Server in Linux
- Usare la **Get-SqlInstance** per connettersi alle **Server** e visualizzare alcune proprietà

Facoltativamente, è sufficiente sostituire il `$serverInstance` variabile con l'indirizzo IP o il nome host dell'istanza di SQL Server.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
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

## <a name="using-the-sql-server-powershell-provider"></a>Tramite il Provider PowerShell per SQL Server

Un'altra opzione per la connessione all'istanza di SQL Server consiste nell'usare la [PowerShell Provider per SQL Server](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider).  Questo provider consente di passare l'istanza di SQL Server simile a come se si sono stati passando la struttura ad albero in Esplora oggetti, ma nella riga di comando.  Per impostazione predefinita questo provider viene presentato come un oggetto PSDrive denominato `SQLSERVER:\` che è possibile usare per connettersi ed esplorare le istanze di SQL Server che ha accesso l'account di dominio.  Visualizzare [passaggi di configurazione](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-auth-overview#configuration-steps) per informazioni su come configurare l'autenticazione di Active Directory per SQL Server in Linux.

È anche possibile usare l'autenticazione di SQL con il PowerShell Provider per SQL Server. A questo scopo, usare il `New-PSDrive` cmdlet per creare un nuovo dispositivo PSDrive e fornire le credenziali appropriate per la connessione.

In questo esempio riportato di seguito, si noterà un esempio di come creare un nuovo dispositivo PSDrive mediante l'autenticazione SQL.

```powershell
# NOTE: We are reusing the values saved in the $credential variable from the above example.
New-PSDrive -Name SQLonDocker -PSProvider SqlServer -Root 'SQLSERVER:\SQL\localhost,10002\Default\' -Credential $credential
```

È possibile verificare che l'unità è stata creata eseguendo la `Get-PSDrive` cmdlet.

```powershell
Get-PSDrive
```

Dopo aver creato il nuovo PSDrive, è possibile avviare lo spostamento.

```powershell
dir SQLonDocker:\Databases
```

Ecco ciò che l'output potrebbe essere simile.  È possibile notare che l'output è simile a ciò che SSMS verrà visualizzato nel nodo database.  Visualizza i database utente, ma non i database di sistema.

```powershell
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2016   Normal      209.63 MB    1.31 MB Simple       130 sa
AdventureWorksDW2012 Normal      167.00 MB   32.47 MB Simple       110 sa
AdventureWorksDW2014 Normal      188.00 MB   78.10 MB Simple       120 sa
AdventureWorksDW2016 Normal      172.00 MB   74.76 MB Simple       130 sa
AdventureWorksDW2017 Normal      208.00 MB   40.57 MB Simple       140 sa
```

Se si desidera vedere tutti i database sull'istanza, una possibilità consiste nell'utilizzare il [Get-SqlDatabase](https://docs.microsoft.com/powershell/module/sqlserver/Get-SqlDatabase) cmdlet.

## <a name="examine-sql-server-error-logs"></a>Esaminare i log degli errori di SQL Server

La procedura seguente usa PowerShell in Windows per esaminare l'errore di connessione di log nell'istanza di SQL Server in Linux. Si userà anche il **Out-GridView** cmdlet per visualizzare le informazioni dall'errore log in una visualizzazione griglia.

Copiare e incollare i comandi seguenti al prompt di PowerShell. Si potrebbero richiedere alcuni minuti per l'esecuzione. Questi comandi le operazioni seguenti:
- Visualizzare una finestra di dialogo che richiede il nome host o indirizzo IP dell'istanza di
- Visualizzare il *richiesta di credenziali di Windows PowerShell* finestra di dialogo che richiede le credenziali. È possibile usare il *username SQL* e *password SQL* per connettersi all'istanza di SQL Server in Linux
- Usare il **Get-SqlErrorLog** log di cmdlet per connettersi all'istanza di SQL Server in Linux e recuperare l'errore poiché **ieri**
- Inviare tramite pipe l'output per il **Out-GridView** cmdlet

Facoltativamente, è possibile sostituire il `$serverInstance` variabile con l'indirizzo IP o il nome host dell'istanza di SQL Server.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday | Out-GridView
# done
```
## <a name="see-also"></a>Vedere anche
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)
- [Cmdlet di SqlServer](https://docs.microsoft.com/powershell/module/sqlserver)
