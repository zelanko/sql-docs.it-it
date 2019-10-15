---
title: syssubscriptions (vista di sistema) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- syssubscriptions_TSQL
- syssubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syssubscriptions view
ms.assetid: c9613858-9512-43a9-aa53-7ee8064f064c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 517d9359085f7cb4bc4c94eb941981a09ca06eef
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304783"
---
# <a name="syssubscriptions-system-view-transact-sql"></a>syssubscriptions (vista di sistema) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La vista **syssubscriptions** espone informazioni sulla sottoscrizione. Questa vista è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|ID univoco di un articolo sottoscritto.|  
|**srvid**|**smallint**|ID del Sottoscrittore.|  
|**dest_db**|**sysname**|Nome del database di sottoscrizione.|  
|**status**|**tinyint**|Stato della sottoscrizione:<br /><br /> **0** = inattivo.<br /><br /> **1** = sottoscritto.<br /><br /> **2** = attivo.|  
|**sync_type**|**tinyint**|Tipo di sincronizzazione iniziale:<br /><br /> **1** = automatico.<br /><br /> **2** = nessuna.|  
|**login_name**|**sysname**|Nome dell'account di accesso utilizzato per la connessione al server di pubblicazione per l'aggiunta della sottoscrizione.|  
|**subscription_type**|**int**|Tipo di sottoscrizione:<br /><br /> **0** = push: l'agente di distribuzione viene eseguito nel server di distribuzione.<br /><br /> **1** = pull: l'agente di distribuzione viene eseguito nel Sottoscrittore.|  
|**distribution_jobid**|**binary(16)**|Identifica il processo dell'agente di distribuzione utilizzato per sincronizzare la sottoscrizione.|  
|**timestmap**|**timestamp**|Data e ora di creazione della sottoscrizione.|  
|**update_mode**|**tinyint**|Modalità di aggiornamento:<br /><br /> **0** = sola lettura.<br /><br /> **1** = aggiornamento immediato.|  
|**loopback_detection**|**bit**|Si applica alle sottoscrizioni che fanno parte di una topologia di replica transazionale bidirezionale. Il rilevamento di loopback determina se l'agente di distribuzione deve inviare nuovamente al Sottoscrittore le transazioni provenienti dal Sottoscrittore:<br /><br /> **0** = restituisce.<br /><br /> **1** = non viene restituito.|  
|**queued_reinit**|**bit**|Specifica se l'articolo è contrassegnato per l'inizializzazione o la reinizializzazione. Il valore **1** indica che l'articolo sottoscritto è contrassegnato per l'inizializzazione o la reinizializzazione.|  
|**nosync_type**|**tinyint**|Tipo di inizializzazione della sottoscrizione:<br /><br /> **0** = automatico (snapshot)<br /><br /> **1** = solo supporto replica<br /><br /> **2** = inizializzazione con backup<br /><br /> **3** = inizializzazione dal numero di sequenza del file di log (LSN)<br /><br /> Per ulteriori informazioni, vedere il parametro **\@sync_type** di [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md).<br /><br /> **3** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**srvname**|**sysname**|Nome del Sottoscrittore.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle &#40;di replica Transact-&#41;SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste &#40;della replica Transact-&#41;SQL](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [syssubscriptions &#40;Transact-SQL&#41;](../../relational-databases/system-tables/syssubscriptions-transact-sql.md)  
  
  
