---
description: sysarticlecolumns (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 142ed0bfaad34607422b69929450ae9f7b09bd9e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540224"
---
# <a name="sysarticlecolumns-transact-sql"></a>sysarticlecolumns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabella **sysarticlecolumns** contiene una riga per ogni colonna di tabella pubblicata in una pubblicazione snapshot o transazionale ed esegue il mapping di ogni colonna al relativo articolo. Questa tabella è archiviata nel database di pubblicazione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Identifica un articolo.|  
|**colid**|**smallint**|Identifica una colonna di un articolo.|  
|**is_udt**|**bit**|Indica se il tipo di dati della colonna è un tipo definito dall'utente (UDT). Il valore **1** indica una colonna con tipo definito dall'utente.|  
|**is_xml**|**bit**|Indica se la colonna è una colonna **XML** . Il valore **1** indica una colonna XML.|  
|**is_max**|**bit**|Indica se la colonna è una colonna con tipo di dati con valori di grandi dimensioni, **varchar (max)**, **nvarchar (max)** e **varbinary (max)**. Il valore **1** indica una colonna con valori di grandi dimensioni.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
