---
title: Ripristina database (pagina Generale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restoredb.general.f1
ms.assetid: 160cf58c-b06a-475f-9a69-2b051e5767ab
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e659023f09701e9e14e852b3ac8c8c2e0642446b
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154733"
---
# <a name="restore-database-general-page"></a>Ripristina database (pagina Generale)
  Usare la pagina **Generale** per specificare informazioni sui database di destinazione e di origine per un'operazione di ripristino di un database.  
  
 **Per utilizzare SQL Server Management Studio per il ripristino del backup di un database**  
  
-   [Ripristinare un backup &#40;del database SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [Definire un dispositivo di backup logico per un'unità nastro &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
> [!NOTE]  
>  Quando si specifica un'attività di ripristino utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], è possibile generare lo script [!INCLUDE[tsql](../../includes/tsql-md.md)]di [ripristino](/sql/t-sql/statements/restore-statements-transact-sql) corrispondente facendo clic su **script** , quindi selezionando una destinazione per lo script.  
  
## <a name="permissions"></a>Permissions  
 Se il database da ripristinare non esiste, per eseguire un'operazione RESTORE l'utente deve disporre delle autorizzazioni CREATE DATABASE. Se il database esiste, le autorizzazioni per l'istruzione RESTORE vengono assegnate per impostazione predefinita ai membri dei ruoli predefiniti del server **sysadmin** e **dbcreator** e al proprietario (**dbo**) del database.  
  
 Le autorizzazioni per l'istruzione RESTORE vengono assegnate ai ruoli in cui le informazioni sull'appartenenza sono sempre disponibili per il server. Poiché è possibile controllare l'appartenenza ai ruoli predefiniti del database solo quando il database è accessibile e non è danneggiato, condizioni che non risultano sempre vere quando si esegue un'operazione RESTORE, i membri del ruolo predefinito del database **db_owner** non dispongono delle autorizzazioni per l'istruzione RESTORE.  
  
 Per il ripristino da un backup crittografato sono necessarie le autorizzazioni `VIEW DEFINITION` per la chiave asimmetrica o il certificato utilizzato per la crittografia durante il backup.  
  
## <a name="options"></a>Opzioni  
  
### <a name="source"></a>Source  
 Le opzioni incluse nel pannello **Ripristina da**identificano il percorso dei set di backup del database e determinano i set di backup da ripristinare.  
  
|Nome|Definizione|  
|----------|----------------|  
|**Database**|Selezionare il database da ripristinare dall'elenco a discesa. Nell'elenco sono inclusi solo i database di cui è stato eseguito il backup in base alla cronologia dei backup di **msdb** .|  
|**Dispositivo**|Selezionare i dispositivi di backup logici o fisici (nastri, URL o file) in cui sono inclusi i backup da ripristinare. Questo è necessario se il backup del database è stato effettuato su un'istanza diversa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Per selezionare uno o più dispositivi di backup logici o fisici, fare clic sul pulsante per la ricerca. Verrà visualizzata la finestra di dialogo **Seleziona dispositivi di backup** . È possibile selezionare fino a 64 dispositivi che appartengono a un singolo set di supporti. I dispositivi nastro devono essere fisicamente collegati al computer in cui è in esecuzione l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un file di backup può trovarsi su un dispositivo disco locale o rimovibile. Per altre informazioni, vedere [Dispositivi di backup &#40;SQL Server&#41;](backup-devices-sql-server.md). È anche possibile selezionare **URL** come tipo di dispositivo per i file di backup archiviati in archiviazione di Azure.<br /><br /> Quando si chiude la finestra di dialogo **Seleziona dispositivi di backup** , il dispositivo selezionato viene visualizzato sotto forma di valori di sola lettura nell'elenco **Dispositivo** .|  
|**Database**|Nell'elenco a discesa selezionare il nome del database da cui i backup devono essere ripristinati.<br /><br /> Nota: Questo elenco è disponibile solo quando l'opzione **Dispositivo** è selezionata. Saranno disponibili solo i database che dispongono di backup sui dispositivi selezionati.|  
  
### <a name="destination"></a>Destination  
 Con le opzioni incluse nel pannello **Ripristina fino a** vengono identificati il database e il punto di ripristino.  
  
|Nome|Definizione|  
|----------|----------------|  
|**Database**|Immettere il database da ripristinare nell'elenco. È possibile immettere un nuovo database oppure sceglierne uno esistente dall'elenco a discesa. Nell'elenco sono inclusi tutti i database presenti nel server, ad eccezione dei database di sistema **master** e **tempdb**.<br /><br /> Nota: Per ripristinare un backup protetto da password, è necessario usare l'istruzione [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) .|  
|**Ripristina fino a**|Per impostazione predefinita, l'opzione **Ripristina fino a** verrà impostata su "Ultimo backup eseguito". È anche possibile fare clic su **Sequenza temporale** per visualizzare la finestra di dialogo **Sequenza temporale backup** in cui viene visualizzata la cronologia dei backup del database sotto forma di sequenza temporale. Fare clic su **sequenza temporale** per definire `datetime` un oggetto specifico in cui si desidera ripristinare il database. Quest'ultimo sarà quindi ripristinato allo stato in cui si trovava in quel preciso momento. Vedere [Backup Timeline](backup-timeline.md).|  
  
### <a name="restore-plan"></a>Piano di ripristino  
  
|Nome|Definizione|  
|----------|----------------|  
|**Set di backup da ripristinare**|Visualizza i set di backup disponibili per il percorso specificato. Ogni set di backup è il risultato di una singola operazione di backup e viene distribuito in tutti i dispositivi nel set di supporti. Per impostazione predefinita, viene suggerito un piano di recupero, basato sulla selezione dei set di backup necessari per completare l'operazione di ripristino. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] viene utilizzata la cronologia di backup in **msdb** per identificare i backup necessari per ripristinare un database e creare un piano di ripristino. Per il ripristino di un database, ad esempio, il piano di ripristino seleziona il backup completo di database più recente e quindi l'eventuale backup di database differenziale successivo. Nel modello di recupero con registrazione completa, il piano di ripristino seleziona quindi tutti i successivi backup dei log.<br /><br /> Per eseguire l'override del piano di ripristino suggerito, è possibile modificare le selezioni seguenti nella griglia. I backup che dipendono da un backup deselezionato vengono automaticamente deselezionati.<br /><br /> **Ripristino**:<br />                          Le caselle di controllo selezionate indicano i set di backup da ripristinare.<br />**Nome**: Nome del set di backup.<br />**Componente**: Componente di cui è stato eseguito il backup: **Database**, **File** o **\<vuoto>** (per i log delle transazioni).<br />**Tipo**: Tipo di operazione di backup eseguita: **Completo**, **Differenziale** o **Log delle transazioni**.<br />**Server**: Nome dell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] che ha eseguito l'operazione di backup.<br />**Database**: Nome del database interessato dall'operazione di backup.<br />**Posizione**: Posizione del set di backup nel volume.<br />**Primo LSN**: Numero di sequenza del file di log della prima transazione nel set di backup. Vuoto per i backup dei file.<br />**Ultimo LSN**: Numero di sequenza del file di log dell'ultima transazione nel set di backup. Vuoto per i backup dei file.<br />**LSN checkpoint**: Numero di sequenza del file di log (LSN) del checkpoint più recente al momento della creazione del backup.<br />**LSN completo**: Numero di sequenza del file di log del backup completo più recente del database.<br />**Data di inizio**: Data e ora di inizio dell'operazione di backup, visualizzate in base alle impostazioni internazionali del client.<br />**Data di fine**: Data e ora di fine dell'operazione di backup, visualizzate in base alle impostazioni internazionali del client.<br />**Dimensioni**: Dimensioni in byte del set di backup.<br />**Nome utente**: Nome dell'utente che ha eseguito l'operazione di backup.<br /><br /> **Scadenza**: Data e ora di scadenza del set di backup.<br /><br /> Le caselle di controllo sono abilitate solo quando la casella **Selezione manuale** è selezionata. In tal caso è possibile scegliere i set di backup da ripristinare.<br /><br /> Quando la casella **Selezione manuale** è selezionata, l'accuratezza del piano di ripristino viene controllata in occasione di ogni modifica. Se la sequenza dei backup è errata, verrà visualizzato un messaggio di errore.|  
|**Verifica supporti di backup**|Chiama un'istruzione RESTORE VERIFY_ONLY sui set di backup selezionati.<br /><br /> Nota: Si tratta di un'operazione con esecuzione prolungata e il relativo stato di avanzamento può essere rilevato e annullato tramite il monitoraggio dell'avanzamento nel framework della finestra di dialogo.<br /><br /> Questo pulsante consente di controllare l'integrità dei file di backup selezionati prima di ripristinarli.<br /><br /> Durante il controllo dell'integrità dei set di backup, lo stato di avanzamento visualizzato nella parte inferiore sinistra della finestra di dialogo indicherà che è in corso una verifica anziché un'esecuzione.|  
  
## <a name="compatibility-support"></a>Informazioni sulla compatibilità  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]è possibile ripristinare un database utente dal backup di un database creato tramite [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versione successiva. Tuttavia, i backup dei database **master**, **model** e **msdb** creati da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] non possono essere ripristinati tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Inoltre, i backup creati in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] non possono essere ripristinati tramite alcuna versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] viene utilizzato un percorso predefinito diverso rispetto alle versioni precedenti. Pertanto, per ripristinare un database creato nel percorso predefinito di una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario utilizzare l'opzione MOVE.  
  
 Dopo aver ripristinato un database di una versione precedente a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], il database viene aggiornato automaticamente. In genere, il database diventa subito disponibile. Tuttavia, se in un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] sono inclusi indici full-text, questi vengono importati, reimpostati o ricompilati dal processo di aggiornamento, a seconda dell'impostazione della proprietà del server **Opzione di aggiornamento full-text** . Se l'opzione di aggiornamento è impostata su **Importa** o **Ricompila**, gli indici full-text non saranno disponibili durante l'aggiornamento. A seconda della quantità di dati indicizzati, l'importazione può richiedere diverse ore, mentre la ricompilazione può risultare dieci volte più lunga. Si noti inoltre che, quando l'opzione di aggiornamento è impostata su **Importa**e un catalogo full-text non è disponibile, gli indici full-text associati vengono ricompilati.  
  
