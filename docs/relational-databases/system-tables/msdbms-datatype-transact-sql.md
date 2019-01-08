---
title: MSdbms_datatype (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_datatype
- MSdbms_datatype_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_datatype system table
ms.assetid: 606168cc-79a8-442f-ab43-936f8f884d72
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bf246256471931292d6dfcee8a83386bce256e08
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52810543"
---
# <a name="msdbmsdatatype-transact-sql"></a>MSdbms_datatype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSdbms_datatype** tabella contiene l'elenco completo dei tipi di dati nativi in ogni sistema di gestione supportate del database (DBMS) utilizzato come server di pubblicazione o sottoscrittore nella replica di database eterogenei. Questa tabella è archiviata nel **msdb** database.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**datatype_id**|**int**|Identifica ogni tipo di dati univoco.|  
|**dbms_id**|**int**|Identifica il sistema DBMS al quale appartiene il tipo.|  
|**type**|**sysname**|Nome del tipo di dati (nativo).|  
|**CreateParams**|**int**|Mappa di bit che descrive la combinazione di lunghezza, precisione e scala valida per ogni tipo di dati, che include:<br /><br /> **0x1** = PRECISION.<br /><br /> **0x2** = scala.<br /><br /> **0x4** = lunghezza.|  
  
## <a name="remarks"></a>Note  
 Questa tabella contiene le voci per i tipi di dati di SQL Server perché un'istanza di SQL Server può sottoscrivere un database non SQL Server sia per un sottoscrittore non SQL Server di pubblicazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Replica di database eterogenei](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Specificare i mapping dei tipi di dati per un server di pubblicazione Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
