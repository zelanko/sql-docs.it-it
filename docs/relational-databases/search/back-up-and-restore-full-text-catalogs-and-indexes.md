---
title: Eseguire backup e ripristino di cataloghi full-text e indici
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], backing up
- full-text search [SQL Server], back up and restore
- recovery [full-text search]
- backups [SQL Server], full-text indexes
- full-text indexes [SQL Server], restoring
- restore operations [full-text search]
ms.assetid: 6a4080d9-e43f-4b7b-a1da-bebf654c1194
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.custom: seo-lt-2019
ms.openlocfilehash: 38eaba8bdf2772fe03690773881c67306a024b64
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "74056128"
---
# <a name="back-up-and-restore-full-text-catalogs-and-indexes"></a>Backup e ripristino di indici e cataloghi full-text
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In questo argomento viene illustrato come eseguire il backup e il ripristino di indici full-text creati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]il catalogo full-text è un concetto logico e non è contenuto in un filegroup. Pertanto, per eseguire il backup di un catalogo full-text in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario identificare ogni filegroup che contiene un indice full-text appartenente al catalogo, quindi eseguirne il backup uno alla volta.  
  
> [!IMPORTANT]  
>  È possibile importare cataloghi full-text quando si aggiorna un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] . Ogni catalogo full-text importato è un file di database nel proprio filegroup. Per eseguire il backup di un catalogo importato, eseguire il backup del relativo filegroup. Per altre informazioni, vedere [Backup e ripristino di cataloghi full-text](https://go.microsoft.com/fwlink/?LinkID=121052)nella documentazione online di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
##  <a name="backing-up-the-full-text-indexes-of-a-full-text-catalog"></a><a name="backingup"></a> Backup degli indici full-text di un catalogo full-text  
  
###  <a name="finding-the-full-text-indexes-of-a-full-text-catalog"></a><a name="Find_FTIs_of_a_Catalog"></a> Individuazione degli indici full-text di un catalogo full-text  
 È possibile recuperare le proprietà degli indici full-text usando l'istruzione [SELECT](../../t-sql/queries/select-transact-sql.md) seguente che consente di selezionare le colonne dalle viste del catalogo [sys.fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md) e [sys.fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) .  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @TableID int;  
SET @TableID = (SELECT OBJECT_ID('AdventureWorks2012.Production.Product'));  
SELECT object_name(@TableID), i.is_enabled, i.change_tracking_state,   
   i.has_crawl_completed, i.crawl_type, c.name as fulltext_catalog_name   
   FROM sys.fulltext_indexes i, sys.fulltext_catalogs c   
   WHERE i.fulltext_catalog_id = c.fulltext_catalog_id;  
GO  
```  
  
  
###  <a name="finding-the-filegroup-or-file-that-contains-a-full-text-index"></a><a name="Find_FG_of_FTI"></a> Individuazione del filegroup o del file che contiene un indice full-text  
 Quando viene creato, l'indice full-text viene inserito in una delle posizioni seguenti:  
  
-   Filegroup specificato dall'utente.  
  
-   Lo stesso filegroup della vista o della tabella di base, per una tabella non partizionata.  
  
-   Filegroup primario, per una tabella partizionata.  
  
> [!NOTE]  
>  Per informazioni sulla creazione di un indice full-text, vedere [Creare e gestire indici full-text](../../relational-databases/search/create-and-manage-full-text-indexes.md) e [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md).  
  
 Per trovare il filegroup dell'indice full-text in una tabella o vista, usare la query seguente, dove *object_name* rappresenta il nome della tabella o della vista:  
  
```  
SELECT name FROM sys.filegroups f, sys.fulltext_indexes i   
   WHERE f.data_space_id = i.data_space_id   
      and i.object_id = object_id('object_name');  
GO  
  
```  
  
  
###  <a name="backing-up-the-filegroups-that-contain-full-text-indexes"></a><a name="Back_up_FTIs_of_FTC"></a> Backup dei filegroup che contengono gli indici full-text  
 Dopo avere trovato i filegroup che contengono gli indici di un catalogo full-text, è necessario eseguire il backup di ognuno. Durante il processo di backup non è consentito eliminare o aggiungere cataloghi full-text.  
  
 Il primo backup di un filegroup deve essere un backup di file completo. Dopo avere creato un backup di file completo per un filegroup, è possibile eseguire il backup delle sole modifiche avvenute in un filegroup creando una serie di uno o più backup di file differenziali basati sul backup di file completo.  
  
 **Per eseguire il backup di file e filegroup**  
  
-   [Backup di file e filegroup &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)  
  
  
##  <a name="restoring-a-full-text-index"></a><a name="Restore_FTI"></a> Ripristino di un indice full-text  
 Il ripristino del backup di un filegroup include il ripristino dei file di indice full-text e degli altri file nel filegroup. Per impostazione predefinita, il filegroup viene ripristinato nel percorso del disco in cui è stato eseguito il backup.  
  
 Se alla creazione del backup era online una tabella indicizzata full-text con un popolamento in corso, quest'ultimo verrà ripreso dopo il ripristino.  
  
 **Per ripristinare un filegroup**  
  
-   [Ripristino di file e filegroup &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [Ripristinare file e filegroup sovrascrivendo file esistenti &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [Ripristino dei file in una nuova posizione &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione e monitoraggio della ricerca full-text per un'istanza del server](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md)   
 [Aggiornare la ricerca full-text](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
