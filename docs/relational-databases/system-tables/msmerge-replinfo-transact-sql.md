---
title: MSmerge_replinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_replinfo_TSQL
- MSmerge_replinfo
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_replinfo system table
ms.assetid: b0924094-c0cc-49c1-869a-65be0d0465a0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 045f9ab13b701b8dbd5e0895531932c21767853f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67909064"
---
# <a name="msmerge_replinfo-transact-sql"></a>MSmerge_replinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabella **MSmerge_replinfo** contiene una riga per ogni sottoscrizione. In questa tabella viene tenuta traccia delle informazioni relative alle sottoscrizioni. Questa tabella è archiviata nei database di pubblicazione e di sottoscrizione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**repid**|**uniqueidentifier**|ID univoco della replica.|  
|**use_interactive_resolver**|**bit**|Specifica se nella fase di riconciliazione dei conflitti viene utilizzato il sistema di risoluzione interattivo.<br /><br /> **0** = non viene utilizzato il sistema di risoluzione interattivo.<br /><br /> **1** = usa il sistema di risoluzione interattivo.|  
|**validation_level**|**int**|Tipo di convalida da eseguire sulla sottoscrizione. I possibili valori sono i seguenti:<br /><br /> **0** = nessuna convalida.<br /><br /> **1** = convalida con solo conteggio delle righe.<br /><br /> **2** = convalida tramite conteggio delle righe e checksum.<br /><br /> **3** = convalida tramite conteggio delle righe e checksum binario.|  
|**resync_gen**|**bigint**|Numero di generazione utilizzato per la risincronizzazione della sottoscrizione. Il valore **-1** indica che la sottoscrizione non è contrassegnata per la risincronizzazione.|  
|**login_name**|**sysname**|Nome dell'utente che ha creato la sottoscrizione.|  
|**nome host**|**sysname**|Valore utilizzato dal filtro di riga con parametri durante la generazione della partizione per la sottoscrizione.|  
|**merge_jobid**|**binario (16)**|ID del processo di merge della sottoscrizione.|  
|**sync_info**|**int**|Solo per uso interno.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
