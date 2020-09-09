---
description: MSrepl_errors (Transact-SQL)
title: MSrepl_errors (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_errors
- MSrepl_errors_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_errors system table
ms.assetid: c6e023c1-2c32-4269-8d76-e442ea309e4b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5afa86de5a33eab4f7e77da1c825619a738381de
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540280"
---
# <a name="msrepl_errors-transact-sql"></a>MSrepl_errors (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabella **MSrepl_errors** contiene righe con informazioni estese su agente di distribuzione e agente di merge errore. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID dell'errore.|  
|**time**|**datetime**|Ora in cui si è verificato l'errore.|  
|**error_type_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**source_type_id**|**int**|ID del tipo di origine dell'errore.|  
|**source_name**|**nvarchar (100)**|Nome dell'origine dell'errore.|  
|**error_code**|**sysname**|Codice di errore.|  
|**error_text**|**ntext**|Messaggio di errore.|  
|**xact_seqno**|**varbinary(16)**|Numero di sequenza iniziale del log delle transazioni per il batch con errori di esecuzione. Viene utilizzato solo dagli agenti di distribuzione e corrisponde al numero di sequenza del log delle transazioni per la prima transazione nel batch con errori di esecuzione.|  
|**command_id**|**int**|ID di comando del batch che ha avuto esito negativo. Viene utilizzato solo dagli agenti di distribuzione e corrisponde all'ID del primo comando di tale batch.|  
|**session_id**|**int**|ID della sessione dell'agente in cui si è verificato l'errore.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
