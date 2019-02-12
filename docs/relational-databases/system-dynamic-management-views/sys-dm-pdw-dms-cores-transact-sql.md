---
title: sys.dm_pdw_dms_cores (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: b3f09b15-0863-4418-9347-a4f5fd2ab7c7
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 1099a2e78a0985878d8b55ed2bfb573295d94251
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56026775"
---
# <a name="sysdmpdwdmscores-transact-sql"></a>sys.dm_pdw_dms_cores (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene informazioni su tutti i servizi di migrazione del database in esecuzione nei nodi di calcolo dell'appliance. Elenca una riga per ogni istanza del servizio, che attualmente corrisponde una riga per ogni nodo.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|dms_core_id|**int**|Id numerico univoco associato a questa base del servizio migrazione del database.<br /><br /> Chiave per questa visualizzazione.|Impostare su pdw_node_id del nodo che core questo servizio migrazione del database è in esecuzione.|  
|pdw_node_id|**int**|ID del nodo in cui è in esecuzione il servizio migrazione del database.|Vedere node_id nelle [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|status|**nvarchar(32)**|Stato corrente del servizio migrazione del database.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
 Per informazioni sul numero massimo di righe mantenuto da questa vista, vedere la sezione i valori massimi vista di sistema nel [valori minimi e massimi (SQL Server PDW)](https://msdn.microsoft.com/5243f018-2713-45e3-9b61-39b2a57401b9) argomento.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel Data Warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
