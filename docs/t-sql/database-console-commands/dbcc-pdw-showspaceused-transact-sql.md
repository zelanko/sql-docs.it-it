---
title: DBCC PDW_SHOWSPACEUSED (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
author: pmasl
ms.author: umajay
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: fc06dca68c6b6a4cedc730433401076ca07b126b
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "59042340"
---
# <a name="dbcc-pdwshowspaceused-transact-sql"></a>DBCC PDW_SHOWSPACEUSED (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Visualizza il numero di righe, lo spazio su disco riservato e lo spazio su disco usato per una tabella specifica o per tutte le tabelle in un database [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```sql
-- Show the space used for all user tables and system tables in the current database  
DBCC PDW_SHOWSPACEUSED  
[;]  
  
-- Show the space used for a table  
DBCC PDW_SHOWSPACEUSED ( " [ database_name . [ schema_name ] . ] | [ schema_name .] table_name  " )  
[;]  
```  
  
## <a name="arguments"></a>Argomenti  
 `[ database_name . [ schema_name ] . | schema_name . ] table_name`  
 Il nome di tabella composto da una, due o tre parti da visualizzare. Per i nomi di tabella composti da due o tre parti, il nome deve essere racchiuso tra virgolette doppie (""). L'uso delle virgolette nei nomi di tabella composti da una parte è facoltativo. Quando non viene specificato alcun nome di tabella, vengono visualizzate le informazioni per il database corrente.  
  
## <a name="permissions"></a>Autorizzazioni  
È richiesta l'autorizzazione VIEW SERVER STATE.
  
## <a name="result-sets"></a>Set di risultati  
Il set di risultati per tutte le tabelle è il seguente.
  
|colonna|Tipo di dati|Descrizione|  
|------------|---------------|-----------------|  
|reserved_space|BIGINT|Spazio totale usato per il database, in KB.|  
|data_space|BIGINT|Spazio usato per i dati, in KB.|  
|index_space|BIGINT|Spazio usato per gli indici, in KB.|  
|unused_space|BIGINT|Spazio che è parte dello spazio riservato e non usato, in KB.|  
|pdw_node_id|INT|Nodo di calcolo usato per i dati.|  
  
Il set di risultati per una tabella è il seguente.
  
|colonna|Tipo di dati|Descrizione|Intervallo|  
|------------|---------------|-----------------|-----------|  
|rows|BIGINT|Numero di righe.||  
|reserved_space|BIGINT|Spazio totale riservato per l'oggetto, in KB.||  
|data_space|BIGINT|Spazio usato per i dati, in KB.||  
|index_space|BIGINT|Spazio usato per gli indici, in KB.||  
|unused_space|BIGINT|Spazio che è parte dello spazio riservato e non usato, in KB.||  
|pdw_node_id|INT|Nodo di calcolo usato per i report relativi all'uso dello spazio.||  
|distribution_id|INT|Distribuzione usata per i report relativi all'uso dello spazio.|Il valore è -1 per le tabelle replicate.|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowspaceused-basic-syntax"></a>A. Sintassi di base di DBCC PDW_SHOWSPACEUSED  
Gli esempi seguenti illustrano i diversi modi di visualizzare il numero di righe, lo spazio su disco riservato e lo spazio su disco usato dalla tabella FactInternetSales nel database [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)].
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012.dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012..FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( FactInternetSales );  
```  
  
### <a name="b-show-the-disk-space-used-by-all-tables-in-the-current-database"></a>B. Visualizzare lo spazio su disco usato da tutte le tabelle nel database corrente  
 L'esempio seguente visualizza lo spazio su disco riservato e usato da tutte le tabelle utente e le tabelle di sistema nel database [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)].  
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED;  
```  
 ## <a name="see-also"></a>Vedere anche
[DBCC PDW_SHOWEXECUTIONPLAN &#40;Transact-SQL&#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWPARTITIONSTATS &#40;Transact-SQL&#41;](dbcc-pdw-showpartitionstats-transact-sql.md)

  
