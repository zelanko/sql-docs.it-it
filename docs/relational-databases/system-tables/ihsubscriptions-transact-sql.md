---
description: IHsubscriptions (Transact-SQL)
title: IHsubscriptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHsubscriptions_TSQL
- IHsubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- IHsubscriptions system table
ms.assetid: 9ec21119-35f1-4e39-abaa-b2c790c485b1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b8dafdba96014fe7c60524a34d76d8bc36792762
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540932"
---
# <a name="ihsubscriptions-transact-sql"></a>IHsubscriptions (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabella di sistema **IHsubscriptions** contiene una riga per ogni sottoscrizione di una pubblicazione da un server di pubblicazione non SQL Server che utilizza il server di distribuzione corrente. Questa tabella è archiviata nel database di distribuzione.  
  
## <a name="definition"></a>Definizione  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|Identifica in modo univoco un articolo pubblicato.|  
|**srvid**|**smallint**|ID del Sottoscrittore.|  
|**dest_db**|**sysname**|Nome del database di destinazione.|  
|**login_name**|**sysname**|Nome dell'account di accesso utilizzato quando si aggiunge la sottoscrizione.|  
|**distribution_jobid**|**binary(16)**|ID del processo dell'agente di distribuzione|  
|**timestamp**|**timestamp**|Data e ora di creazione della sottoscrizione.|  
|**queued_reinit**|**bit**|Specifica se l'articolo è contrassegnato per l'inizializzazione o la reinizializzazione. Il valore **1** indica che l'articolo sottoscritto è contrassegnato per l'inizializzazione o la reinizializzazione.|  
|**Stato**|**tinyint**|Stato della sottoscrizione:<br /><br /> **0** = inattivo.<br /><br /> **1** = sottoscritto.<br /><br /> **2** = attivo.|  
|**sync_type**|**tinyint**|Tipo di sincronizzazione iniziale:<br /><br /> **1** = automatico.<br /><br /> **2** = nessuna.|  
|**subscription_type**|**int**|Tipo di sottoscrizione:<br /><br /> **0** = push: l'agente di distribuzione viene eseguito nel Sottoscrittore.<br /><br /> **1** = pull: l'agente di distribuzione viene eseguito nel server di distribuzione.|  
|**update_mode**|**tinyint**|Modalità di aggiornamento:<br /><br /> **0** = sola lettura.<br /><br /> **1** = aggiornamento immediato.|  
|**loopback_detection**|**bit**|Si applica alle sottoscrizioni che fanno parte di una topologia di replica transazionale bidirezionale. Il rilevamento di loopback determina se l'agente di distribuzione deve inviare nuovamente al Sottoscrittore le transazioni provenienti dal Sottoscrittore:<br /><br /> **0** = restituisce.<br /><br /> **1** = non viene restituito.|  
  
## <a name="see-also"></a>Vedere anche  
 [Replica di database eterogenei](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelle di replica &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste di replica &#40;&#41;Transact-SQL ](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addsubscription &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
