---
title: Visualizzare il contenuto di un nastro o di un file di backup (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup devices [SQL Server], tapes
- displaying backup content
- viewing backup content
- tape backup devices, viewing contents
- database backups [SQL Server], viewing content
- backing up databases [SQL Server], viewing content
ms.assetid: cd6674a2-ca55-4b5a-a971-878ba001821e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: dfee2d0f32ffaaf73527effdeea13d43b83a39fb
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537289"
---
# <a name="view-the-contents-of-a-backup-tape-or-file-sql-server"></a>Visualizzare il contenuto di un nastro o di un file di backup (SQL Server)
  In questo argomento si illustra come visualizzare il contenuto di un nastro o file di backup in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!NOTE]  
>  Il supporto per i dispositivi di backup su nastro verrà rimosso in una versione futura di SQL Server. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per visualizzare il contenuto di un nastro o di un file di backup utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
 Per informazioni sulla sicurezza, vedere [RESTORE HEADERONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-headeronly-transact-sql).  
  
####  <a name="Permissions"></a> Autorizzazioni  
 In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive, per ottenere informazioni su un set o un dispositivo di backup è necessario disporre dell'autorizzazione CREATE DATABASE. Per altre informazioni, vedere [GRANT - autorizzazioni per database &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-database-permissions-transact-sql).  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-view-the-content-of-a-backup-tape-or-file"></a>Per visualizzare il contenuto di un nastro o di un file di backup  
  
1.  Dopo aver stabilito la connessione all'istanza appropriata del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], in Esplora oggetti fare clic sul nome del server per espandere l'albero del server.  
  
2.  Espandere **Database**e, a seconda del database, selezionare un database utente o espandere **Database di sistema** e selezionare un database di sistema.  
  
3.  Fare clic con il pulsante destro del mouse sul database di cui eseguire il backup, scegliere **Attività**e quindi fare clic su **Backup**. Verrà visualizzata la finestra di dialogo **Backup database** .  
  
4.  Nella sezione **Destinazione** della pagina **Generale** fare clic su **Disco** o **Nastro**. Nella casella di riepilogo **Backup su** cercare il file su disco o il nastro desiderato.  
  
     Se il file su disco o il nastro non è visualizzato nella casella di riepilogo, fare clic su **Aggiungi**. Selezionare un nome file o un'unità nastro. Per aggiungere l'elemento alla casella di riepilogo **Backup su** , fare clic su **OK**.  
  
5.  Nella casella di riepilogo **Backup su** selezionare il percorso del disco o dell'unità nastro che si desidera visualizzare e quindi fare clic su **Contenuto**. Verrà visualizzata la finestra di dialogo **Contenuto dispositivo** .  
  
6.  Il riquadro di destra visualizza informazioni sul set di supporti e i set di backup sul nastro o sul file selezionato.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-view-the-content-of-a-backup-tape-or-file"></a>Per visualizzare il contenuto di un nastro o di un file di backup  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Utilizzare l'istruzione [RESTORE HEADERONLY](/sql/t-sql/statements/restore-statements-headeronly-transact-sql) . In questo esempio vengono restituite informazioni sul fine denominato `AdventureWorks2012-FullBackup.bak`.  
  
```sql  
USE AdventureWorks2012;  
RESTORE HEADERONLY   
FROM DISK = N'C:\AdventureWorks2012-FullBackup.bak' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [backupfilegroup &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupfilegroup-transact-sql)   
 [backupfile &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupfile-transact-sql)   
 [backupset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)   
 [backupmediaset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupmediaset-transact-sql)   
 [backupmediafamily &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupmediafamily-transact-sql)   
 [Dispositivi di backup &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [Definizione di un dispositivo di backup logico per un file su disco &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [Definire un dispositivo di backup logico per un'unità nastro &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
  
