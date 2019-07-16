---
title: MSdbms_datatype_mapping (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_datatype_mapping_TSQL
- MSdbms_datatype_mapping
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_datatype_mapping system table
ms.assetid: 13289a0b-dfb0-4771-ad80-4c5f83cded99
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9a1042bb3aa7b6113121693cc66440ebbf81ce1b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907538"
---
# <a name="msdbmsdatatypemapping-transact-sql"></a>MSdbms_datatype_mapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSdbms_datatype_mapping** tabella contiene i mapping dei tipi di dati consentiti dal tipo di dati nel sistema di gestione di database (DBMS) origine a uno o più tipi di dati specifici nel sistema DBMS di destinazione. Questa tabella è archiviata nel **msdb** del database e viene usato per la replica di database eterogenei.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**datatype_mapping_id**|**int**|Identifica ogni mapping univoco di tipi di dati.|  
|**map_id**|**int**|Identifica il tipo di dati di origine.|  
|**dest_datatype_id**|**int**|Identifica il tipo di dati di destinazione.|  
|**dest_precision**|**bigint**|Definisce la precisione del tipo di dati di destinazione, in cui un valore NULL indica che la precisione non viene utilizzata, e il valore **-1** indica che viene utilizzata la precisione del tipo di dati di origine.|  
|**dest_scale**|**int**|Definisce la scala del tipo di dati di destinazione, in cui un valore NULL indica che la scala non viene utilizzata, e il valore **-1** indica che viene utilizzata la scala del tipo di dati di origine.|  
|**dest_length**|**bigint**|Definisce la lunghezza del tipo di dati di destinazione, in cui un valore NULL indica che la lunghezza non viene utilizzata, e il valore **-1** indica che viene utilizzata la lunghezza del tipo di dati di origine.|  
|**dest_nullable**|**bit**|Specifica se la colonna di destinazione nel mapping ammette valori NULL. Il valore NULL indica che questa definizione non è necessaria.|  
|**dest_createparams**|**int**|Mappa di bit che descrive quale combinazione di lunghezza, precisione e scala è applicabile a ogni tipo di dati. Sono disponibili i valori seguenti:<br /><br /> **0x1** = PRECISION.<br /><br /> **0x2** = scala.<br /><br /> **0x4** = lunghezza.|  
  
## <a name="see-also"></a>Vedere anche  
 [Replica di database eterogenei](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Specificare i mapping dei tipi di dati per un server di pubblicazione Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
