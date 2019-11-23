---
title: Backup database (pagina Generale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.backupdatabase.general.f1
ms.assetid: 5c344dfd-1ad3-41cc-98cd-732973b4a162
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fc6680702fd32c670d2f3c3861c47bab96c52c47
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155080"
---
# <a name="back-up-database-general-page"></a>Backup database (pagina Generale)
  Utilizzare la pagina **Generale** della finestra di dialogo **Backup database** per visualizzare o modificare le impostazioni per un'operazione di backup del database.  
  
 Per altre informazioni di base sui backup di database, vedere [Panoramica del backup &#40;SQL Server&#41;](backup-overview-sql-server.md).  
  
> [!NOTE]  
>  Quando si specifica un'attività di backup usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], è possibile generare lo script [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](/sql/t-sql/statements/backup-transact-sql) corrispondente facendo clic sul pulsante **Script** e quindi selezionando una destinazione per lo script.  
  
 **Per utilizzare SQL Server Management Studio per la creazione di un backup**  
  
-   [Creazione di un backup completo del database &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [Creazione di un backup differenziale del database &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
    > [!IMPORTANT]  
    >  È possibile definire un piano di manutenzione database per creare backup di database. Per ulteriori informazioni, vedere [Piani di manutenzione dei database](../maintenance-plans/maintenance-plans.md) nella documentazione online di [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .  
  
 **Per creare un backup parziale**  
  
-   Per un backup parziale, è necessario utilizzare l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](/sql/t-sql/statements/backup-transact-sql) con l'opzione PARTIAL.  
  
## <a name="options"></a>Opzioni  
  
### <a name="source"></a>Origine  
 Le opzioni del pannello **Origine** identificano il database e specificano il tipo di backup e il componente per l'operazione di backup.  
  
 **Database**  
 È possibile selezionare il database di cui eseguire il backup.  
  
 **Modello di recupero**  
 È possibile visualizzare il modello di recupero, ovvero SIMPLE, FULL o BULK_LOGGED, per il database selezionato.  
  
 **Tipo di backup**  
 È possibile selezionare il tipo di backup che si desidera eseguire per il database specificato.  
  
|Tipo di backup|Disponibile per|Restrizioni|  
|-----------------|-------------------|------------------|  
|Completo|Database, file e filegroup|Per il database **master** è possibile eseguire solo backup completi.<br /><br /> Quando si utilizza il modello di recupero con registrazione minima, i backup di file e filegroup sono disponibili solo per filegroup di sola lettura.|  
|Differenziale|Database, file e filegroup|Quando si utilizza il modello di recupero con registrazione minima, i backup di file e filegroup sono disponibili solo per filegroup di sola lettura.|  
|Log delle transazioni|Log delle transazioni|I backup dei log delle transazioni non sono disponibili per il modello di recupero con registrazione minima.|  
  
 **Backup di sola copia**  
 Selezionare questa opzione per creare un backup di sola copia. Un *backup di sola copia* è un backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indipendente dalla sequenza di backup convenzionali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Backup di sola copia &#40;SQL Server&#41;](copy-only-backups-sql-server.md).  
  
> [!NOTE]  
>  Quando si seleziona l'opzione **Differenziale**, non è possibile creare un backup di sola copia.  
  
 **Componente di cui eseguire il backup**  
 Con questa opzione è possibile selezionare il componente del database di cui eseguire il backup. Se nell'elenco **Tipo backup** è selezionato **Log delle transazioni** , questa opzione non è attivata.  
  
 Selezionare uno dei pulsanti di opzione seguenti:  
  
|||  
|-|-|  
|**Database**|È possibile specificare di eseguire il backup dell'intero database.|  
|**File e filegroup**|È possibile specificare di eseguire il backup dei file e/o dei filegroup specificati.<br /><br /> Selezionando questa opzione, viene visualizzata la finestra di dialogo **Seleziona file e filegroup** . Dopo avere selezionato i filegroup o i file di cui eseguire il backup e avere scelto **OK**, le opzioni selezionate verranno visualizzate nella casella **File e filegroup** .|  
  
### <a name="destination"></a>Destination  
 Con le opzioni del pannello **Destinazione** è possibile specificare il tipo di dispositivo di backup per l'operazione di backup e di trovare un dispositivo di backup logico o fisico esistente.  
  
> [!NOTE]  
>  Per informazioni sui dispositivi di backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Dispositivi di backup &#40;SQL Server&#41;](backup-devices-sql-server.md).  
  
 **Backup su**  
 Selezionare uno dei tipi di supporti seguenti su cui eseguire il backup. Le destinazioni selezionate vengono visualizzate nell'elenco **Backup su** .  
  
|||  
|-|-|  
|**Disco**|Indica di eseguire il backup su disco. Può trattarsi di un file di sistema o di un dispositivo di backup logico su disco creato per il database. I dischi attualmente selezionati vengono visualizzati nell'elenco **Backup su** . È possibile selezionare fino a 64 dispositivi disco per l'operazione di backup.|  
|**Tape**|Indica di eseguire il backup su nastro. Può trattarsi di un'unità nastro locale o di un dispositivo di backup logico su nastro creato per il database. I nastri attualmente selezionati vengono visualizzati nell'elenco **Backup su** . Il numero massimo è 64. Se al server non è collegato alcun dispositivo nastro, questa opzione è disattivata. I nastri selezionati vengono visualizzati nell'elenco **Backup su** .<br /><br /> Nota: il supporto per i dispositivi di backup su nastro verrà rimosso in una versione futura di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata.|  
|**URL**|Esegue il backup nell'archiviazione BLOB di Azure.|  
  
 Il set successivo di opzioni visualizzate dipende dal tipo di destinazione selezionata. Se si seleziona Disco o Nastro, vengono visualizzate le opzioni riportate di seguito.  
  
 **Aggiungi**  
 È possibile aggiungere un file o un dispositivo all'elenco **Backup su** . È possibile eseguire il backup su 64 dispositivi contemporaneamente su un disco locale o remoto. Per specificare un file su un disco remoto, utilizzare il nome completo in formato UNC (Universal Naming Convention). Per altre informazioni, vedere [Backup Devices &#40;SQL Server&#41;](backup-devices-sql-server.md).  
  
 **Rimuovi**  
 È possibile rimuovere uno o più dispositivi attualmente selezionati dall'elenco **Backup su** .  
  
 **Sommario**  
 È possibile visualizzare il contenuto dei supporti per il dispositivo selezionato.  
  
 Se si seleziona URL come destinazione di backup, vengono visualizzate le opzioni seguenti:  
  
 **Nome file**  
 Specificare il nome del file di backup.  
  
 **Credenziali SQL**  
 Selezionare le credenziali SQL usate per l'autenticazione nell'archiviazione di Azure. Se non si dispone di credenziali SQL esistenti utilizzabili, fare clic sul pulsante **Crea** per crearne delle nuove.  
  
> [!IMPORTANT]  
>  La finestra di dialogo visualizzata quando si fa clic su **Crea** richiede un certificato di gestione o il profilo di pubblicazione per la sottoscrizione. Se non si dispone dell'accesso al certificato di gestione o al profilo di pubblicazione, è possibile creare le credenziali di SQL specificando il nome dell'account di archiviazione e le informazioni sulla chiave di accesso tramite Transact-SQL o SQL Server Management Studio. Vedere il codice di esempio nella nell'argomento [per creare una credenziale](../security/authentication-access/create-a-credential.md#Credential) per creare una credenziale usando Transact-SQL. In alternativa, utilizzando SQL Server Management Studio, dall'istanza del motore di database, fare clic con il pulsante destro del mouse su **Sicurezza**, scegliere **Nuovo**e selezionare **Credenziale**. Specificare il nome dell'account di archiviazione per **Identity** e la chiave di accesso nel campo **Password** .  
  
 **Contenitore di archiviazione di Azure**  
 Specificare il nome del contenitore di Archiviazione di Azure  
  
 **Prefisso URL**  
 Viene generato automaticamente in base alle informazioni sull'account di archiviazione archiviate nelle credenziali SQL e al nome del contenitore di archiviazione di Azure specificato. Si consiglia di non modificare le informazioni in questo campo a meno che non si usi un dominio con un formato diverso da **\<account di archiviazione.blob.core.windows.net**.  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire il backup di un log delle transazioni &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)   
 [Eseguire il backup di file e filegroup &#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)   
 [Definizione di un dispositivo di backup logico per un file su disco &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [Definizione di un dispositivo di backup logico per un'unità nastro &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [Modelli di recupero &#40;SQL Server&#41;](recovery-models-sql-server.md)  
  
  
