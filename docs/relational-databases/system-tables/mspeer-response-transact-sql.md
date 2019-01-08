---
title: MSpeer_response (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_response
- MSpeer_response_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_response system table
ms.assetid: 510e24cf-0292-47a9-b1d9-71a30fef030f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: adbddf6f26c28c5fba396b00892b97d828e60222
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52757993"
---
# <a name="mspeerresponse-transact-sql"></a>MSpeer_response (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSpeer_response** tabella viene utilizzata nella replica Peer-to-Peer per archiviare la risposta di ogni nodo a una richiesta di stato di pubblicazione. Questa tabella è archiviata nel database di pubblicazione.  
  
## <a name="definition"></a>Definizione  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**request_id**|**int**|Identifica una voce di richiesta di stato nella [MSpeer_request](../../relational-databases/system-tables/mspeer-request-transact-sql.md) tabella.|  
|**peer**|**sysname**|Peer che ha generato la risposta.|  
|**peer_db**|**sysname**|Database di sottoscrizione del peer che ha generato la risposta.|  
|**received_date**|**datetime**|Data e ora di ricezione della richiesta peer.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
