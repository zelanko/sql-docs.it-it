---
title: 'SQL Server Managed Backup in Windows Azure: Interoperabilità e coesistenza | Microsoft Docs'
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
ms.openlocfilehash: d4d883d54a1ad933d4e248f292d9b6a222915a00
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62842908"
---
# <a name="sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence"></a>SQL Server Managed Backup in Windows Azure: Interoperabilità e coesistenza
  In questo argomento vengono descritte l'interoperabilità e la coesistenza di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] con alcune funzionalità di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], Di seguito vengono descritte alcune di queste caratteristiche: Gruppi di disponibilità AlwaysOn, mirroring del Database, piani di manutenzione di Backup, Log Shipping, backup Ad hoc, Scollega Database e Drop Database.  
  
### <a name="alwayson-availability-groups"></a>Gruppi di disponibilità AlwaysOn  
 Gruppi di disponibilità AlwaysOn configurati come una soluzione solo Azure supportata per Windows [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Le configurazioni del gruppo di disponibilità AlwaysOn ibride o solo in locale non sono supportate. Per altre informazioni e altre considerazioni, vedere [configurazione di SQL Server Managed Backup to Windows Azure per i gruppi di disponibilità](../../2014/database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)  
  
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
 I backup ad hoc o eseguiti una volta creati esternamente a [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] tramite Transact-SQL o SQL Server Management Studio possono influire sul processo di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] a seconda del tipo di backup e dei supporti di archiviazione utilizzati. I backup del log in un account di archiviazione Windows Azure diverso da quello utilizzato da [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] o in un'altra destinazione diversa dal servizio di archiviazione BLOB di Windows Azure comporteranno un'interruzione della catena di log. È consigliabile usare la [smart_admin.sp_backup_on_demand &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql) stored procedure per avviare un backup nei database che presentano [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] abilitata. È possibile avviare un backup completo del database o un backup del log tramite questa stored procedure.  
  
### <a name="drop-database-and-detach-database"></a>Elimina database e Scollega database  
 Se un database con [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] abilitato viene scollegato o eliminato, sebbene non siano possibili backup aggiuntivi, i backup precedenti rimangono nella risorsa di archiviazione finché il periodo di memorizzazione non è scaduto, vale a dire quando i backup verranno eliminati.  
  
### <a name="changes-to-recovery-model"></a>Modifiche al modello di recupero  
  
-   Se si modifica il modello di recupero di un database da **semplice** a **completo** oppure **minima delle operazioni Bulk**, si dispone dell'opzione di configurazione [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per il database. In questo modo verrà considerato come un nuovo database dalla prospettiva di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
-   Se si modifica il modello di recupero di un database da **completa** o **minima delle operazioni Bulk** al **semplice**, che ha [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] operazioni abilitate, backup non saranno più possibile pianificata. L'impostazione del periodo di memorizzazione rimarrà attiva e i file di backup rimarranno nell'account di archiviazione finché non scade il periodo di memorizzazione. Se si desidera mantenere i backup, si consiglia di scaricare i file in un account di archiviazione diverso o in un percorso locale. Le impostazioni di configurazione vengono mantenute e possono essere riutilizzate se il modello di recupero viene ripristinata **completa** oppure **minima delle operazioni Bulk** nuovamente.  
  
### <a name="log-backups-using-other-backup-tools-or-custom-scripts"></a>Backup del log tramite altri strumenti di backup o script personalizzati  
 Due backup configurati per l'esecuzione di backup del log nello stesso database causeranno l'interruzione della catena dei log di backup. Anche se tramite [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] si tenterà di porre rimedio all'interruzione della catena di backup pianificando backup completi al rilevamento di una situazione di questo tipo, ciò significa mantenersi continuamente aggiornati sulle interruzioni periodiche e sui backup del log eseguiti da due strumenti in competizione. Questa condizione può inoltre influire potenzialmente sulla recuperabilità del database poiché non vi sono strumenti in grado di garantire un set completo di backup in sequenza. Sebbene questo sia valido per due funzionalità o strumenti con cui si eseguono i backup del log, è utile illustrare esempi specifici come descritto di seguito. Si tratta anche della base per i problemi relativi alla configurazione dei piani di manutenzione o del log shipping come descritto nelle sezioni precedenti di questo argomento.  
  
 **Backup basati su Data Protection Manager (DPM):** Microsoft Data Protection Manager consente di eseguire backup completi e incrementali. I backup incrementali sono backup del log tramite cui viene eseguito un troncamento del log dopo la creazione di un backup della parte finale del log. Pertanto, la configurazione di DPM e di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per lo stesso database non è supportata.  
  
 **Strumenti di terze parti o script:** Qualsiasi strumento di terze parti o script che eseguono i backup del log che provocano il troncamento del log non è compatibile con [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]e non è supportato.  
  
 Se hai [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] abilitata per un'istanza di database e si desidera eseguire un backup ad hoc è possibile usare il [smart_admin.sp_backup_on_demand &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql) stored procedure, come descritto in precedenza sezione. Se inoltre si ha l'esigenza di pianificare o eseguire backup periodici all'esterno di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], è possibile utilizzare Backup di sola copia.  Per altre informazioni, vedere [Backup di sola copia &#40;SQL Server&#41;](../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
  
