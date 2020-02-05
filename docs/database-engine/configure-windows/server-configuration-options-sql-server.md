---
title: Opzioni di configurazione del server (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/13/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
keywords:
- configurazione server (SQL Server)
helpviewer_keywords:
- surface area configuration [SQL Server], sp_configure
- configuration options [SQL Server], when take effect
- server management [SQL Server], configuration options
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], configuring
- configuration options [SQL Server], setting
- options [SQL Server], configuration
- RECONFIGURE statement
- performance [SQL Server], servers
- configuration options [SQL Server]
- RECONFIGURE WITH OVERRIDE statement
- SQL Server, configuring
- sp_configure
- stored procedures [SQL Server], configuration options
- server configuration [SQL Server]
- administering SQL Server, configuration options
ms.assetid: 9f38eba6-39b1-4f1d-ba24-ee4f7e2bc969
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c42c9501772972c523d5635a159fcdeb54bf107b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "75001983"
---
# <a name="server-configuration-options-sql-server"></a>Opzioni di configurazione del server (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  È possibile gestire e ottimizzare le risorse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite le opzioni di configurazione, utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oppure la stored procedure di sistema sp_configure. Le opzioni di configurazione del server utilizzate più di frequente sono disponibili in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Tramite la stored procedure sp_configure è possibile accedere a tutte le opzioni di configurazione. Prima di impostare tali opzioni è importante valutare con attenzione i possibili effetti sul sistema. Per altre informazioni, vedere [Visualizzare o modificare le proprietà del server &#40;SQL Server&#41;](../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md).  
  
>**IMPORTANTE** La modifica delle opzioni avanzate è riservata ad amministratori di database esperti o a tecnici dotati di certificazione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="categories-of-configuration-options"></a>Categorie delle opzioni di configurazione  
 Le opzioni di configurazione diventano effettive:  
  
-   Immediatamente dopo l'impostazione dell'opzione e l'esecuzione dell'istruzione **RECONFIGURE** oppure, in determinati casi, dell'istruzione **RECONFIGURE WITH OVERRIDE**. La riconfigurazione di alcune opzioni invalida i piani nella cache dei piani, richiedendo la compilazione di nuovi piani. Per altre informazioni, vedere [DBCC FREEPROCCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md).
  
     -oppure-  
  
-   Dopo l'esecuzione delle azioni precedenti e il riavvio dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
Le opzioni per cui è necessario un riavvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indicheranno inizialmente il valore modificato solo nella colonna value. Dopo il riavvio, il nuovo valore verrà visualizzato sia nella colonna value che nella colonna value_in_use.  
  
Nel caso di alcune opzioni, per rendere effettivo il nuovo valore di configurazione è necessario riavviare il server. Se si imposta il nuovo valore e si esegue sp_configure prima di riavviare il server, il nuovo valore verrà visualizzato nella colonna **value** delle opzioni di configurazione, ma non nella colonna **value_in_use** . Dopo il riavvio del server, il nuovo valore verrà visualizzato anche nella colonna **value_in_use** .  
  
Le opzioni a configurazione automatica sono opzioni che vengono modificate automaticamente da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in base alle esigenze del sistema. Nella maggior parte dei casi non è necessario impostare manualmente i valori di tali opzioni. Tra le opzioni di questo tipo sono incluse, ad esempio, **max worker threads** e user connections.  
  
## <a name="configuration-options-table"></a>Tabella delle opzioni di configurazione  
 Nella tabella seguente sono elencate tutte le opzioni di configurazione disponibili, l'intervallo di impostazioni possibili e i valori predefiniti. Le opzioni di configurazione sono contrassegnate con i seguenti codici a lettere:  
  
-   A= Opzioni avanzate, che devono essere modificate solo da un amministratore di database esperto o un professionista dotato di certificazione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e che richiedono l'impostazione di show advanced options su 1.  
  
-   RR = opzioni che richiedono il riavvio del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   RP = opzioni che richiedono il riavvio del motore PolyBase.  
  
