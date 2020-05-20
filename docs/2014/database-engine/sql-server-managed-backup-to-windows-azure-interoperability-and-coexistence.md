---
title: 'SQL Server backup gestito in Azure: interoperabilità e coesistenza | Microsoft Docs'
description: Questo articolo descrive SQL Server backup gestito per Microsoft Azure interoperabilità e coesistenza con diverse funzionalità di SQL Server 2014.
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 78fb78ed-653f-45fe-a02a-a66519bfee1b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dcfa6636e5fc4391b42d2077bd55e0811dc0ca39
ms.sourcegitcommit: 553d5b21bb4bf27e232b3af5cbdb80c3dcf24546
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2020
ms.locfileid: "82849829"
---
# <a name="sql-server-managed-backup-to-azure-interoperability-and-coexistence"></a>Backup gestito di SQL Server in Azure: Interoperabilità e coesistenza
  In questo argomento vengono descritte l'interoperabilità e la coesistenza di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] con alcune funzionalità di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], tra cui gruppi di disponibilità AlwaysOn, mirroring del database, piani di manutenzione di backup, log shipping, backup ad hoc, scollegamento del database ed eliminazione del database.  
  
### <a name="alwayson-availability-groups"></a>Gruppi di disponibilità AlwaysOn  
 Gruppi di disponibilità AlwaysOn configurate come una soluzione solo Azure supportata per [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] . Le configurazioni del gruppo di disponibilità AlwaysOn ibride o solo in locale non sono supportate. Per altre informazioni e altre considerazioni, vedere [configurazione di SQL Server backup gestito in Azure per i gruppi di disponibilità](../../2014/database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)  
  
### <a name="database-mirroring"></a>Mirroring del database  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] è supportato solo nel database principale. Se sia il server principale che il server mirror sono configurati per l'utilizzo di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], il database con mirroring viene ignorato e non ne verrà eseguito il backup. Tuttavia, in caso di failover, tramite [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] verrà avviato il processo di backup dopo il completamento del cambio di ruolo da parte del mirror e quest'ultimo è online. I backup verranno archiviati in un nuovo contenitore in questo caso. Se il mirror non è configurato per utilizzare [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], in caso di failover non verrà eseguito alcun backup. È consigliabile configurare [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] sia nel server principale che nel server mirror in modo tale che i backup possano continuare in caso di failover.  
  
> [!TIP]  
>  Se si crea un database con mirroring in un'istanza con le impostazioni predefinite di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], può essere preferibile disabilitare le impostazioni predefinite dell'istanza di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], in modo da non essere applicate al database con mirroring, e quindi riabilitare le impostazioni predefinite dell'istanza dopo aver configurato il server principale e mirror.  
  
### <a name="maintenance-plan"></a>Piano di manutenzione  
 L'utilizzo dei piani di manutenzione per la creazione di backup di un database quando [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] è abilitato non è supportato. I piani di manutenzione comporteranno un'interruzione della catena di log e tramite [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] non sarà possibile supportare una recuperabilità garantita del database durante il ripristino. Ciò è valido anche se [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] è abilitato a livello di istanza.  
  
> [!TIP]  
>  I piani di manutenzione con backup di sola copia sono supportati con [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] configurato per lo stesso database o istanza.  
  
### <a name="log-shipping"></a>Log shipping  
 Non è possibile configurare il log shipping e [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per lo stesso database contemporaneamente. Questa operazione avrà effetto sulla recuperabilità del database utilizzando entrambe le funzionalità.  
  
### <a name="ad-hoc-backups-using-transact-sql-and-sql-server-management-studio"></a>Backup ad hoc tramite Transact-SQL e SQL Server Management Studio  
 I backup ad hoc o eseguiti una volta creati esternamente a [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] tramite Transact-SQL o SQL Server Management Studio possono influire sul processo di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] a seconda del tipo di backup e dei supporti di archiviazione utilizzati. I backup del log in un account di archiviazione di Azure diverso rispetto a quello che [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] USA, o qualsiasi altra destinazione rispetto al servizio di archiviazione BLOB di Azure, provocheranno un'interrotta di catena di log. È consigliabile utilizzare il [smart_admin. sp_backup_on_demand &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql) stored procedure per avviare un backup nei database [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] abilitati. È possibile avviare un backup completo del database o un backup del log tramite questa stored procedure.  
  
### <a name="drop-database-and-detach-database"></a>Elimina database e Scollega database  
 Se un database con [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] abilitato viene scollegato o eliminato, sebbene non siano possibili backup aggiuntivi, i backup precedenti rimangono nella risorsa di archiviazione finché il periodo di memorizzazione non è scaduto, vale a dire quando i backup verranno eliminati.  
  
### <a name="changes-to-recovery-model"></a>Modifiche al modello di recupero  
  
-   Se si modifica il modello di recupero di un database da **semplice** a **completo** o con **registrazione minima delle operazioni bulk**, è possibile scegliere di configurare [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per il database. In questo modo verrà considerato come un nuovo database dalla prospettiva di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
-   Se si modifica il modello di recupero di un database da **completo** o con **registrazione minima** delle operazioni bulk a **Simple**, che ha [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] abilitato, le operazioni di backup non verranno più pianificate. L'impostazione del periodo di memorizzazione rimarrà attiva e i file di backup rimarranno nell'account di archiviazione finché non scade il periodo di memorizzazione. Se si desidera mantenere i backup, si consiglia di scaricare i file in un account di archiviazione diverso o in un percorso locale. Le impostazioni di configurazione vengono mantenute e possono essere riutilizzate se il modello di recupero viene impostato nuovamente su **completo** o con **registrazione minima delle operazioni bulk** .  
  
### <a name="log-backups-using-other-backup-tools-or-custom-scripts"></a>Backup del log tramite altri strumenti di backup o script personalizzati  
 Due backup configurati per l'esecuzione di backup del log nello stesso database causeranno l'interruzione della catena dei log di backup. Anche se tramite [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] si tenterà di porre rimedio all'interruzione della catena di backup pianificando backup completi al rilevamento di una situazione di questo tipo, ciò significa mantenersi continuamente aggiornati sulle interruzioni periodiche e sui backup del log eseguiti da due strumenti in competizione. Questa condizione può inoltre influire potenzialmente sulla recuperabilità del database poiché non vi sono strumenti in grado di garantire un set completo di backup in sequenza. Sebbene questo sia valido per due funzionalità o strumenti con cui si eseguono i backup del log, è utile illustrare esempi specifici come descritto di seguito. Si tratta anche della base per i problemi relativi alla configurazione dei piani di manutenzione o del log shipping come descritto nelle sezioni precedenti di questo argomento.  
  
 **Backup basati su Data Protection Manager (DPM):** Microsoft Data Protection Manager consente di eseguire backup completi e incrementali. I backup incrementali sono backup del log tramite cui viene eseguito un troncamento del log dopo la creazione di un backup della parte finale del log. Pertanto, la configurazione di DPM e di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per lo stesso database non è supportata.  
  
 **Strumenti o script di terze parti:** Qualsiasi strumento o script di terze parti che esegue backup del log che causa il troncamento del log non è compatibile con [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] e non è supportato.  
  
 Se è stata [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] abilitata un'istanza di database e si desidera eseguire un backup ad hoc, è possibile utilizzare il [smart_admin. Sp_backup_on_demand &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql) stored procedure come descritto nella sezione precedente. Se inoltre si ha l'esigenza di pianificare o eseguire backup periodici all'esterno di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], è possibile utilizzare Backup di sola copia.  Per altre informazioni, vedere [Backup di sola copia &#40;SQL Server&#41;](../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
  
