---
title: Filtrare una traccia | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], events
- events [SQL Server], filters
- filters [SQL Server]
- filters [SQL Server], traces
- traces [SQL Server], filters
ms.assetid: 019c10ab-68f6-4e40-a5e8-735b2e1270db
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 20cebbb314e2830272e677da2d26bf53668798ab
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67579834"
---
# <a name="filter-a-trace"></a>Filtrare una traccia
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  I filtri consentono di limitare gli eventi raccolti in una traccia. Se non si imposta un filtro, tutti gli eventi delle classi di evento selezionate vengono restituiti nell'output di traccia. Ad esempio, se si limitano i nomi utente di Windows in una traccia, consentendo solo utenti specifici, i dati dell'output saranno ridotti solo a tali utenti.  
  
 L'impostazione di un filtro per una traccia non è obbligatoria. Un filtro consente, tuttavia, di ridurre l'overhead che si verifica durante una traccia, restituendo dati specifici e quindi semplificando l'analisi delle prestazioni e i controlli.  
  
 Per filtrare i dati di evento acquisiti in una traccia, selezionare i criteri per gli eventi di traccia che restituiscono solo i dati rilevanti disponibili nella traccia. Ad esempio, è possibile includere o escludere il monitoraggio dell'attività di un'applicazione specifica dalla traccia.  
  
> [!NOTE]  
>  Durante la creazione di tracce da parte di [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] , per impostazione predefinita le attività specifiche del programma stesso vengono escluse tramite filtro.  
  
 Come ulteriore esempio, se si esegue il monitoraggio delle query per determinare quali batch richiedono i tempi di esecuzione più lunghi, impostare i criteri per gli eventi di traccia in modo da monitorare solo i batch la cui esecuzione richiede più di 30 secondi (un valore minimo della CPU di 30.000 millisecondi).  
  
## <a name="filter-creation-guidelines"></a>Linee guida per la creazione di filtri  
 In generale, per filtrare una traccia, eseguire la procedura seguente.  
  
1.  Identificare gli eventi da includere nella traccia.  
  
2.  Identificare i dati e le colonne di dati contenenti le informazioni necessarie.  
  
3.  Identificare un subset dei dati necessari e definire filtri in base a tale subset di dati.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 Ad esempio, è possibile che si desideri filtrare solo gli eventi con durata superiore a un determinato intervallo. In tal caso, è possibile creare una traccia che include gli eventi per i quali il valore nella colonna **Duration** è maggiore di 300 millisecondi. Nella traccia non saranno inclusi gli eventi con durata inferiore a 300 millisecondi.  
  
 È possibile creare filtri tramite SQL Server Profiler o le stored procedure Transact-SQL.  
  
 **Per filtrare gli eventi di un modello di traccia**  
  
 [Filtrare eventi in una traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)  
  
 [Impostare un filtro di traccia &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md)  
  
 **Per modificare i filtri**  
  
 [Modificare un filtro &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)  
  
 La disponibilità dei filtri dipende dalla colonna di dati. Non è possibile filtrare alcune colonne di dati. Le colonne di dati che possono essere filtrate consentono solo determinati operatori relazionali, come illustrato nella tabella seguente.  
  
|Operatore relazionale|Simbolo operatore|Descrizione|  
|-------------------------|---------------------|-----------------|  
|Simile a|Simile a|Consente di specificare che i dati dell'evento di traccia devono essere simili al testo specificato. Supporta più valori.|  
|Non simile a|Non simile a|Specifica che i dati dell'evento di traccia devono essere diversi dal testo specificato. Supporta più valori.|  
|Uguale a|=|Specifica che i dati dell'evento di traccia devono essere uguali al valore specificato. Supporta più valori.|  
|Diverso da|<>|Specifica che i dati dell'evento di traccia devono essere diversi dal valore specificato. Supporta più valori.|  
|Maggiore di|>|Specifica che i dati dell'evento di traccia devono essere maggiori del valore specificato.|  
|Maggiore o uguale a|>=|Specifica che i dati dell'evento di traccia devono essere maggiori o uguali al valore specificato.|  
|Minore di|<|Specifica che i dati dell'evento di traccia devono essere minori del valore specificato.|  
|Minore o uguale a|<=|Specifica che i dati dell'evento di traccia devono essere minori o uguali al valore specificato.|  
  
 Nella tabella seguente sono elencate le colonne di dati a cui è possibile applicare un filtro e gli operatori relazionali disponibili.  
  
