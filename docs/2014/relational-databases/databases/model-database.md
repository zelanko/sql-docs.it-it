---
title: Database model | Microsoft Docs
ms.custom: ''
ms.date: 10/02/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- template databases [SQL Server]
- model database [SQL Server], about model databases
- model database [SQL Server]
ms.assetid: 4e4f739b-fd27-4dce-8be6-3d808040d8d7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c2886fffebdf06ea16ebe8b6992387be3c22e0bf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62916947"
---
# <a name="model-database"></a>Database model
  Il database **model** viene usato come modello per tutti i database creati in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Poiché il database **tempdb** viene creato ogni volta che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene avviato, il database **model** deve essere sempre presente in un sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . L'intero contenuto del database **model** , incluse le opzioni del database, viene copiato nel nuovo database. Alcune impostazioni del database **model** vengono inoltre usate per la creazione di un nuovo database **tempdb** all'avvio, pertanto in un sistema **il database** model [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere sempre presente.  
  
 I database utente appena creati utilizzano lo stesso [modello di recupero](../backup-restore/recovery-models-sql-server.md) del database model. La stringa predefinita è configurabile dall'utente. Per informazioni sull'attuale modello di recupero, vedere [Visualizzazione o modifica del modello di recupero di un database &#40;SQL Server&#41;](../backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
> [!IMPORTANT]  
>  Se si modifica il database **modello** con le informazioni sul modello specifiche dell'utente, è consigliabile eseguire il backup del **modello**. Per altre informazioni, vedere [Backup e ripristino di Database di sistema &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
## <a name="model-usage"></a>Utilizzo del database model  
 Quando viene eseguita un'istruzione CREATE DATABASE, la prima parte del database viene creata copiando i contenuti del database **model** . La parte restante del nuovo database viene riempita con pagine vuote.  
  
 Se si modifica il database **model** , le modifiche vengono ereditate da tutti i database creati successivamente. È ad esempio possibile impostare autorizzazioni o opzioni di database oppure aggiungere oggetti, ad esempio tabelle, funzioni o stored procedure. Le proprietà dei file del database **model** rappresentano un'eccezione e vengono ignorate, eccetto le dimensioni iniziali del file di dati.  
  
## <a name="physical-properties-of-model"></a>Proprietà fisiche del database model  
 Nella tabella seguente sono illustrati i valori di configurazione iniziali dei file di dati e di log del database **model** . Le dimensioni di tali file potrebbero essere leggermente diverse per le diverse versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|File|Nome logico|Nome fisico|Aumento di dimensioni del file|  
|----------|------------------|-------------------|-----------------|  
|Dati primari|modeldev|model.mdf|Aumento automatico del 10% fino a quando il disco risulta pieno.|  
|File di log|modellog|modellog.ldf|Aumento automatico del 10% fino a un massimo di 2 terabyte.|  
  
 Per spostare il database **modello** o i file di log, vedere [Spostare i database di sistema](system-databases.md).  
  
### <a name="database-options"></a>Opzioni di database  
 Nella tabella seguente vengono elencati i valori predefiniti per ogni opzione di database del database **model** ed è indicato se è possibile modificare le varie opzioni. Per visualizzare le impostazioni correnti di queste opzioni, usare la vista del catalogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) .  
  
|Opzione di database|Valore predefinito|Modificabile|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|Sì|  
|ANSI_NULL_DEFAULT|OFF|Sì|  
|ANSI_NULLS|OFF|Sì|  
|ANSI_PADDING|OFF|Sì|  
|ANSI_WARNINGS|OFF|Sì|  
|ARITHABORT|OFF|Sì|  
|AUTO_CLOSE|OFF|Sì|  
|AUTO_CREATE_STATISTICS|ON|Sì|  
|AUTO_SHRINK|OFF|Sì|  
|AUTO_UPDATE_STATISTICS|ON|Sì|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|Sì|  
|CHANGE_TRACKING|OFF|No|  
|CONCAT_NULL_YIELDS_NULL|OFF|Sì|  
|CURSOR_CLOSE_ON_COMMIT|OFF|Sì|  
|CURSOR_DEFAULT|GLOBAL|Sì|  
|Opzioni relative alla disponibilità del database|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|No<br /><br /> Sì<br /><br /> Sì|  
|DATE_CORRELATION_OPTIMIZATION|OFF|Sì|  
|DB_CHAINING|OFF|No|  
|ENCRYPTION|OFF|No|  
|NUMERIC_ROUNDABORT|OFF|Sì|  
|PAGE_VERIFY|CHECKSUM|Sì|  
|PARAMETERIZATION|SEMPLICE|Sì|  
|QUOTED_IDENTIFIER|OFF|Sì|  
|READ_COMMITTED_SNAPSHOT|OFF|Sì|  
|RECOVERY|Dipende dall' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] edizione<sup>1</sup>|Sì|  
|RECURSIVE_TRIGGERS|OFF|Sì|  
|Opzioni relative a Service Broker|DISABLE_BROKER|No|  
|TRUSTWORTHY|OFF|No|  
  
 <sup>1</sup> per verificare il modello di recupero corrente del database, vedere [visualizzare o modificare il modello di recupero di un database &#40;SQL Server&#41;](../backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md) o [sys. databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql).  
  
 Per una descrizione di queste opzioni di database, vedere [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
## <a name="restrictions"></a>Restrizioni  
 Nel database **model** non è possibile eseguire le operazioni seguenti:  
  
-   Aggiunta di file o di filegroup.  
  
-   Modifica delle regole di confronto. Le regole di confronto predefinite corrispondono a quelle del server.  
  
-   Modifica del proprietario del database. **model** è di proprietà di **sa**.  
  
-   Eliminazione del database.  
  
-   Eliminazione dell'utente **Guest** dal database.  
  
-   Abilitazione dell'acquisizione dei dati delle modifiche.  
  
-   Partecipazione al mirroring del database.  
  
-   Rimozione del filegroup primario, del file di dati primario o del file di log.  
  
-   Ridenominazione del filegroup primario o del database.  
  
-   Impostazione del database su OFFLINE.  
  
-   Impostazione del filegroup primario su READ_ONLY.  
  
-   Creazione di procedure, viste o trigger utilizzando l'opzione WITH ENCRYPTION. La chiave di crittografia è correlata al database in cui viene creato l'oggetto. Gli oggetti crittografati creati nel database **model** possono essere usati solo in **model**.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Database di sistema](system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
 [Spostare file del database](move-database-files.md)  
  
  
