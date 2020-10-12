---
title: Ripristina database (pagina Generale) | Microsoft Docs
description: Durante il ripristino di un database in SQL Server, usare la pagina Generale per specificare informazioni sui database di destinazione e di origine per un'operazione di ripristino di un database.
ms.custom: ''
ms.date: 09/28/2020
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restoredb.general.f1
ms.assetid: 160cf58c-b06a-475f-9a69-2b051e5767ab
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5c322f8c798a7b4a319df67e56565af54ceac20f
ms.sourcegitcommit: 9386ae1b90705a39d37d5541b70c5e8a6564f253
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2020
ms.locfileid: "91662180"
---
# <a name="restore-database-general-page"></a>Ripristina database (pagina Generale)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Usare la pagina **Generale** per specificare informazioni sui database di destinazione e di origine per un'operazione di ripristino di un database.  
    
-   [Ripristinare un backup del database con SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [Definizione di un dispositivo di backup logico per un'unità nastro &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
> [!NOTE]  
>  Quando si specifica un'attività di ripristino usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], è possibile generare lo script [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) corrispondente di [!INCLUDE[tsql](../../includes/tsql-md.md)] facendo clic su **Script** e quindi selezionando una destinazione per lo script.  
  
## <a name="permissions"></a>Autorizzazioni  
Per eseguire RESTORE per un database che non esiste, l'utente deve avere le autorizzazioni CREATE DATABASE. Le autorizzazioni RESTORE vengono assegnate per impostazione predefinita ai membri dei ruoli predefiniti del server **sysadmin** e **dbcreator** e al proprietario (**dbo**) per i database esistenti.  

Le informazioni di appartenenza per i ruoli con le autorizzazioni RESTORE sono sempre disponibili nell'istanza.

In un database accessibile e non danneggiato è possibile controllare l'appartenenza a un ruolo predefinito del database. I membri del ruolo predefinito del database **db_owner** non hanno le autorizzazioni RESTORE.  

È possibile controllare l'appartenenza a un ruolo predefinito del database solo quando il database è accessibile e non è danneggiato. Questo non è sempre il caso durante l'esecuzione di RESTORE. I membri del ruolo predefinito del database **db_owner** non hanno le autorizzazioni RESTORE.  

Le autorizzazioni per l'istruzione RESTORE vengono assegnate ai ruoli in cui le informazioni sull'appartenenza sono sempre disponibili per il server. È possibile controllare l'appartenenza a un ruolo predefinito del database solo quando il database è accessibile e non è danneggiato. Periodicamente, durante l'esecuzione di RESTORE, i membri del ruolo predefinito del database **db_owner** non hanno le autorizzazioni RESTORE.  

Per il ripristino da un backup crittografato sono necessarie le autorizzazioni **VIEW DEFINITION** per la chiave asimmetrica o il certificato utilizzato per la crittografia durante il backup.  
  
## <a name="options"></a>Opzioni  
  
### <a name="source"></a>Source (Sorgente)  

Queste opzioni identificano il percorso dei set di backup per il database e determinano i set di backup da ripristinare.  
  
|Termine|Definizione|  
|----------|----------------|  
|**Database**|Selezionare il database da ripristinare dall'elenco a discesa. Nell'elenco sono inclusi solo i database di cui è stato eseguito il backup in base alla cronologia dei backup di **msdb**.|  
|**Dispositivo**|Selezionare i dispositivi di backup logici o fisici (nastri, URL o file) che contengono i backup da ripristinare. Il dispositivo è necessario se il backup del database è stato creato in un'istanza diversa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Per selezionare uno o più dispositivi di backup logici o fisici, selezionare il pulsante sfoglia che apre la finestra di dialogo **Seleziona dispositivi di backup**. È possibile selezionare fino a 64 dispositivi che appartengono a un singolo set di supporti. I dispositivi nastro devono essere fisicamente collegati al computer in cui è in esecuzione l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un file di backup può trovarsi su un dispositivo disco locale o rimovibile. Per altre informazioni, vedere [Dispositivi di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md). È anche possibile selezionare **URL** come tipo di dispositivo per i file di backup archiviati in Archiviazione di Azure.<br /><br /> Quando si chiude la finestra di dialogo **Seleziona dispositivi di backup** , il dispositivo selezionato viene visualizzato sotto forma di valori di sola lettura nell'elenco **Dispositivo** .|  
|**Database**|Nell'elenco a discesa selezionare il nome del database da cui i backup devono essere ripristinati.<br /><br /> Nota: Questo elenco è disponibile solo quando l'opzione **Dispositivo** è selezionata. Saranno disponibili solo i database che dispongono di backup sui dispositivi selezionati.|  
  
### <a name="destination"></a>Destination  
 Con le opzioni incluse nel pannello **Ripristina fino a** vengono identificati il database e il punto di ripristino.  
  
|Termine|Definizione|  
|----------|----------------|  
|**Database**|Immettere il database da ripristinare nell'elenco. È possibile immettere un nuovo database oppure sceglierne uno esistente dall'elenco a discesa. Nell'elenco sono inclusi tutti i database presenti nel server, ad eccezione dei database di sistema **master** e **tempdb**.<br /><br /> Nota: Per ripristinare un backup protetto da password, è necessario usare l'istruzione [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) .|  
|**Ripristina fino a**|Per impostazione predefinita, l'opzione **Ripristina fino a** verrà impostata su "Ultimo backup eseguito". È anche possibile selezionare **Sequenza temporale** per visualizzare la finestra di dialogo **Sequenza temporale backup** in cui viene visualizzata la cronologia dei backup del database sotto forma di sequenza temporale. Selezionare **Sequenza temporale** per scegliere un valore **datetime** specifico in base al quale ripristinare il database. Quest'ultimo verrà quindi ripristinato nello stato in cui si trovava in quel preciso momento. Vedere [Backup Timeline](../../relational-databases/backup-restore/backup-timeline.md).|  
  
### <a name="restore-plan"></a>Piano di ripristino  
  
|Termine|Definizione|Valori|  
|----------|----------------|------------|  
|**Set di backup da ripristinare**|Visualizza i set di backup disponibili per il percorso specificato. Un'operazione di backup crea un set di backup che viene distribuito in tutti i dispositivi nel set di supporti. Per impostazione predefinita, viene suggerito un piano di recupero, basato sulla selezione dei set di backup necessari per completare l'operazione di ripristino. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usa la cronologia di backup in **msdb**. La cronologia viene usata per identificare i backup necessari per ripristinare un database e creare un piano di ripristino. Per il ripristino di un database, ad esempio, il piano di ripristino seleziona il backup completo di database più recente e quindi l'eventuale backup di database differenziale più recente. Nel modello di recupero con registrazione completa, il piano di ripristino seleziona quindi tutti i backup dei log.<br /><br /> Per ignorare il piano di recupero suggerito, è possibile modificare le impostazioni selezionate nella griglia. I backup che dipendono da un backup deselezionato vengono automaticamente deselezionati.<br /><br /> Le caselle di controllo sono abilitate solo quando la casella **Selezione manuale** è selezionata. È possibile selezionare i set di backup da ripristinare.<br /><br /> Quando la casella **Selezione manuale** è selezionata, l'accuratezza del piano di ripristino viene controllata in occasione di ogni modifica. Se la sequenza dei backup è errata, verrà visualizzato un messaggio di errore.|**Ripristino**: <br />                          Le caselle di controllo selezionate indicano i set di backup da ripristinare.<br /><br /> **Name**: <br />                          Nome del set di backup.<br /><br /> **Component**: Componente di cui è stato eseguito il backup: **database**, **file** o **\<blank>** , nel caso dei log delle transazioni.<br /><br /> **Tipo**: tipo di backup: **Completol**, **Differenziale** o **Log delle transazioni**.<br /><br /> **Server**: nome dell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] che ha completato l'operazione di backup.<br /><br /> **Database**: <br />                          Nome del database interessato dall'operazione di backup.<br /><br /> **Posizione**: Posizione del set di backup nel volume.<br /><br /> **Primo LSN**: <br />                          Numero di sequenza del file di log della prima transazione nel set di backup. Vuoto per i backup dei file.<br /><br /> **Ultimo LSN**: <br />                          Numero di sequenza del file di log dell'ultima transazione nel set di backup. Vuoto per i backup dei file.<br /><br /> **LSN checkpoint**: <br />                          Numero di sequenza del file di log (LSN) del checkpoint più recente al momento della creazione del backup.<br /><br /> **LSN completo**: <br />                          Numero di sequenza del file di log del backup completo più recente del database.<br /><br /> **Data di inizio**: <br />                          Data e ora di inizio dell'operazione di backup, visualizzate in base alle impostazioni internazionali del client.<br /><br /> **Data di fine**: <br />                          Data e ora di fine dell'operazione di backup, visualizzate in base alle impostazioni internazionali del client.<br /><br /> **Size**: <br />                          Dimensioni in byte del set di backup.<br /><br /> **Nome utente**: <br />                          nome dell'utente che ha completato l'operazione di backup.<br /><br /> **Scadenza**: <br />                          Data e ora di scadenza del set di backup.|  
|**Verifica supporti di backup**|Chiama un'istruzione RESTORE VERIFY_ONLY sui set di backup selezionati.<br /><br /> Nota: la verifica è un'operazione di lunga durata e il relativo stato di avanzamento può essere rilevato e annullato tramite il monitoraggio dell'avanzamento nel framework della finestra di dialogo.<br /><br /> Il pulsante consente di controllare l'integrità dei file di backup selezionati prima di ripristinarli.<br /><br /> Durante il controllo dell'integrità dei set di backup, lo stato di avanzamento visualizzato nella parte inferiore sinistra della finestra di dialogo indicherà che è in corso una verifica anziché un'esecuzione.||  
  
## <a name="compatibility-support"></a>Informazioni sulla compatibilità  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]è possibile ripristinare un database utente dal backup di un database creato tramite [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versione successiva. I backup dei database **master**, **model** e **msdb** creati da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] non possono essere ripristinati tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Inoltre, i backup creati in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] non possono essere ripristinati tramite alcuna versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] viene utilizzato un percorso predefinito diverso rispetto alle versioni precedenti. Per ripristinare un database creato nel percorso predefinito di una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario usare l'opzione MOVE.  
  
 Dopo aver ripristinato un database di una versione precedente a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], il database viene aggiornato automaticamente. In genere, il database diventa subito disponibile. Tuttavia, se in un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] sono inclusi indici full-text, questi vengono importati, reimpostati o ricompilati dal processo di aggiornamento, a seconda dell'impostazione della proprietà del server **Opzione di aggiornamento full-text** . Se l'opzione di aggiornamento è impostata su **Importa** o **Ricompila**, gli indici full-text non saranno disponibili durante l'aggiornamento. A seconda della quantità di dati indicizzati, l'importazione può richiedere diverse ore, mentre la ricompilazione può risultare 10 volte più lunga. Si noti inoltre che, quando l'opzione di aggiornamento è impostata su **Importa**e un catalogo full-text non è disponibile, gli indici full-text associati vengono ricompilati.  
  
