---
title: Database msdb | Microsoft Docs
ms.custom: ''
ms.date: 11/10/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, msdb database
- alerts [SQL Server], msdb database
- jobs [SQL Server], msdb database
- msdb database [SQL Server]
ms.assetid: 5032cb2d-65a0-40dd-b569-4dcecdd58ceb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cee4c5d802447488930ffd04d698edcd2015e86b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62871712"
---
# <a name="msdb-database"></a>Database msdb
  Il database **msdb** viene usato dall'agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la pianificazione di avvisi e processi e da altre funzionalità, ad esempio [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssSB](../../includes/sssb-md.md)] e Posta elettronica database.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ad esempio, l'intera cronologia di backup e ripristino online viene gestita in modo automatico nelle tabelle del database **msdb**. Queste informazioni includono il nome della parte che ha eseguito il backup, l'ora del backup e i dispositivi o i file in cui viene archiviato il backup. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usa queste informazioni per proporre un piano per il ripristino di un database e l'applicazione di qualsiasi backup di log delle transazioni. Vengono inoltre registrati gli eventi di backup di tutti i database che sono stati creati con applicazioni personalizzate o strumenti di terze parti. Se, ad esempio, si usa un'applicazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] che chiama oggetti SMO (SQL Server Management Objects) per l'esecuzione di operazioni di backup, l'evento viene registrato nelle tabelle di sistema **msdb** , nel registro applicazioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e nel log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per facilitare la protezione delle informazioni archiviate in **msdb**, è consigliabile considerare l'inserimento del log delle transazioni di **msdb** in uno spazio di archiviazione a tolleranza d'errore.  
  
 Per impostazione predefinita, **msdb** usa il modello di recupero con registrazione minima. Se si usano le tabelle di [cronologia di backup e ripristino](../backup-restore/backup-history-and-header-information-sql-server.md), è consigliabile usare il modello di recupero per **msdb**. Per altre informazioni, vedere [Modelli di recupero &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md). Si noti che durante l'installazione o l'aggiornamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ogni volta che si usa il file Setup.exe per ricompilare i database di sistema, il modello di recupero di **msdb** viene impostato automaticamente su SIMPLE.  
  
> [!IMPORTANT]  
>  Successivamente a qualsiasi operazione che aggiorna **msdb**, ad esempio per il backup o il ripristino di un database qualsiasi, è consigliabile eseguire il backup **msdb**. Per altre informazioni, vedere [Backup e ripristino di database di sistema &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
## <a name="physical-properties-of-msdb"></a>Proprietà fisiche del database msdb  
 Nella tabella seguente sono illustrati i valori di configurazione iniziali dei file di dati e di log del database **msdb** . Le dimensioni di questi file possono variare leggermente a seconda dell'edizione di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
|File|Nome logico|Nome fisico|Aumento di dimensioni del file|  
|----------|------------------|-------------------|-----------------|  
|Dati primari|MSDBData|MSDBData.mdf|Aumento automatico del 10% fino a quando il disco risulta pieno.|  
|File di log|MSDBLog|MSDBLog.ldf|Aumento automatico del 10% fino a un massimo di 2 terabyte.|  
  
 Per spostare il database **msdb** o i file di log, vedere [Spostare i database di sistema](move-system-databases.md).  
  
### <a name="database-options"></a>Opzioni di database  
 Nella tabella seguente vengono elencati i valori predefiniti per ogni opzione di database del database **msdb** ed è indicato se è possibile modificare le varie opzioni. Per visualizzare le impostazioni correnti di queste opzioni, usare la vista del catalogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) .  
  
|Opzione di database|Valore predefinito|Modificabile|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|ON|No|  
|ANSI_NULL_DEFAULT|OFF|Yes|  
|ANSI_NULLS|OFF|Yes|  
|ANSI_PADDING|OFF|Yes|  
|ANSI_WARNINGS|OFF|Yes|  
|ARITHABORT|OFF|Yes|  
|AUTO_CLOSE|OFF|Yes|  
|AUTO_CREATE_STATISTICS|ON|Yes|  
|AUTO_SHRINK|OFF|Yes|  
|AUTO_UPDATE_STATISTICS|ON|Yes|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|Yes|  
|CHANGE_TRACKING|OFF|No|  
|CONCAT_NULL_YIELDS_NULL|OFF|Yes|  
|CURSOR_CLOSE_ON_COMMIT|OFF|Yes|  
|CURSOR_DEFAULT|GLOBAL|Yes|  
|Opzioni relative alla disponibilità del database|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|No<br /><br /> Yes<br /><br /> Yes|  
|DATE_CORRELATION_OPTIMIZATION|OFF|Yes|  
|DB_CHAINING|ON|Yes|  
|ENCRYPTION|OFF|no|  
|NUMERIC_ROUNDABORT|OFF|Yes|  
|PAGE_VERIFY|CHECKSUM|Yes|  
|PARAMETERIZATION|SIMPLE|Yes|  
|QUOTED_IDENTIFIER|OFF|Yes|  
|READ_COMMITTED_SNAPSHOT|OFF|no|  
|RECOVERY|SIMPLE|Yes|  
|RECURSIVE_TRIGGERS|OFF|Yes|  
|Opzioni relative a Service Broker|ENABLE_BROKER|Yes|  
|TRUSTWORTHY|ON|Yes|  
  
 Per una descrizione di queste opzioni di database, vedere [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
## <a name="restrictions"></a>Restrictions  
 Nel database **msdb** non è possibile eseguire le operazioni seguenti:  
  
-   Modifica delle regole di confronto. Le regole di confronto predefinite corrispondono a quelle del server.  
  
-   Eliminazione del database.  
  
-   Eliminazione dell'utente **guest** dal database.  
  
-   Abilitazione dell'acquisizione dei dati delle modifiche.  
  
-   Partecipazione al mirroring del database.  
  
-   Rimozione del filegroup primario, del file di dati primario o del file di log.  
  
-   Ridenominazione del filegroup primario o del database.  
  
-   Impostazione del database su OFFLINE.  
  
-   Impostazione del filegroup primario su READ_ONLY.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Database di sistema.](system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
 [Spostare file del database](move-database-files.md)  
  
 [Posta elettronica database](../database-mail/database-mail.md)  
  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
