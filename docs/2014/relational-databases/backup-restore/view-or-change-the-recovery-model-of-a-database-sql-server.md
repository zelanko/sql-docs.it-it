---
title: Visualizzare o modificare il modello di recupero di un database (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- database backups [SQL Server], recovery models
- recovery [SQL Server], recovery model
- backing up databases [SQL Server], recovery models
- recovery models [SQL Server], switching
- recovery models [SQL Server], viewing
- database restores [SQL Server], recovery models
- modifying database recovery models
ms.assetid: 94918d1d-7c10-4be7-bf9f-27e00b003a0f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4bc7254d8a3eafa3c7c7d152d323051a3c5bea94
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62875084"
---
# <a name="view-or-change-the-recovery-model-of-a-database-sql-server"></a>Visualizzazione o modifica del modello di recupero di un database (SQL Server)
  In questo argomento viene illustrato come visualizzare o modificare il modello di recupero di un database in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Un *modello di recupero* è una proprietà del database che determina la modalità di registrazione delle transazioni, se è necessario e possibile eseguire il backup del log delle transazioni e quali tipi di operazioni di ripristino sono disponibili. Sono tre i modelli di recupero disponibili: con registrazione minima, con registrazione completa e con registrazione minima delle operazioni bulk. In genere, un database utilizza il modello di recupero con registrazione completa o con registrazione minima. In un database è possibile passare a un modello di recupero diverso in qualsiasi momento. Il database **modello** imposta il modello di recupero predefinito dei nuovi database.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Indicazioni](#Recommendations)  
  
     [Sicurezza](#Security)  
  
-   **Per visualizzare o modificare il modello di recupero di un database utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Indicazioni sul completamento:**  [Dopo la modifica del modello di recupero](#FollowUp)  
  
-   [Attività correlate](#RelatedTasks)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Indicazioni  
  
-   Prima di passare dal modello di recupero con registrazione completa o con registrazione minima delle operazioni bulk, eseguire il backup del log delle transazioni.  
  
-   Il recupero temporizzato non è possibile con il modello di recupero con registrazione minima delle operazioni bulk. Pertanto, se si eseguono transazioni nel modello di recupero con registrazione minima delle operazioni bulk durante le quali potrebbe essere richiesto il ripristino di un log delle transazioni, queste ultime potrebbero essere esposte alla perdita di dati. Per ottimizzare la recuperabilità in uno scenario di recupero di emergenza, è consigliabile passare al modello di recupero con registrazione minima delle operazioni bulk esclusivamente nelle condizioni seguenti:  
  
    -   Agli utenti non è attualmente consentito l'accesso al database.  
  
    -   Tutte le modifiche effettuate durante l'elaborazione bulk possano essere recuperate senza dipendere da un backup del log, ad esempio ripetendo i processi bulk.  
  
     Se queste due condizioni sono soddisfatte, l'utente non sarà esposto ad alcuna perdita di dati durante il ripristino di un log delle transazioni di cui è stato eseguito il backup nel modello di recupero con registrazione minima delle operazioni bulk.  
  
> [!NOTE]  
>  Se si passa al modello di recupero con registrazione completa durante un'operazione bulk, la registrazione dell'operazione bulk cambia da registrazione minima a completa, e viceversa.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione ALTER per il database.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-view-or-change-the-recovery-model"></a>Per visualizzare o modificare il modello di recupero  
  
1.  Dopo aver effettuato la connessione all'istanza appropriata del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], in Esplora oggetti fare clic sul nome del server per espanderne l'albero.  
  
2.  Espandere **Database**e, a seconda del database, selezionare un database utente o espandere **Database di sistema** e selezionare un database di sistema.  
  
3.  Fare clic con il pulsante destro del mouse sul database e quindi scegliere **Proprietà**per visualizzare la finestra di dialogo **Proprietà database** .  
  
4.  Nel riquadro **Selezione pagina** fare clic su **Opzioni**.  
  
5.  Il modello di recupero attualmente implementato è visualizzato nella casella di riepilogo **Modello di recupero** .  
  
6.  Se desiderato, è possibile modificare il modello di recupero selezionandone uno differente nell'elenco. Le scelte possibili sono **Con registrazione completa**, **Con registrazione minima delle operazioni bulk**e **Con registrazione minima**.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-view-the-recovery-model"></a>Per visualizzare il modello di recupero  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene mostrato come eseguire una query sulla vista del catalogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) per individuare il modello di recupero del database **model** .  
  
```sql  
SELECT name, recovery_model_desc  
   FROM sys.databases  
      WHERE name = 'model' ;  
GO  
  
```  
  
#### <a name="to-change-the-recovery-model"></a>Per modificare il modello di recupero  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene mostrato come impostare il modello di recupero nel database `model` su `FULL` utilizzando l'opzione `SET RECOVERY` dell'istruzione [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options) .  
  
```sql  
USE master ;  
ALTER DATABASE model SET RECOVERY FULL ;  
```  
  
##  <a name="follow-up-recommendations-after-you-change-the-recovery-model"></a><a name="FollowUp"></a>Suggerimenti per il completamento: dopo la modifica del modello di recupero  
  
-   **Dopo il passaggio tra i modelli di recupero con registrazione completa e con registrazione minima delle operazioni bulk**  
  
    -   Dopo il completamento delle operazioni bulk, tornare immediatamente alla modalità di recupero con registrazione completa.  
  
    -   Dopo il passaggio dal modello di recupero con registrazione minima delle operazioni bulk al modello di recupero con registrazione completa, eseguire il backup del log.  
  
        > [!NOTE]  
        >  La strategia di backup rimane invariata, cioè continua l'esecuzione di backup del database, del log e differenziali periodici.  
  
-   **Dopo il passaggio dal modello di recupero con registrazione minima**  
  
    -   Immediatamente dopo il passaggio al modello di recupero con registrazione completa o con registrazione minima delle operazioni bulk, eseguire un backup di database completo o differenziale per avviare la catena di log.  
  
        > [!NOTE]  
        >  Il passaggio al modello di recupero con registrazione completa o con registrazione minima delle operazioni bulk ha effetto solo dopo il primo backup dei dati.  
  
    -   Pianificare backup regolari dei log e aggiornare il piano di ripristino di conseguenza.  
  
        > [!IMPORTANT]  
        >  Se non si esegue il backup del log con la necessaria frequenza, il log delle transazioni può espandersi fino a esaurire lo spazio su disco.  
  
-   **Dopo il passaggio al modello di recupero con registrazione minima**  
  
    -   Interrompere tutti i processi pianificati per l'esecuzione del backup del log delle transazioni.  
  
    -   Verificare la pianificazione di backup di database periodici. Il backup del database è essenziale sia per proteggere i dati sia per troncare la porzione inattiva del log delle transazioni.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
  
-   [Creazione di un backup completo del database &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [Eseguire il backup di un log delle transazioni &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [Creazione di un processo](../../ssms/agent/create-a-job.md)  
  
-   [Abilitare o disabilitare un processo](../../ssms/agent/disable-or-enable-a-job.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Contenuto correlato  
  
-   [Database Maintenance Plans](../maintenance-plans/maintenance-plans.md) nella documentazione online di [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Modelli di recupero &#40;SQL Server&#41;](recovery-models-sql-server.md)   
 [Log delle transazioni &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [Modelli di recupero &#40;SQL Server&#41;](recovery-models-sql-server.md)  
  
  
