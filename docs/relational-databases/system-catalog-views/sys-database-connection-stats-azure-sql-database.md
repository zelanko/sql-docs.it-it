---
title: Sys. database_connection_stats (Database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_connection_stats
- database_connection_stats
- database_connection_stats_TSQL
- sys.database_connection_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_connection_stats
- database_connection_stats
ms.assetid: 5c8cece0-63b0-4dee-8db7-6b43d94027ec
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 86e8c5af0a2b992a1167e23497a419e0f90abe56
ms.sourcegitcommit: 97340deee7e17288b5eec2fa275b01128f28e1b8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/30/2019
ms.locfileid: "55421108"
---
# <a name="sysdatabaseconnectionstats-azure-sql-database"></a>sys.database_connection_stats (Database di SQL Azure)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Contiene le statistiche relative [!INCLUDE[ssSDS](../../includes/sssds-md.md)] database **connettività** eventi, che fornisce una panoramica delle connessioni al database riuscite e gli errori. Per altre informazioni sugli eventi di connettività, vedere tipi di eventi in [Sys. event_log &#40;Database SQL di Azure&#41;](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md).  
  
|Statistiche|Tipo|Descrizione|  
|---------------|----------|-----------------|  
|**database_name**|**sysname**|Nome del database.|  
|**start_time**|**datetime2**|Data e ora UTC dell'inizio dell'intervallo di aggregazione. L'ora è sempre un multiplo di 5 minuti. Ad esempio:<br /><br /> 28/09/2011 16:00:00<br />'2011-09-28 16:05:00'<br />'2011-09-28 16:10:00'|  
|**end_time**|**datetime2**|Data e ora UTC della fine dell'intervallo di aggregazione. **End_time** è sempre esattamente 5 minuti dopo rispetto al relativo **start_time** nella stessa riga.|  
|**success_count**|**int**|Numero di connessioni riuscite.|  
|**total_failure_count**|**int**|Numero totale di connessioni non riuscite. Questa è la somma dei **connection_failure_count**, **terminated_connection_count**, e **throttled_connection_count**e non include gli eventi deadlock.|  
|**connection_failure_count**|**int**|Numero di errori di accesso.|  
|**terminated_connection_count**|**int**|**_Applicabile solo per [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] v11._**<br /><br /> Numero di connessioni chiuse.|  
|**throttled_connection_count**|**int**|**_Applicabile solo per [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] v11._**<br /><br /> Numero di connessioni limitate.|  
  
## <a name="remarks"></a>Note  
  
### <a name="event-aggregation"></a>Aggregazione evento

 Le informazioni sull'evento per questa vista vengono raccolte e aggregate in intervalli di 5 minuti. Le colonne del conteggio rappresentano il numero di volte in cui si è verificato un determinato evento di connettività per un database specifico in un intervallo di tempo specificato.  
  
 Ad esempio, se un utente non è in grado di connettersi al database Database1 per sette volte tra le 11:00 e le 11:05 in 2/5/2012 (UTC), queste informazioni sono disponibili in una singola riga in questa vista:  
  
|**database_name**|**start_time**|**end_time**|**success_count**|**total_failure_count**|**connection_failure_count**|**terminated_connection_count**|**throttled_connection_count**|  
|------------------------|---------------------|-------------------|------------------------|-------------------------------|------------------------------------|---------------------------------------|--------------------------------------|  
|`Database1`|`2012-02-05 11:00:00`|`2012-02-05 11:05:00`|`0`|`7`|`7`|`0`|`0`|  
  
### <a name="interval-starttime-and-endtime"></a>start_time e end_time dell'intervallo

 Un evento è incluso in un intervallo di aggregazione quando si verifica l'evento *sul* oppure _dopo_**start_time** e _prima_  **end_time** per tale intervallo. Ad esempio, un evento che si verifica esattamente il `2012-10-30 19:25:00.0000000` è incluso solo nel secondo intervallo indicato di seguito:  
  
```  
  
start_time                    end_time  
2012-10-30 19:20:00.0000000   2012-10-30 19:25:00.0000000  
2012-10-30 19:25:00.0000000   2012-10-30 19:30:00.0000000  
```  
  
### <a name="data-updates"></a>Aggiornamenti dei dati

 I dati in questa vista vengono accumulati nel tempo. In genere, vengono accumulati entro un'ora dall'inizio dell'intervallo di aggregazione, ma la visualizzazione di tutti i dati nella vista potrebbe richiedere fino a un massimo di 24 ore. Durante questo tempo, le informazioni contenute all'interno di una singola riga possono essere aggiornate periodicamente.  
  
### <a name="data-retention"></a>Mantenimento dei dati

 I dati in questa vista vengono mantenuti per un massimo di 30 giorni o meno, a seconda del numero di database e il numero di eventi univoci generati da ciascun database. Per prolungare il mantenimento di queste informazioni, copiare i dati in un database separato. Dopo aver creato una copia iniziale della vista, le relative righe possono essere aggiornate quando i dati vengono accumulati. Per mantenere aggiornata la copia dei dati, eseguire periodicamente un'analisi delle righe della tabella per cercare un eventuale aumento del numero di eventi di righe esistenti e per identificare le righe nuove (è possibile effettuare questa operazione per le righe univoche mediante le ore di inizio e di fine), quindi aggiornare la copia dei dati con queste modifiche.  
  
### <a name="errors-not-included"></a>Errori non inclusi

 In questa vista non possono essere incluse tutte le informazioni relative a connessioni ed errori:  
  
- In questa vista non include tutti [!INCLUDE[ssSDS](../../includes/sssds-md.md)] gli errori che possono verificarsi, solo quelli specificati in tipi di evento nel database [Sys. event_log &#40;Database SQL di Azure&#41;](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md).  
  
- Se si verifica un errore di computer all'interno di [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Data Center, una piccola quantità di dati potrebbe essere mancante dalla tabella eventi.  
  
- Se un indirizzo IP è stato bloccato tramite DoSGuard, gli eventi di tentativi di connessione dall'indirizzo IP in questione non possono essere raccolti, né verranno visualizzati in questa vista.  
  
## <a name="permissions"></a>Permissions

 Gli utenti che dispongono dell'autorizzazione di accesso di **master** database hanno accesso in lettura a questa visualizzazione.  
  
## <a name="example"></a>Esempio

 Nell'esempio seguente viene illustrata una query del **Sys. database_connection_stats** per restituire un riepilogo delle connessioni al database che si sono verificate tra mezzogiorno del 9/25/2011 e mezzogiorno del 9/28 o 2011 (UTC). Per impostazione predefinita, i risultati della query vengono ordinati **start_time** (ordine crescente).  
  
```sql
SELECT *  
FROM sys.database_connection_stats
WHERE start_time>='2011-09-25:12:00:00' and end_time<='2011-09-28 12:00:00';  
```  

## <a name="see-also"></a>Vedere anche

 [Risoluzione dei problemi di Database SQL di Azure](https://msdn.microsoft.com/library/windowsazure/ee730906.aspx)  
  
  
