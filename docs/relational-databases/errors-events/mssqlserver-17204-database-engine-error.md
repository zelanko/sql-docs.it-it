---
description: MSSQLSERVER_17204
title: MSSQLSERVER_17204 | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17204 (Database Engine error)
ms.assetid: 40db66f9-dd5e-478c-891e-a06d363a2552
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3853181bad494232b1874a7e19da9652738b546f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456493"
---
# <a name="mssqlserver_17204"></a>MSSQLSERVER_17204
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |
| :-------- | :---- |
|Nome prodotto|SQL Server|  
|ID evento|17204|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBLKIO_DEVOPENFAILED|  
|Testo del messaggio|%ls: Impossibile aprire il file %ls per il numero di file %d.  Errore del sistema operativo: %ls.|  
  
## <a name="explanation"></a>Spiegazione  
SQL Server non è riuscito ad aprire il file specificato a causa dell'errore del sistema indicato.  

È possibile che venga visualizzato l'errore 17204 nell'evento dell'applicazione Windows o nel log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando SQL Server non è in grado di aprire un file di database e/o un log delle transazioni. L'errore può avere un aspetto simile al seguente:

``` 
Error: 17204, Severity: 16, State: 1.
FCB::Open failed: Could not open file c:\Program Files\Microsoft SQL Server\MSSQL10.SQL2008\MSSQL\data\MyDB_Prm.mdf for file number 1.  OS error: 5(Access is denied.).
```

È possibile che questi errori vengano visualizzati durante il processo di avvio dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o per qualsiasi operazione del database che prova ad avviare il database, ad esempio ALTER DATABASE. In alcuni scenari è possibile che vengano visualizzati sia errori 17204 che errori 17207, in altre occasioni è possibile che ne venga visualizzato solo uno.

Se questi errori si verificano in un database utente, il database viene lasciato nello stato RECOVERY_PENDING e le applicazioni non potranno accedere al database stesso. Se questi errori si verificano in un database di sistema, l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non viene avviata e non è possibile connettersi a questa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un errore con un database di sistema può anche portare offline una risorsa in un cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="cause"></a>Causa
Prima di poter usare qualsiasi database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è necessario avviare il database. Il processo di avvio del database implica quanto segue: 
1. Inizializzazione di varie strutture di dati che rappresentano il database e i file di database
1. Apertura di tutti i file che appartengono al database
1. Esecuzione del ripristino sul database 

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa la funzione dell'API Windows [CreateFile](https://docs.microsoft.com/windows/win32/api/fileapi/nf-fileapi-createfilea) per aprire i file che appartengono a un database.
 
I messaggi 17204 (e 17207) indicano che si è verificato un errore quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha provato ad aprire i file di database durante il processo di avvio.
 
Questi messaggi di errore includono le informazioni seguenti:
1. Nome della funzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che sta provando ad aprire il file. Il nome della funzione che viene visualizzato normalmente in questi messaggi di errore è uno dei seguenti:
   - FCB::Open: si è verificato un errore nel file mentre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provava ad aprirlo
   - FileMgr::StartPrimaryDataFiles: un file di dati primario o un file appartenente al gruppo di file primario
   - FileMgr::StartSecondaryDataFiles: un file appartenente a un gruppo di file secondario
   - FileMgr::StartLogFiles: un file registro transazioni
   - STREAMFCB::Startup: un contenitore SQL FileStream
   - FCB::RemoveAlternateStreams
  
      
1. Le informazioni sullo stato distinguono più posizioni all'interno di una funzione che possono generare questo messaggio di errore
1. Il percorso fisico completo del file
1. L'ID file corrispondente al file
1. Il codice di errore del sistema operativo e la descrizione dell'errore. In alcuni casi viene visualizzato solo il codice di errore.
 
Le informazioni sull'errore del sistema operativo visualizzate in questi messaggi di errore indicano la causa principale all'origine dell'errore 17204. Sono cause comuni di questi messaggi di errore un problema di autorizzazione o un percorso del file errato.


