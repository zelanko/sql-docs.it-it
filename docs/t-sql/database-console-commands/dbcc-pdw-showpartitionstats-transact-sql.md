---
title: DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: pmasl
ms.author: umajay
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 8d53158198b2df5ae5aaa0fbc3b176bdcd544367
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/09/2019
ms.locfileid: "57684912"
---
# <a name="dbcc-pdwshowpartitionstats-transact-sql"></a>DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Visualizza le dimensioni e il numero di righe di ogni partizione di una tabella in un database [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].
  
![Icona di collegamento ad articolo](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento ad articolo") [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```sql
Show the partition stats for a table  
DBCC PDW_SHOWPARTITIONSTATS ( " [ database_name . [ schema_name ] . ] | [ schema_name.] table_name  ")  
[;]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ *database_name* . [ *schema_name* ] . | *schema_name* . ] *table_name*  
 Il nome di tabella composto da una, due o tre parti da visualizzare.  Per i nomi di tabella composti da due o tre parti, il nome deve essere racchiuso tra virgolette doppie (""). L'uso delle virgolette nei nomi di tabella composti da una sola parte è facoltativo.  
  
## <a name="permissions"></a>Permissions
È richiesta l'autorizzazione **VIEW SERVER STATE**.
  
## <a name="result-sets"></a>Set di risultati  
Questo set include i risultati del comando DBCC PDW_SHOWPARTITIONSTATS.
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|partition_number|INT|Numero di partizioni.|  
|used_page_count|BIGINT|Numero totale di pagine usate per i dati.|  
|reserved_page_count|BIGINT|Numero di pagine riservate per la partizione.|  
|row_count|BIGINT|Numero di righe nella partizione.|  
|pdw_node_id|INT|Nodo di calcolo per i dati.|  
|distribution_id|INT|Identificatore di distribuzione per i dati.|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowpartitionstats-basic-syntax-examples"></a>A. Esempi di sintassi di base DBCC PDW_SHOWPARTITIONSTATS  
Gli esempi seguenti visualizzano lo spazio usato e il numero di righe per partizione per la tabella FactInternetSales nel database [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)].
  
```sql
DBCC PDW_SHOWPARTITIONSTATS ("ssawPDW.dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS ("dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS (FactInternetSales);  
```  
## <a name="see-also"></a>Vedere anche
[DBCC PDW_SHOWEXECUTIONPLAN &#40;Transact-SQL&#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED &#40;Transact-SQL&#41;](dbcc-pdw-showspaceused-transact-sql.md)  
 