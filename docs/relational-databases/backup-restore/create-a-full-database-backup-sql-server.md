---
title: Creare un backup completo del database (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [SQL Server], full backups
- backing up databases [SQL Server], SQL Server Management Studio
- backups [SQL Server], creating
- database backups [SQL Server], SQL Server Management Studio
ms.assetid: 586561fc-dfbb-4842-84f8-204a9100a534
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 729464b51af6c9450f9166bd9a3c51d35541810f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52530536"
---
# <a name="create-a-full-database-backup-sql-server"></a>Creazione di un backup completo del database (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 > Per SQL Server 2014, vedere [Creazione di un backup completo del database (SQL Server)](create-a-full-database-backup-sql-server.md).

  In questo argomento viene descritto come creare un backup completo del database in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o PowerShell.  
  
>  Per informazioni sul backup di SQL Server con il servizio di archiviazione BLOB di Azure, vedere [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) e [Backup di SQL Server nell'URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare 
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Non è possibile utilizzare l'istruzione BACKUP in una transazione esplicita o implicita.  
  
-   I backup creati nella versione più recente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non possono essere ripristinati nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Per una panoramica approfondita dei concetti e delle operazioni di backup, vedere [Panoramica del backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md) prima di procedere.  
  
###  <a name="Recommendations"></a> Indicazioni  
  
-   Con l'aumento delle dimensioni del database, i backup completi del database richiedono più tempo e più spazio di archiviazione. Per un database di grandi dimensioni, provare a integrare un backup completo del database con una serie di [backup di database differenziali](../../relational-databases/backup-restore/differential-backups-sql-server.md). Per altre informazioni, vedere [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).  
  
-   Stimare la dimensione di un backup del database completo tramite la stored procedure di sistema [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) .  
  
-   Per impostazione predefinita, per ogni operazione di backup eseguita in modo corretto viene aggiunta una voce al log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e al registro eventi di sistema. Se si eseguono frequenti backup, questi messaggi verranno accumulati, creando log di errori enormi. Ciò può rendere difficile l'individuazione di altri messaggi. In questo caso è possibile eliminare tali voci di log di backup usando il flag di traccia 3226 se nessuno degli script dipende da esse. Per altre informazioni, vedere [Flag di traccia &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  
  
###  <a name="Security"></a> Sicurezza  
 TRUSTWORTHY è impostato su OFF in un backup del database. Per informazioni su come impostare TRUSTWORTHY su ON, vedere [Opzioni ALTER DATABASE SET &#40; Transact-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 A partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , le opzioni **PASSWORD** e **MEDIAPASSWORD** non sono più disponibile per la creazione di backup. È possibile ripristinare backup creati con password.  
  
####  <a name="Permissions"></a> Permissions  
 Le autorizzazioni BACKUP DATABASE e BACKUP LOG vengono assegnate per impostazione predefinita ai membri del ruolo predefinito del server **sysadmin** e dei ruoli predefiniti del database **db_owner** e **db_backupoperator** .  
  
 Eventuali problemi correlati alla proprietà e alle autorizzazioni sul file fisico del dispositivo di backup possono interferire con l'operazione di backup. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è necessario poter leggere e scrivere nel dispositivo; l'account con il quale viene eseguito il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **deve** avere autorizzazioni di scrittura. Tuttavia, [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), che aggiunge una voce per un dispositivo di backup nelle tabelle di sistema, non controlla le autorizzazioni di accesso al file. Di conseguenza, i problemi relativi all'accesso e alla proprietà del file fisico del dispositivo di backup potrebbero emergere solo in fase di accesso alla risorsa fisica durante un tentativo di backup o ripristino.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
>  Quando si specifica un'attività di backup usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], è possibile generare lo script [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) corrispondente facendo clic sul pulsante **Script** e selezionando una destinazione per lo script.  
  
### <a name="back-up-a-database"></a>Eseguire il backup del database  
  
1.  Dopo aver stabilito la connessione all'istanza appropriata del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], in **Esplora oggetti**fare clic sul nome del server per espanderne l'albero.  
  
2.  Espandere **Database**e selezionare un database utente o espandere **Database di sistema** e selezionare un database di sistema.  
  
3.  Fare clic con il pulsante destro del mouse sul database, scegliere **Attività**e quindi fare clic su **Backup**. Verrà visualizzata la finestra di dialogo **Backup database** .  

  #### <a name="general-page"></a>**Pagina Generale**
  
4.  Verificare il nome del database nell'elenco a discesa **Database** . È possibile selezionare facoltativamente un database diverso nell'elenco.  
  
5.  La casella di testo **Modello di recupero** serve solo come riferimento.  È possibile eseguire il backup di un database per qualsiasi modello di recupero (**FULL**, **BULK_LOGGED**, o **SIMPLE**).  
  
6.  Nell'elenco a discesa **Tipo backup** selezionare **Completo**.  
  
     Si noti che dopo aver eseguito un backup completo, è possibile creare un backup differenziale del database. Per altre informazioni, vedere [Creare un backup differenziale del database &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md).  
  
7.  Facoltativamente, è possibile selezionare la casella di controllo **Backup di sola copia** per creare un backup di sola copia. Un *backup di sola copia* è un backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indipendente dalla sequenza di backup convenzionali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Backup di sola copia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  Per il tipo di backup **Differenziale** non è possibile creare un backup di sola copia.  

8.  Per **Componente di cui eseguire il backup**selezionare il pulsante di opzione **Database** .  
  
9. Nella sezione **Destinazione** usare l'elenco a discesa **Backup su** per selezionare la destinazione di backup. Fare clic su **Aggiungi** per aggiungere ulteriori oggetti e/o destinazioni di backup.
  
     Per rimuovere una destinazione di backup, selezionarla e fare clic su **Rimuovi**. Per visualizzare il contenuto di una destinazione di backup, selezionarla e fare clic su **Contenuto**.  

  #### <a name="media-options-page"></a>**Pagina Opzioni supporti**  
10. Per visualizzare o selezionare le opzioni dei supporti, fare clic su **Opzioni supporti** nel riquadro **Selezione pagina** .   
    
11. Selezionare un'opzione **Sovrascrivi supporti** facendo clic su una delle opzioni seguenti: 

    > [!IMPORTANT]  
    >  L'opzione **Sovrascrivi supporti** è disabilitata se è stato selezionato **URL** come destinazione di backup nella pagina **Generale**. Per altre informazioni, vedere [Backup database &#40;pagina Opzioni di backup &#41;](../../relational-databases/backup-restore/back-up-database-media-options-page.md)  


  -   **Esegui backup nel set di supporti esistente**  
  
      > [!IMPORTANT]  
      >  Se si intende utilizzare la crittografia, non selezionare questa opzione. Se si seleziona questa opzione, le opzioni di crittografia nella pagina **Opzioni di backup** saranno disabilitate. La crittografia non è supportata quando si esegue un accodamento al set di backup esistenti.  
  
         Per questa opzione, fare clic su **Accoda al set di backup esistente** o **Sovrascrivi tutti i set di backup esistenti**. Per altre informazioni, vedere [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
         Selezionare facoltativamente l'opzione **Controlla nome set di supporti e scadenza set di backup** per impostare la verifica della data e dell'ora di scadenza del set di supporti e del set di backup durante l'operazione di backup.  
  
         Immettere facoltativamente un nome nella casella di testo **Nome set di supporti** . Se non si specifica un nome, verrà creato un set di supporti con nome vuoto. Se si specifica un nome per il set di supporti, il supporto (nastro o disco) verrà controllato per verificare che il nome effettivo corrisponda al nome specificato.  
  
-   **Esegui backup in un nuovo set di supporti e cancella tutti i set di backup esistenti**  
  
    Per questa opzione, immettere un nome nella casella di testo **Nome nuovo set di supporti** e, facoltativamente, aggiungere una descrizione per il set di supporti nella casella di testo **Descrizione nuovo set di supporti** .  
  
14. Nella sezione **Affidabilità** è possibile selezionare facoltativamente:  
  
    -   **Verifica backup al termine**.  
  
    -   **Esegui checksum prima della scrittura nei supporti**.  Per informazioni sui checksum, vedere [Possibili errori relativi ai supporti durante il backup e il ripristino &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
    
    -   **Continua in caso di errori**. 

15. La sezione **Log delle transazioni** è attiva solo in caso di backup di un log delle transazioni, come specificato nella sezione **Tipo backup** della pagina **Generale** .  
      
16. Nella sezione **Unità nastro** l'opzione **Scarica nastro, al termine del backup** è attiva se si esegue il backup su un'unità nastro, come specificato nella sezione **Destinazione** della pagina **Generale** . Se si seleziona questa opzione, verrà inoltre attivata l'opzione **Riavvolgi il nastro prima di scaricarlo** .   

  #### <a name="backup-options-page"></a>**Pagina Opzioni di backup**  

17. Per visualizzare o selezionare le opzioni di backup, fare clic su **Opzioni di backup** nel riquadro **Selezione pagina** .  
  
18. Nella casella di testo **Nome** accettare il nome predefinito del set di backup oppure immettere un nome diverso per il set di backup.  
  
19. Nella casella di testo **Descrizione** è possibile immettere facoltativamente una descrizione del set di backup.  
  
20. Specificare quando il set di backup scadrà e potrà essere sovrascritto senza ignorare esplicitamente la verifica dei dati relativi alla scadenza:  
  
    -   Per impostare una scadenza specifica per il set di backup, fare clic su **Dopo** (opzione predefinita) e immettere il numero di giorni dopo la creazione del set trascorsi i quali il set scadrà. È possibile impostare un valore compreso nell'intervallo da 0 a 99999 giorni. L'impostazione del valore 0 giorni indica che il set di backup non ha scadenza.  
  
         Il valore predefinito viene impostato nell'opzione **Periodo di memorizzazione predefinito supporti di backup (giorni)** della finestra di dialogo **Proprietà server** (pagina delle impostazioni del database). Per accedere alla pagina, fare clic con il pulsante destro del mouse sul nome del server in Esplora oggetti e scegliere Proprietà, quindi selezionare la pagina **Impostazioni database** .  
  
    -   Per impostare una data di scadenza specifica per il set di backup, fare clic su **Il**e immettere la data di scadenza del set.  
  
         Per altre informazioni sulle date di scadenza dei backup, vedere [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).  
  
21. Nella sezione **Compressione** usare l'elenco a discesa **Imposta compressione backup** per selezionare il livello di compressione desiderato.  [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] e versioni successive supporta la [compressione dei backup](../../relational-databases/backup-restore/backup-compression-sql-server.md). Per impostazione predefinita, la compressione di un backup dipende dal valore dell'opzione di configurazione del server **Valore predefinito di compressione backup**. Tuttavia, indipendentemente dall'impostazione predefinita a livello di server corrente, è possibile comprimere un backup selezionando **Comprimi backup**ed è possibile impedire la compressione selezionando **Non comprimere il backup**.  
  
     Per altre informazioni sulle impostazioni della compressione dei backup, vedere [Visualizzare o configurare l'opzione di configurazione del server backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
22. Nella sezione **crittografia** usare la casella di controllo **Crittografa backup** per decidere se utilizzare la crittografia per il backup. Usare l'elenco a discesa **Algoritmo** per selezionare un algoritmo di crittografia.  Usare l'elenco a discesa **Certificato o chiave asimmetrica** per selezionare un certificato o una chiave asimmetrica esistente. La crittografia è supportata in SQL Server 2014 o versioni successive. Per altre informazioni sulle opzioni di crittografia, vedere [Eseguire il backup di database &#40;pagina Opzioni di backup&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md).  
  
  
È possibile creare i backup di database tramite [Creazione guidata piano di manutenzione](../maintenance-plans/use-the-maintenance-plan-wizard.md) . 

### <a name="examples"></a>Esempi  
#### <a name="a--full-back-up-to-disk-to-default-location"></a>**A.  Eseguire il backup completo su disco nel percorso predefinito**
In questo esempio verrà eseguito il backup su disco del database `Sales` nel percorso di backup predefinito.  Il backup di `Sales` non è mai stato eseguito.
1.  In **Esplora oggetti**connettersi a un'istanza del motore di database di SQL Server e, successivamente, espanderla.

2.  Espandere i **database**, fare clic con il pulsante destro del mouse su `Sales`, scegliere **Attività**, quindi fare clic su **Backup...**.

3.  Fare clic su **OK**.

#### <a name="b--full-back-up-to-disk-to-non-default-location"></a>**B.  Eseguire il backup completo su disco in un percorso non predefinito**
In questo esempio verrà eseguito il backup su disco del database `Sales` nel percorso `E:\MSSQL\BAK`.  In precedenza sono stati eseguiti backup di `Sales` .
1.  In **Esplora oggetti**connettersi a un'istanza del motore di database di SQL Server e, successivamente, espanderla.

2.  Espandere i **database**, fare clic con il pulsante destro del mouse su `Sales`, scegliere **Attività**, quindi fare clic su **Backup...**.

3.  Nella sezione **Destinazione** della pagina **Generale** selezionare **Disco** dall'elenco a discesa **Backup su:** .

4.  Fare clic su **Rimuovi** fino a quando non sono stati rimossi tutti i file di backup esistenti.

5.  Fare clic su **Aggiungi** e verrà aperta la finestra di dialogo **Selezionare la destinazione di backup** .

6.  Immettere `E:\MSSQL\BAK\Sales_20160801.bak` nella casella di testo del **nome file** .

7.  Fare clic su **OK**.

8.  Fare clic su **OK**.

#### <a name="c--create-an-encrypted-backup"></a>**C.  Creare un backup crittografato**
In questo esempio verrà eseguito il backup con crittografia del database `Sales` nel percorso di backup predefinito.  È già stata creata una  [**chiave master del database**](../../relational-databases/security/encryption/create-a-database-master-key.md) .  Inoltre, è già stato creato un  [**certificato**](../../t-sql/statements/create-certificate-transact-sql.md) denominato `MyCertificate`. Per un esempio T-SQL di creazione di una **chiave master del database** e di un **certificato** , vedere [Creare un backup crittografato](../../relational-databases/backup-restore/create-an-encrypted-backup.md).  
1.  In **Esplora oggetti**connettersi a un'istanza del motore di database di SQL Server e, successivamente, espanderla.

2.  Espandere i **database**, fare clic con il pulsante destro del mouse su `Sales`, scegliere **Attività**, quindi fare clic su **Backup...**.

3.  Nella sezione **Sovrascrivi supporti** della pagina **Opzioni supporti** selezionare **Esegui backup di un nuovo set di supporti e cancella tutti i set di backup esistenti**.

4.  Nella sezione **Crittografia** della pagina **Opzioni di backup** selezionare la casella di controllo **Crittografa backup** .

5.  Nell'elenco a discesa **Algoritmo** selezionare **AES 256**.

6.  Nell'elenco a discesa **Certificato o chiave asimmetrica** selezionare `MyCertificate`.

7.  Fare clic su **OK**.

#### <a name="d--back-up-to-the-azure-blob-storage-service"></a>**D.  Backup nel servizio di archiviazione BLOB di Azure**
#### <a name="common-steps"></a>**Passaggi comuni**  
Nei tre esempi seguenti viene eseguito un backup completo del database di `Sales` nel servizio di archiviazione BLOB di Microsoft Azure.  Il nome dell'account di archiviazione è `mystorageaccount`.  Il contenitore è denominato `myfirstcontainer`.  Per brevità, i primi quattro passaggi sono elencati di seguito una volta sola e tutti gli esempi verranno avviati con il **passaggio 5**.
1.  In **Esplora oggetti**connettersi a un'istanza del motore di database di SQL Server e, successivamente, espanderla.

2.  Espandere i **database**, fare clic con il pulsante destro del mouse su `Sales`, scegliere **Attività**, quindi fare clic su **Backup...**.

3.  Nella pagina **Generale** nella sezione **Destinazione** selezionare l' **URL** dall'elenco a discesa **Backup in:** .

4.  Fare clic su **Aggiungi** e verrà aperta la finestra di dialogo **Selezionare la destinazione di backup** .

    **D1.  Il backup con striping nell'URL e una credenziale di SQL Server esistono già**  
Sono stati creati i criteri di accesso archiviati con diritti di lettura, scrittura ed elenco.  Le credenziali di SQL Server, `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`, sono stati creati usando una firma di accesso condiviso associata a criteri di accesso archiviati.  
*
    5.  Selezionare `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` dalla casella di testo **Contenitore di Archiviazione di Azure:**

    6.  Nella casella di testo **File di Backup:** digitare `Sales_stripe1of2_20160601.bak`.

    7.  Fare clic su **OK**.

    8.  Ripetere i passaggi **4** e **5**.

    9.  Nella casella di testo **File di Backup:** digitare `Sales_stripe2of2_20160601.bak`.

    10.  Fare clic su **OK**.

    11.   Fare clic su **OK**.

    **D2.  Esiste una firma di accesso condiviso e le credenziali di SQL Server non esistono**
  5.    Digitare `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` nella casella di testo **Contenitore di Archiviazione di Azure:**
  
  6.    Digitare la firma di accesso condiviso nella casella di testo **Criteri di accesso condiviso:** .
  
  7.    Fare clic su **OK**.
  
  8.    Fare clic su **OK**.

    **D3.  Non esiste una firma di accesso condiviso**
  5.    Fare clic sul pulsante **Nuovo contenitore** e si aprirà la finestra di dialogo **Connetti a una sottoscrizione Microsoft** .  
  
  6.    Completare la finestra di dialogo **Connetti a una sottoscrizione Microsoft** e fare clic su **OK** per ritornare alla finestra di dialogo **Selezionare la destinazione di backup** .  Per altre informazioni, vedere [Connect to a Microsoft Azure Subscription (Connettersi a una sottoscrizione di Microsoft Azure)](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md) .
  
  7.    Fare clic su **OK** nella finestra di dialogo **Selezionare la destinazione di backup** .
  
  8.    Fare clic su **OK**.

  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
### <a name="create-a-full-database-backup"></a>Creare un backup completo del database  
  
1.  Per creare backup completo del database, eseguire l'istruzione BACKUP DATABASE specificando:  
  
    -   Il nome del database di cui eseguire il backup.  
  
    -   Il dispositivo di backup in cui archiviare il backup completo del database.  
  
     La sintassi di base dell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] per un backup completo del database è la seguente:  
  
     BACKUP DATABASE *database*  
  
     TO *dispositivo_backup* [ **,**...*n* ]  
  
     [ WITH *con_opzioni* [ **,**...*o* ] ];  
  
    |Opzione|Descrizione|  
    |------------|-----------------|  
    |*database*|Corrisponde al database di cui eseguire il backup.|  
    |*dispositivo_backup* [ **,**...*n* ]|Specifica un elenco di dispositivi di backup da 1 a 64 da utilizzare per l'operazione di backup. È possibile specificare un dispositivo di backup fisico oppure un dispositivo di backup logico corrispondente se è già stata definito. Per specificare un dispositivo di backup fisico, utilizzare l'opzione DISK o TAPE:<br /><br /> { DISK &#124; TAPE } **=**_nome\_dispositivo\_fisico\_backup_<br /><br /> Per altre informazioni, vedere [Dispositivi di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).|  
    |WITH *con_opzioni* [ **,**...*o* ]|Facoltativamente, specifica una o più opzioni aggiuntive, *o*. Per informazioni su alcune opzioni WITH di base, vedere il passaggio 2.|  
  
2.  Facoltativamente, specificare uno o più opzioni WITH. Alcune opzioni WITH di base sono descritte di seguito. Per informazioni su tutte le opzioni WITH, vedere [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).  
  
    -   Opzioni WITH del set di backup di base:  
  
         { COMPRESSION | NO_COMPRESSION }  
         Solo in [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] e versioni successive, specifica se la [compressione backup](../../relational-databases/backup-restore/backup-compression-sql-server.md) è eseguita su questo backup, ignorando l'impostazione predefinita a livello di server.  
  
         ENCRYPTION (ALGORITHM,  SERVER CERTIFICATE |ASYMMETRIC KEY)  
         Solo in SQL Server 2014 o versioni successive specificare l'algoritmo di crittografia da utilizzare e il certificato o la chiave asimmetrica da utilizzare per proteggere la crittografia.  
  
         DESCRIPTION **=** { **'**_text_**'** | **@**_text\_variable_ }  
         Specifica il testo in formato libero che descrive il set di backup. La stringa può essere composta da un massimo di 255 caratteri.  
  
         NAME **=** { *nome_set_backup* | **@**_var\_nome\_set\_backup_ }  
         Specifica il nome del set di backup. I nomi possono essere composti da un massimo di 128 caratteri. Se si omette NAME, al set di backup non viene assegnato alcun nome specifico.  
  
    -   Opzioni WITH del set di backup di base:  
  
         Per impostazione predefinita, BACKUP accoda il backup a un set di supporti esistente, conservando i set di backup esistenti. E possibile specificarlo in modo esplicito utilizzando l'opzione NOINIT. Per informazioni sull'accodamento a set di backup esistenti, vedere [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
         In alternativa, utilizzare l'opzione FORMAT per formattare i supporti di backup:  
  
         FORMAT [ **,** MEDIANAME**=** { *nome_supporto* | **@**_variabile\_nome\_supporto_ } ] [ **,** MEDIADESCRIPTION **=** { *testo* | **@**_variabile\_testo_ } ]  
         Utilizzare la clausola FORMAT, se i supporti vengono utilizzati per la prima volta o si desiderano sovrascrivere tutti i dati esistenti. Facoltativamente, assegnare al nuovo supporto un nome e una descrizione.  
  
        > [!IMPORTANT]  
        >  Utilizzare la clausola FORMAT dell'istruzione BACKUP con estrema cautela, in quanto entrambe comportano la cancellazione di eventuali backup archiviati in precedenza nei supporti di backup.  
  
###  <a name="TsqlExample"></a> Esempi (Transact-SQL)  
  
#### <a name="a-back-up-to-a-disk-device"></a>**A. Backup su un dispositivo disco**  
 Nell'esempio riportato di seguito viene eseguito il backup su disco del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] completo, utilizzando `FORMAT` per creare un nuovo set di supporti.  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.Bak'  
   WITH FORMAT,  
      MEDIANAME = 'Z_SQLServerBackups',  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="b-back-up-to-a-tape-device"></a>**B. Backup su un dispositivo nastro**  
 Nell'esempio seguente viene eseguito il backup completo su nastro del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] , accodandolo ai backup precedenti.  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO TAPE = '\\.\Tape0'  
   WITH NOINIT,  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="c-back-up-to-a-logical-tape-device"></a>**C. Backup su un dispositivo nastro logico**  
 Nell'esempio seguente viene creato in un dispositivo di backup logico per un'unità nastro. Nell'esempio viene quindi eseguito il backup completo del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] su quel dispositivo.  
  
```sql  
-- Create a logical backup device,   
-- AdventureWorks2012_Bak_Tape, for tape device \\.\tape0.  
USE master;  
GO  
EXEC sp_addumpdevice 'tape', 'AdventureWorks2012_Bak_Tape', '\\.\tape0'; USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO AdventureWorks2012_Bak_Tape  
   WITH FORMAT,  
      MEDIANAME = 'AdventureWorks2012_Bak_Tape',  
      MEDIADESCRIPTION = '\\.\tape0',   
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> Utilizzo di PowerShell  
Usare il cmdlet **Backup-SqlDatabase** . Per indicare in modo esplicito che si tratta di un backup completo del database, specificare il parametro **-BackupAction**  con il relativo valore predefinito **Database**. Questo parametro è facoltativo per i backup completi di database.  

### <a name="examples"></a>Esempi
#### <a name="a--full-local-backup"></a>**A.  Backup locale completo**  
L'esempio seguente consente di creare un backup di database completo del database di `MyDB` nel percorso di backup predefinito dell'istanza del server `Computer\Instance`. Facoltativamente, questo esempio specifica **-BackupAction Database**.  
```powershell 
Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Database  
```
 
#### <a name="b--full-backup-to-microsoft-azure"></a>**B.  Backup completo in Microsoft Azure**  
Nell'esempio seguente viene creato un backup completo del database `Sales` sull'istanza `MyServer` per il servizio di archiviazione Blob di Microsoft Azure.  Sono stati creati i criteri di accesso archiviati con diritti di lettura, scrittura ed elenco.  Le credenziali di SQL Server, `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`, sono stati creati usando una firma di accesso condiviso associata a criteri di accesso archiviati.  Il comando di PowerShell usa il parametro **BackupFile** per specificare il percorso (URL) e il nome del file di backup.

```powershell  
import-module sqlps;
$container = 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer';
$FileName = 'Sales.bak';
$database = 'Sales';
$BackupFile = $container + '/' + $FileName ;
  
Backup-SqlDatabase -ServerInstance "MyServer" -Database $database -BackupFile $BackupFile;
```
 
 **Per impostare e utilizzare il provider PowerShell per SQL Server**  
  
-   [Provider PowerShell per SQL Server](../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Eseguire il backup di un database (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Creare un backup differenziale del database &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
-   [Ripristinare un backup del database tramite SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [Ripristinare un backup del database nel modello di recupero con registrazione minima &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [Ripristinare un database fino al punto di errore nel modello di recupero con registrazione completa &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Ripristinare un database in una nuova posizione &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
  
-   [Utilizzare la Creazione guidata piano di manutenzione](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
## <a name="see-also"></a>Vedere anche  
**[Risoluzione dei problemi di backup in SQL Server e operazioni di ripristino](https://support.microsoft.com/kb/224071)**          
[Panoramica del backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Backup di log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Eseguire il backup di database &#40;pagina Generale&#41;](../../relational-databases/backup-restore/back-up-database-general-page.md)   
 [Eseguire il backup di database &#40;pagina Opzioni di backup&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)   
 [Backup differenziali &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [Backup completo del database &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)  
  
  
