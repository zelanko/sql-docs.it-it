---
title: DM db_resource_stats (Database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 05/21/2019
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_resource_stats
- sys.dm_db_resource_stats_TSQL
- dm_db_resource_stats
- dm_db_resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_resource_stats
- dm_db_resource_stats
ms.assetid: 6e76b39f-236e-4bbf-b0b5-38be190d81e8
author: julieMSFT
ms.author: jrasnick
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 22d771f57e5ac0d9035b8c283eb6da69027eadb3
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716682"
---
# <a name="sysdmdbresourcestats-azure-sql-database"></a>sys.dm_db_resource_stats (Database SQL di Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Restituisce il consumo di CPU, I/O e memoria per un database [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. È presente una riga ogni 15 secondi, anche se non c'è attività di database. I dati cronologici vengono mantenuti per un'ora.  
  
|Colonne|Tipo di dati|Descrizione|  
|-------------|---------------|-----------------|  
|end_time|**datetime**|Ora UTC che indica la fine dell'intervallo di reporting corrente.|  
|avg_cpu_percent|**numero decimale (5,2)**|Percentuale dell'utilizzo medio del calcolo del limite del livello del servizio.|  
|avg_data_io_percent|**numero decimale (5,2)**|Media di dati utilizzo i/o in percentuale del limite del livello di servizio.|  
|avg_log_write_percent|**numero decimale (5,2)**|Medio scrittura utilizzo di velocità effettiva dei / o come percentuale del limite del livello di servizio.|  
|avg_memory_usage_percent|**numero decimale (5,2)**|Percentuale dell'utilizzo medio della memoria del limite del livello del servizio.<br /><br /> Ciò include la memoria usata per l'archiviazione di oggetti di OLTP In memoria e le pagine del pool di buffer.|  
|xtp_storage_percent|**numero decimale (5,2)**|Utilizzo spazio di archiviazione per OLTP In memoria, espresso in percentuale del limite del livello di servizio (alla fine dell'intervallo di reporting). Ciò include la memoria usata per l'archiviazione degli oggetti OLTP In memoria seguenti: tabelle con ottimizzazione per la memoria, indici e le variabili di tabella. Include anche la memoria utilizzata per l'elaborazione di operazioni ALTER TABLE.<br /><br /> Restituisce 0 se OLTP In memoria non viene utilizzato nel database.|  
|max_worker_percent|**numero decimale (5,2)**|Massimi ruoli di lavoro simultanei (richieste) espresso come percentuale del limite del livello di servizio del database.|  
|max_session_percent|**numero decimale (5,2)**|Numero massimo di sessioni simultaneo espresso in percentuale del limite del livello di servizio del database.|  
|dtu_limit|**int**|Database max DTU impostazione corrente per il database durante questo intervallo. Per i database usando il modello basato su vCore, questa colonna è NULL.|
|cpu_limit|**numero decimale (5,2)**|Numero di Vcore per il database durante questo intervallo. Per i database usando il modello basato su DTU, questa colonna è NULL.|
|avg_instance_cpu_percent|**numero decimale (5,2)**|Database medio della CPU in percentuale.|
|avg_instance_memory_percent|**numero decimale (5,2)**|Utilizzo della memoria medio del database in percentuale.|
|avg_login_rate_percent|**numero decimale (5,2)**|Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.|
|replica_role|**int**|Rappresenta il corrente ruolo della replica con 0 come primario, 1 come replica secondaria e 2 come utilità di inoltro (primario con del replica geografica secondaria). Verrà visualizzato "1" quando si è connessi con finalità di sola lettura a tutte le repliche secondarie leggibili. Se ci si connette a una replica geografica secondaria senza specificare la finalità di sola lettura, si dovrebbe vedere "2" (la connessione al server di inoltro).|
|||
  
> [!TIP]  
>  Per altre informazioni su questi limiti e i livelli di servizio, vedere gli argomenti [livelli di servizio](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) e [limiti e funzionalità dei livelli di servizio](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/).  
  
## <a name="permissions"></a>Permissions  
 Questa vista richiede l'autorizzazione VIEW DATABASE STATE.  
  
## <a name="remarks"></a>Note  
 I dati restituiti da **DM db_resource_stats** viene espresso come percentuale dei limiti massimi consentiti per il livello di prestazioni/livello di servizio in esecuzione.
 
 Se è stato effettuato il failover del database in un altro server negli ultimi 60 minuti, la vista restituirà solo i dati relativi al tempo in cui il database è stato primario dopo il failover.  
  
 Per una vista meno dettagliata di questi dati, usare **Sys. resource_stats** vista del catalogo il **master** database. Questa vista acquisisce i dati ogni 5 minuti e conserva i dati cronologici per 14 giorni.  Per altre informazioni, vedere [Sys. resource_stats &#40;Database SQL di Azure&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md).  
  
 Quando un database è un membro di un pool elastico, le statistiche di resource presentate come valori percentuali, sono espresse come percentuale del limite massimo per database impostato nella configurazione del pool elastico.  
  
## <a name="example"></a>Esempio  
  
L'esempio seguente restituisce i dati di utilizzo delle risorse ordinati in base l'ora più recente per il database attualmente connesso.  
  
```  
SELECT * FROM sys.dm_db_resource_stats ORDER BY end_time DESC;  
  
```  
  
 L'esempio seguente identifica il consumo medio di DTU in termini di percentuale del limite massimo consentito di DTU nel livello di prestazioni per il database utente nell'ora precedente. Provare ad aumentare il livello di prestazioni se queste percentuali si avvicinano in modo continuativo al 100%.  
  
```  
SELECT end_time,   
  (SELECT Max(v)    
   FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS    
   value(v)) AS [avg_DTU_percent]   
FROM sys.dm_db_resource_stats;  
  
```  
  
 L'esempio seguente restituisce i valori medi e massimi relativi alla percentuale di utilizzo della CPU, all'utilizzo di dati e I/O del log e al consumo di memoria nell'ultima ora.  
  
```  
SELECT    
    AVG(avg_cpu_percent) AS 'Average CPU Utilization In Percent',   
    MAX(avg_cpu_percent) AS 'Maximum CPU Utilization In Percent',   
    AVG(avg_data_io_percent) AS 'Average Data IO In Percent',   
    MAX(avg_data_io_percent) AS 'Maximum Data IO In Percent',   
    AVG(avg_log_write_percent) AS 'Average Log Write I/O Throughput Utilization In Percent',   
    MAX(avg_log_write_percent) AS 'Maximum Log Write I/O Throughput Utilization In Percent',   
    AVG(avg_memory_usage_percent) AS 'Average Memory Usage In Percent',   
    MAX(avg_memory_usage_percent) AS 'Maximum Memory Usage In Percent'   
FROM sys.dm_db_resource_stats;  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Sys. resource_stats &#40;Database SQL di Azure&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [Livelli di servizio](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [Limiti e le funzionalità del livello servizio](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