## <a name="user-action"></a>Azione dell'utente  
1. Per la risoluzione dell'errore 17204 è necessario comprendere il codice di errore del sistema operativo associato e diagnosticare l'errore corrispondente. Dopo aver risolto la condizione di errore del sistema operativo, è possibile provare a riavviare il database (ad esempio usando ALTER DATABASE SET ONLINE) o l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per portare online il database interessato. In alcuni casi potrebbe non essere possibile risolvere l'errore del sistema operativo. In questi casi è necessario eseguire azioni correttive specifiche. Le azioni sono illustrate in questa sezione.
1. Se il messaggio di errore 17204 contiene solo un codice di errore e non una descrizione dell'errore, è possibile provare a risolvere il codice di errore usando il comando da una shell del sistema operativo: net helpmsg <error code>. Se si riceve come codice di errore un codice di stato a 8 cifre, vedere fonti di informazioni come [How do I convert an HRESULT to a Win32 error code?](https://devblogs.microsoft.com/oldnewthing/20061103-07/?p=29133) (Come convertire uno stato HRESULT in un codice di errore Win32?) per convertire questi codici di stato in errori del sistema operativo.
1. Se si riceve l'errore del sistema operativo `Access is Denied` = 5, prendere in considerazione questi metodi:
   -  Controllare le autorizzazioni impostate per il file esaminando le proprietà del file in Esplora risorse. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa i gruppi di Windows per eseguire il provisioning del controllo di accesso sulle varie risorse di file. Verificare che il gruppo appropriato [con nomi come SQLServerMSSQLUser$ComputerName$MSSQLSERVER o SQLServerMSSQLUser$ComputerName$InstanceName] abbia le autorizzazioni necessarie per il file di database indicato nel messaggio di errore. Per altre informazioni, vedere [Configurare le autorizzazioni del file system per l'accesso al motore di database](/previous-versions/sql/2014/database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access?view=sql-server-2014). Verificare che il gruppo di Windows includa l'account di avvio del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o il SID del servizio.
   -  Esaminare l'account utente in cui è attualmente in esecuzione il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile ottenere queste informazioni tramite Gestione attività di Windows. Cercare il valore "User Name" (Nome utente) nel file eseguibile "sqlservr.exe". Se è stato modificato di recente l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tenere presente che il metodo supportato per eseguire questa operazione è l'utilità Gestione configurazione SQL Server. Per altre informazioni su questo aspetto, vedere [Gestione configurazione SQL Server](../sql-server-configuration-manager.md). 
   -  A seconda del tipo di operazione (apertura dei database durante l'avvio del server, collegamento di un database, ripristino del database e così via), l'account usato per la rappresentazione e l'accesso al file di database può variare. Vedere l'argomento [Sicurezza dei dati e dei file di log](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms189128(v=sql.105)?redirectedfrom=MSDN) per informazioni sulle interazioni tra operazioni, autorizzazioni e account. Usare uno strumento come [Process Monitor](https://docs.microsoft.com/sysinternals/downloads/procmon) di Windows SysInternals per determinare se l'accesso ai file avviene nel contesto di sicurezza dell'account di avvio del servizio dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (o SID del servizio) o di un account rappresentato.

      Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rappresenta le credenziali dell'utente che esegue l'operazione ALTER DATABASE o CREATE DATABASE, si noteranno ad esempio le informazioni seguenti nello strumento Process Monitor:
        ```Date & Time:      3/27/2010 8:26:08 PM
        Event Class:        File System
        Operation:          CreateFile
        Result:                ACCESS DENIED
        Path:                  C:\Program Files\Microsoft SQL Server\MSSQL10.SQL2008\MSSQL\DATA\attach_test.mdf
        TID:                   4288
        Duration:             0.0000366
        Desired Access:Generic Read/Write
        Disposition:        Open
        Options:            Synchronous IO Non-Alert, Non-Directory File, Open No Recall
        Attributes:          N
        ShareMode:       Read
        AllocationSize:   n/a
        Impersonating: DomainName\UserName```
  
1. If you are getting `The system cannot find the file specified` OS error = 3:
   - Review the complete path from the error message
   - Ensure the disk drive and the folder path is visible and accessible from Windows Explorer
   - Review the Windows Event log to find out if any problems exist with this disk drive
   - If the path is incorrect and if this database already exists in the system, you can change the database file paths using the methods explained in the topic [Move Database Files](../databases/move-database-files.md). You may have to use this procedure, especially for system database files that encounter 17204 or 17207 and you are working through a disaster recovery scenario where the specified disk drives are unavailable. This topic also explains how you can identify the current location of the various system databases [master, model, tempdb, msdb and mssqlsystemresource].
   - If you see this error because the database files are missing, you have to restore the database from a valid backup.
     - If the database file associated with the error belongs to a secondary filegroup, then you can optionally mark that filegroup offline, bring the database online and then perform a restore of that filegroup alone. For more information, refer to the OFFLINE section of the topic [ALTER DATABASE File and Filegroup Options (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).
     - If the file that produced the error is a transaction log file, review the information under the sections "FOR ATTACH" and "FOR ATTACH_REBUILD_LOG" of the topic [CREATE DATABASE (Transact-SQL)](../../t-sql/statements/create-database-transact-sql.md) to understand how you can recreate the missing transaction log files.
   - Ensure that any disk or network location [like iSCSI drive] is available before [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] attempts to access the database files on these locations. If needed create the required dependencies in Cluster Administrator or Service Control Manager.
1. If you're getting the `The process cannot access the file because it is being used by another process` operating system error = 32:
   - Use a tool like [Process Explorer](https://docs.microsoft.com/sysinternals/downloads/process-explorer) or [Handle](https://docs.microsoft.com/sysinternals/downloads/handle) from Windows Sysinternals to find out if another process or service has acquired exclusive lock on this database file
   - Stop that process from accessing [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database files. Common examples include anti-virus programs (see guidance for file exclusions in the following [KB article](https://support.microsoft.com/help/309422/choosing-antivirus-software-for-computers-that-run-sql-server) )
   - In a cluster environment, make sure that the sqlservr.exe process from the previous owning node has actually released the handles to the database files. Normally, this doesn't occur, but misconfigurations of the cluster or I/O paths can lead to such issues.
  
