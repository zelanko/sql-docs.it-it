---
description: MSsnapshotdeliveryprogress (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 733f82a23c61d41691c3845b2482a0aa0c3c2bcc
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540209"
---
# <a name="mssnapshotdeliveryprogress-transact-sql"></a>MSsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabella **MSsnapshotdeliveryprogress** viene utilizzata per tenere traccia dei file che sono stati recapitati correttamente al Sottoscrittore durante l'applicazione di uno snapshot. Questi dati vengono utilizzati per riprendere il recapito di file nel caso in cui l'agente di merge non sia in grado di recapitare tutti i file durante la sessione e pertanto per evitare di recapitare gli stessi file alla successiva esecuzione dell'agente di merge. Questa tabella è archiviata nel database di sottoscrizione del Sottoscrittore.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**session_token**|**nvarchar(260)**|Identifica il percorso della cartella snapshot dalla quale il file è stato recapitato con esito positivo. Per le pubblicazioni che utilizzano filtri con parametri, la stringa **dynsnap** verrà aggiunta al valore.|  
|**progress_token_hash**|**int**|Valore hash generato in base al valore di *progress_token* usato per migliorare l'efficienza della ricerca per un valore di *progress_token* specificato.|  
|**progress_token**|**nvarchar (500)**|Identifica un file recapitato con esito positivo, dove il valore è dato dalla combinazione di nome file e percorso.|  
|**progress_timestamp**|**datetime**|Valore **DateTime** che indica quando un file di snapshot è stato recapitato correttamente.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
