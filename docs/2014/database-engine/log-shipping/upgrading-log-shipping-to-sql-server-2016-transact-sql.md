---
title: Aggiornamento del log shipping a SQL Server 2014 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], upgrading
ms.assetid: b1289cc3-f5be-40bb-8801-0e3eed40336e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 773426ed91039ee4c0c6fd224547e44102f9846b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175420"
---
# <a name="upgrade-log-shipping-to-sql-server-2014-transact-sql"></a>Aggiornare il log shipping a SQL Server 2014 (Transact-SQL)
  Quando si effettua l'aggiornamento da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], è possibile mantenere le configurazioni per il log shipping. In questo argomento vengono descritti scenari alternativi e procedure consigliate per aggiornare una configurazione per il log shipping.

> [!NOTE]
>  La[compressione dei backup](../../relational-databases/backup-restore/backup-compression-sql-server.md) è stata introdotta in [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]. In una configurazione per il log shipping aggiornata viene usata l'opzione di configurazione a livello di server **backup compression default** per controllare se la compressione dei backup viene usata per i file di backup del log delle transazioni. Il comportamento della compressione dei backup relativa ai backup del log può essere specificato per ogni configurazione per il log shipping. Per altre informazioni, vedere [Configurare il log shipping &#40;SQL Server&#41;](configure-log-shipping-sql-server.md).


##  <a name="protect-your-data-before-the-upgrade"></a><a name="ProtectData"></a> Protezione dei dati prima dell'aggiornamento
 Prima di eseguire un aggiornamento del log shipping, è consigliabile proteggere i dati.

 **Per proteggere i dati**

1.  Eseguire un backup completo di ciascun database primario.

     Per altre informazioni, vedere [Creare un backup completo del database &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).

2.  Eseguire il comando [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) in ciascun database primario.

##  <a name="upgrading-the-monitor-server-instance"></a><a name="UpgradeMonitor"></a>Aggiornamento dell'istanza del server di monitoraggio
 L'istanza del server di monitoraggio, se presente, può essere aggiornata in qualsiasi momento.

 Durante l'aggiornamento del server di monitoraggio, la configurazione per il log shipping continua a funzionare, ma lo stato relativo non viene registrato nelle tabelle sul monitor e non verrà attivato alcun avviso configurato. Dopo l'aggiornamento, è possibile eseguire la stored procedure di sistema [sp_refresh_log_shipping_monitor](/sql/relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql) per aggiornare le informazioni contenute nelle tabelle di monitoraggio.

##  <a name="upgrading-log-shipping-configurations-with-a-single-secondary-server"></a><a name="UpgradeSingleSecondary"></a>Aggiornamento delle configurazioni per il log shipping con un unico server secondario
 Il processo di aggiornamento descritto in questa sezione prevede l'utilizzo di una configurazione costituita dal server primario e da un unico server secondario. Tale configurazione è rappresentata nella figura seguente, in cui vengono illustrate un'istanza del server primario, A, e un'unica istanza del server secondario, B.

 ![Un server secondario e nessun server di monitoraggio](../media/ls-2-wayconfig-nomonitor.gif "Un server secondario e nessun server di monitoraggio")

 Per informazioni sull'aggiornamento di più server secondari, vedere [Aggiornamento di più istanze del server secondario](#MultipleSecondaries)più avanti in questo argomento.
 

