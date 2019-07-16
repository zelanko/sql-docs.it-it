---
title: sys.dm_hadr_auto_page_repair (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/05/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_hadr_auto_page_repair_TSQL
- sys.dm_hadr_auto_page_repair
- sys.dm_hadr_auto_page_repair_TSQL
- dm_hadr_auto_page_repair
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- automatic page repair
- sys.dm_hadr_auto_page_repair dynamic management view
ms.assetid: d7840adf-4a1b-41ac-bc94-102c07ad1c79
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e817b17de8a8af93a13628334337686abbe66b5f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900692"
---
# <a name="sysdmhadrautopagerepair-transact-sql"></a>sys.dm_hadr_auto_page_repair (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni tentativo di correzione automatica della pagina in qualsiasi database di disponibilità in una replica di disponibilità ospitata per qualsiasi gruppo di disponibilità dall'istanza del server. Questa vista contiene le righe degli ultimi tentativi automatici di correzione automatica della pagina in un database primario o secondario, con un massimo di 100 righe per database. Non appena un database raggiunge il limite massimo, la riga per il tentativo successivo di correzione automatica della pagina sostituisce una delle voci esistenti.
  
  Nella tabella seguente definisce il significato delle varie colonne:  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID del database al quale corrisponde questa riga.|  
|**file_id**|**int**|ID del file in cui si trova la pagina.|  
|**page_id**|**bigint**|ID della pagina nel file.|  
|**error_type**|**int**|Tipo di errore. I valori possibili sono i seguenti.<br /><br /> **-** 1 = tutti gli errori hardware 823<br /><br /> 1 = 824 errori diversi da un errore nel checksum o di una pagina incompleta (ad esempio un ID pagina errato)<br /><br /> 2 = Errore nel checksum<br /><br /> 3 = Pagina incompleta|  
|**page_status**|**int**|La stato del tentativo di ripristino della pagina:<br /><br /> 2 = in coda per la richiesta dal partner.<br /><br /> 3 = richiesta inviata al partner.<br /><br /> 4 = è stato correttamente correzione della pagina.<br /><br /> 5 = la pagina non poteva essere ripristinata durante l'ultimo tentativo / correzione automatica della pagina proverà a ripristinare nuovamente la pagina.|  
|**modification_time**|**datetime**|Ora dell'ultima modifica dello stato della pagina.|  
  
## <a name="security"></a>Sicurezza  
  
### <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
## <a name="see-also"></a>Vedere anche  
 [Correzione automatica della pagina &#40;Gruppi di disponibilità: Mirroring del database&#41;](../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [suspect_pages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md)   
 [Gestione della tabella suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  

