---
description: Ripristinare un database a uno snapshot del database
title: Ripristinare un database a uno snapshot del database | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], reverting to
- reverting databases
ms.assetid: 8f74dd31-c9ca-4537-8760-0c7648f0787d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 21b00ef447dd9312fc0ad3b4bb41cc414f91ff0f
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196706"
---
# <a name="revert-a-database-to-a-database-snapshot"></a>Ripristinare un database a uno snapshot del database
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Se i dati in un database online sono danneggiati, in alcuni casi il ripristino del database a un snapshot del database precedente alla data del danno può essere un'alternativa appropriata per ripristinare il database da un backup. Il ripristino di un database può, ad esempio, risultare utile per annullare un errore grave dell'utente verificatosi di recente, come l'eliminazione di una tabella. Tutte le modifiche apportate dopo la creazione dello snapshot verranno tuttavia perse.  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Prerequisiti](#Prerequisites)  
  
     [Sicurezza](#Security)  
  
-   **To Revert a Database to a Database Snapshot, using:**  [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
 Il ripristino da snapshot non è supportato nei casi seguenti:  
  
-   Sono disponibili più snapshot per il database. Per il ripristino deve essere presente un solo snapshot con cui ripristinare il database.  
  
-   Nel database sono presenti filegroup di sola lettura o compressi.  
  
-   Alcuni file sono attualmente offline ma erano online al momento della creazione dello snapshot.  
  
 Prima di ripristinare un database, considerare le limitazioni seguenti:  
  
-   Non è previsto il ripristino per il recupero di supporti. Un snapshot del database è una copia incompleta dei file di database, pertanto se il database o lo snapshot del database è danneggiato, è probabile che il ripristino da uno snapshot risulti impossibile. Anche quando possibile, è inoltre improbabile che il ripristino in caso di danneggiamento consenta di risolvere il problema. Per proteggere un database è pertanto essenziale eseguire backup regolari e testare il piano di ripristino. Per altre informazioni, vedere [Backup e ripristino di database SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
    > [!NOTE]  
    >  Se è necessario essere in grado di ripristinare il database di origine al punto nel tempo in cui è stato creato uno snapshot del database, utilizzare il modello di recupero completo e implementare criteri di backup che consentano di eseguire tale operazione.  
  
-   Il database di origine originale viene sovrascritto dal database ripristinato, pertanto qualsiasi aggiornamento apportato al database dalla creazione dello snapshot verrà perso.  
  
-   Tramite l'operazione di ripristino viene inoltre sovrascritto il file di log precedente e viene ricompilato il log. Di conseguenza, non è possibile eseguire il rollforward del database ripristinato al punto in cui si è verificato l'errore dell'utente. Si consiglia pertanto di eseguire il backup del log prima di ripristinare un database.  
  
    > [!NOTE]  
    >  Sebbene non sia possibile ripristinare il log originale per eseguire il rollforward del database, le informazioni del file di log originale saranno utili per ricostruire i dati persi.  
  
-   Tramite il ripristino viene interrotta la catena di backup del log. Prima di eseguire backup del log del database ripristinato, è pertanto necessario eseguire un backup completo del database o il backup del file. È consigliabile eseguire un backup completo del database.  
  
-   Durante un'operazione di ripristino, sia lo snapshot che il database di origine non sono disponibili. Entrambi sono contrassegnati come in fase di ripristino. Se si verifica un errore durante l'operazione di ripristino, al nuovo avvio del database verrà eseguito un tentativo di completamento dell'operazione.  
  
-   I metadati di un database ripristinato corrispondono a quelli del database al momento dello snapshot.  
  
-   Il ripristino causa l'eliminazione di tutti i cataloghi full-text.  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Prerequisiti  
 Assicurarsi che il database di origine e lo snapshot del database soddisfino i prerequisiti seguenti:  
  
-   Verificare che il database non sia stato danneggiato.  
  
    > [!NOTE]  
    >  Se il database è stato danneggiato, sarà necessario ripristinarlo dai backup. Per altre informazioni, vedere [Ripristini di database completi &#40;modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md) o [Ripristini di database completi &#40;modello di recupero con registrazione completa &#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md).  
  
-   Identificare un recente snapshot creato prima dell'errore. Per altre informazioni, vedere [Visualizzare uno snapshot del database &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md).  
  
-   Eliminare qualsiasi altro snapshot del database attualmente presente nel database. Per altre informazioni, vedere [Eliminare uno snapshot del database &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)o a un'istanza diversa.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Qualsiasi utente con autorizzazioni RESTORE DATABASE sul database di origine può ripristinarne lo stato corrispondente al momento in cui è stato creato lo snapshot.  
  
##  <a name="how-to-revert-a-database-to-a-database-snapshot-using-transact-sql"></a><a name="TsqlProcedure"></a> Come ripristinare un database a uno snapshot del database (tramite Transact-SQL)  
 **Per ripristinare un database a uno snapshot del database**  
  
> [!NOTE]  
>  Per un esempio di questa procedura, vedere [Esempi (Transact-SQL)](#TsqlExample)più avanti in questa sezione.  
  
1.  Individuare lo snapshot del database a cui ripristinare il database. È possibile visualizzare gli snapshot di un database in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . Vedere [Visualizzare uno snapshot del database &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md). È anche possibile trovare il database di origine di una vista dalla colonna **source_database_id** della vista del catalogo [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) .  
  
2.  Eliminare eventuali altri snapshot del database.  
  
     Per informazioni sull'eliminazione di snapshot, vedere [Eliminare uno snapshot del database &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md). Se nel database viene utilizzato il modello di recupero con registrazione completa, prima del ripristino è necessario eseguire il backup del log. Per altre informazioni, vedere [Eseguire il backup di un log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md) oppure [Eseguire il backup del log delle transazioni quando il database è danneggiato &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md).  
  
3.  Eseguire l'operazione di ripristino.  
  
     Per un'operazione di ripristino è necessario disporre delle autorizzazioni RESTORE DATABASE nel database di origine. Utilizzare quindi l'istruzione Transact-SQL per ripristinare il database:  
  
     RESTORE DATABASE *nome_database* FROM DATABASE_SNAPSHOT **=**_nome_snapshot_database_  
  
     dove *nome_database* è il database di origine e *nome_snapshot_database* è il nome dello snapshot con cui ripristinare il database. Si noti che in questa istruzione è necessario specificare un nome di snapshot anziché un dispositivo di backup.  
  
     Per altre informazioni, vedere [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
    > [!NOTE]  
    >  Durante l'operazione di ripristino sia lo snapshot che il database di origine risultano indisponibili e sono contrassegnati come in fase di ripristino. In caso di errori durante il ripristino, al riavvio del database verrà eseguito un tentativo di completamento dell'operazione.  
  
4.  Se il proprietario del database è cambiato dalla creazione dello snapshot, è opportuno aggiornare il proprietario del database ripristinato.  
  
    > [!NOTE]  
    >  Per il database ripristinato vengono mantenute le autorizzazioni e la configurazione dello snapshot, ad esempio il proprietario del database e il modello di recupero.  
  
5.  Avviare il database.  
  
6.  Facoltativamente, eseguire il backup del database ripristinato, in particolare se viene utilizzato il modello di recupero con registrazione completa o con registrazione minima delle operazioni bulk. Per eseguire il backup di un database, vedere [Creare un backup completo del database &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  

###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> Esempi (Transact-SQL)  
 In questa sezione sono inclusi i seguenti esempi di ripristino di un database a uno snapshot del database:  
  
-   R. [Ripristino di uno snapshot nel database AdventureWorks](#Reverting_AW)  
  
-   B. [Ripristino di uno snapshot del database Sales](#Reverting_Sales)  
  
####  <a name="a-reverting-a-snapshot-on-the-adventureworks-database"></a><a name="Reverting_AW"></a> A. Ripristino di uno snapshot nel database AdventureWorks  
 Nell'esempio si presuppone che per il database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] esista un solo snapshot. Per l'esempio in cui viene creato lo snapshot usato per il ripristino, vedere [Creare uno snapshot del database &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md).  
  
```  
USE master;  
-- Reverting AdventureWorks to AdventureWorks_dbss1800  
RESTORE DATABASE AdventureWorks from   
DATABASE_SNAPSHOT = 'AdventureWorks_dbss1800';  
GO  
```  
  
####  <a name="b-reverting-a-snapshot-on-the-sales-database"></a><a name="Reverting_Sales"></a> B. Ripristino di uno snapshot del database Sales  
 In questo esempio si suppone che esistano attualmente due snapshot del database **Sales** : **sales_snapshot0600** e **sales_snapshot1200**. Nell'esempio viene eliminato lo snapshot meno recente e il database viene ripristinato in base allo snapshot più recente.  
  
 Per il codice di creazione del database di esempio e degli snapshot su cui si basa questo esempio, vedere:  
  
-   Per il database **Sales** e lo snapshot **sales_snapshot0600** vedere "Creazione di un database con filegroup" e "Creazione di uno snapshot del database" in [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md).  
  
-   Per il database **sales_snapshot1200** , vedere "Creazione di uno snapshot del database Sales" in [Creare uno snapshot del database &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md).  
  
```  
--Test to see if sales_snapshot0600 exists and if it   
-- does, delete it.  
IF EXISTS (SELECT dbid FROM sys.databases  
    WHERE NAME='sales_snapshot0600')  
    DROP DATABASE SalesSnapshot0600;  
GO  
-- Reverting Sales to sales_snapshot1200  
USE master;  
RESTORE DATABASE Sales FROM DATABASE_SNAPSHOT = 'sales_snapshot1200';  
GO  
```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
  
-   [Creare uno snapshot del database &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [Visualizzazione di uno snapshot del database &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)  
  
-   [Eliminare uno snapshot del database &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Snapshot del database &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Mirroring e snapshot del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-database-snapshots-sql-server.md)  
  
