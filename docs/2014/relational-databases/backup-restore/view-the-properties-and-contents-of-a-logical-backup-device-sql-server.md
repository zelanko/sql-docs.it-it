---
title: Visualizzare le proprietà e il contenuto di un dispositivo di backup logico (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- displaying backup content
- viewing backup content
- database backups [SQL Server], viewing content
- backing up databases [SQL Server], viewing content
- backing up databases [SQL Server], properties
- displaying backup properties
- backup devices [SQL Server], viewing information
- viewing backup properties
- database backups [SQL Server], properties
ms.assetid: 3a309074-e816-454d-b6c3-fcfdde0cbf74
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e593a5d64b6a1b009a68c434fe9ce1a32cb2de20
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535839"
---
# <a name="view-the-properties-and-contents-of-a-logical-backup-device-sql-server"></a>Visualizzazione delle proprietà e del contenuto di un dispositivo di backup logico (SQL Server)
  In questo argomento viene illustrato come visualizzare le proprietà e il contenuto di un dispositivo di backup logico in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per visualizzare le proprietà e il contenuto di un dispositivo di backup logico utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
 Per informazioni sulla sicurezza, vedere [RESTORE LABELONLY & #40; Transact-SQL & #41;](/sql/t-sql/statements/restore-statements-labelonly-transact-sql).  
  
####  <a name="Permissions"></a> Autorizzazioni  
 In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive, per ottenere informazioni su un set o un dispositivo di backup è necessario disporre dell'autorizzazione CREATE DATABASE. Per altre informazioni, vedere [GRANT - autorizzazioni per database &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-database-permissions-transact-sql).  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-view-the-properties-and-contents-of-a-logical-backup-device"></a>Per visualizzare le proprietà e il contenuto di un dispositivo di backup logico  
  
1.  Dopo aver stabilito la connessione all'istanza appropriata del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], in Esplora oggetti fare clic sul nome del server per espandere l'albero del server.  
  
2.  Espandere **Oggetti server**e quindi **Dispositivi di backup**.  
  
3.  Fare clic sul dispositivo e quindi fare clic con il pulsante destro del mouse su **Proprietà**per visualizzare la finestra di dialogo **Dispositivo di backup** .  
  
4.  Nella pagina **Generale** sono indicati il nome del dispositivo e la destinazione, costituita da un dispositivo nastro o da un percorso di file.  
  
5.  Nel riquadro **Selezione pagina** fare clic su **Contenuto supporti**.  
  
6.  Nel riquadro di destra verranno visualizzati i pannelli delle proprietà seguenti:  
  
    -   **Supporti**  
  
         Informazioni sulla sequenza dei supporti, ovvero numero di sequenza dei supporti, numero di sequenza del gruppo e identificatore mirror, se presente, e data e ora di creazione dei supporti.  
  
    -   **Set di supporti**  
  
         Informazioni sul set di supporti: nome e, se disponibile, descrizione del set di supporti e numero di gruppi nel set.  
  
7.  Nella griglia **Set di backup** sono visualizzate le informazioni sui contenuti del set di supporti.  
  
> [!NOTE]  
>  Per altre informazioni, vedere [Pagina Contenuto supporti](backup-device-media-contents-page.md).  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-view-the-properties-and-contents-of-a-logical-backup-device"></a>Per visualizzare le proprietà e il contenuto di un dispositivo di backup logico  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Utilizzare l'istruzione [RESTORE LABELONLY](/sql/t-sql/statements/restore-statements-labelonly-transact-sql) . In questo esempio vengono restituite informazioni sul dispositivo di backup logico `AdvWrks2008R2Backup` .  
  
```sql  
USE AdventureWorks2012 ;  
RESTORE LABELONLY  
   FROM AdvWrks2008R2Backup ;  
GO  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [backupfilegroup &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupfilegroup-transact-sql)   
 [backupfile &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupfile-transact-sql)   
 [backupset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)   
 [backupmediaset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupmediaset-transact-sql)   
 [backupmediafamily &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupmediafamily-transact-sql)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [Dispositivi di backup &#40;SQL Server&#41;](backup-devices-sql-server.md)  
  
  
