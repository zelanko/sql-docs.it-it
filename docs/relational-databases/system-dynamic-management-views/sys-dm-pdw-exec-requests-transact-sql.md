---
title: proprietà sys.dm_pdw_exec_requests (Transact-SQL) Documenti Microsoft
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 390225cc-23e8-4051-a5f6-221e33e4c0b4
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 851c138e00300a303b1618041a16e2c38516968e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301251"
---
# <a name="sysdm_pdw_exec_requests-transact-sql"></a>sys.dm_pdw_exec_requests (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene informazioni su tutte le [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]richieste attualmente o recentemente attive in . Elenca una riga per richiesta/query.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Chiave per questa vista. ID numerico univoco associato alla richiesta.|Univoco in tutte le richieste nel sistema.|  
|session_id|**nvarchar(32)**|ID numerico univoco associato alla sessione in cui è stata eseguita la query. Vedere [sys.dm_pdw_exec_sessions &#40;&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).||  
|status|**nvarchar(32)**|Stato corrente della richiesta.|'In esecuzione', 'Sospeso', 'Completato', 'Annullato', 'Non riuscito'.|  
|submit_time|**datetime**|Ora in cui la richiesta è stata inviata per l'esecuzione.|**Datetime** più piccolo o uguale all'ora e all'start_time correnti.|  
|start_time|**datetime**|Ora di inizio dell'esecuzione della richiesta.|NULL per le richieste in coda; in caso contrario, **datetime** valido minore o uguale all'ora corrente.|  
|end_compile_time|**datetime**|Ora in cui il motore ha completato la compilazione della richiesta.|NULL per le richieste che non sono ancora state compilate; in caso contrario, un **valore datetime** valido minore di start_time e minore o uguale all'ora corrente.|
|end_time|**datetime**|Ora in cui l'esecuzione della richiesta è stata completata, non è riuscita o è stata annullata.|Null per le richieste in coda o attive; in caso contrario, un **valore datetime** minore o uguale all'ora corrente.|  
|total_elapsed_time|**Int**|Tempo trascorso nell'esecuzione dall'avvio della richiesta, in millisecondi.|Tra 0 e la differenza tra start_time e end_time.</br></br> Se total_elapsed_time supera il valore massimo per un numero intero, total_elapsed_time continuerà a essere il valore massimo. Questa condizione genererà l'avviso "Il valore massimo è stato superato".</br></br> Il valore massimo in millisecondi è uguale a 24,8 giorni.|  
|label|**nvarchar(255)**|Stringa di etichetta facoltativa associata ad alcune istruzioni di query SELECT.|Qualsiasi stringa contenente 'a-z','A-''','0-9','_'.|  
|error_id|**nvarchar(36)**|ID univoco dell'errore associato alla richiesta, se presente.|Vedere [sys.dm_pdw_errors &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md); impostato su NULL se non si è verificato alcun errore.|  
|database_id|**Int**|Identificatore del database utilizzato dal contesto esplicito (ad esempio, USE DB_X).|Vedere ID in [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|command|**nvarchar(4000)**|Contiene il testo completo della richiesta inviata dall'utente.|Qualsiasi query o testo di richiesta valido. Le query più lunghe di 4000 byte vengono troncate.|  
|resource_class|**nvarchar(20)**|Gruppo del carico di lavoro utilizzato per questa richiesta. |Classi di risorse statiche</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80</br>            </br>Classi di risorse dinamiche</br>PiccoloRC</br>MediaRC</br>GrandeRC</br>XLargeRC (informazioni in cui i valori xico|
|importance|**nvarchar(128)**|Impostazione importanza in cui è stata eseguita la richiesta.  Questa è l'importanza relativa di una richiesta in questo gruppo di carico di lavoro e tra i gruppi di carico di lavoro per le risorse condivise.  L'importanza specificata nel classificatore sostituisce l'impostazione di importanza del gruppo di carico di lavoro.</br>Si applica a: Azure SQL Data Warehouse|NULL</br>low</br>below_normal</br>normal (predefinito)</br>above_normal</br>high|
|group_name|**sysname** |Per le richieste che utilizzano le risorse, group_name è il nome del gruppo di carico di lavoro con cui viene eseguita la richiesta.  Se la richiesta non utilizza risorse, group_name è null.</br>Si applica a: Azure SQL Data Warehouse|
|classifier_name|**sysname**|Per le richieste che utilizzano risorse, nome del classificatore utilizzato per l'assegnazione di risorse e importanza.||
|resource_allocation_percentage|**decimale(5,2)**|Quantità percentuale di risorse allocate alla richiesta.</br>Si applica a: Azure SQL Data Warehouse|
|result_cache_hit|**Esadecimale**|Indica se una query completata ha utilizzato la cache del set di risultati.  </br>Si applica a: Azure SQL Data Warehouse| 1 - Hit della cache del set di risultati </br> 0 - Mancata cache del set di risultati </br> Valori negativi: motivi per cui non è stata utilizzata la memorizzazione nella cache del set di risultati.  Vedere la sezione Osservazioni per i dettagli.|
||||
  
## <a name="remarks"></a>Osservazioni 
 Per informazioni sul numero massimo di righe mantenute da questa visualizzazione, vedere la sezione Metadati nell'argomento [Limiti di capacità.](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)

 Il result_cache_hit è una maschera di bit dell'utilizzo della cache del set di risultati da parte di una query.  Questa colonna può essere [il (OR bit per bit)](../../t-sql/language-elements/bitwise-or-transact-sql.md) prodotto di uno o più di questi valori:  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**1**|Hit della cache del set di risultatiResult set cache hit|  
|-**0x00 (in questo 0x00)**|Mancata cache del set di risultatiResult set cache miss|  
|-**0x01 (in tissuta (in ti**|La memorizzazione nella cache del set di risultati è disabilitata nel database.|  
|-**0x02 (in tissuta 0x0**|La memorizzazione nella cache del set di risultati è disabilitata nella sessione. | 
|-**0x04 (in tissuta 0x0**|La memorizzazione nella cache del set di risultati è disabilitata a causa di nessuna origine dati per la query.|  
|-**0x08 (in tissuta 0x0**|La memorizzazione nella cache del set di risultati è disabilitata a causa di predicati di sicurezza a livello di riga.|  
|-**0x10 (in modo 0x10)**|La memorizzazione nella cache del set di risultati è disabilitata a causa dell'utilizzo della tabella di sistema, della tabella temporanea o della tabella esterna nella query.|  
|-**0x20 (in questo 0x20)**|La memorizzazione nella cache del set di risultati è disabilitata perché la query contiene costanti di runtime, funzioni definite dall'utente o funzioni non deterministiche.|  
|-**0x40 (in questo 0x40)**|La memorizzazione nella cache del set di risultati è disabilitata perché le dimensioni stimate del set di risultati sono troppo grandi (> 1 milione di righe).|  
|-**0x80 (in questo 0x80)**|La memorizzazione nella cache del set di risultati è disabilitata perché il set di risultati contiene righe con dimensioni grandi (>64kb).|  
  
## <a name="permissions"></a>Autorizzazioni

 È richiesta l'autorizzazione VIEW SERVER STATE.  
  
## <a name="security"></a>Sicurezza

 sys.dm_pdw_exec_requests non filtra i risultati delle query in base alle autorizzazioni specifiche del database. Gli account di accesso con l'autorizzazione VIEW SERVER STATE possono ottenere i risultati delle query dei risultati per tutti i database  
  
>[!WARNING]  
>Un utente malintenzionato può utilizzare sys.dm_pdw_exec_requests per recuperare informazioni su oggetti di database specifici semplicemente disponendo dell'autorizzazione VIEW SERVER STATE e non disponendo dell'autorizzazione specifica del database.  
  
## <a name="see-also"></a>Vedere anche

 [Viste a gestione dinamica di SQL Data Warehouse e Parallel Data Warehouse &#40;&#41;sql](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)
