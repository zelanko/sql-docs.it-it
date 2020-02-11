---
title: Destinazione buffer circolare | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- targets [SQL Server extended events], ring buffer target
- ring buffer target [SQL Server extended events]
ms.assetid: 54494e11-b56b-43b7-aa5e-c8724e56b251
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 920cc72a9d99da61575249559661c01826b0e89b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66088962"
---
# <a name="ring-buffer-target"></a>Destinazione del buffer circolare
  La destinazione del buffer circolare mantiene brevemente in memoria i dati relativi agli eventi. Questa destinazione può gestire gli eventi in due modalità diverse.  
  
-   La prima è una modalità di tipo puramente FIFO, in base alla quale l'evento meno recente viene eliminato una volta utilizzata tutta la memoria allocata alla destinazione. In questa modalità, che rappresenta quella predefinita, il valore dell'opzione occurrence_number è impostato su 0.  
  
-   La seconda è una modalità FIFO basata sul tipo di evento, che prevede di mantenere in memoria un numero specificato di eventi di ciascun tipo. In questa modalità, gli eventi meno recenti di ogni tipo vengono eliminati quando viene utilizzata tutta la memoria allocata alla destinazione. È possibile configurare occurrence_number per specificare il numero di eventi di ciascun tipo da mantenere.  
  
 Nella tabella seguente vengono descritte le opzioni disponibili per la configurazione della destinazione del buffer circolare.  
  
|Opzione|Valori consentiti|Descrizione|  
|------------|--------------------|-----------------|  
|max_memory|Qualsiasi intero a 32 bit. Questo valore è facoltativo.|Quantità massima di memoria che può essere utilizzata in kilobyte (KB). Gli eventi esistenti vengono eliminati sulla base del limite che viene raggiunto per primo: max_event_limit o max_memory. Il valore massimo è 4194303 KB. Prima di impostare le dimensioni del buffer circolare su limiti nell'intervallo di GB, è necessario prendere in considerazione una particolare attenzione, in quanto può influito su altri consumer di memoria in SQL Server|  
|max_event_limit|Qualsiasi intero a 32 bit. Questo valore è facoltativo.|Il numero massimo di eventi tenuto in ring_buffer. Gli eventi esistenti vengono eliminati sulla base del limite che viene raggiunto per primo: max_event_limit o max_memory. Valore predefinito = 1000.|  
|occurrence_number|Uno dei valori seguenti:<br /><br /> 0 (valore predefinito) = l'evento meno recente viene eliminato una volta utilizzata tutta la memoria allocata alla destinazione.<br /><br /> Qualsiasi Integer a 32 bit = il numero di eventi di ogni tipo da contenere prima di essere scartati per ogni singolo evento.<br /><br /> <br /><br /> Questo valore è facoltativo.|Modalità FIFO da utilizzare e, se il valore impostato è maggiore di 0, numero desiderato di eventi di ciascun tipo da mantenere nel buffer.|
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="adding-the-target-to-a-session"></a>Aggiunta della destinazione a una sessione  
 Per aggiungere la destinazione del buffer circolare a una sessione di eventi estesi, è necessario includere l'istruzione seguente quando si crea o modifica una sessione eventi:  
  
```sql
ADD TARGET package0.ring_buffer  
```  
  
## <a name="reviewing-the-target-output"></a>Analisi dell'output di destinazione  
 Per esaminare l'output dalla destinazione del buffer circolare, è possibile usare la query seguente, sostituendo *nome_sessione* con il nome della sessione eventi.  
  
```sql
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 Nell'esempio seguente viene illustrato il formato di output della destinazione del buffer circolare.  
  
```  
<RingBufferTarget eventsPerSec="" processingTime="" totalEventsProcessed="" eventCount="" droppedCount="" memoryUsed="">  
 <event name="" package="" id="" version="" timestamp="">  
    <data name="">  
      <type name="" package="" />  
      <value></value>  
      <text></text>  
    </data>  
    <action name="" package="">  
      <type name="" package="" />  
      <value></value>  
      <text></text>  
    </action>  
  </event>  
</RingBufferTarget>  
```


## <a name="see-also"></a>Vedere anche

- [Destinazioni degli eventi estesi di SQL Server](../../2014/database-engine/sql-server-extended-events-targets.md)
- [sys.dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql?view=sql-server-2016)
- [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql?view=sql-server-2016)
- [ALTER EVENT SESSION &#40;Transact-SQL&#41;](https://docs.microsoft.com/sql/t-sql/statements/alter-event-session-transact-sql?view=sql-server-2016)