## <a name="restoring-from-an-encrypted-backup"></a>Ripristino da un backup crittografato  
 Per un'operazione di ripristino è necessario che la chiave asimmetrica o il certificato utilizzato originariamente per creare il backup sia disponibile nell'istanza in cui si esegue il ripristino. L'account che esegue il ripristino deve disporre delle autorizzazioni `VIEW DEFINITIONS` per il certificato o la chiave asimmetrica. I certificati utilizzati per crittografare il backup non devono essere rinnovati o aggiornati.  
  
## <a name="restoring-from-azure-storage"></a>Ripristino da archiviazione di Azure  
 Quando si ripristina un backup archiviato in archiviazione di Azure, l'interfaccia utente di ripristino dispone di una nuova opzione per il dispositivo di backup. **URL** , nella finestra di dialogo **Seleziona dispositivi di backup** . Quando si fa clic su **Aggiungi**, viene visualizzata la finestra di dialogo **Connetti ad Azure** che consente di specificare le informazioni sulle credenziali SQL per l'autenticazione nell'account di archiviazione.  Una volta connessi all'account di archiviazione, i file di backup vengono visualizzati nella finestra di dialogo **individua un file di backup in Azure** in cui è possibile selezionare il file da usare per il ripristino.  
  
## <a name="see-also"></a>Vedere anche  
 [Dispositivi di backup &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [Ripristino di un backup da un dispositivo &#40;SQL Server&#41;](restore-a-backup-from-a-device-sql-server.md)   
 [Ripristino di un database fino a una transazione contrassegnata &#40;SQL Server Management Studio&#41;](restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)   
 [Ripristinare un backup del log delle transazioni &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)   
 [Visualizzare il contenuto di un nastro o di un file di backup &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)   
 [Visualizzazione delle proprietà e del contenuto di un dispositivo di backup logico &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)   
 [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)   
 [Argomenti dell'istruzione RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)   
 [Applicare backup di log delle transazioni &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)  
  
  