## <a name="restoring-from-an-encrypted-backup"></a>Ripristino da un backup crittografato  
 Per un'operazione di ripristino è necessario che la chiave asimmetrica o il certificato usato originariamente per creare il backup sia disponibile nell'istanza in cui si esegue il ripristino. L'account che esegue il ripristino deve disporre delle autorizzazioni **VIEW DEFINITIONS** per il certificato o la chiave asimmetrica. Non rinnovare o aggiornare i certificati usati per crittografare il backup.  
  
## <a name="restoring-from-microsoft-azure-storage"></a>Ripristino dal servizio di archiviazione di Microsoft Azure  
Nella finestra di dialogo **Seleziona dispositivi di backup** selezionare **URL** dall'elenco a discesa **Tipo di supporti di backup** .  Selezionare quindi **Aggiungi** per aprire la finestra di dialogo **Selezionare un percorso del file di backup**. Selezionare una credenziale di SQL Server esistente e un contenitore di archiviazione di Azure. Aggiungere un nuovo contenitore di archiviazione di Azure con firma di accesso condiviso oppure generare una firma di accesso condiviso e credenziali di SQL Server per un contenitore di archiviazione esistente. Dopo aver eseguito la connessione all'account di archiviazione, i file di backup vengono visualizzati nella finestra di dialogo **Trova file di backup in Microsoft Azure** in cui è possibile selezionare il file da usare per il ripristino.  Vedere anche [Connect to A Microsoft Azure Subscription](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md)(Connettersi a una sottoscrizione di Microsoft Azure).
  
## <a name="see-also"></a>Vedere anche  
 [Dispositivi di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Ripristino di un backup da un dispositivo &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)   
 [Ripristino di un database fino a una transazione contrassegnata &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)   
 [Ripristinare un backup del log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)   
 [Visualizzare il contenuto di un nastro o di un file di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)   
 [Visualizzazione delle proprietà e del contenuto di un dispositivo di backup logico &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)   
 [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [Argomenti dell'istruzione RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)   
 [Applicare backup di log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)  
  
  
