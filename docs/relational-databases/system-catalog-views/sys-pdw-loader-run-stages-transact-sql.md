---
description: sys.pdw_loader_run_stages (Transact-SQL)
title: sys.pdw_loader_run_stages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 255681e9-323c-42c0-a63c-1f05536efdd5
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: ee8eb27964a7fc26d5af6c8f7a13293720ca7821
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475152"
---
# <a name="syspdw_loader_run_stages-transact-sql"></a>sys.pdw_loader_run_stages (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Contiene informazioni sulle operazioni di caricamento in corso e completate in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] . Le informazioni vengono mantenute tra un riavvio di sistema e l'altro.  
  
| Nome colonna | Tipo di dati | Descrizione | Range |
| ----------- | --------- | ----------- | ----- |
|run_id|**int**|Identificatore univoco di un'esecuzione del caricatore.||  
|fase|**nvarchar(30)**|Fase corrente dell'esecuzione.|' CREATE_STAGING ',' DMS_LOAD ',' LOAD_INSERT ',' LOAD_CLEANUP '|  
|request_id|**nvarchar(32)**|ID della richiesta che esegue questa fase.||  
|status|**nvarchar (16)**|Stato di questa fase.||  
|start_time|**datetime**|Ora di inizio della fase.||  
|end_time|**datetime**|Ora in cui è terminata la fase, se disponibile.|NULL se non è stato avviato o in corso.|  
|total_elapsed_time|**int**|Tempo totale impiegato per la fase (o che è trascorso finora).|Se total_elapsed_time supera il valore massimo per un numero intero (24,8 giorni in millisecondi), si verificherà un errore di materializzazione causato da un overflow.<br /><br /> Il valore massimo in millisecondi equivale a 24,8 giorni.|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo di Azure Synapse Analytics e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
