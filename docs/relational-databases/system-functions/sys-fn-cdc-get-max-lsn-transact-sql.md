---
title: sys.fn_cdc_get_max_lsn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_cdc_get_max_lsn
- fn_cdc_get_max_lsn
- fn_cdc_get_max_lsn_TSQL
- sys.fn_cdc_get_max_lsn_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_max_lsn
- sys.fn_cdc_get_max_lsn
ms.assetid: 93f3a4c8-b91f-4ebb-8e96-9397bb3a1c43
author: rothja
ms.author: jroth
ms.openlocfilehash: c51a69eb3604b937b9bf2aaf9a09aa383f2c1490
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046454"
---
# <a name="sysfncdcgetmaxlsn-transact-sql"></a>sys.fn_cdc_get_max_lsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce il numero di sequenza massima del log (LSN) nella colonna start_lsn il [CDC. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) tabella di sistema. È possibile utilizzare questa funzione per restituire l'endpoint superiore della cronologia dell'acquisizione dei dati delle modifiche per qualsiasi istanza di acquisizione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.fn_cdc_get_max_lsn ()  
```  
  
## <a name="return-types"></a>Tipi restituiti  
 **binary(10)**  
  
## <a name="remarks"></a>Note  
 Questa funzione restituisce il valore LSN massimo nella colonna start_lsn della [CDC. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) tabella. Pertanto, è l'ultimo valore LSN elaborato dal processo di acquisizione quando le modifiche vengono propagate alle tabelle delle modifiche del database. Viene utilizzato come endpoint superiore per tutte le cronologie associate alle istanze di acquisizione definite per il database.  
  
 La funzione viene utilizzata in genere per ottenere un endpoint superiore appropriato per un intervallo di query.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo del database public.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-returning-the-maximum-lsn-value"></a>R. Restituzione del valore LSN massimo  
 Nell'esempio seguente viene restituito il valore LSN massimo per tutte le istanze di acquisizione nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
SELECT sys.fn_cdc_get_max_lsn()AS max_lsn;  
```  
  
### <a name="b-setting-the-high-endpoint-of-a-query-range"></a>B. Impostazione dell'endpoint superiore di un intervallo di query  
 Nell'esempio seguente è utilizzato il numero LSN massimo restituito da `sys.fn_cdc_get_max_lsn` per impostare l'endpoint superiore per un intervallo di query per l'istanza di acquisizione `HumanResources_Employee`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10);  
SET @from_lsn = sys.fn_cdc_get_min_lsn(N'HumanResources_Employee');  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
SELECT * FROM cdc.fn_cdc_get_all_changes_HumanResources_Employee(@from_lsn, @to_lsn, 'all');  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sys.fn_cdc_get_min_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md)   
 [Log delle transazioni &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)  
  
  
