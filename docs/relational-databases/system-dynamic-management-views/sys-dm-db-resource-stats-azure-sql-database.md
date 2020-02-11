---
title: sys. dm_db_resource_stats (database SQL di Azure) | Microsoft Docs
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
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 1dd66834788896e6952a0352eb2a19fd1a828513
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "75245958"
---
# <a name="sysdm_db_resource_stats-azure-sql-database"></a>sys.dm_db_resource_stats (Database SQL di Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Restituisce il consumo di CPU, I/O e memoria per un database [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. È presente una riga ogni 15 secondi, anche se non c'è attività di database. I dati cronologici vengono conservati per circa un'ora.  
  
|Colonne|Tipo di dati|Descrizione|  
|-------------|---------------|-----------------|  
|end_time|**datetime**|Ora UTC che indica la fine dell'intervallo di reporting corrente.|  
|avg_cpu_percent|**Decimal (5, 2)**|Percentuale dell'utilizzo medio del calcolo del limite del livello del servizio.|  
|avg_data_io_percent|**Decimal (5, 2)**|Utilizzo medio di I/O dei dati in percentuale rispetto al limite del livello di servizio. Per i database con iperscalabilità, vedere i/o [dati nelle statistiche sull'utilizzo delle risorse](https://docs.microsoft.com/azure/sql-database/sql-database-hyperscale-performance-diagnostics#data-io-in-resource-utilization-statistics).|  
|avg_log_write_percent|**Decimal (5, 2)**|Numero medio di scritture del log delle transazioni (in MBps) come percentuale del limite del livello di servizio.|  
|avg_memory_usage_percent|**Decimal (5, 2)**|Percentuale dell'utilizzo medio della memoria del limite del livello del servizio.<br /><br /> Questo include la memoria usata per le pagine del pool di buffer e l'archiviazione di oggetti OLTP in memoria.|  
|xtp_storage_percent|**Decimal (5, 2)**|Utilizzo dello spazio di archiviazione per OLTP in memoria, in percentuale rispetto al limite del livello di servizio (alla fine dell'intervallo di Reporting). Ciò include la memoria usata per l'archiviazione dei seguenti oggetti di OLTP in memoria: tabelle ottimizzate per la memoria, indici e variabili di tabella. Include inoltre la memoria utilizzata per l'elaborazione delle operazioni ALTER TABLE.<br /><br /> Restituisce 0 se OLTP in memoria non viene utilizzato nel database.|  
|max_worker_percent|**Decimal (5, 2)**|Numero massimo di ruoli di lavoro simultanei (richieste) in percentuale rispetto al limite del livello di servizio del database.|  
|max_session_percent|**Decimal (5, 2)**|Numero massimo di sessioni simultanee in percentuale del limite del livello di servizio del database.|  
|dtu_limit|**int**|Impostazione DTU database Max corrente per questo database durante questo intervallo. Per i database che usano il modello basato su vCore, questa colonna è NULL.|
|cpu_limit|**Decimal (5, 2)**|Numero di Vcore per il database durante questo intervallo. Per i database che usano il modello basato su DTU, questa colonna è NULL.|
|avg_instance_cpu_percent|**Decimal (5, 2)**|Utilizzo medio della CPU del database come percentuale del processo di database SQL.|
|avg_instance_memory_percent|**Decimal (5, 2)**|Utilizzo medio della memoria del database come percentuale del processo di database SQL.|
|avg_login_rate_percent|**Decimal (5, 2)**|Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.|
|replica_role|**int**|Rappresenta il ruolo della replica corrente con 0 come primario, 1 come secondario e 2 come server di trasmissione (primario della replica geografica secondaria). Quando si è connessi con la finalità ReadOnly a tutti i database secondari leggibili, viene visualizzato "1". Se ci si connette a una replica geografica secondaria senza specificare la finalità di sola lettura, verrà visualizzato "2" (connessione al server d'istruzione).|
|||
  
> [!TIP]  
>  Per ulteriori informazioni sui limiti e sui livelli di servizio, vedere gli argomenti [livelli di servizio](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) e [funzionalità e limiti del livello di servizio](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/).  
  
## <a name="permissions"></a>Autorizzazioni  
 Questa vista richiede l'autorizzazione VIEW DATABASE STATE.  
  
## <a name="remarks"></a>Osservazioni  
 I dati restituiti da **sys. dm_db_resource_stats** vengono espressi come percentuale dei limiti massimi consentiti per il livello di servizio o il livello di prestazioni che si sta eseguendo.
 
 Se è stato effettuato il failover del database in un altro server negli ultimi 60 minuti, la vista restituirà solo i dati relativi al tempo in cui il database è stato primario dopo il failover.  
  
 Per una visualizzazione meno granulare di questi dati con un periodo di conservazione più lungo, utilizzare la vista del catalogo **sys. resource_stats** nel database **Master** . Questa vista acquisisce i dati ogni 5 minuti e conserva i dati cronologici per 14 giorni.  Per altre informazioni, vedere [sys. resource_stats &#40;database SQL di Azure&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md).  
  
 Quando un database è membro di un pool elastico, le statistiche sulle risorse presentate come valori percentuali vengono espresse come percentuale del limite massimo per i database impostati nella configurazione del pool elastico.  
  
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
 [sys. resource_stats &#40;database SQL di Azure&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [Livelli di servizio](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [Limiti e funzionalità dei livelli di servizio](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
