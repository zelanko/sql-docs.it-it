---
description: MSmerge_replinfo (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ce4bee70ea5ef410512ce399e8d715fbc321e1a6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545609"
---
# <a name="msmerge_replinfo-transact-sql"></a>MSmerge_replinfo (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabella **MSmerge_replinfo** contiene una riga per ogni sottoscrizione. In questa tabella viene tenuta traccia delle informazioni relative alle sottoscrizioni. Questa tabella è archiviata nei database di pubblicazione e di sottoscrizione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**repid**|**uniqueidentifier**|ID univoco della replica.|  
|**use_interactive_resolver**|**bit**|Specifica se nella fase di riconciliazione dei conflitti viene utilizzato il sistema di risoluzione interattivo.<br /><br /> **0** = non viene utilizzato il sistema di risoluzione interattivo.<br /><br /> **1** = usa il sistema di risoluzione interattivo.|  
|**validation_level**|**int**|Tipo di convalida da eseguire sulla sottoscrizione. I possibili valori sono i seguenti:<br /><br /> **0** = nessuna convalida.<br /><br /> **1** = convalida con solo conteggio delle righe.<br /><br /> **2** = convalida tramite conteggio delle righe e checksum.<br /><br /> **3** = convalida tramite conteggio delle righe e checksum binario.|  
|**resync_gen**|**bigint**|Numero di generazione utilizzato per la risincronizzazione della sottoscrizione. Il valore **-1** indica che la sottoscrizione non è contrassegnata per la risincronizzazione.|  
|**login_name**|**sysname**|Nome dell'utente che ha creato la sottoscrizione.|  
|**hostname**|**sysname**|Valore utilizzato dal filtro di riga con parametri durante la generazione della partizione per la sottoscrizione.|  
|**merge_jobid**|**binary(16)**|ID del processo di merge della sottoscrizione.|  
|**sync_info**|**int**|Solo per uso interno.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
