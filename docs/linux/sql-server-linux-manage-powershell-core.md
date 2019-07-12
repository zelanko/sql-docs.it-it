---
title: Gestire SQL Server in Linux con PowerShell Core
description: Questo articolo offre una panoramica dell'uso di PowerShell Core con SQL Server in Linux.
ms.date: 04/22/2019
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
author: SQLvariant
ms.author: aanelson
ms.reviewer: vanto
manager: jroth
ms.openlocfilehash: e96fe471f78e02e5667431f7065a169a5c136417
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834949"
---
# <a name="manage-sql-server-on-linux-with-powershell-core"></a>Gestire SQL Server in Linux con PowerShell Core

Questo articolo introduce [SQL Server PowerShell](../powershell/sql-server-powershell.md) e illustra alcuni esempi su come usarlo con il Core di PowerShell (PS Core) in macOS e Linux. PowerShell Core è ora un progetto Open Source sul [GitHub](https://github.com/powershell/powershell).

## <a name="cross-platform-editor-options"></a>Opzioni dell'editor multipiattaforma

Tutti i passaggi seguenti di PowerShell Core funzionerà in un terminale regolare oppure è possibile eseguirli da un terminale all'interno di Visual Studio Code o Data Studio di Azure.  Visual Studio Code sia Data Studio di Azure sono disponibili in macOS e Linux.  Per altre informazioni su Azure Data Studio, vedere [questa Guida introduttiva](https://docs.microsoft.com/sql/azure-data-studio/quickstart-sql-server).  È anche possibile provare a usare il [estensione PowerShell](https://docs.microsoft.com/sql/azure-data-studio/powershell-extension) appositamente.

## <a name="installing-powershell-core"></a>Installazione di PowerShell Core

Per altre informazioni sull'installazione di PowerShell Core in varie piattaforme supportate e sperimentale, vedere gli articoli seguenti:

- [Installazione di PowerShell Core in Windows](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-windows?view=powershell-6)
- [Installazione di PowerShell Core in Linux](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6)
- [Installazione di PowerShell Core in macOS](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-6)
- [Installazione di PowerShell Core in ARM](https://docs.microsoft.com/powershell/scripting/install/powershell-core-on-arm?view=powershell-6)

## <a name="install-the-sqlserver-module"></a>Installare il modulo SqlServer

Il `SqlServer` modulo viene mantenuto nel [PowerShell Gallery](https://www.powershellgallery.com/packages/SqlServer/). Quando si lavora con SQL Server, è consigliabile usare sempre la versione più recente del modulo SqlServer PowerShell.

Per installare il modulo SqlServer, aprire una sessione di PowerShell Core ed eseguire il codice seguente:

```powerhsell
Install-Module -Name SqlServer
```

Per altre informazioni su come installare il modulo SqlServer da PowerShell Gallery, vedere questo [pagina](../powershell/download-sql-server-ps-module.md).

## <a name="using-the-sqlserver-module"></a>Usando il modulo SqlServer

Per iniziare, avviare PowerShell Core.  Se si usa macOS o Linux, aprire una *sessione terminal* nel computer e digitare **pwsh** per avviare una nuova sessione di PowerShell Core.  In Windows, usare <kbd>vincere</kbd>+<kbd>R</kbd>e il tipo `pwsh` per avviare una nuova sessione di PowerShell Core.

```
pwsh
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

La procedura seguente usa PowerShell Core per connettersi all'istanza di SQL Server in Linux e visualizzare un paio di proprietà del server.

Copiare e incollare i comandi seguenti al prompt di PowerShell. Quando si eseguono questi comandi, verranno PowerShell:
- Visualizzare una finestra di dialogo che richiede il nome host o indirizzo IP dell'istanza di
- Visualizzare il *richiesta di credenziali di PowerShell* finestra di dialogo che richiede le credenziali. È possibile usare il *username SQL* e *password SQL* per connettersi all'istanza di SQL Server in Linux
- Usare la **Get-SqlInstance** per connettersi alle **Server** e visualizzare alcune proprietà

Facoltativamente, è sufficiente sostituire il `$serverInstance` variabile con l'indirizzo IP o il nome host dell'istanza di SQL Server.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Connect to the Server and return a few properties
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

Un'altra opzione per la connessione all'istanza di SQL Server consiste nell'usare la [PowerShell Provider per SQL Server](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider).  Utilizzando il provider consente di passare l'istanza di SQL Server simile a come se si sono stati passando la struttura ad albero in Esplora oggetti, ma nella riga di comando.  Per impostazione predefinita questo provider viene presentato come un oggetto PSDrive denominato `SQLSERVER:\` che è possibile usare per connettersi ed esplorare le istanze di SQL Server che ha accesso l'account di dominio.  Visualizzare [passaggi di configurazione](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-auth-overview#configuration-steps) per informazioni su come configurare l'autenticazione di Active Directory per SQL Server in Linux.

È anche possibile usare l'autenticazione di SQL con il PowerShell Provider per SQL Server. A questo scopo, usare il `New-PSDrive` cmdlet per creare un nuovo dispositivo PSDrive e fornire le credenziali appropriate per la connessione.

In questo esempio riportato di seguito, si verrà visualizzato un esempio di come creare un nuovo dispositivo PSDrive mediante l'autenticazione SQL.

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

Ecco ciò che l'output potrebbe essere simile.  Si può notare questo output è simile a ciò che SSMS verrà visualizzato nel nodo database.  Visualizza i database utente, ma non i database di sistema.

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

Se si desidera vedere tutti i database sull'istanza, una possibilità consiste nell'utilizzare il `Get-SqlDatabase` cmdlet.

## <a name="get-databases"></a>Ottenere i database

È un cmdlet importante conoscere il `Get-SqlDatabase`.  Per molte operazioni che coinvolgono un database o oggetti all'interno di un database, il `Get-SqlDatabase` cmdlet può essere utilizzato.  Se si specificano valori per entrambe le `-ServerInstance` e `-Database` verranno recuperati i parametri, solo tale oggetto di un database.  Tuttavia, se si specifica solo il `-ServerInstance` parametro, verrà restituito un elenco completo di tutti i database in tale istanza.

```powershell
# NOTE: We are reusing the values saved in the $credential variable from the above example.

# Connect to the Instance and retrieve all databases
Get-SqlDatabase -ServerInstance ServerB -Credential $credential
```

Ecco un esempio di ciò che potrebbe essere restituito dal comando Get-SqlDatabase precedente:

```powershell
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2016   Normal      209.63 MB    1.31 MB Simple       130 sa
AdventureWorksDW2012 Normal      167.00 MB   32.47 MB Simple       110 sa
AdventureWorksDW2014 Normal      188.00 MB   78.10 MB Simple       120 sa
AdventureWorksDW2016 Normal      172.00 MB   74.88 MB Simple       130 sa
AdventureWorksDW2017 Normal      208.00 MB   40.63 MB Simple       140 sa
master               Normal        6.00 MB  600.00 KB Simple       140 sa
model                Normal       16.00 MB    5.70 MB Full         140 sa
msdb                 Normal       15.50 MB    1.14 MB Simple       140 sa
tempdb               Normal       16.00 MB    5.49 MB Simple       140 sa

```

## <a name="examine-sql-server-error-logs"></a>Esaminare i log degli errori di SQL Server

La procedura seguente usa PowerShell Core per esaminare l'errore di connessione di log nell'istanza di SQL Server in Linux.

Copiare e incollare i comandi seguenti al prompt di PowerShell. Si potrebbero richiedere alcuni minuti per l'esecuzione. Questi comandi procedere come segue:
- Visualizzare una finestra di dialogo che richiede il nome host o indirizzo IP dell'istanza di
- Visualizzare il *richiesta di credenziali di PowerShell* finestra di dialogo in cui vengono richieste le credenziali. È possibile usare il *username SQL* e *password SQL* per connettersi all'istanza di SQL Server in Linux
- Usare il **Get-SqlErrorLog** log di cmdlet per connettersi all'istanza di SQL Server in Linux e recuperare l'errore poiché **ieri**

Facoltativamente, è possibile sostituire il `$serverInstance` variabile con l'indirizzo IP o il nome host dell'istanza di SQL Server.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday
# done
```

## <a name="explore-cmdlets-currently-available-in-ps-core"></a>Esplorare i cmdlet è attualmente disponibili in Powershell Core
Mentre il modulo SqlServer ha attualmente 106 cmdlet disponibili in Windows PowerShell, sono disponibili in PSCore 59 solo del 106. Di seguito è incluso un elenco completo dei 59 cmdlet attualmente disponibili.  Per documentazione approfondita di tutti i cmdlet nel modulo SqlServer, vedere SqlServer [riferimento ai cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/).

Il comando seguente illustra tutti i cmdlet disponibili nella versione di PowerShell in uso.

```powershell
Get-Command -Module SqlServer -CommandType Cmdlet |
SORT -Property Noun |
SELECT Name
```

- ConvertFrom-EncodedSqlName
- ConvertTo-EncodedSqlName
- Get-SqlAgent
- Get-SqlAgentJob
- Get-SqlAgentJobHistory
- Get-SqlAgentJobSchedule
- Get-SqlAgentJobStep
- Get-SqlAgentSchedule
- Remove-SqlAvailabilityDatabase
- Resume-SqlAvailabilityDatabase
- Add-SqlAvailabilityDatabase
- Suspend-SqlAvailabilityDatabase
- New-SqlAvailabilityGroup
- Set-SqlAvailabilityGroup
- Remove-SqlAvailabilityGroup
- Switch-SqlAvailabilityGroup
- Join-SqlAvailabilityGroup
- Revoke-SqlAvailabilityGroupCreateAnyDatabase
- Grant-SqlAvailabilityGroupCreateAnyDatabase
- New-SqlAvailabilityGroupListener
- Set-SqlAvailabilityGroupListener
- Add-SqlAvailabilityGroupListenerStaticIp
- Set-SqlAvailabilityReplica
- Remove-SqlAvailabilityReplica
- New-SqlAvailabilityReplica
- Set-SqlAvailabilityReplicaRoleToSecondary
- New-SqlBackupEncryptionOption
- Get-SqlBackupHistory
- Invoke-Sqlcmd
- New-SqlCngColumnMasterKeySettings
- Remove-SqlColumnEncryptionKey
- Get-SqlColumnEncryptionKey
- Remove-SqlColumnEncryptionKeyValue
- Add-SqlColumnEncryptionKeyValue
- Get-SqlColumnMasterKey
- Remove-SqlColumnMasterKey
- New-SqlColumnMasterKey
- Get-SqlCredential
- Set-SqlCredential
- New-SqlCredential
- Remove-SqlCredential
- New-SqlCspColumnMasterKeySettings
- Get-SqlDatabase
- Restore-SqlDatabase
- Backup-SqlDatabase
- Set-SqlErrorLog
- Get-SqlErrorLog
- New-SqlHADREndpoint
- Set-SqlHADREndpoint
- Get-SqlInstance
- Add-SqlLogin
- Remove-SqlLogin
- Get-SqlLogin
- Set-SqlSmartAdmin
- Get-SqlSmartAdmin
- Read-SqlTableData
- Write-SqlTableData
- Read-SqlViewData
- Convert-UrnToPath

## <a name="see-also"></a>Vedere anche
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)
