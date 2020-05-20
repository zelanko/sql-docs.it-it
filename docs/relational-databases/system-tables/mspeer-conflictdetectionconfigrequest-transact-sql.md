---
title: MSpeer_conflictdetectionconfigrequest (T-SQL)
description: Viene descritto il MSPeer_conflictdetectionconfigurerequest stored procedure utilizzato per tenere traccia delle richieste di configurazione a livello di topologia per una pubblicazione peer-to-peer.
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_conflictdetectionconfigrequest_TSQL
- MSpeer_conflictdetectionconfigrequest
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_conflictdetectionconfigurerequest
ms.assetid: 83afa0ca-707e-4468-a888-228268ed4e10
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3fa3f6ead24faff78fd37eeb4e7cd9d427346d00
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829205"
---
# <a name="mspeer_conflictdetectionconfigrequest-transact-sql"></a>MSpeer_conflictdetectionconfigrequest (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Utilizzata nella replica peer-to-peer per tenere traccia delle richieste di configurazione a livello di topologia per una pubblicazione. Questa tabella è archiviata nel database di pubblicazione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|ID|**int**|Identifica una richiesta di configurazione in conflitto. La colonna request_id in [MSpeer_conflictdetectionconfigresponse](../../relational-databases/system-tables/mspeer-conflictdetectionconfigresponse-transact-sql.md) utilizza questo valore.|  
|pubblicazione|**sysname**|Nome della pubblicazione da cui viene originata la richiesta di configurazione in conflitto.|  
|sent_date|**datetime**|Data e ora di invio della richiesta di configurazione in conflitto.|  
|timeout|**int**|Tempo di attesa da parte di una procedura per la restituzione delle informazioni sul conflitto da tutti i peer.|  
|modified_date|**datetime**|Data e ora del completamento di una fase.|  
|progress_phase|**nvarchar(32)**|Identifica la fase di elaborazione corrente utilizzando uno dei valori seguenti:<br /><br /> Avviato<br /><br /> Esplorazione topologia<br /><br /> Raccolta stato<br /><br /> Stato raccolto|  
|phase_timed_out|**bit**|Indica se si è verificato un timeout nella fase corrente.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
