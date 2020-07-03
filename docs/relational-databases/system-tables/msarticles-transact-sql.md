---
title: MSarticles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSarticles
- MSarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSarticles system table
ms.assetid: 1acd79a5-b3e2-4161-9592-7acc2a41ba38
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d6272b8370b461db0a7a2259be3de4d584ea8498
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890050"
---
# <a name="msarticles-transact-sql"></a>MSarticles (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabella **MSarticles** contiene una riga per ogni articolo replicato da un server di pubblicazione. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|ID del server di pubblicazione.|  
|**publisher_db**|**sysname**|Nome del database del server di pubblicazione.|  
|**publication_id**|**int**|ID della pubblicazione.|  
|**articolo**|**sysname**|Nome dell'articolo.|  
|**article_id**|**int**|ID dell'articolo.|  
|**destination_object**|**sysname**|Nome della tabella creata nel Sottoscrittore.|  
|**source_owner**|**sysname**|Nome dello schema della tabella di origine nel server di pubblicazione.|  
|**source_object**|**sysname**|Nome dell'oggetto di origine da cui aggiungere l'articolo.|  
|**Descrizione**|**nvarchar(255)**|Descrizione dell'articolo.|  
|**destination_owner**|**sysname**|Nome dello schema della tabella creata nel Sottoscrittore.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
