---
title: MSmerge_metadataaction_request (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_metadataaction_request
- MSmerge_metadataaction_request_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_metadataaction_request system table
ms.assetid: cd31a114-900a-4218-ab58-d959e547c647
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a46570a30254341fede1fb96fd368e94a09e58ea
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62910296"
---
# <a name="msmergemetadataactionrequest-transact-sql"></a>MSmerge_metadataaction_request (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSmerge_metadataaction_request** tabella contiene una riga per ogni azione di compensazione necessaria. Usa sincronizzazione Web, se si verifica un errore ed eseguire di nuovo la sincronizzazione, viene creata una voce in **MSmerge_metadataaction_request**. Durante la fase di caricamento del merge successivo, le richieste di tutti gli articoli facenti parte della pubblicazione in fase di sincronizzazione vengono recuperate da questa tabella e caricate. Quando la sincronizzazione viene completata correttamente, la riga corrispondente nella **MSmerge_metadataaction_request** tabella viene eliminata. Questa tabella è archiviata nel database di pubblicazione del server di pubblicazione e nel database di sottoscrizione del Sottoscrittore.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|Nome alternativo della tabella pubblicata.|  
|**rowguid**|**uniqueidentifier**|Identificatore della riga specificata.|  
|**action**|**tinyint**|Identifica l'azione di compensazione necessaria.|  
|**generation**|**bigint**|Valore della generazione per cui l'azione di compensazione è necessaria.|  
|**changed**|**int**|Solo per uso interno.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica di &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Sincronizzazione Web per la replica di tipo merge](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
