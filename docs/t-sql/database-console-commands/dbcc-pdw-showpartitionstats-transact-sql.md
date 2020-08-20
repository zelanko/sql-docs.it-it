---
description: DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL)
title: DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL)
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
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 03ef74fb824c39aee0045f378f6aaf5268052794
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479838"
---
# <a name="dbcc-pdw_showpartitionstats-transact-sql"></a>DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL)

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

Visualizza le dimensioni e il numero di righe di ogni partizione di una tabella in un database [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].
  
![Icona di collegamento a un articolo](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un articolo") [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
Show the partition stats for a table  
DBCC PDW_SHOWPARTITIONSTATS ( " [ database_name . [ schema_name ] . ] | [ schema_name.] table_name  ")  
[;]  
```  

## <a name="arguments"></a>Argomenti  
 `[ database_name . [ schema_name ] . | schema_name . ] table_name`  
 Il nome di tabella composto da una, due o tre parti da visualizzare.  Per i nomi di tabella composti da due o tre parti, il nome deve essere racchiuso tra virgolette doppie (""). L'uso delle virgolette nei nomi di tabella composti da una sola parte è facoltativo.  
  
## <a name="permissions"></a>Autorizzazioni
È richiesta l'autorizzazione **VIEW SERVER STATE**.
  
## <a name="result-sets"></a>Set di risultati  
Questo set include i risultati del comando DBCC PDW_SHOWPARTITIONSTATS.
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|partition_number|INT|Numero di partizioni.|  
|used_page_count|bigint|Numero totale di pagine usate per i dati.|  
|reserved_page_count|bigint|Numero di pagine riservate per la partizione.|  
|row_count|bigint|Numero di righe nella partizione.|  
|pdw_node_id|INT|Nodo di calcolo per i dati.|  
|distribution_id|INT|Identificatore di distribuzione per i dati.|  
  
## <a name="examples-sssdw-and-sspdw"></a>Esempi: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdw_showpartitionstats-basic-syntax-examples"></a>R. Esempi di sintassi di base DBCC PDW_SHOWPARTITIONSTATS  
Gli esempi seguenti visualizzano lo spazio usato e il numero di righe per partizione per la tabella FactInternetSales nel database [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)].
  
```sql
DBCC PDW_SHOWPARTITIONSTATS ("ssawPDW.dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS ("dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS (FactInternetSales);  
```  

## <a name="see-also"></a>Vedere anche

- [DBCC PDW_SHOWEXECUTIONPLAN &#40;Transact-SQL&#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
- [DBCC PDW_SHOWSPACEUSED &#40;Transact-SQL&#41;](dbcc-pdw-showspaceused-transact-sql.md)  
