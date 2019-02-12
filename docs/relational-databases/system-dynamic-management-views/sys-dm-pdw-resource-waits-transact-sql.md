---
title: Sys.dm_pdw_resource_waits (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a43ce9a2-5261-41e3-97f0-555ba05ebed9
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 634cded452697c91dfd2ff60635faa7fe1163958
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56027502"
---
# <a name="sysdmpdwresourcewaits-transact-sql"></a>sys.dm_pdw_resource_waits (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Consente di visualizzare informazioni per tutti i tipi di risorse in attesa [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|Posizione della richiesta nella lista di attesa.|ordinale in base 0. Ciò non è univoco in tutte le voci di attesa.|  
|session_id|**nvarchar(32)**|ID della sessione in cui si è verificato lo stato di attesa.|Vedere ID_sessione [DM pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|Tipo|**nvarchar(255)**|Tipo di attesa che questa voce rappresenta.|I valori possibili sono:<br /><br /> Connessione<br /><br /> Concorrenza di query locali<br /><br /> Concorrenza di query distribuite<br /><br /> Concorrenza DMS<br /><br /> Concorrenza di backup|  
|object_type|**nvarchar(255)**|Tipo di oggetto interessato dell'attesa.|I valori possibili sono:<br /><br /> **OBJECT**<br /><br /> **DATABASE**<br /><br /> **SYSTEM**<br /><br /> **SCHEMA**<br /><br /> **APPLICATION**|  
|object_name|**nvarchar(386)**|Nome o GUID dell'oggetto specificato che è stata interessata dall'attesa.|Tabelle e viste vengono visualizzate con nomi in tre parti.<br /><br /> Gli indici e le statistiche vengono visualizzate con nomi in quattro parti.<br /><br /> Database, le entità e i nomi sono nomi di tipo stringa.|  
|request_id|**nvarchar(32)**|ID della richiesta in cui si è verificato lo stato di attesa.|Identificatore QID della richiesta.<br /><br /> Identificatore GUID per le richieste di caricamento.|  
|request_time|**datetime**|Ora in cui è stato richiesto il blocco o risorsa.||  
|acquire_time|**datetime**|Ora in cui è stata acquisita il blocco o risorsa.||  
|state|**nvarchar(50)**|Stato di stato di attesa.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|Priorità dell'elemento in attesa.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|concurrency_slots_used|**int**|Numero di slot di concorrenza (massimo 32) riservato per questa richiesta.|1 - per SmallRC<br /><br /> 3 - per MediumRC<br /><br /> 7 per LargeRC<br /><br /> 22 - per XLargeRC|  
|resource_class|**nvarchar(20)**|La classe di risorse per questa richiesta.|SmallRC<br /><br /> MediumRC<br /><br /> LargeRC<br /><br /> XLargeRC|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel Data Warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
