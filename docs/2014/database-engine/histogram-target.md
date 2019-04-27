---
title: Destinazione dell'istogramma | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- bucketing target [SQL Server extended events]
- event bucketing target
- targets [SQL Server extended events], bucketing
ms.assetid: 2ea39141-7eb0-4c74-abf8-114c2c106a19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8672fc9932dd18f73424f83a81299421186aec9c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62778889"
---
# <a name="histogram-target"></a>Destinazione dell'istogramma
  La destinazione dell'istogramma raggruppa le occorrenze di un tipo di evento specifico in base ai dati relativi all'evento. I raggruppamenti di eventi sono conteggiati in base a una colonna di evento oppure a un'azione specificata. È possibile utilizzare la destinazione dell'istogramma dell'evento per risolvere i problemi relativi alle prestazioni. Grazie all'identificazione degli eventi che si verificano più di frequente, è infatti possibile individuare elementi specifici che indicano la causa potenziale di un problema relativo alle prestazioni.  
  
 Nella tabella seguente vengono descritte le opzioni che consentono di configurare la destinazione dell'istogramma.  
  
|Opzione|Valori consentiti|Descrizione|  
|------------|--------------------|-----------------|  
|slot|Qualsiasi valore intero. Questo valore è facoltativo.|Valore specificato dall'utente che indica il numero massimo di raggruppamenti da mantenere. Quando questo valore viene raggiunto, i nuovi eventi che non appartengono ai gruppi esistenti vengono ignorati.<br /><br /> Si noti che per migliorare le prestazioni, il numero di slot viene arrotondato alla potenza di 2 più vicina.|  
|filtering_event_name|Qualsiasi evento presente nella sessione degli eventi estesi. Questo valore è facoltativo.|Valore specificato dall'utente utilizzato per identificare una classe di eventi. Nel bucket vengono inserite solo le istanze dell'evento specificato. Tutti gli altri eventi vengono ignorati.<br /><br /> Se si specifica questo valore, è necessario usare il formato *nome_pacchetto*.*nome_evento*, ad esempio `'sqlserver.checkpoint_end'`. Per identificare il nome del pacchetto, è possibile utilizzare la query seguente:<br /><br /> SELECT p.name, se.event_name<br />DA sys.dm_xe_session_events se<br />JOIN xe_packages p<br />ON se_event_package_guid = p.guid<br />ORDER BY p.name, se.event_name<br /><br /> <br /><br /> Se non si specifica il valore filtering_event_name, l'opzione source_type deve essere impostata su 1 (impostazione predefinita).|  
|source_type|Tipo di oggetto su cui è basato il bucket. Si tratta di un valore facoltativo che, se non è specificato, assumerà il valore predefinito 1.|I valori consentiti sono i seguenti:<br /><br /> 0 per un evento<br /><br /> 1 per un'azione|  
|origine|Colonna di evento o nome dell'azione.|Colonna di evento o nome dell'azione utilizzato come origine dati.<br /><br /> Quando si specifica una colonna di evento per origine, è necessario specificare una colonna dall'evento utilizzato per il valore filtering_event_name. Per identificare le possibili colonne, utilizzare la query seguente:<br /><br /> SELECT name FROM sys.dm_xe_object_columns<br />WHERE object_name = '\<NomeEvento >'<br />AND column_type != 'readonly'<br /><br /> Quando si specifica una colonna di evento per origine, non è necessario includere il nome del pacchetto nel valore dell'origine.<br /><br /> Quando si specifica un nome di azione per origine, è necessario utilizzare una delle azioni configurate per la raccolta nella sessione eventi per cui viene utilizzata la destinazione specifica. Per individuare valori potenziali per il nome di azione, è possibile eseguire una query sulla colonna action_name della vista sys.dm_xe_sesssion_event_actions.<br /><br /> Se si usa un nome di azione come origine dati, è necessario specificare il valore dell'origine nel formato *nome_pacchetto*.*nome_azione*.|  
  
 Nell'esempio seguente viene illustrato, a un livello elevato, il modo in cui i dati vengono raccolti nella destinazione dell'istogramma. Nell'esempio la destinazione dell'istogramma viene utilizzata per contare il numero di volte in cui si verifica ogni tipo di attesa. A tale scopo, è necessario specificare le opzioni seguenti quando si definisce la destinazione dell'istogramma:  
  
-   filtering_event_name = 'wait_info'  
  
-   source = 'wait_type'  
  
-   source_type = 0 (poiché wait_type è una colonna di evento)  
  
 Nello scenario di esempio per l'origine wait_type vengono registrati i dati seguenti:  
  
|Nome evento di filtro|Valore colonna di origine|  
|--------------------------|-------------------------|  
|wait_info|file_io|  
|wait_info|file_io|  
|wait_info|di rete|  
|wait_info|di rete|  
|wait_info|sospensione|  
  
 I valori relativi al tipo di attesa verranno suddivisi in tre slot, cui sono associati i valori e i conteggi di slot seguenti:  
  
|Value|Conteggio di slot|  
|-----------|----------------|  
|file_io|2|  
|di rete|2|  
|sospensione|1|  
  
 Nella destinazione dell'istogramma vengono mantenuti solo i dati degli eventi per l'origine specificata. Nel caso in cui le dimensioni dei dati degli eventi siano troppo elevate per mantenere completamente i dati, questi ultimi vengono troncati. Quando i dati degli eventi sono troncati, il numero di byte è registrato e visualizzato come output XML.  
  
## <a name="adding-the-target-to-a-session"></a>Aggiunta della destinazione a una sessione  
 Per aggiungere la destinazione dell'istogramma a una sessione di eventi estesi, è necessario includere una delle istruzioni seguenti quando si crea o modifica una sessione eventi, a seconda del tipo di destinazione desiderato:  
  
```  
ADD TARGET package0.histogram  
```  
  
 È possibile utilizzare l'istruzione SET per impostare le varie opzioni. Nell'esempio seguente viene illustrata l'aggiunta della destinazione dell'istogramma, in cui vengono raccolti dati per l'evento sqlserver.checkpoint_end.  
  
```  
ADD TARGET package0.histogram  
(SET slots = 32, filtering_event_name = 'sqlserver.checkpoint_end', source_type = 0, source = 'database_id')  
```  
  
 Per altre informazioni, vedere [Cercare gli oggetti con il maggior numero di blocchi acquisiti](../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)e [Monitorare l'attività del sistema mediante gli eventi estesi](../relational-databases/extended-events/monitor-system-activity-using-extended-events.md).  
  
## <a name="reviewing-the-target-output"></a>Analisi dell'output di destinazione  
 La destinazione dell'istogramma serializza i dati in un programma o una procedura chiamante in formato XML. L'output della destinazione non è conforme ad alcuno schema.  
  
 Per esaminare l'output dalla destinazione istogramma, è possibile usare la query seguente, sostituendo *nome_sessione* con il nome della sessione eventi.  
  
```  
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 Nell'esempio seguente viene illustrato il formato di output della destinazione dell'istogramma.  
  
```  
<Slots truncated = "0" buckets=[count]>  
    <Slot count=[count] trunc=[truncated bytes]>  
        <value>  
        </value>  
    </Slot>  
</Slots>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Destinazioni degli eventi estesi di SQL Server](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys.dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
