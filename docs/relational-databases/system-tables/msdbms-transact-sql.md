---
title: MSdbms (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_TSQL
- MSdbms
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms system table
ms.assetid: 2be631bf-de09-4e7a-9ccb-d6c37b81c237
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e21108f2fccbc614fc71ff6ae132ae14cd457ea7
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890001"
---
# <a name="msdbms-transact-sql"></a>MSdbms (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabella **MSdbms** contiene un elenco principale di tutte le versioni dei sistemi di gestione di database (DBMS) supportate per la replica di database eterogenei. Questa tabella è archiviata nel database **msdb** .  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**dbms_id**|**int**|Identifica ogni versione e DBMS univoci.|  
|**DBMS**|**sysname**|Il nome DBMS.<br /><br /> MSSQLSERVER<br /><br /> DB2<br /><br /> ORACLE<br /><br /> SYBASE|  
|**version**|**varchar (10)**|La versione DBMS.|  
  
## <a name="see-also"></a>Vedere anche  
 [Replica di database eterogenei](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelle di replica &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