###  <a name="upgrading-the-secondary-server-instance"></a><a name="UpgradeSecondary"></a>Aggiornamento dell'istanza del server secondario
 Il processo di aggiornamento prevede innanzitutto l'aggiornamento delle istanze del server secondario di una configurazione per il log shipping di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versione successiva a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] prima di aggiornare l'istanza del server primario. È sempre necessario aggiornare prima l'istanza del server secondario per evitare che il log shipping funzioni in modo non corretto poiché un backup creato in una versione più recente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non può essere ripristinato in una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

 Il log shipping non viene interrotto durante tutto il processo di aggiornamento poiché tramite i server secondari aggiornati si continuano a ripristinare i backup del log dal server primario [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versione successiva. Il processo di aggiornamento delle istanze del server secondario dipende in parte dalla presenza di più server secondari nella configurazione per il log shipping. Per ulteriori informazioni, vedere [Aggiornamento di più istanze del server secondario](#MultipleSecondaries)più avanti in questo argomento.

 Durante l'aggiornamento dell'istanza del server secondario, i processi di copia del log shipping e di ripristino non sono in esecuzione e di conseguenza i backup del log delle transazioni non ripristinati si accumuleranno. La quantità di accumulo dipende dalla frequenza di esecuzione dei backup pianificati nel server primario. Se è stato configurato un server di monitoraggio separato, inoltre, è possibile che vengano generati avvisi che indicano che i ripristini non sono stati eseguiti per un tempo maggiore rispetto all'intervallo configurato.

 Dopo che il server secondario è stato aggiornato, i processi dell'agente di log shipping riprendono e continuano a copiare e ripristinare i backup del log dall'istanza del server primario, ovvero il server A. La quantità di tempo necessaria affinché il server secondario aggiorni il database secondario varia a seconda del tempo impiegato per aggiornare il server secondario e della frequenza dei backup nel server primario.

> [!NOTE]
>  Durante l'aggiornamento del server, il database secondario non viene aggiornato a un database di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Per eseguire l'aggiornamento, è necessario attivare la modalità online per il database.

> [!IMPORTANT]
>  L'opzione RESTORE WITH STANDBY non è supportata per i database che richiedono aggiornamenti. Se un database secondario aggiornato è stato configurato tramite RESTORE WITH STANDBY, non sarà più possibile ripristinare i log delle transazioni dopo l'aggiornamento. Per riprendere il log shipping sul database secondario, sarà necessario configurarlo nuovamente sul server di standby. Per ulteriori informazioni sull'opzione STANDBY, vedere [argomenti di ripristino &#40;&#41;Transact-SQL ](/sql/t-sql/statements/restore-statements-arguments-transact-sql).

###  <a name="upgrading-the-primary-server-instance"></a><a name="UpgradePrimary"></a> Aggiornamento dell'istanza del server primario
 Quando si pianifica un aggiornamento, un aspetto significativo da considerare è la quantità di tempo in cui il database non risulterà disponibile. Nello scenario di aggiornamento più semplice il database non è disponibile durante l'aggiornamento del server primario (scenario 1 riportato di seguito).

 A fronte di una maggiore complessità del processo di aggiornamento, è possibile aumentare la disponibilità del database eseguendo il failover del server primario [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versione successiva su un server secondario [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] prima di aggiornare il server primario originale (scenario 2 riportato di seguito). Sono disponibili due scenari di failover diversi. È possibile tornare al server primario originale e mantenere la configurazione per il log shipping originale oppure è possibile rimuovere la configurazione per il log shipping originale prima di aggiornare il server primario originale e creare in un secondo momento una nuova configurazione utilizzando il nuovo server primario. In questa sezione vengono descritti entrambi gli scenari.

> [!IMPORTANT]
>  Prima di aggiornare l'istanza del server primario, è necessario accertarsi di avere aggiornato l'istanza del server secondario. Per ulteriori informazioni, vedere [Aggiornamento dell'istanza del server secondario](#UpgradeSecondary)in precedenza in questo argomento.


####  <a name="scenario-1-upgrade-primary-server-instance-without-failover"></a><a name="Scenario1"></a>Scenario 1: aggiornamento dell'istanza del server primario senza failover
 Questo scenario è quello più semplice, ma provoca un tempo di inattività maggiore rispetto all'utilizzo del failover. L'istanza del server primario viene semplicemente aggiornata e il database non è disponibile durante l'aggiornamento.

 Dopo che il server è stato aggiornato, viene attivata automaticamente la modalità online per il database determinandone pertanto l'aggiornamento. Dopo che il database è stato aggiornato, viene ripresa l'esecuzione dei processi per il log shipping.

#### <a name="scenario-2-upgrade-primary-server-instance-with-failover"></a>Scenario 2. Aggiornamento dell'istanza del server primario con failover
 In questo scenario viene aumentata al massimo la disponibilità e ridotto al minimo il tempo di inattività. Nello scenario viene utilizzato un failover controllato sull'istanza del server secondario che consente di mantenere il database disponibile durante l'aggiornamento dell'istanza del server primario originale. Il tempo di inattività è limitato al tempo relativamente breve necessario per eseguire il failover anziché essere costituito dal tempo necessario per aggiornare l'istanza del server primario.

 L'aggiornamento dell'istanza del server primario con failover è un processo costituito da tre procedure generali, ovvero l'esecuzione di un failover controllato sul server secondario, l'aggiornamento dell'istanza del server primario originale a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]e l'impostazione del log shipping in un'istanza del server primario di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Tali procedure vengono descritte in questa sezione.

> [!IMPORTANT]
>  Se si intende disporre dell'istanza del server secondario come nuova istanza del server primario, è necessario rimuovere la configurazione per il log shipping. Il log shipping dovrà essere riconfigurato dal nuovo server primario nel nuovo server secondario dopo l'aggiornamento dell'istanza del server primario originale. Per ulteriori informazioni, vedere [Remove Log Shipping &#40;SQL Server&#41;](remove-log-shipping-sql-server.md).


#####  <a name="procedure-1-perform-a-controlled-failover-to-the-secondary-server"></a><a name="Procedure1"></a>Procedura 1: eseguire un failover controllato sul server secondario
 Failover controllato sul server secondario:

1.  Eseguire manualmente un [backup](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) della parte finale del log delle transazioni nel database primario SPECIFICAndo WITH NORECOVERY. Tale backup acquisisce qualsiasi record di log di cui non è stato eseguito il backup e attiva la modalità offline per il database. Si noti che mentre il database è offline, il processo di backup del log shipping non riuscirà.

     Nell'esempio seguente viene creato un backup della parte finale del log del database `AdventureWorks` nel server primario. Il file di backup viene denominato `Failover_AW_20080315.trn`:

    ```
    BACKUP LOG AdventureWorks 
      TO DISK = N'\\FileServer\LogShipping\AdventureWorks\Failover_AW_20080315.trn' 
       WITH NORECOVERY;
    GO
    ```

     È consigliabile utilizzare una convenzione di denominazione del file distinta per differenziare il file di backup creato manualmente da quelli creati dal processo di backup del log shipping.

2.  Nel server secondario effettuare le seguenti operazioni:

    1.  Verificare che tutti i backup eseguiti automaticamente dai processi di backup del log shipping siano stati applicati. Per verificare quali processi di backup sono stati applicati, usare l'stored procedure di sistema [sp_help_log_shipping_monitor](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-transact-sql) sul server di monitoraggio o sul server primario e secondario. Lo stesso file deve essere elencato nelle colonne **last_backup_file**, **last_copied_file**e **last_restored_file** . Se un file di backup non è stato copiato né ripristinato, richiamare manualmente i processi di copia dell'agente e di ripristino relativi alla configurazione per il log shipping.

         Per informazioni sull'avvio di un processo, vedere [Start a Job](../../ssms/agent/start-a-job.md).

    2.  Copiare il file di backup del log finale creato nel passaggio 1 dalla condivisione file nel percorso locale utilizzato dal log shipping nel server secondario.

    3.  Ripristinare il backup del log finale specificando WITH RECOVERY per attivare la modalità online per il database. In seguito a quest'ultima operazione, il database verrà aggiornato a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].

         Nell'esempio seguente viene ripristinato il backup della parte finale del log del database `AdventureWorks` nel database secondario. Nell'esempio viene utilizzata l'opzione WITH RECOVERY che consente di attivare la modalità online per il database:

        ```
        RESTORE LOG AdventureWorks 
          FROM DISK = N'c:\logshipping\Failover_AW_20080315.trn' 
           WITH RECOVERY;
        GO
        ```

        > [!NOTE]
        >  Per una configurazione in cui è presente più di un server secondario, è necessario tenere presente considerazioni aggiuntive. Per ulteriori informazioni, vedere [Aggiornamento di più istanze del server secondario](#MultipleSecondaries)più avanti in questo argomento.

    4.  Eseguire il failover del database reindirizzando i client dal server primario originale (server A) al server secondario online (server B).

    5.  Verificare che lo spazio disponibile sul log delle transazioni del database secondario non si esaurisca mentre il database è online. Per evitare che si verifichi questa situazione, potrebbe essere necessario eseguire un backup del log. In questo caso è consigliabile eseguire il backup in un percorso condiviso, ovvero una *condivisione di backup*, in modo che i backup siano disponibili per eseguire il ripristino nell'altra istanza del server.

#####  <a name="procedure-2-upgrade-the-original-primary-server-instance-to-sscurrent"></a><a name="Procedure2"></a>Procedura 2: aggiornare l'istanza del server primario originale a[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
 Dopo aver aggiornato l'istanza del server primario originale a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], per il database sarà ancora attivata la modalità offline e il formato.

#####  <a name="procedure-3-set-up-log-shipping-on-sscurrent"></a><a name="Procedure3"></a>Procedura 3: impostare il log shipping in[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
 La parte rimanente del processo di aggiornamento dipende dalla presenza della configurazione per il log shipping, come indicato di seguito:

-   Se è stata mantenuta la configurazione per il log shipping di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]o versione successiva, tornare all'istanza del server primario originale. Per ulteriori informazioni, vedere [Per tornare all'istanza del server primario originale](#SwitchToOrigPrimary)più avanti in questa sezione.

-   Se la configurazione per il log shipping è stata rimossa prima dell'esecuzione del failover, creare una nuova configurazione per il log shipping in cui l'istanza del server secondario originale costituisce la nuova istanza del server primario. Per ulteriori informazioni, vedere [Per mantenere l'istanza precedente del server secondario come nuova istanza del server primario](#KeepOldSecondaryAsNewPrimary)più avanti in questa sezione.

######  <a name="to-switch-back-to-the-original-primary-server-instance"></a><a name="SwitchToOrigPrimary"></a>Per tornare all'istanza del server primario originale

1.  Nel server primario provvisorio (server B) eseguire il backup della parte finale del log utilizzando WITH NORECOVERY per crearlo e per attivare la modalità offline per il database. La parte finale del log viene denominata `Switchback_AW_20080315.trn`, ad esempio:

    ```
    BACKUP LOG AdventureWorks 
      TO DISK = N'\\FileServer\LogShipping\AdventureWorks\Switchback_AW_20080315.trn' 
       WITH NORECOVERY;
    GO
    ```

2.  Se nel database primario provvisorio sono stati eseguiti backup del log delle transazioni, ripristinare questi ultimi utilizzando WITH NORECOVERY nel database offline nel server primario originale (server A) anziché ripristinare il backup della parte finale del log creato nel passaggio 1. Il database viene aggiornato al formato di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] nel momento in cui viene eseguito il primo ripristino del backup del log.

3.  Ripristinare il backup della parte finale del log, `Switchback_AW_20080315.trn`, nel database primario originale (nel server A) utilizzando WITH RECOVERY per attivare la modalità online per il database.

4.  Eseguire nuovamente il failover sul database primario originale (nel server A) reindirizzando i client al server secondario online dal server primario originale.

 Dopo che il database è online, verrà ripresa la configurazione per il log shipping originale.

######  <a name="to-keep-the-old-secondary-server-instance-as-the-new-primary-server-instance"></a><a name="KeepOldSecondaryAsNewPrimary"></a>Per conservare l'istanza precedente del server secondario come nuova istanza del server primario
 Definire una nuova configurazione per il log shipping utilizzando l'istanza precedente del server secondario, B, come server primario e l'istanza precedente del server primario, A, come nuovo server secondario nel modo indicato di seguito:

> [!IMPORTANT]
>  All'inizio del processo, prima di recuperare il backup del log delle transazioni manuale in base al quale è stata attivata la modalità offline per il database, è necessario che la configurazione per il log shipping sia stata rimossa dal server primario originale.

1.  Per evitare di eseguire un backup completo e di ripristinare il database nel nuovo server secondario (server A), applicare i backup del log dal nuovo database primario al nuovo database secondario. Nella configurazione di esempio questa operazione prevede il ripristino dei backup del log eseguiti nel server B nel database nel server A.

2.  Eseguire il backup del log dal nuovo database primario (nel server B).

3.  Ripristinare i backup del log nella nuova istanza del server secondario (server A) tramite WITH NORECOVERY. La prima operazione di ripristino aggiorna il database a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].

4.  Configurare il log shipping con il server secondario precedente (server B) come istanza del server primario.

    > [!IMPORTANT]
    >  Se si utilizza [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], specificare che il database secondario è già inizializzato.

     Per altre informazioni, vedere [Configurare il log shipping &#40;SQL Server&#41;](configure-log-shipping-sql-server.md).

5.  Eseguire il failover del database reindirizzando i client dal server primario originale (server A) al server secondario online (server B).

    > [!IMPORTANT]
    >  Quando si esegue il failover sul nuovo database primario, è necessario verificare che tutti i relativi metadati siano coerenti con quelli del database primario originale. Per ulteriori informazioni, vedere [gestire i metadati quando si rende disponibile un database in un'altra istanza del Server &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).

##  <a name="upgrading-multiple-secondary-server-instances"></a><a name="MultipleSecondaries"></a>Aggiornamento di più istanze del server secondario
 Tale configurazione è rappresentata nella figura seguente, in cui vengono illustrate un'istanza del server primario, A, e due istanze del server secondario, B e C.

 ![Due server secondari e nessun server di monitoraggio](../media/ls-3-wayconfig-nomonitor.gif "Due server secondari e nessun server di monitoraggio")

 In questa sezione viene descritto come eseguire l'aggiornamento tramite un failover e ritornare quindi al server primario originale. Se sono presenti più istanze del server secondario, l'aggiornamento dell'istanza primaria con failover costituisce un processo più complesso. Nella procedura seguente, dopo l'aggiornamento di tutti i server secondari, viene eseguito il failover del server primario su uno dei database secondari aggiornati. Successivamente il server primario originale viene aggiornato e il failover del log shipping viene eseguito nuovamente su tale server.

> [!IMPORTANT]
>  È necessario aggiornare sempre tutte le istanze del server secondario prima di aggiornare il server primario.

 **Per eseguire l'aggiornamento utilizzando un failover e ritornare quindi al server primario originale**

1.  Aggiornare tutte le istanze del server secondario (server B e server C).

2.  Eseguire la parte finale del log delle transazioni del database primario (nel server A), quindi attivare la modalità offline per il database eseguendo il backup del log delle transazioni tramite WITH NORECOVERY.

3.  Nel server secondario su cui si intende eseguire il failover (server B) attivare la modalità online per il database secondario ripristinando il backup del log tramite WITH RECOVERY.

4.  Nell'altro server secondario (server C) lasciare attivata la modalità offline per il database ripristinando il backup del log tramite WITH NORECOVERY.

    > [!NOTE]
    >  I processi di copia del log shipping e di ripristino verranno eseguiti nei server secondari, ma non eseguiranno alcuna operazione poiché i nuovi file di backup del log non saranno posizionati nella condivisione di backup.

5.  Eseguire il failover del database reindirizzando i client dal server primario originale (server A) al server secondario online (server B). Il database online diventa un server primario provvisorio, mantenendo disponibile il database mentre per il server primario originale è attivata la modalità offline (server A).

6.  Aggiornare il server primario originale (server A).

7.  Nel database in cui è stato eseguito il failover del database primario provvisorio (nel server B), eseguire manualmente il backup del log delle transazioni utilizzando WITH NORECOVERY. In questo modo viene attivata la modalità offline per il database.

8.  Ripristinare tutti i backup del log delle transazioni creati nel database primario provvisorio (nel server B) a ogni altro database secondario (nel server C) tramite WITH NORECOVERY. In questo modo il log shipping continuerà a funzionare dal database primario originale dopo il relativo aggiornamento, senza che sia necessario eseguire un ripristino completo di ogni database secondario.

9. Ripristinare il log delle transazioni dal server primario provvisorio (server B) al database primario originale (nel server A) tramite WITH RECOVERY.

##  <a name="redeploying-log-shipping"></a><a name="Redeploying"></a>Ridistribuzione del log shipping
 Se non si desidera eseguire la migrazione della configurazione per il log shipping tramite una delle procedure illustrate in precedenza, è possibile ridistribuire il log shipping reinizializzando il database secondario con un backup e ripristino completi del database primario. Questa operazione è consigliabile nel caso di un database di piccole dimensioni oppure se non è essenziale garantire un livello di disponibilità elevato durante il processo di aggiornamento.

 Per informazioni sull'abilitazione di log shipping, vedere [configurare il log shipping &#40;SQL Server&#41;](configure-log-shipping-sql-server.md).

## <a name="see-also"></a>Vedere anche
 [Backup del log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md) [applicare backup del log delle transazioni &#40;SQL Server](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md) [tabelle e stored procedure per il log shipping](log-shipping-tables-and-stored-procedures.md)
