---
title: sys.dm_clr_appdomains (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_clr_appdomains
- sys.dm_clr_appdomains
- dm_clr_appdomains_TSQL
- sys.dm_clr_appdomains_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_appdomains dynamic management dynamic management view
ms.assetid: 9fe0d4fd-950a-4274-a493-85e776278045
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3ebcda61d95cc5131048ab32701d9d68228646ea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138407"
---
# <a name="sysdmclrappdomains-transact-sql"></a>sys.dm_clr_appdomains (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni dominio dell'applicazione nel server. Dominio dell'applicazione (**AppDomain**) è un costrutto nella [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] common language runtime (CLR) che è l'unità di isolamento per un'applicazione. È possibile utilizzare questa vista per comprendere e risolvere i problemi di oggetti di integrazione CLR che sono in esecuzione nello [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Esistono diversi tipi di oggetti di database gestito dell'integrazione con CLR. Per informazioni generali su questi oggetti, vedere [compilazione di oggetti di Database con Common Language Runtime (CLR) Integration](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md). Ogni volta che questi oggetti vengono eseguiti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea un' **AppDomain** in cui viene caricato ed eseguito il codice richiesto. Il livello di isolamento per un **AppDomain** uno **AppDomain** per ogni database per proprietario. Vale a dire tutti gli oggetti CLR appartenenti a un utente vengono sempre eseguiti nella stessa **AppDomain** per ogni database (se un utente registra oggetti di database CLR in database diversi, il database CLR gli oggetti verranno eseguiti in domini applicazione diversi). Un' **AppDomain** non viene eliminato al termine dell'esecuzione del codice. ma viene memorizzato nella cache per le future esecuzioni. Ciò migliora le prestazioni.  
  
 Per altre informazioni, vedere [domini applicazione](https://go.microsoft.com/fwlink/p/?LinkId=299658).  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**appdomain_address**|**varbinary(8)**|Indirizzo della **AppDomain**. Database gestiti tutti gli oggetti appartenenti a un utente vengono sempre caricati nello stesso **AppDomain**. È possibile usare questa colonna per cercare tutti gli assembly attualmente caricati in questo **AppDomain** nelle **DM clr_loaded_assemblies**.|  
|**appdomain_id**|**int**|ID del **AppDomain**. Ciascuna **AppDomain** ha un ID univoco.|  
|**appdomain_name**|**varchar(386)**|Nome del **AppDomain** come da assegnazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**creation_time**|**datetime**|Ora in cui il **AppDomain** è stato creato. In quanto **AppDomain** vengono memorizzati nella cache e riutilizzati per migliorare le prestazioni, **creation_time** non è necessariamente il tempo di cui è stato eseguito il codice.|  
|**db_id**|**int**|ID del database in cui questo **AppDomain** è stato creato. Codice archiviato in due database diversi non può condividere uno **AppDomain**.|  
|**user_id**|**int**|ID dell'utente il cui oggetti possono essere eseguiti in questo **AppDomain**.|  
|**state**|**nvarchar(128)**|Un descrittore per lo stato corrente del **AppDomain**. Un AppDomain può trovarsi in stati diversi dalla creazione all'eliminazione. Per ulteriori informazioni, vedere la sezione Osservazioni di questo argomento.|  
|**strong_refcount**|**int**|Numero di riferimenti forti al **AppDomain**. Questo riflette il numero di batch in esecuzione che usano questo **AppDomain**. Si noti che l'esecuzione di questa visualizzazione consente di creare un **strong refcount**; anche se nessun codice in esecuzione **strong_refcount** avrà un valore pari a 1.|  
|**weak_refcount**|**int**|Numero di riferimenti deboli al **AppDomain**. Indica il numero di oggetti all'interno di **AppDomain** vengono memorizzati nella cache. Quando si esegue un oggetto di database gestito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] memorizza nella cache all'interno di **AppDomain** per un riutilizzo futuro. Ciò migliora le prestazioni.|  
|**cost**|**int**|Costo dei **AppDomain**. Maggiore è il costo, più è probabile che ciò **AppDomain** debba essere scaricato eccessivo della memoria. Costo dipende in genere la quantità di memoria è necessario creare di nuovo questa **AppDomain**.|  
|**Valore**|**int**|Valore della **AppDomain**. Minore è il valore, più è probabile che ciò **AppDomain** debba essere scaricato eccessivo della memoria. Valore dipende in genere che utilizzano il numero di connessioni o batch **AppDomain**.|  
|**total_processor_time_ms**|**bigint**|Tempo totale del processore, in millisecondi, utilizzato da tutti i thread durante l'esecuzione nel dominio dell'applicazione corrente dall'avvio del processo. Ciò equivale a **System.AppDomain.MonitoringTotalProcessorTime**.|  
|**total_allocated_memory_kb**|**bigint**|Dimensioni totali, in kilobyte, di tutte le allocazioni di memoria eseguite dal dominio dell'applicazione dalla sua creazione, senza sottrarre la memoria raccolta. Ciò equivale a **System.AppDomain.MonitoringTotalAllocatedMemorySize**.|  
|**survived_memory_kb**|**bigint**|Numero di kilobyte rimanenti dall'ultima raccolta di blocco completa e a cui fa riferimento il dominio dell'applicazione corrente. Ciò equivale a **System.AppDomain.MonitoringSurvivedMemorySize**.|  
  
## <a name="remarks"></a>Note  
 È presente una relazione uno-a-molti tra **dm_clr_appdomains** e **dm_clr_loaded_assemblies**.  
  
 Nelle tabelle seguenti sono elencati i possibili **lo stato** i valori, le relative descrizioni, e quando si verificano nel **AppDomain** ciclo di vita. È possibile usare queste informazioni per seguire il ciclo di vita di un' **AppDomain** nonché per monitorare sospette o ripetitive **AppDomain** senza la necessità di analizzare il registro eventi di Windows lo scaricamento di istanze.  
  
## <a name="appdomain-initialization"></a>Inizializzazione di AppDomain  
  
|Stato|Descrizione|  
|-----------|-----------------|  
|E_APPDOMAIN_CREATING|Il **AppDomain** viene creato.|  
  
## <a name="appdomain-usage"></a>Utilizzo di AppDomain  
  
|Stato|Descrizione|  
|-----------|-----------------|  
|E_APPDOMAIN_SHARED|Il runtime **AppDomain** può essere usata da più utenti.|  
|E_APPDOMAIN_SINGLEUSER|Il **AppDomain** è pronto per l'utilizzo nelle operazioni DDL. Queste ultime differiscono da E_APPDOMAIN_SHARED per il fatto che gli AppDomain condivisi vengono utilizzati per le esecuzioni di integrazione di CLR e non per operazioni DDL. Tali AppDomain sono isolati da altre operazioni simultanee.|  
|E_APPDOMAIN_DOOMED|Il **AppDomain** è pianificato per essere scaricato, ma sono attualmente presenti thread in esecuzione in esso.|  
  
## <a name="appdomain-cleanup"></a>Eliminazione di AppDomain  
  
|Stato|Descrizione|  
|-----------|-----------------|  
|E_APPDOMAIN_UNLOADING|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha richiesto che CLR scarichi il **AppDomain**, solitamente perché l'assembly che contiene gli oggetti di database gestito è stato modificato o eliminato.|  
|E_APPDOMAIN_UNLOADED|Il CLR ha scaricato i **AppDomain**. Si tratta in genere il risultato di una procedura di escalation a causa dell'errore **ThreadAbort**, **OutOfMemory**, o un'eccezione non gestita nel codice utente.|  
|E_APPDOMAIN_ENQUEUE_DESTROY|Il **AppDomain** è stato scaricato in CLR e impostato per l'eliminazione da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|E_APPDOMAIN_DESTROY|Il **AppDomain** è in corso di eliminazione da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|E_APPDOMAIN_ZOMBIE|Il **AppDomain** è stata eliminata dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; tuttavia, non tutti i riferimenti per il **AppDomain** sono stati puliti.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW SERVER STATE nel database.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato come visualizzare i dettagli di un' **AppDomain** per un determinato assembly:  
  
```  
select appdomain_id, creation_time, db_id, user_id, state  
from sys.dm_clr_appdomains a  
where appdomain_address =   
(select appdomain_address   
 from sys.dm_clr_loaded_assemblies  
   where assembly_id = 500);  
```  
  
 Nell'esempio seguente viene illustrato come visualizzare tutti gli assembly in un determinato **AppDomain**:  
  
```  
select a.name, a.assembly_id, a.permission_set_desc, a.is_visible, a.create_date, l.load_time   
from sys.dm_clr_loaded_assemblies as l   
inner join sys.assemblies as a  
on l.assembly_id = a.assembly_id  
where l.appdomain_address =   
(select appdomain_address   
from sys.dm_clr_appdomains  
where appdomain_id = 15);  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sys.dm_clr_loaded_assemblies &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)   
 [Viste a gestione dinamica relative a Common Language Runtime &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
