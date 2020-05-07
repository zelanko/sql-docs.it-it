---
title: MSSQLSERVER_5228 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5120 (Database Engine error)
ms.assetid: ''
author: PijoCoder
ms.author: mathoma
ms.openlocfilehash: ff8fb262b643390f2914a4a5e6c42dcc887206f8
ms.sourcegitcommit: 66407a7248118bb3e167fae76bacaa868b134734
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81728618"
---
# <a name="mssqlserver_5120"></a>MSSQLSERVER_5120
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|5120|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DSK_FCB_FAILURE|  
|Testo del messaggio|Errore di tabella: Impossibile aprire il file fisico "%.*ls". Errore %d: "%ls" del sistema operativo.|  
  
## <a name="explanation"></a>Spiegazione  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è riuscito ad aprire un file di database.  L'errore del sistema operativo visualizzato nel messaggio indica motivi più specifici all'origine dell'errore. Questo errore può essere visualizzato insieme ad altri errori, ad esempio [17204](mssqlserver-17204-database-engine-error.md) o [17207](mssqlserver-17207-database-engine-error.md)
  
## <a name="user-action"></a>Azione dell'utente  
  
  Trovare e correggere l'errore del sistema operativo, quindi provare di nuovo l'operazione. Diversi stati consentono a Microsoft di circoscrivere l'area del prodotto in cui si è verificato l'errore. 
  
### <a name="access-is-denied"></a>Accesso negato 
Se si riceve l'errore del sistema operativo ```Access is Denied``` = 5, prendere in considerazione questi metodi:
   -  Controllare le autorizzazioni impostate per il file esaminando le proprietà del file in Esplora risorse. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa i gruppi di Windows per eseguire il provisioning del controllo di accesso sulle varie risorse di file. Verificare che il gruppo appropriato [con nomi come SQLServerMSSQLUser$ComputerName$MSSQLSERVER o SQLServerMSSQLUser$ComputerName$InstanceName] abbia le autorizzazioni necessarie per il file di database indicato nel messaggio di errore. Per altre informazioni, vedere [Configurare le autorizzazioni del file system per l'accesso al motore di database](../../2014/database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access.md). Verificare che il gruppo di Windows includa l'account di avvio del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o il SID del servizio.
   -  Esaminare l'account utente in cui è attualmente in esecuzione il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile ottenere queste informazioni tramite Gestione attività di Windows. Cercare il valore "User Name" (Nome utente) nel file eseguibile "sqlservr.exe". Se è stato modificato di recente l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tenere presente che il metodo supportato per questa operazione è l'uso dell'utilità [Gestione configurazione SQL Server](../sql-server-configuration-manager.md). 
   -  A seconda del tipo di operazione (apertura dei database durante l'avvio del server, collegamento di un database, ripristino del database e così via), l'account usato per la rappresentazione e l'accesso al file di database può variare. Vedere l'argomento [Sicurezza dei dati e dei file di log](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms189128(v=sql.105)?redirectedfrom=MSDN) per informazioni sulle interazioni tra operazioni, autorizzazioni e account. Usare uno strumento come [Process Monitor](https://docs.microsoft.com/sysinternals/downloads/procmon) di Windows SysInternals per determinare se l'accesso ai file avviene nel contesto di sicurezza dell'account di avvio del servizio dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (o SID del servizio) o di un account rappresentato.

      Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rappresenta le credenziali utente dell'accesso che esegue l'operazione ALTER DATABASE o CREATE DATABASE, si noteranno ad esempio le informazioni seguenti nello strumento Process Monitor:
        ```Date & Time:      3/27/2010 8:26:08 PM
        Event Class:        File System
        Operation:          CreateFile
        Result:                ACCESS DENIED
        Path:                  C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\DATA\attach_test.mdf
        TID:                   4288
        Duration:             0.0000366
        Desired Access:Generic Read/Write
        Disposition:        Open
        Options:            Synchronous IO Non-Alert, Non-Directory File, Open No Recall
        Attributes:          N
        ShareMode:       Read
        AllocationSize:   n/a
        Impersonating: DomainName\UserName```
  
  
### Attaching Files that Reside on a Network-attached storage  
If you cannot re-attach a database that resides on network-attached storage, a message like this may be logged in the Application log:

```Msg 5120, Level 16, State 101, Line 1 Unable to open the physical file "\\servername\sharename\filename.mdf". Operating system error 5: (Access is denied.).```

This problem occurs because [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resets the file permissions when the database is detached. When you try to reattach the database, a failure occurs because of limited share permissions.

To resolve, follow these steps:
1. Use the -T startup option to start [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use this startup option to turn on trace flag 1802 in [SQL Server Configuration Manager](../sql-server-configuration-manager.md) (see [Trace Flags](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md) for information on 1802). For more information about how to change the startup parameters, see [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md)

2. Use the following command to detach the database.
```tsql
 exec sp_detach_db DatabaseName
 go 
```

3. Usare il comando seguente per riconnettere il database.
```tsql
exec sp_attach_db DatabaseName, '\\Network-attached storage_Path\DatabaseMDFFile.mdf', '\\Network-attached storage_Path\DatabaseLDFFile.ldf'
go
```
 
