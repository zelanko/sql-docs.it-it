---
title: Sys.server_resource_stats (Database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 06/28/2018
ms.service: sql-database
ms.reviewer: carlrab, edmaca
ms.topic: language-reference
f1_keywords:
- resource_stats
- sys.resource_stats
- sys.resource_stats_TSQL
- resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_stats
- resource_stats
ms.assetid: ''
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: 1f3d69d8fdfffaa6573f4813392509d0ca71c684
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66462780"
---
# <a name="sysserverresourcestats-azure-sql-database"></a>Sys.server_resource_stats (Database SQL di Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Restituisce i dati di archiviazione, i/o e utilizzo della CPU per un'istanza gestita di Azure SQL. I dati vengono raccolti e aggregati in intervalli di cinque minuti. È disponibile una riga per ogni 15 secondi reporting. I dati restituiti includono utilizzo della CPU, dimensioni di archiviazione, utilizzo di IO e SKU delle istanze gestito. I dati cronologici vengono mantenuti per circa 14 giorni.

Il **sys.server_resource_stats** visualizzazione contiene diverse definizioni a seconda della versione dell'istanza gestita SQL di Azure che è associato il database. Prendere in considerazione queste differenze e le eventuali modifiche richieste dall'applicazione durante l'aggiornamento a una nuova versione del server.
 
  
 La tabella seguente descrive le colonne disponibili in un server v12:  
  
|Colonne|Tipo di dati|Descrizione|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime2**|Ora UTC che indica l'inizio dell'intervallo di reporting di quindici secondi|  
|end_time|**datetime**|Ora UTC che indica la fine dell'intervallo di reporting di quindici secondi|
|resource_type|Nvarchar(128)|Tipo di risorsa per il quale vengono fornite metriche|
|resource_name|nvarchar(128)|Nome della risorsa.|
|sku|nvarchar(128)|Gestito istanza livello di servizio dell'istanza. Di seguito sono indicati i valori possibili: <br><ul><li>Utilizzo generico</li></ul><ul><li>Business Critical</li></ul>|
|hardware_generation|nvarchar(128)|Identificatore di generazione di hardware: ad esempio Gen 4 o generazione 5|
|virtual_core_count|INT|Rappresenta i numero di core virtuali per ogni istanza (8, 16 o 24 in anteprima pubblica)|
|avg_cpu_percent|Decimal(5,2)|Utilizzo di calcolo medio in percentuale del limite del livello di servizio istanza gestita utilizzato dall'istanza. Viene calcolata come somma del tempo di CPU di tutti i pool di risorse per tutti i database nell'istanza e diviso per tempo di CPU disponibile per tale livello nell'intervallo specificato.|
|reserved_storage_mb|BIGINT|Spazio di archiviazione per istanza riservata (quantità di spazio di archiviazione spazio quel cliente acquistato per l'istanza gestita)|
|storage_space_used_mb|Decimal(18,2)|Spazio di archiviazione usato dai file di tutti i database istanza gestita (inclusi i database utente e di sistema)|
|io_request|BIGINT|Numero totale di operazioni fisiche dei / o entro l'intervallo|
|io_bytes_read|BIGINT|Numero di byte fisici entro l'intervallo di lettura|
|io_bytes_written|BIGINT|Numero di byte fisici scritti all'interno dell'intervallo|

 
> [!TIP]  
>  Per altre informazioni su questi limiti e i livelli di servizio, vedere gli argomenti [livelli di servizio istanza gestita](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance#managed-instance-service-tiers).  
    
## <a name="permissions"></a>Permissions  
 Questa vista è disponibile per tutti i ruoli utente con autorizzazioni per la connessione per il **master** database.  
  
## <a name="remarks"></a>Note  
 I dati restituiti da **sys.server_resource_stats** sono espressi come il totale utilizzato in un byte o megabyte (indicati nei nomi di colonna) diverso da avg_cpu, espressa come percentuale dei limiti massimi consentiti per il servizio livello di prestazioni/livello in esecuzione.  
 
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituiti tutti i database che hanno una media di almeno l'80% di utilizzo del calcolo nell'ultima settimana.  
  
```sql  
DECLARE @s datetime;  
DECLARE @e datetime;  
SET @s= DateAdd(d,-7,GetUTCDate());  
SET @e= GETUTCDATE();  
SELECT resource_name, AVG(avg_cpu_percent) AS Average_Compute_Utilization   
FROM sys.server_resource_stats   
WHERE start_time BETWEEN @s AND @e  
GROUP BY resource_name  
HAVING AVG(avg_cpu_percent) >= 80  
```  
    
## <a name="see-also"></a>Vedere anche  
 [I livelli di servizio istanza gestita](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance#managed-instance-service-tiers)
