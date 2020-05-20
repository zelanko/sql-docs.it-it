---
title: IHpublishertables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishertables
- IHpublishertables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishertables system table
ms.assetid: 7d16ac39-633a-4fe2-8f22-1d9afc191ee9
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f9c80d1f3a4ac02cac11c4ecbd912fe766a58050
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82813241"
---
# <a name="ihpublishertables-transact-sql"></a>IHpublishertables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabella di sistema **IHpublishertables** rappresenta i metadati archiviati nel server di pubblicazione. Questa tabella contiene una riga per ogni tabella di origine pubblicata da un server di pubblicazione non SQL Server tramite il server di distribuzione corrente. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|Identificatore della tabella pubblicata.|  
|**publisher_id**|**smallint**|Identificatore del server di pubblicazione non SQL Server dal quale la tabella viene pubblicata.|  
|**name**|**sysname**|Nome della tabella pubblicata.|  
|**proprietario**|**sysname**|Proprietario della tabella.|  
  
## <a name="see-also"></a>Vedere anche  
 [Replica di database eterogenei](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelle di replica &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
