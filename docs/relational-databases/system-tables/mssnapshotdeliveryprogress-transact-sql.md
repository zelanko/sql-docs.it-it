---
title: MSsnapshotdeliveryprogress (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsnapshotdeliveryprogress_TSQL
- MSsnapshotdeliveryprogress
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshotdeliveryprogress system table
ms.assetid: 9164bfe2-6fc4-4b52-946a-09ea3cf67041
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 67b6a2c048f8e873d6daa447270e00c1eda86c3e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52751453"
---
# <a name="mssnapshotdeliveryprogress-transact-sql"></a>MSsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSsnapshotdeliveryprogress** tabella viene utilizzata per tenere traccia dei file che sono stati recapitati al sottoscrittore quando viene applicato uno snapshot. Questi dati vengono utilizzati per riprendere il recapito di file nel caso in cui l'agente di merge non sia in grado di recapitare tutti i file durante la sessione e pertanto per evitare di recapitare gli stessi file alla successiva esecuzione dell'agente di merge. Questa tabella è archiviata nel database di sottoscrizione del Sottoscrittore.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**session_token**|**nvarchar(260)**|Identifica il percorso della cartella snapshot dalla quale il file è stato recapitato con esito positivo. Per le pubblicazioni che utilizzano filtri con parametri, la stringa **dynsnap** verrà aggiunto al valore.|  
|**progress_token_hash**|**int**|Un valore hash generato in base al valore della *progress_token* utilizzato migliorare l'efficienza di ricerca per un determinato *progress_token* valore.|  
|**progress_token**|**nvarchar(500)**|Identifica un file recapitato con esito positivo, dove il valore è dato dalla combinazione di nome file e percorso.|  
|**progress_timestamp**|**datetime**|Il **datetime** valore che indica quando è stato recapitato con un file di snapshot.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
