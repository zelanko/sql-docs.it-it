---
title: Destinazione di abbinamento degli eventi | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- pairing target [SQL Server extended events]
- event pairing target
- targets [SQL Server extended events], pairing target
ms.assetid: 3c87dcfb-543a-4bd8-a73d-1390bdf4ffa3
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 39e444077c3dbe27ae243e4292b7a047e21de2b9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66064853"
---
# <a name="event-pairing-target"></a>Destinazione di abbinamento degli eventi
  La destinazione di abbinamento degli eventi stabilisce la corrispondenza di due eventi utilizzando una o più colonne di dati presenti in ciascun evento. Molti eventi entrano nelle coppie, ad esempio, le acquisizioni e i rilasci del blocco. Dopo che una sequenza dell'evento viene abbinata, entrambi gli eventi sono ignorati. Il fatto di ignorare i set corrispondenti consente un facile rilevamento di acquisizioni del blocco che non sono state rilasciate.  
  
 Utilizzando filtri a livello di evento, la destinazione di abbinamento può essere utilizzata solo per acquisire eventi che non corrispondono a criteri preimpostati.  
  
 Quando si utilizza la destinazione di abbinamento degli eventi, è possibile scegliere due eventi di cui verrà stabilita la corrispondenza, insieme a una sequenza di colonne su cui eseguire la corrispondenza. Tutte le colonne nella sequenza devono essere dello stesso tipo.  
  
 Nella tabella seguente vengono descritte le opzioni disponibili per configurare l'abbinamento degli eventi.  
  
|Opzione|Valori consentiti|Descrizione|  
|------------|--------------------|-----------------|  
|begin_event|Qualsiasi nome di evento presente nella sessione corrente.|Nome di evento che specifica l'evento di inizio in una sequenza abbinata.|  
|end_event|Qualsiasi nome di evento presente nella sessione corrente.|Nome di evento che specifica l'evento di fine in una sequenza abbinata.|  
|begin_matching_columns|Elenco ordinato di nomi di colonne separati da virgole.|Colonne su cui eseguire la corrispondenza.|  
|end_matching_columns|Elenco ordinato di nomi di colonne separati da virgole.|Colonne su cui eseguire la corrispondenza.|  
|begin_matching_actions|Elenco ordinato di azioni separate da virgole.|Azioni su cui eseguire la corrispondenza.|  
|end_matching_actions|Elenco ordinato di azioni separate da virgole.|Azioni su cui eseguire la corrispondenza.|  
|respond_to_memory_pressure|Uno dei valori seguenti:<br /><br /> 0 = non rispondere.<br /><br /> 1 = arrestare l'aggiunta di nuovi orfani all'elenco quando sono presenti richieste di memoria.|Risposta della destinazione agli eventi della memoria. Se il valore è impostato su 1 e la memoria del server è insufficiente, le informazioni non abbinate mantenute vengono rimosse.|  
|max_orphans||Specifica il numero totale di eventi non abbinati che saranno raccolti nella destinazione. Una volta raggiunto il limite, gli eventi non abbinati vengono rimossi secondo la modalità FIFO. Valore predefinito = 10,000.|  
  
 Tutti i dati associati a un evento sono acquisiti e archiviati per un abbinamento futuro. Vengono raccolti anche i dati aggiunti dalle azioni. I dati degli eventi raccolti vengono archiviati in memoria e, come tali, hanno un limite finito. Questo limite è basato sulla capacità e sull'attività del sistema. Anziché utilizzare il valore massimo di memoria come parametro, la quantità di memoria utilizzata sarà basata sulle risorse di sistema disponibili. Quando queste non sono disponibili, gli eventi non abbinati che sono stati mantenuti saranno eliminati. Se un evento non è stato abbinato ed è stato eliminato, l'evento corrispondente comparirà come un evento non abbinato.  
  
 La destinazione abbinamento serializza gli eventi non abbinati a un formato XML. Questo formato non è conforme ad alcuno schema. Il formato contiene solo due tipi di elementi. L' ** \<elemento>non abbinato** è la radice, seguita da uno. evento>elemento per ogni evento non abbinato attualmente rilevato. ** \<** L' ** \<elemento>dell'evento** contiene un attributo che contiene il nome dell'evento non abbinato.  
  
## <a name="adding-the-target-to-a-session"></a>Aggiunta della destinazione a una sessione  
 Per aggiungere la destinazione di corrispondenza delle coppie a una sessione di eventi estesi, è necessario includere l'istruzione seguente quando si crea o modifica una sessione eventi:  
  
```  
ADD TARGET package0.pair_matching   
```  
  
 Far seguire all'istruzione un'istruzione SET per definire gli eventi di inizio e di fine e le azioni o le colonne di cui eseguire la corrispondenza. L'esempio seguente mostra la sintassi di esempio per la corrispondenza della coppia di eventi sqlserver.lock_acquired e sqlserver.lock_released.  
  
```  
   ( SET begin_event = 'sqlserver.lock_acquired',  
      begin_matching_columns = 'database_id, resource_0, resource_1, resource_2, transaction_id, mode',  
      end_event = 'sqlserver.lock_released',  
      end_matching_columns = 'database_id, resource_0, resource_1, resource_2, transaction_id, mode',  
   respond_to_memory_pressure = 1)  
```  
  
 Per altre informazioni, vedere [Individuare le query che mantengono attivi i blocchi](../relational-databases/extended-events/determine-which-queries-are-holding-locks.md).  
  
## <a name="reviewing-the-target-output"></a>Analisi dell'output di destinazione  
 Per esaminare l'output per la destinazione di corrispondenza delle coppie, è possibile usare la query seguente sostituendo *session_name* con il nome della sessione eventi.  
  
```  
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 Nell'esempio seguente viene illustrato il formato di output della destinazione di abbinamento.  
  
```  
<unpaired truncated = "0" matchedCount = "[matched count]" memoryPressureDroppedCount = " [lost count]">  
    <event name  = "[event name]" package = "[package]" id= "[event ID value]" version = "[event version]">  
    <data name = "[column name]">   
    <type name = "[column type]" package = "[type package]" />   
    <value>[column value]</value>  
    <text value>[text value]</text>>  
        </data>  
    </event>  
</unpaired>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Destinazioni degli eventi estesi di SQL Server](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys.dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
