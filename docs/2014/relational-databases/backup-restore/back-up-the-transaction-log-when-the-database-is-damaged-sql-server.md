---
title: Eseguire il backup del log delle transazioni quando il database è danneggiato (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], damaged
- backing up [SQL Server]. damaged database
- transaction log backups [SQL Server], damaged databases
ms.assetid: 9b8873cc-df54-4336-ab9b-8f525132c2b0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 69e887cc2a8f35710a0c7c910e0e912d6a4a0a61
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62922846"
---
# <a name="back-up-the-transaction-log-when-the-database-is-damaged-sql-server"></a>Esecuzione del backup del log delle transazioni quando il database è danneggiato (SQL Server)
  In questo argomento viene spiegato come eseguire il backup di un log delle transazioni quando il database è danneggiato in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Indicazioni](#Recommendations)  
  
     [Sicurezza](#Security)  
  
-   **Per eseguire il backup del log delle transazioni quando il database è danneggiato utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Non è possibile utilizzare l'istruzione BACKUP in una transazione esplicita o implicita.  
  
###  <a name="Recommendations"></a> Indicazioni  
  
-   Per un database che utilizza il modello di recupero con registrazione completa o il modello di recupero con registrazione minima delle operazioni bulk, è in genere necessario eseguire il backup della parte finale del log prima di avviare il ripristino del database. È inoltre consigliabile eseguire il backup della parte finale del log del database primario prima del failover di una configurazione di log shipping. Il ripristino del backup della parte finale del log come backup del log finale prima del recupero del database consente di evitare la perdita di dati in seguito a un errore. Per altre informazioni sui backup della parte finale del log, vedere [Backup della parte finale del log &#40;SQL Server&#41;](tail-log-backups-sql-server.md).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Le autorizzazioni BACKUP DATABASE e BACKUP LOG vengono assegnate per impostazione predefinita ai membri del ruolo predefinito del server **sysadmin** e dei ruoli predefiniti del database **db_owner** e **db_backupoperator** .  
  
 Eventuali problemi correlati alla proprietà e alle autorizzazioni sul file fisico del dispositivo di backup possono interferire con l'operazione di backup. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sia possibile leggere e scrivere sul dispositivo e che l'account utilizzato per eseguire il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponga delle autorizzazioni di scrittura. Le autorizzazioni di accesso ai file, tuttavia, non vengono controllate dalla stored procedure [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)che aggiunge una voce per un dispositivo di backup nelle tabelle di sistema. Di conseguenza, i problemi relativi all'accesso e alla proprietà del file fisico del dispositivo di backup potrebbero emergere solo in fase di accesso alla risorsa fisica durante un tentativo di backup o ripristino.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-back-up-the-tail-of-the-transaction-log"></a>Per eseguire il backup della parte finale del log delle transazioni  
  
1.  Dopo aver stabilito la connessione all'istanza appropriata del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], in Esplora oggetti fare clic sul nome del server per espandere l'albero del server.  
  
2.  Espandere **Database**e, a seconda del database, selezionare un database utente o espandere **Database di sistema** e selezionare un database di sistema.  
  
3.  Fare clic con il pulsante destro del mouse sul database, scegliere **Attività**e quindi fare clic su **Back Up**. Verrà visualizzata la finestra di dialogo **Backup database** .  
  
4.  Verificare il nome del database nella casella di riepilogo **Database** . È possibile selezionare facoltativamente un database diverso nell'elenco.  
  
5.  Verificare che il modello di recupero sia impostato su **FULL** o **BULK_LOGGED**.  
  
6.  Nella casella di riepilogo **Tipo backup** selezionare **Log delle transazioni**.  
  
7.  Lasciare deselezionata l'opzione **Copia solo backup** .  
  
8.  Nell'area **Set di backup** , accettare il nome predefinito del set di backup indicato nella casella di testo **Nome** oppure immettere un nome diverso per il set di backup.  
  
9. Nella casella di testo **Descrizione** immettere una descrizione per il backup della parte finale del log.  
  
10. Specificare la scadenza del set di backup:  
  
    -   Per impostare la scadenza del set di backup dopo un numero di giorni specifico, fare clic su **Dopo** (opzione predefinita) e immettere il numero di giorni dopo la creazione del set trascorsi i quali il set scadrà. È possibile impostare un valore compreso nell'intervallo da 0 a 99999 giorni. L'impostazione del valore 0 giorni indica che il set di backup non ha scadenza.  
  
         Il valore predefinito viene impostato nell'opzione **Periodo di memorizzazione predefinito supporti di backup (giorni)** della finestra di dialogo **Proprietà server** (pagina**Impostazioni database** ). Per accedere a questa finestra di dialogo, fare clic con il pulsante destro del mouse sul nome del server in Esplora oggetti, scegliere Proprietà e quindi selezionare la pagina **Impostazioni database** .  
  
    -   Per impostare una data di scadenza specifica per il set di backup, fare clic su **Il**e immettere la data di scadenza del set.  
  
11. Fare clic su **Disco** o su **Nastro**per selezionare il tipo di destinazione del backup. Per selezionare i percorsi per un massimo di 64 unità disco o nastro contenenti un singolo set di supporti, fare clic su **Aggiungi**. I percorsi selezionati vengono visualizzati nella casella di riepilogo **Backup su** .  
  
     Per rimuovere una destinazione di backup, selezionarla e fare clic su **Rimuovi**. Per visualizzare il contenuto di una destinazione di backup, selezionarla e fare clic su **Contenuto**.  
  
12. Nella pagina **Opzioni** , selezionare un'opzione **Sovrascrivi supporti** facendo clic su una delle impostazioni seguenti:  
  
    -   **Esegui backup nel set di supporti esistente**  
  
         Per questa opzione, fare clic su **Accoda al set di backup esistente** o **Sovrascrivi tutti i set di backup esistenti**.  
  
         Selezionare facoltativamente l'opzione **Controlla nome set di supporti e scadenza set di backup** per impostare la verifica della data e dell'ora di scadenza del set di supporti e del set di backup durante l'operazione di backup.  
  
         Immettere facoltativamente un nome nella casella di testo **Nome set di supporti** . Se non si specifica un nome, verrà creato un set di supporti con nome vuoto. Se si specifica un nome per il set di supporti, il supporto (nastro o disco) verrà controllato per verificare che il nome effettivo corrisponda al nome specificato.  
  
         Se non si specifica il nome del set di supporti e si seleziona la casella di controllo per il controllo del nome, in caso di esito positivo anche il nome dei supporti nei supporti risulterà vuoto.  
  
    -   **Esegui backup in un nuovo set di supporti e cancella tutti i set di backup esistenti**  
  
         Per questa opzione, immettere un nome nella casella di testo **Nome nuovo set di supporti** e, facoltativamente, aggiungere una descrizione per il set di supporti nella casella di testo **Descrizione nuovo set di supporti** .  
  
     Per altre informazioni sulle opzioni dei set di supporti, vedere [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md).  
  
13. Nella sezione **Affidabilità** selezionare facoltativamente una delle opzioni seguenti:  
  
    -   **Verifica backup al termine**.  
  
    -   **Esegui checksum prima della scrittura nei supporti**.  
  
    -   **Continuare su errore di checksum**  
  
     Per informazioni sui checksum, vedere [Possibili errori relativi ai supporti durante il backup e il ripristino &#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md).  
  
14. Nella sezione **Log delle transazioni** selezionare **Esegui backup della parte finale del log e lascia il database in stato di ripristino**.  
  
     Questa opzione equivale a specificare l'istruzione [BACKUP](/sql/t-sql/statements/backup-transact-sql) seguente:  
  
     `BACKUP LOG <database_name> TO <backup_device> WITH NORECOVERY`  
  
    > [!IMPORTANT]  
    >  In fase di ripristino nella finestra di dialogo Ripristina database il tipo di backup della parte finale del log verrà visualizzato come **Log delle transazioni (solo copia)** .  
  
15. Se si esegue il backup su un'unità nastro, come specificato nella sezione **Destinazione** della pagina **Generale** , l'opzione **Scarica nastro al termine del backup** sarà attiva. Se si seleziona questa opzione, verrà inoltre attivata l'opzione **Riavvolgi il nastro prima di scaricarlo** .  
  
16. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] e versioni successive supporta la [compressione dei backup](backup-compression-sql-server.md). Per impostazione predefinita, la compressione di un backup dipende dal valore dell'opzione di configurazione del server **Valore predefinito di compressione backup**. Tuttavia, indipendentemente dall'impostazione predefinita a livello di server corrente, è possibile comprimere un backup selezionando **Comprimi backup**ed è possibile impedire la compressione selezionando **Non comprimere il backup**.  
  
     **Per visualizzare l'impostazione predefinita corrente della compressione dei backup**  
  
    -   [Visualizzare o configurare l'opzione di configurazione del server backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-create-a-backup-of-the-currently-active-transaction-log"></a>Per creare una copia di backup del log delle transazioni attivo  
  
1.  Eseguire l'istruzione BACKUP LOG per eseguire il backup del log delle transazioni attivo, specificando:  
  
    -   Il nome del database a cui appartiene il log delle transazioni di cui si desidera eseguire il backup.  
  
    -   Il dispositivo di backup in cui verrà memorizzato il backup del log delle transazioni.  
  
    -   Clausola NO_TRUNCATE.  
  
         Questa clausola consente di eseguire il backup della parte attiva del log delle transazioni anche se non è possibile accedere al database, purché il file del log delle transazioni sia accessibile e non danneggiato.  
  
###  <a name="TsqlExample"></a> Esempio (Transact-SQL)  
  
> [!NOTE]  
>  In questo esempio viene utilizzato [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]che utilizza il modello di recupero con registrazione minima. Per consentire i backup del log, prima di eseguire un backup completo del database, il database viene impostato in modo da utilizzare il modello di recupero con registrazione completa. Per altre informazioni, vedere [Visualizzare o modificare il modello di recupero di un database &#40;SQL Server&#41;](view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
 In questo esempio viene eseguito il backup del log della transazione attualmente attivo quando un database è danneggiato e inaccessibile, se il log delle transazioni non è danneggiato ed è accessibile.  
  
```scr  
BACKUP LOG AdventureWorks2012  
   TO MyAdvWorks_FullRM_log1  
   WITH NO_TRUNCATE;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Ripristinare un backup del log delle transazioni &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)   
 [Ripristinare un database di SQL Server fino a un punto specifico &#40;modello di recupero con registrazione completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)   
 [Eseguire il backup di database &#40;pagina Opzioni di backup&#41;](back-up-database-backup-options-page.md)   
 [Eseguire il backup di database &#40;pagina Generale&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)   
 [Applicare backup del log delle transazioni &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Ripristini di file &#40;modello di recupero con registrazione minima&#41;](file-restores-simple-recovery-model.md)   
 [Ripristini di file &#40;modello di recupero con registrazione completa&#41;](file-restores-full-recovery-model.md)  
  
  
