---
title: Backup di un log delle transazioni (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- transaction log backups [SQL Server], SQL Server Management Studio
- backups [SQL Server], creating
- backing up transaction logs [SQL Server], SQL Server Management Studio
ms.assetid: 3426b5eb-6327-4c7f-88aa-37030be69fbf
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d36963c5107a1a25ce25201ac38883e5c0925315
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "64478921"
---
# <a name="back-up-a-transaction-log-sql-server"></a>Backup di un log delle transazioni (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene descritto come eseguire il backup di un log delle transazioni in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o PowerShell.  
  
   
##  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Non è possibile usare l'istruzione BACKUP in una transazione esplicita o [implicita](../../t-sql/statements/set-implicit-transactions-transact-sql.md) .  Per transazione esplicita si intende una transazione di cui vengono definiti in modo esplicito l'inizio e la fine.
  
##  <a name="Recommendations"></a> Indicazioni  
  
-   Se un database usa il [modello di recupero](recovery-models-sql-server.md) con registrazione completa o il modello di recupero con registrazione minima delle operazioni bulk, è necessario eseguire il backup del log delle transazioni con una frequenza sufficiente per garantire la protezione dei dati e per evitare il [riempimento del log delle transazioni](../logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md) stesso. Tronca il log e supporta il ripristino del database in corrispondenza di uno specifico punto nel tempo. 
  
-   Per impostazione predefinita, per ogni operazione di backup eseguita in modo corretto viene aggiunta una voce al log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e al registro eventi di sistema. Se il backup del log viene eseguito di frequente, questi messaggi possono aumentare rapidamente, provocando la creazione di log degli errori di dimensioni elevate e rendendo difficile l'individuazione di altri messaggi. In questo caso è possibile eliminare tali voci di log di backup usando il flag di traccia 3226 se nessuno degli script dipende da esse. Per altre informazioni, vedere [Flag di traccia &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  
  
  
##  <a name="Permissions"></a> Autorizzazioni  
**Controllare che le autorizzazioni siano corrette prima di iniziare.** 

Le autorizzazioni BACKUP DATABASE e BACKUP LOG vengono assegnate per impostazione predefinita ai membri del ruolo predefinito del server **sysadmin** e dei ruoli predefiniti del database **db_owner** e **db_backupoperator** .  
  
 Eventuali problemi correlati alla proprietà e alle autorizzazioni sul file fisico del dispositivo di backup possono interferire con l'operazione di backup. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sia possibile leggere e scrivere sul dispositivo e che l'account utilizzato per eseguire il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponga delle autorizzazioni di scrittura. Le autorizzazioni di accesso ai file, tuttavia, non vengono controllate dalla stored procedure [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), che aggiunge una voce per un dispositivo di backup nelle tabelle di sistema. I problemi relativi alle autorizzazioni del file fisico del dispositivo di backup potrebbero emergere solo in fase di accesso alla [risorsa fisica](backup-devices-sql-server.md) quando si prova a eseguire il backup o il ripristino. Anche in questo caso, controllare le autorizzazioni prima di iniziare.

[!INCLUDE[Freshness](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="back-up-using-ssms"></a>Eseguire il backup usando SSMS  
  
1.  Dopo aver effettuato la connessione all'istanza appropriata del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], in Esplora oggetti fare clic sul nome del server per espanderne l'albero.  
  
2.  Espandere **Database**e, a seconda del database, selezionare un database utente o espandere **Database di sistema** e selezionare un database di sistema.  
  
3.  Fare clic con il pulsante destro del mouse sul database, scegliere **Attività**e quindi fare clic su **Back Up**. Verrà visualizzata la finestra di dialogo **Backup database** .  
  
4.  Verificare il nome del database nella casella di riepilogo **Database** . È possibile selezionare facoltativamente un database diverso nell'elenco.  
  
5.  Verificare che il modello di recupero sia impostato su **FULL** o **BULK_LOGGED**.  
  
6.  Nella casella di riepilogo **Tipo backup** selezionare **Log delle transazioni**.  
  
7.  Facoltativamente, è possibile selezionare **Backup di sola copia** per creare un backup di sola copia. Un *backup di sola copia* è un backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indipendente dalla sequenza di backup convenzionali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Backup di sola copia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
    >** NOTA** Quando si seleziona l'opzione **Differenziale**, non è possibile creare un backup di sola copia.  
  
8.  Accettare il nome predefinito del set di backup indicato nella casella di testo **Nome** oppure immettere un nome diverso per il set di backup.  
  
9. Facoltativamente, immettere una descrizione del set di backup nella casella di testo **Descrizione** .  
  
10. Specificare la scadenza del set di backup:  
  
    -   Per impostare la scadenza del set di backup dopo un numero di giorni specifico, fare clic su **Dopo** (opzione predefinita) e immettere il numero di giorni dopo la creazione del set trascorsi i quali il set scadrà. È possibile impostare un valore compreso nell'intervallo da 0 a 99999 giorni. L'impostazione del valore 0 giorni indica che il set di backup non ha scadenza.  
  
         Il valore predefinito viene impostato nell'opzione **Periodo di memorizzazione predefinito supporti di backup (giorni)** della finestra di dialogo **Proprietà server** (pagina**Impostazioni database** ). Per accedere a questa finestra di dialogo, fare clic con il pulsante destro del mouse sul nome del server in Esplora oggetti, scegliere Proprietà e quindi selezionare la pagina **Impostazioni database** .  
  
    -   Per impostare una data di scadenza specifica per il set di backup, fare clic su **Il**e immettere la data di scadenza del set.  
  
11. Per selezionare il tipo di destinazione del backup fare clic su **Disco**, **URL** o **Nastro**. Per selezionare i percorsi per un massimo di 64 unità disco o nastro contenenti un singolo set di supporti, fare clic su **Aggiungi**. I percorsi selezionati vengono visualizzati nella casella di riepilogo **Backup su** .  
  
     Per rimuovere una destinazione di backup, selezionarla e fare clic su **Rimuovi**. Per visualizzare il contenuto di una destinazione di backup, selezionarla e fare clic su **Contenuto**.  
  
12. Per visualizzare o selezionare le opzioni avanzate, fare clic su **Opzioni** nel riquadro **Selezione pagina** .  
  
13. Selezionare un'opzione **Sovrascrivi supporti** facendo clic su una delle opzioni seguenti:  
  
    -   **Esegui backup nel set di supporti esistente**  
  
         Per questa opzione, fare clic su **Accoda al set di backup esistente** o **Sovrascrivi tutti i set di backup esistenti**. Per altre informazioni, vedere [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
         Selezionare facoltativamente l'opzione **Controlla nome set di supporti e scadenza set di backup** per impostare la verifica della data e dell'ora di scadenza del set di supporti e del set di backup durante l'operazione di backup.  
  
         Immettere facoltativamente un nome nella casella di testo **Nome set di supporti** . Se non si specifica un nome, verrà creato un set di supporti con nome vuoto. Se si specifica un nome per il set di supporti, il supporto (nastro o disco) verrà controllato per verificare che il nome effettivo corrisponda al nome specificato.  
  
         Se non si specifica il nome del set di supporti e si seleziona la casella di controllo per il controllo del nome, in caso di esito positivo anche il nome dei supporti nei supporti risulterà vuoto.  
  
    -   **Esegui backup in un nuovo set di supporti e cancella tutti i set di backup esistenti**  
  
         Per questa opzione, immettere un nome nella casella di testo **Nome nuovo set di supporti** e, facoltativamente, aggiungere una descrizione per il set di supporti nella casella di testo **Descrizione nuovo set di supporti** . Per altre informazioni, vedere [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
14. Nella sezione **Affidabilità** selezionare facoltativamente una delle opzioni seguenti:  
  
    -   **Verifica backup al termine**.  
  
    -   **Esegui checksum prima della scrittura nei supporti**e, facoltativamente, **Continua in caso di errori checksum**. Per informazioni sui checksum, vedere [Possibili errori relativi ai supporti durante il backup e il ripristino &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
15. Nella sezione **Log delle transazioni** eseguire le operazioni seguenti:  
  
    -   Per i backup dei log di routine, mantenere l'impostazione predefinita **Tronca il log delle transazioni rimuovendo le voci inattive**.  
  
    -   Per eseguire il backup della parte finale del log, ovvero il log attivo, selezionare **Esegui backup della parte finale del log e lascia il database in stato di ripristino**.  
  
         Un backup della parte finale del log viene eseguito dopo un errore per evitare la perdita di dati salvando la parte finale del log. Eseguire il backup del log attivo, ovvero il backup della parte finale del log, sia dopo un errore, prima di iniziare a ripristinare il database, sia quando si esegue il failover a un database secondario. Selezionare questa opzione corrisponde a specificare l'opzione NORECOVERY nell'istruzione BACKUP LOG di Transact-SQL. Per altre informazioni sui backup della parte finale del log, vedere [Backup della parte finale del log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
16. Se si esegue il backup su un'unità nastro, come specificato nella sezione **Destinazione** della pagina **Generale** , l'opzione **Scarica nastro al termine del backup** sarà attiva. Se si seleziona questa opzione, verrà inoltre attivata l'opzione **Riavvolgi il nastro prima di scaricarlo** .  
  
17. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] e versioni successive supporta la [compressione dei backup](../../relational-databases/backup-restore/backup-compression-sql-server.md). Per impostazione predefinita, la compressione di un backup dipende dal valore dell'opzione di configurazione del server **Valore predefinito di compressione backup**. Tuttavia, indipendentemente dall'impostazione predefinita a livello di server corrente, è possibile comprimere un backup selezionando **Comprimi backup**ed è possibile impedire la compressione selezionando **Non comprimere il backup**.  
  
     **Per visualizzare l'impostazione predefinita corrente della compressione dei backup**  
  
    -   [Visualizzare o configurare l'opzione di configurazione del server backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
 **Crittografia**  
  
 Per crittografare il file di backup, selezionare la casella di controllo **Crittografa backup** . Selezionare un algoritmo di crittografia da utilizzare per la crittografia del file di backup e fornire un certificato o una chiave asimmetrica. Gli algoritmi di crittografia disponibili sono:  
  
-   AES 128  
  
-   AES 192  
  
-   AES 256  
  
-   Triple DES  
  
 
## <a name="back-up-using-t-sql"></a>Eseguire il backup usando T-SQL  
  
1.  Per eseguire il backup del log delle transazioni, eseguire l'istruzione BACKUP LOG specificando gli elementi seguenti:  
  
    -   Il nome del database a cui appartiene il log delle transazioni di cui si desidera eseguire il backup.  
  
    -   Il dispositivo di backup in cui viene scritto il backup del log della transazione.  
  
###  <a name="TsqlExample"></a> Esempio (Transact-SQL)  
  
> **IMPORTANTE** In questo esempio viene utilizzato il database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] in cui viene utilizzato il modello di recupero con registrazione minima. Per consentire i backup del log, prima di eseguire un backup completo del database, il database viene impostato in modo da utilizzare il modello di recupero con registrazione completa. Per altre informazioni, vedere [Visualizzazione o modifica del modello di recupero di un database &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
 In questo esempio viene creato un backup del log delle transazioni per il database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] nel dispositivo di backup denominato creato in precedenza, `MyAdvWorks_FullRM_log1`.  
  
```sql  
BACKUP LOG AdventureWorks2012  
   TO MyAdvWorks_FullRM_log1;  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> Utilizzo di PowerShell  
  
1.  Usare il cmdlet **Backup-SqlDatabase** e specificare **Log** per il valore del parametro **-BackupAction** .  
  
     L'esempio seguente consente di creare un backup del log del database di `MyDB` nel percorso di backup predefinito dell'istanza del server `Computer\Instance`.  
  
    ```sql  
    --Enter this command at the PowerShell command prompt, C:\PS>  
    Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Log  
    ```  
  
 **Per impostare e utilizzare il provider PowerShell per SQL Server**  
  
-   [Provider PowerShell per SQL Server](../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> Related tasks  
  
-   [Ripristinare un backup del log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [Ripristino di un database di SQL Server fino a un punto specifico all'interno di un backup &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
-   [Risolvere i problemi relativi a un log delle transazioni completo &#40;Errore di SQL Server 9002&#41;](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
## <a name="more-information"></a>Ulteriori informazioni 
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Applicare backup del log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [Piani di manutenzione](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Backup completi del file &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)  
  
  
