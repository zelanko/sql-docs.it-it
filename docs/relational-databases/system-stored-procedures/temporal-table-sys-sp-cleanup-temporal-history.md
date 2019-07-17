---
title: Sys.sp_cleanup_temporal_history | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 6eff30b4-b261-4f1f-b93c-1f69d754298d
author: CarlRabeler
ms.author: carlrab
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 111986a771b9cfb156c0d37688565b39401411f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037235"
---
# <a name="sysspcleanuptemporalhistory-transact-sql"></a>Sys.sp_cleanup_temporal_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

Rimuove tutte le righe dalla tabella di cronologia temporale che corrispondono a periodo HISTORY_RETENTION configurato all'interno di una singola transazione.
  
## <a name="syntax"></a>Sintassi  
```  
sp_cleanup_temporal_history [@schema_name = ] schema_name, [@table_name = ] table_name [, [@row_count=] @row_count_var [OUTPUT]]
```  
  
## <a name="arguments"></a>Argomenti  

*@table_name*

Il nome della tabella temporale per la conservazione del quale viene richiamata pulizia.

*schema_name*

Il nome dello schema a cui appartiene la tabella temporale corrente a

*row_count_var* [OUTPUT]

Il parametro di output che restituisce in numero di righe eliminate. Se la tabella di cronologia con indice cluster columnstore, questo parametro restituirà sempre 0.
  
## <a name="remarks"></a>Note
Questa stored procedure può essere utilizzata solo con le tabelle temporali che have un periodo di conservazione specificato.
Utilizzare questa stored procedure solo se è necessario eliminare immediatamente tutte le righe obsolete dalla tabella di cronologia. È necessario sapere che può avere un impatto significativo sul log del database e del sottosistema dei / o come vengono eliminate tutte le righe idonee nella stessa transazione. 

È sempre consigliabile fare affidamento su un'attività in background interno per la pulizia che rimuove le righe con un impatto minimo sul database in generale e i carichi di lavoro normali di obsolete.

## <a name="permissions"></a>Permissions  
 Richiede autorizzazioni db_owner.  

## <a name="example"></a>Esempio

```
declare @rowcnt int
EXEC sys.sp_cleanup_temporal_history 'dbo', 'Department', @rowcnt output
select @rowcnt
```

## <a name="see-also"></a>Vedere anche

[Criteri di conservazione delle tabelle temporali](https://docs.microsoft.com/azure/sql-database/sql-database-temporal-tables-retention-policy)
