---
title: sysarticlecolumns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticlecolumns
- sysarticlecolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticlecolumns system table
ms.assetid: 55918592-e05d-43b6-843b-7e4d82fa6275
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4d31293e6e6b562e8ccfbb624a9ea9e226205ef2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62714188"
---
# <a name="sysarticlecolumns-transact-sql"></a>sysarticlecolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **sysarticlecolumns** tabella contiene una riga per ogni colonna della tabella è pubblicata in una pubblicazione snapshot o transazionale che esegue il mapping di ogni colonna per l'articolo. Questa tabella è archiviata nel database di pubblicazione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Identifica un articolo.|  
|**colid**|**smallint**|Identifica una colonna di un articolo.|  
|**is_udt**|**bit**|Indica se il tipo di dati della colonna è un tipo definito dall'utente (UDT). Un valore pari **1** indica una colonna con tipo definito dall'utente.|  
|**is_xml**|**bit**|Indica se la colonna è un' **xml** colonna. Un valore pari **1** indica una colonna xml.|  
|**is_max**|**bit**|Indica se la colonna è una colonna di tipo, valori di grandi dimensioni **varchar (max)**, **nvarchar (max)**, e **varbinary (max)**. Un valore pari **1** indica una colonna con valori di grandi dimensioni.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