|Colonne di dati|Operatori relazionali|  
|------------------|--------------------------|  
|**ApplicationName**|LIKE, NOT LIKE|  
|**BigintData1**|=, <>, >=, <=|  
|**BigintData2**|=, <>, >=, <=|  
|**BinaryData**|Utilizzare [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] per filtrare gli eventi in questa colonna di dati. Per altre informazioni, vedere [Filtrare le tracce tramite SQL Server Profiler](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md).|  
|**ClientProcessID**|=, <>, >=, <=|  
|**ColumnPermissions**|=, <>, >=, <=|  
|**CPU**|=, <>, >=, <=|  
|**DatabaseID**|=, <>, >=, <=|  
|**DatabaseName**|LIKE, NOT LIKE|  
|**DBUserName**|LIKE, NOT LIKE|  
|**Durata**|=, <>, >=, \<=|  
|**EndTime**|>=, <=|  
|**Errore**|=, <>, >=, <=|  
|**EventSubClass**|=, <>, >=, <=|  
|**FileName**|LIKE, NOT LIKE|  
|**GUID**|Utilizzare [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] per filtrare gli eventi in questa colonna di dati. Per altre informazioni, vedere [Filtrare le tracce tramite SQL Server Profiler](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md).|  
|**Handle**|=, <>, >=, <=|  
|**HostName**|LIKE, NOT LIKE|  
|**IndexID**|=, <>, >=, <=|  
|**IntegerData**|=, <>, >=, <=|  
|**IntegerData2**|=, <>, >=, <=|  
|**IsSystem**|=, <>, >=, <=|  
|**LineNumber**|=, <>, >=, <=|  
|**LinkedServerName**|LIKE, NOT LIKE|  
|**LoginName**|LIKE, NOT LIKE|  
|**LoginSid**|Utilizzare [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] per filtrare gli eventi in questa colonna di dati. Per altre informazioni, vedere [Filtrare le tracce tramite SQL Server Profiler](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md).|  
|**MethodName**|LIKE, NOT LIKE|  
|**Mode**|=, <>, >=, <=|  
|**NestLevel**|=, <>, >=, <=|  
|**NTDomainName**|LIKE, NOT LIKE|  
|**NTUserName**|LIKE, NOT LIKE|  
|**ObjectID**|=, <>, >=, <=|  
|**ObjectID2**|=, <>, >=, <=|  
|**ObjectName**|LIKE, NOT LIKE|  
|**ObjectType**|=, <>, >=, <=|  
|**Offset**|=, <>, >=, <=|  
|**OwnerID**|=, <>, >=, <=|  
|**OwnerName**|LIKE, NOT LIKE|  
|**ParentName**|LIKE, NOT LIKE|  
|**Autorizzazioni**|=, <>, >=, <=|  
|**ProviderName**|LIKE, NOT LIKE|  
|**Reads**|=, <>, >=, <=|  
|**RequestID**|=, <>, >=, <=|  
|**RoleName**|LIKE, NOT LIKE|  
|**RowCounts**|=, <>, >=, <=|  
|**SessionLoginName**|LIKE, NOT LIKE|  
|**Severity**|=, <>, >=, <=|  
|**SourceDatabaseID**|=, <>, >=, <=|  
|**SPID**|=, <>, >=, \<=|  
|**SqlHandle**|Utilizzare [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] per filtrare gli eventi in questa colonna di dati. Per altre informazioni, vedere [Filtrare le tracce tramite SQL Server Profiler](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md).|  
|**StartTime**|>=, <=|  
|**State**|=, <>, >=, <=|  
|**Esito positivo**|=, <>, >=, <=|  
|**TargetLoginName**|LIKE, NOT LIKE|  
|**TargetLoginSid**|Utilizzare [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] per filtrare gli eventi in questa colonna di dati. Per altre informazioni, vedere [Filtrare le tracce tramite SQL Server Profiler](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md).|  
|**TargetUserName**|LIKE, NOT LIKE|  
|**TextData** *|LIKE, NOT LIKE|  
|**TransactionID**|=, <>, >=, <=|  
|**Tipo**|=, <>, >=, <=|  
|**Writes**|=, <>, >=, <=|  
|**XactSequence**|=, <>, >=, <=|  
  
 \* Se si tracciano eventi dall'utilità **osql** o dall'utilità **sqlcmd** , aggiungere sempre **%** ai filtri nella colonna di dati **TextData** .  
  
 A titolo di sicurezza, Traccia SQL omette automaticamente dalla traccia le informazioni sulle stored procedure correlate alla sicurezza che coinvolgono le password. Tale meccanismo di sicurezza non è configurabile ed è sempre attivo. In tale modo viene impedito che le password possano essere acquisite dagli utenti, i quali sono autorizzati a tenere traccia di tutte le attività in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Le stored procedure seguenti correlate alla sicurezza vengono monitorate, ma nella colonna di dati **TextData** non viene scritto alcun output:  
  
 [sp_addapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addapprole-transact-sql.md)  
  
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)  
  
 [sp_adddistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)  
  
 [sp_adddistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)  
  
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)  
  
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)  
  
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)  
  
 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)  
  
 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)  
  
 [sp_addremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)  
  
 [sp_addsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)  
  
 [sp_approlepassword &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-approlepassword-transact-sql.md)  
  
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)  
  
 [sp_changesubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)  
  
 [sp_dsninfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dsninfo-transact-sql.md)  
  
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
 [sp_link_publication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)  
  
 [sp_password &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md)  
  
 [sp_setapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)  
  
  
