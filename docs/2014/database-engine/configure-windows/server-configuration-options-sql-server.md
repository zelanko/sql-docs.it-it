---
title: Opzioni di configurazione del server (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/29/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
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
manager: craigg
ms.openlocfilehash: 645aee1374f7dbf3c290500bb35ca47115983670
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62809569"
---
# <a name="server-configuration-options-sql-server"></a>Opzioni di configurazione del server (SQL Server)
  È possibile gestire e ottimizzare le risorse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite le opzioni di configurazione, utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oppure la stored procedure di sistema sp_configure. Le opzioni di configurazione del server utilizzate più di frequente sono disponibili in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Tramite la stored procedure sp_configure è possibile accedere a tutte le opzioni di configurazione. Prima di impostare tali opzioni è importante valutare con attenzione i possibili effetti sul sistema. Per altre informazioni, vedere [Visualizzare o modificare le proprietà del server &#40;SQL Server&#41;](view-or-change-server-properties-sql-server.md).  
  
> [!IMPORTANT]  
>  La modifica delle opzioni avanzate è riservata ad amministratori di database esperti o a tecnici dotati di certificazione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="categories-of-configuration-options"></a>Categorie delle opzioni di configurazione  
 Le opzioni di configurazione diventano effettive:  
  
-   Immediatamente dopo l'impostazione dell'opzione e l'esecuzione dell'istruzione RECONFIGURE oppure, in determinati casi, dell'istruzione RECONFIGURE WITH OVERRIDE.  
  
     -oppure-  
  
-   Dopo l'esecuzione delle azioni precedenti e il riavvio dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Le opzioni per cui è necessario un riavvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indicheranno inizialmente il valore modificato solo nella colonna value. Dopo il riavvio, il nuovo valore verrà visualizzato sia nella colonna value che nella colonna value_in_use.  
  
 Nel caso di alcune opzioni, per rendere effettivo il nuovo valore di configurazione è necessario riavviare il server. Se si imposta il nuovo valore e si esegue sp_configure prima di riavviare il server, il nuovo valore verrà visualizzato nella colonna value delle opzioni di configurazione, ma non nella colonna value_in_use. Dopo il riavvio del server, il nuovo valore verrà visualizzato anche nella colonna value_in_use.  
  
 Le opzioni a configurazione automatica sono opzioni che vengono modificate automaticamente da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in base alle esigenze del sistema. Nella maggior parte dei casi non è necessario impostare manualmente i valori di tali opzioni. Sono esempi di opzioni a configurazione automatica min server memory, max server memory e user connections.  
  
## <a name="configuration-options-table"></a>Tabella delle opzioni di configurazione  
 Nella tabella seguente sono elencate tutte le opzioni di configurazione disponibili, l'intervallo di impostazioni possibili e i valori predefiniti. Le opzioni di configurazione sono contrassegnate con i seguenti codici a lettere:  
  
-   A= Opzioni avanzate, che devono essere modificate solo da un amministratore di database esperto o un tecnico dotato di certificazione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e che richiedono l'impostazione di show advanced options su 1.  
  
-   RR = opzioni che richiedono il riavvio del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   SC = opzioni a configurazione automatica.  
  
    |Opzione di configurazione|Valore minimo|Valore massimo|Predefinito|  
    |--------------------------|-------------------|-------------------|-------------|  
    |[conteggio bucket cache controllo accessi](access-check-cache-server-configuration-options.md) (A)|0|16384|0|  
    |[quota cache check Access](access-check-cache-server-configuration-options.md) (A)|0|2147483647|0|  
    |[query distribuite ad hoc](ad-hoc-distributed-queries-server-configuration-option.md) (A)|0|1|0|  
    |[affinity I/O mask](affinity-input-output-mask-server-configuration-option.md) (A, RR)|-2147483648|2147483647|0|  
    |[affinity64 I/O mask](affinity64-input-output-mask-server-configuration-option.md) (A, disponibile solo nella versione a 64 bit di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])|-2147483648|2147483647|0|  
    |[affinity mask](affinity-mask-server-configuration-option.md) (A)|-2147483648|2147483647|0|  
    |[affinity64 mask](affinity64-mask-server-configuration-option.md) (A, RR), disponibile solo nella versione a 64 bit di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|-2147483648|2147483647|0|  
    |[Agente XPS](agent-xps-server-configuration-option.md) (A)|0|1|0<br /><br /> (Viene impostato su 1 all'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Il valore predefinito è 0 se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent viene configurato per l'avvio automatico durante l'installazione).|  
    |[Consenti aggiornamenti](allow-updates-server-configuration-option.md) (obsoleti. Non usare. altrimenti si verificherà un errore durante la riconfigurazione).|0|1|0|  
    |[checksum di backup predefinito](../backup-checksum-default.md)|0|1|0|  
    |[valore predefinito di compressione backup](view-or-configure-the-backup-compression-default-server-configuration-option.md)|0|1|0|  
    |[soglia di processo bloccata](blocked-process-threshold-server-configuration-option.md) (A)|0|86400|0|  
    |[modalità di controllo C2](c2-audit-mode-server-configuration-option.md) (A, RR)|0|1|0|  
    |[clr enabled](clr-enabled-server-configuration-option.md)|0|1|0|  
    |[conformità ai criteri comuni abilitata](common-criteria-compliance-enabled-server-configuration-option.md) (A, RR)|0|1|0|  
    |[contained database authentication](contained-database-authentication-server-configuration-option.md)|0||0|  
    |[soglia costo per parallelismo](configure-the-cost-threshold-for-parallelism-server-configuration-option.md) (A)|0|32767|5|  
    |[cross db ownership chaining](cross-db-ownership-chaining-server-configuration-option.md)|0|1|0|  
    |[soglia cursori](configure-the-cursor-threshold-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[Posta elettronica database XPS](database-mail-xps-server-configuration-option.md) (A)|0|1|0|  
    |[lingua predefinita full-text](configure-the-default-full-text-language-server-configuration-option.md) (A)|0|2147483647|1040|  
    |[lingua predefinita](configure-the-default-language-server-configuration-option.md)|0|9999|0|  
    |[traccia predefinita abilitata](default-trace-enabled-server-configuration-option.md) (A)|0|1|1|  
    |[disallow results from triggers](disallow-results-from-triggers-server-configuration-option.md) (A)|0|1|0|  
    |[EKM provider enabled](ekm-provider-enabled-server-configuration-option.md)|0|1|0|  
    |[filestream_access_level](filestream-access-level-server-configuration-option.md)|0|2|0|  
    |[fattore di riempimento](configure-the-fill-factor-server-configuration-option.md) (A, RR)|0|100|0|  
    |ft crawl bandwidth (max), vedere [ft crawl bandwidth](ft-crawl-bandwidth-server-configuration-option.md)(A)|0|32767|100|  
    |ft crawl bandwidth (min), vedere [ft crawl bandwidth](ft-crawl-bandwidth-server-configuration-option.md)(A)|0|32767|0|  
    |ft notify bandwidth (max), vedere [ft notify bandwidth](ft-notify-bandwidth-server-configuration-option.md)(A)|0|32767|100|  
    |ft notify bandwidth (min), vedere [ft notify bandwidth](ft-notify-bandwidth-server-configuration-option.md)(A)|0|32767|0|  
    |[index create memory](configure-the-index-create-memory-server-configuration-option.md) (A, SC)|704|2147483647|0|  
    |[risoluzione XACT in dubbio](in-doubt-xact-resolution-server-configuration-option.md) (a)|0|2|0|  
    |[lightweight pooling](lightweight-pooling-server-configuration-option.md) (A, RR)|0|1|0|  
    |[blocchi](configure-the-locks-server-configuration-option.md) (A, RR, SC)|5000|2147483647|0|  
    |[massimo grado di parallelismo](configure-the-max-degree-of-parallelism-server-configuration-option.md) (A)|0|32767|0|  
    |[intervallo massimo di ricerca per indicizzazione full-text](max-full-text-crawl-range-server-configuration-option.md) (A)|0|256|4|  
    |[memoria massima del server](server-memory-server-configuration-options.md) (A, SC)|16|2147483647|2147483647|  
    |[max text repl size](configure-the-max-text-repl-size-server-configuration-option.md)|0|2147483647|65536|  
    |[numero massimo thread di lavoro](configure-the-max-worker-threads-server-configuration-option.md) (A)|128|32767<br /><br /> (1024 è il valore massimo consigliato per i sistemi operativi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a 32 bit, 2048 per le versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a 64 bit).|0<br /><br /> Zero configura automaticamente il numero massimo di thread di lavoro in base al numero di processori, usando la formula (256 + (*\<processori>* -4) * 8) per 32 bit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e due volte per 64 bit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
    |[conservazione dei supporti](configure-the-media-retention-server-configuration-option.md) (A, RR)|0|365|0|  
    |[memoria minima per query](configure-the-min-memory-per-query-server-configuration-option.md) (A)|512|2147483647|1024|  
    |[min server memory](server-memory-server-configuration-options.md) (A, SC)|0|2147483647|0|  
    |[trigger annidati](configure-the-nested-triggers-server-configuration-option.md)|0|1|1|  
    |[dimensioni del pacchetto di rete](configure-the-network-packet-size-server-configuration-option.md) (A)|512|32767|4096|  
    |[Procedure di automazione OLE](ole-automation-procedures-server-configuration-option.md) (A)|0|1|0|  
    |[oggetti aperti](open-objects-server-configuration-option.md) (A, RR, obsoleti)|0|2147483647|0|  
    |[ottimizzazione per carichi di lavoro ad hoc](optimize-for-ad-hoc-workloads-server-configuration-option.md) (A)|0|1|0|  
    |[PH_timeout](ph-timeout-server-configuration-option.md) (A)|1|3600|60|  
    |[pre-calcolo rango](precompute-rank-server-configuration-option.md) (A)|0|1|0|  
    |[Priority Boost](configure-the-priority-boost-server-configuration-option.md) (A, RR)|0|1|0|  
    |[limite di costo Query Governor](configure-the-query-governor-cost-limit-server-configuration-option.md) (A)|0|2147483647|0|  
    |[attesa query](configure-the-query-wait-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[intervallo di recupero](configure-the-recovery-interval-server-configuration-option.md) (A, SC)|0|32767|0|  
    |[accesso remoto](configure-the-remote-access-server-configuration-option.md) (RR)|0|1|1|  
    |[remote admin connections](remote-admin-connections-server-configuration-option.md)|0|1|0|  
    |[Timeout accesso remoto](configure-the-remote-login-timeout-server-configuration-option.md)|0|2147483647|10|  
    |[Trans proc remoto](configure-the-remote-proc-trans-server-configuration-option.md)|0|1|0|  
    |[remote query timeout](configure-the-remote-query-timeout-server-configuration-option.md)|0|2147483647|600|  
    |[Opzione Replication XPS](replication-xps-server-configuration-option.md) (A)|0|1|0|  
    |[analizza le procedure di avvio](configure-the-scan-for-startup-procs-server-configuration-option.md) (A, RR)|0|1|0|  
    |[server trigger recursion](server-trigger-recursion-server-configuration-option.md)|0|1|1|  
    |[Imposta dimensioni working set](set-working-set-size-server-configuration-option.md) (A, RR, obsolete)|0|1|0|  
    |[show advanced options](show-advanced-options-server-configuration-option.md)|0|1|0|  
    |[SMO e DMO XPS](smo-and-dmo-xps-server-configuration-option.md) (A)|0|1|1|  
    |[trasforma parole non significative](transform-noise-words-server-configuration-option.md) (A)|0|1|0|  
    |cambio [anno A due cifre](configure-the-two-digit-year-cutoff-server-configuration-option.md) (A)|1753|9999|2049|  
    |[connessioni utente](configure-the-user-connections-server-configuration-option.md) (A, RR, SC)|0|32767|0|  
    |[user options](configure-the-user-options-server-configuration-option.md)|0|32767|0|  
    |[xp_cmdshell](xp-cmdshell-server-configuration-option.md) (A)|0|1|0|  
  
## <a name="see-also"></a>Vedere anche  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
