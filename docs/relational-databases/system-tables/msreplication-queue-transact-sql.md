---
description: MSreplication_queue (Transact-SQL)
title: MSreplication_queue (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_queue
- MSreplication_queue_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_queue system table
ms.assetid: 664bf817-8021-4417-96d6-2bb1e4baabff
author: markingmyname
ms.author: maghan
ms.openlocfilehash: caabac10703a39aa88afd357fd1596379f82978d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538258"
---
# <a name="msreplication_queue-transact-sql"></a>MSreplication_queue (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabella **MSreplication_queue** viene utilizzata dal processo di replica per archiviare i comandi in coda eseguiti da tutte le sottoscrizioni ad aggiornamento in coda che utilizzano la coda basata su SQL. Questa tabella è archiviata nel database di sottoscrizione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**pubblicazione**|**sysname**|Nome del server di pubblicazione.|  
|**publisher_db**|**sysname**|Nome del database di pubblicazione.|  
|**pubblicazione**|**sysname**|Nome della pubblicazione.|  
|**tranid**|**sysname**|ID di transazione utilizzato per l'esecuzione del comando in coda.|  
|**data**|**varbinary(8000)**|Flusso di byte compresso in cui sono archiviate informazioni sul comando in coda.|  
|**datalen**|**int**|Lunghezza dei dati in byte.|  
|**CommandType**|**int**|Tipo di comando che viene inserito in coda:<br /><br /> 1 = Comando utente nella transazione.<br /><br /> 2 = Comando di sincronizzazione della sottoscrizione.|  
|**insertdate**|**datetime**|Data dell'inserimento.|  
|**orderkey**|**bigint**|Colonna Identity incrementata in modo monotonico.|  
|**cmdstate**|**bit**|Stato del comando:<br /><br /> 0 = Completo.<br /><br /> 1 = Parziale.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