-   SC = opzioni a configurazione automatica.  
  
    |Opzione di configurazione|Valore minimo|Valore massimo|Predefinito|  
    |--------------------------|-------------------|-------------------|-------------|  
    |[access check cache bucket count](../../database-engine/configure-windows/access-check-cache-server-configuration-options.md) (A)|0|16384|0|  
    |[access check cache quota](../../database-engine/configure-windows/access-check-cache-server-configuration-options.md) (A)|0|2147483647|0|  
    |[ad hoc distributed queries](../../database-engine/configure-windows/ad-hoc-distributed-queries-server-configuration-option.md) (A)|0|1|0|  
    |[affinity I/O mask](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md) (A, RR)|-2147483648|2147483647|0|  
    |[affinity64 I/O mask](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md) (A, disponibile solo sulla versione a 64 bit di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])|-2147483648|2147483647|0|  
    |[affinity mask](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md) (A)|-2147483648|2147483647|0|  
    |[affinity64 mask](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) (A, RR) disponibile solo sulla versione a 64 bit di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|-2147483648|2147483647|0|  
    |[Agent XPs](../../database-engine/configure-windows/agent-xps-server-configuration-option.md) (A)|0|1|0<br /><br /> (Viene impostato su 1 all'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Il valore predefinito è 0 se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent viene configurato per l'avvio automatico durante l'installazione).|  
    |[allow updates](../../database-engine/configure-windows/allow-updates-server-configuration-option.md) (obsoleto. Non usare. altrimenti si verificherà un errore durante la riconfigurazione).|0|1|0|  
    |[automatic soft-NUMA disabled](soft-numa-sql-server.md)|0|1|0|  
    |[checksum di backup predefinito](../../database-engine/configure-windows/backup-checksum-default.md)|0|1|0|  
    |[backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)|0|1|0| 
    |[blocked process threshold](../../database-engine/configure-windows/blocked-process-threshold-server-configuration-option.md) (A)|0|86400|0|  
    |[c2 audit mode](../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md) (A, RR)|0|1|0|  
    |[clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)|0|1|0|  
    |[clr strict security](../../database-engine/configure-windows/clr-strict-security.md) (A) <br /> **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] e versioni successive).|0|1|0|  
    |[common criteria compliance enabled](../../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md) (A, RR)|0|1|0|  
    |[contained database authentication](../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md)|0|1|0|  
    |[cost threshold for parallelism](../../database-engine/configure-windows/configure-the-cost-threshold-for-parallelism-server-configuration-option.md) (A)|0|32767|5|  
    |[cross db ownership chaining](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md)|0|1|0|  
    |[cursor threshold](../../database-engine/configure-windows/configure-the-cursor-threshold-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[Database Mail XPs](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) (A)|0|1|0|  
    |[default full-text language](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md) (A)|0|2147483647|1033|  
    |[lingua predefinita](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)|0|9999|0|  
    |[default trace enabled](../../database-engine/configure-windows/default-trace-enabled-server-configuration-option.md) (A)|0|1|1|  
    |[disallow results from triggers](../../database-engine/configure-windows/disallow-results-from-triggers-server-configuration-option.md) (A)|0|1|0|  
    |[EKM provider enabled](../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)|0|1|0|  
    |[external scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md) (SC)<br /><br /> ** Richiede il riavvio per **: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).|0|1|0|  
    |[filestream_access_level](../../database-engine/configure-windows/filestream-access-level-server-configuration-option.md)|0|2|0|  
    |[fill factor](../../database-engine/configure-windows/configure-the-fill-factor-server-configuration-option.md) (A, RR)|0|100|0|  
    |ft crawl bandwidth (max), vedere [ft crawl bandwidth](../../database-engine/configure-windows/ft-crawl-bandwidth-server-configuration-option.md)(A)|0|32767|100|  
    |ft crawl bandwidth (min), vedere [ft crawl bandwidth](../../database-engine/configure-windows/ft-crawl-bandwidth-server-configuration-option.md)(A)|0|32767|0|  
    |ft notify bandwidth (max), vedere [ft notify bandwidth](../../database-engine/configure-windows/ft-notify-bandwidth-server-configuration-option.md)(A)|0|32767|100|  
    |ft notify bandwidth (min), vedere [ft notify bandwidth](../../database-engine/configure-windows/ft-notify-bandwidth-server-configuration-option.md)(A)|0|32767|0|  
    |[hadoop connectivity](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md) (RP)<br /><br /> **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e versioni successive).|0|7|0|   
    |[index create memory](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) (A, SC)|704|2147483647|0|  
    |[in-doubt xact resolution](../../database-engine/configure-windows/in-doubt-xact-resolution-server-configuration-option.md) (A)|0|2|0|  
    |[lightweight pooling](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md) (A, RR)|0|1|0|  
    |[locks](../../database-engine/configure-windows/configure-the-locks-server-configuration-option.md) (A, RR, SC)|5000|2147483647|0|  
    |[max degree of parallelism](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) (A)|0|32767|0|  
    |[max full-text crawl range](../../database-engine/configure-windows/max-full-text-crawl-range-server-configuration-option.md) (A)|0|256|4|  
    |[max server memory](../../database-engine/configure-windows/server-memory-server-configuration-options.md) (A, SC)|16|2147483647|2147483647|  
    |[max text repl size](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md)|0|2147483647|65536|  
    |[max worker threads](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md) (A)|128|32767<br /><br /> 1024 è il valore massimo consigliato per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a 32 bit, 2048 per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a 64 bit. **Nota:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] è stata l'ultima versione disponibile per i sistemi operativi a 32 bit.|0<br /><br /> Il valore 0 consente di configurare automaticamente il numero massimo di thread di lavoro in base al numero di processori, secondo la formula (256+( *\<processori>* -4) * 8) per le versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a 32 bit e (512 + ( *\<processori>* - 4) * 8) per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a 64 bit. **Nota:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] è stata l'ultima versione disponibile per i sistemi operativi a 32 bit.|  
    |[media retention](../../database-engine/configure-windows/configure-the-media-retention-server-configuration-option.md) (A, RR)|0|365|0|  
    |[min memory per query](../../database-engine/configure-windows/configure-the-min-memory-per-query-server-configuration-option.md) (A)|512|2147483647|1024|  
    |[min server memory](../../database-engine/configure-windows/server-memory-server-configuration-options.md) (A, SC)|0|2147483647|0|  
    |[trigger nidificati](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md)|0|1|1|  
    |[network packet size](../../database-engine/configure-windows/configure-the-network-packet-size-server-configuration-option.md) (A)|512|32767|4096|  
    |[Ole Automation Procedures](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md) (A)|0|1|0|  
    |[open objects](../../database-engine/configure-windows/open-objects-server-configuration-option.md) (A, RR, obsoleto)|0|2147483647|0|  
    |[optimize for ad hoc workloads](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md) (A)|0|1|0|  
    |[PH_timeout](../../database-engine/configure-windows/ph-timeout-server-configuration-option.md) (A)|1|3600|60|  
    |[polybase enabled](../../relational-databases/polybase/polybase-installation.md#enable) (RR) **Si applica a**: [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)])|0|1|0|
    |[precompute rank](../../database-engine/configure-windows/precompute-rank-server-configuration-option.md) (A)|0|1|0|  
    |[priority boost](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md) (A, RR)|0|1|0|  
    |[query governor cost limit](../../database-engine/configure-windows/configure-the-query-governor-cost-limit-server-configuration-option.md) (A)|0|2147483647|0|  
    |[query wait](../../database-engine/configure-windows/configure-the-query-wait-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[recovery interval](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md) (A, SC)|0|32767|0|  
    |[remote access](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md) (RR)|0|1|1|  
    |[remote admin connections](../../database-engine/configure-windows/remote-admin-connections-server-configuration-option.md)|0|1|0|  
    |[remote data archive](../../database-engine/configure-windows/configure-the-remote-data-archive-server-configuration-option.md)|0|1|0|  
    |[remote login timeout](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md)|0|2147483647|10|  
    |[remote proc trans](../../database-engine/configure-windows/configure-the-remote-proc-trans-server-configuration-option.md)|0|1|0|  
    |[remote query timeout](../../database-engine/configure-windows/configure-the-remote-query-timeout-server-configuration-option.md)|0|2147483647|600|  
    |[Replication XPs Option](../../database-engine/configure-windows/replication-xps-server-configuration-option.md) (A)|0|1|0|  
    |[scan for startup procs](../../database-engine/configure-windows/configure-the-scan-for-startup-procs-server-configuration-option.md) (A, RR)|0|1|0|  
    |[server trigger recursion](../../database-engine/configure-windows/server-trigger-recursion-server-configuration-option.md)|0|1|1|  
    |[set working set size](../../database-engine/configure-windows/set-working-set-size-server-configuration-option.md) (A, RR, obsoleto)|0|1|0|  
    |[show advanced options](../../database-engine/configure-windows/show-advanced-options-server-configuration-option.md)|0|1|0|  
    |[SMO e DMO XPs](../../database-engine/configure-windows/smo-and-dmo-xps-server-configuration-option.md) (A)|0|1|1|  
    |[transform noise words](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md) (A)|0|1|0|  
    |[two digit year cutoff](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) (A)|1753|9999|2049|  
    |[user connections](../../database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md) (A, RR, SC)|0|32767|0|  
    |[user options](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)|0|32767|0|  
    |[xp_cmdshell](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md) (A)|0|1|0|  
  
## <a name="see-also"></a>Vedere anche  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
 [DBCC FREEPROCCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)
  
  
