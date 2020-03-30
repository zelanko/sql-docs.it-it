---
title: Query | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5ff02a32-e8d3-479c-ae8b-07581e41f5f8
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 79afe251de0561bbf9dda840eb9ce578efa94b80
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68141296"
---
# <a name="queries"></a>Query

[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Data Manipulation Language (DML) è un vocabolario usato per recuperare e utilizzare i dati in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e nel database SQL. Questo linguaggio è per la maggior parte utilizzabile anche in SQL Data Warehouse e PDW (vedere ogni singola istruzione per i dettagli). Utilizzare queste istruzioni per operazioni di aggiunta, modifica, esecuzione di query o rimozione dei dati di un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 Nella tabella seguente vengono elencate le istruzioni DML utilizzate da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|||  
|-|-|  
|[BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)|[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)|  
|[DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)|  
|[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)|[UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)|  
|[MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)|[WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)|  
|[READTEXT &#40;Transact-SQL&#41;](../../t-sql/queries/readtext-transact-sql.md)| &nbsp; |  
| &nbsp; | &nbsp; |

 Nella tabella seguente vengono elencate le clausole utilizzate in più istruzioni o clausole DML.  
  
|Clausola|Può essere utilizzata in queste istruzioni|  
|------------|-------------------------------------|  
|[FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)|DELETE, SELECT, UPDATE|  
|[Hint &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql.md)|DELETE, INSERT, SELECT, UPDATE|  
|[Clausola OPTION &#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md)|DELETE, SELECT, UPDATE|  
|[Clausola OUTPUT &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md)|DELETE, INSERT, MERGE, UPDATE|  
|[Condizione di ricerca &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md)|DELETE, MERGE, SELECT, UPDATE|  
|[Costruttore di valori di tabella &#40;Transact-SQL&#41;](../../t-sql/queries/table-value-constructor-transact-sql.md)|FROM, INSERT, MERGE|  
|[TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md)|DELETE, INSERT, MERGE, SELECT, UPDATE|  
|[WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)|DELETE, SELECT, UPDATE, MATCH|  
|[WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)|DELETE, INSERT, MERGE, SELECT, UPDATE|  
| &nbsp; | &nbsp; |
