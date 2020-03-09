---
title: CREATE MATERIALIZED VIEW AS SELECT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: data-warehouse
ms.topic: language-reference
f1_keywords:
- CREATE VIEW
- VIEW_TSQL
- VIEW
- CREATE_VIEW_TSQL
- SCHEMABINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- table creation [SQL Server], CREATE VIEW
- views [SQL Server], creating
- CREATE VIEW statement
- updatable partitioned views
- tables [SQL Server], virtual
- updatable views
- modifying partitioned views
- virtual tables [SQL Server]
- number of columns per view
- partitioned views [SQL Server], creating
- WITH ENCRYPTION clause
- WITH CHECK OPTION clause
- partitioned views [SQL Server], modifying
- partitioned views [SQL Server], replication
- distributed partitioned views [SQL Server]
- views [SQL Server], indexed views
- maximum number of columns per view
ms.assetid: aecc2f73-2ab5-4db9-b1e6-2f9e3c601fb9
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: f0f244c15f4183f3214ae28efc2bf3300c571f0e
ms.sourcegitcommit: 85b26bc1abbd8d8e2795ab96532ac7a7e01a954f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2020
ms.locfileid: "78335755"
---
# <a name="create-materialized-view-as-select-transact-sql"></a>CREATE MATERIALIZED VIEW AS SELECT (Transact-SQL)  

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Questo articolo illustra l'istruzione T-SQL CREATE MATERIALIZED VIEW AS SELECT in Azure SQL Data Warehouse per lo sviluppo di soluzioni. L'articolo include anche esempi di codice.

Una vista materializzata rende persistenti i dati restituiti dalla query di definizione della vista e viene aggiornata automaticamente in caso di modifiche dei dati nelle tabelle sottostanti.   Migliora le prestazioni delle query complesse, in genere le query con join e aggregazioni, offrendo allo stesso tempo operazioni di manutenzione semplici.   Con la funzionalità di corrispondenza automatica del piano di esecuzione, non sarà necessario fare riferimento a una vista materializzata nella query per fare in modo che Query Optimizer prenda in considerazione la vista per la sostituzione.  Questa funzionalità consente ai progettisti dei dati di implementare le viste materializzate come meccanismo per migliorare il tempo di risposta delle query, senza doverle modificare.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
CREATE MATERIALIZED VIEW [ schema_name. ] materialized_view_name
    WITH (  
      <distribution_option>
    )
    AS <select_statement>
[;]

<distribution_option> ::=
    {  
        DISTRIBUTION = HASH ( distribution_column_name )  
      | DISTRIBUTION = ROUND_ROBIN  
    }

<select_statement> ::=
    SELECT select_criteria
```  
  
## <a name="arguments"></a>Argomenti

*schema_name*     
 Nome dello schema a cui appartiene la vista.  
  
*materialized_view_name*   
Nome della vista. I nomi di vista devono essere conformi alle regole per gli identificatori. Il nome del proprietario della vista è facoltativo.  

*Opzione di distribuzione*     
Sono supportate solo le distribuzioni HASH e ROUND_ROBIN.

*select_statement*   
L'elenco SELECT nella definizione della vista materializzata deve soddisfare almeno uno di questi due criteri:
- L'elenco SELECT contiene una funzione di aggregazione.
- Viene usata l'istruzione GROUP BY nella definizione della vista materializzata e tutte le colonne in GROUP BY vengono incluse nell'elenco SELECT.  Nella clausola GROUP BY si possono usare fino a 32 colonne.

Sono necessarie funzioni di aggregazione nell'elenco SELECT della definizione della vista materializzata.  Le aggregazioni supportate includono MAX, MIN, AVG, COUNT, COUNT_BIG, SUM, VAR, STDEV.

Se si usano le aggregazioni MIN/MAX nell'elenco SELECT della definizione della vista materializzata, si applicano i requisiti seguenti:
 
- FOR_APPEND è obbligatorio.  Ad esempio:
  ```sql 
  CREATE MATERIALIZED VIEW mv_test2  
  WITH (distribution = hash(i_category_id), FOR_APPEND)  
  AS
  SELECT MAX(i.i_rec_start_date) as max_i_rec_start_date, MIN(i.i_rec_end_date) as min_i_rec_end_date, i.i_item_sk, i.i_item_id, i.i_category_id
  FROM syntheticworkload.item i  
  GROUP BY i.i_item_sk, i.i_item_id, i.i_category_id
  ```

- La vista materializzata verrà disabilitata quando si verifica un'operazione UPDATE o DELETE nelle tabelle di base a cui viene fatto riferimento.  Questa restrizione non si applica alle operazioni INSERT.  Per abilitare nuovamente la vista materializzata, eseguire ALTER MATERIALIZED INDEX con REBUILD.
  
## <a name="remarks"></a>Osservazioni

Una vista materializzata nel data warehouse di Azure è simile a una vista indicizzata in SQL Server.  Condivide quasi le stesse restrizioni della vista indicizzata (vedere [Creare viste indicizzate](/sql/relational-databases/views/create-indexed-views) per informazioni dettagliate) ad eccezione del fatto che una vista materializzata supporta le funzioni di aggregazione.   

La vista materializzata supporta solo CLUSTERED COLUMNSTORE INDEX. 

Una vista materializzata non può fare riferimento ad altre viste.  

Non è possibile creare una vista materializzata in una tabella con Maschera dati dinamica (DDM), anche se la colonna DDM non fa parte della vista materializzata.  Se una colonna della tabella fa parte di una vista materializzata attiva o una vista materializzata disabilitata, non è possibile aggiungere DDM a questa colonna.  

Non è possibile creare una vista materializzata in una tabella con sicurezza a livello di riga abilitata.

È possibile creare viste materializzate su tabelle partizionate.  Le operazioni SPLIT/MERGE sulle partizioni sono supportate per le tabelle di base delle viste materializzate. L'operazione SWITCH per una partizione non è supportata.  
 
Le operazioni ALTER TABLE SWITCH non sono supportate sulle tabelle a cui fanno riferimento le viste materializzate. Disabilitare o eliminare le viste materializzate prima di usare ALTER TABLE SWITCH. Negli scenari seguenti la creazione della vista materializzata richiede l'aggiunta di nuove colonne alla vista materializzata:

|Scenario|Nuove colonne da aggiungere alla vista materializzata|Comment|  
|-----------------|---------------|-----------------|
|COUNT_BIG() non è presente nell'elenco SELECT di una definizione di vista materializzata| COUNT_BIG (*) |Viene aggiunta automaticamente dalla creazione di una vista materializzata.  Non è richiesta alcuna azione da parte dell'utente.|
|La funzione SUM(a) viene specificata dagli utenti nell'elenco SELECT della definizione di una vista materializzata e 'a' è un'espressione che ammette i valori Null |COUNT_BIG (a) |Gli utenti devono aggiungere l'espressione 'a' manualmente nella definizione della vista materializzata.|
|La funzione AVG(a) viene specificata dagli utenti nell'elenco SELECT della definizione di una vista materializzata e 'a' è un'espressione.|SUM(a), COUNT_BIG(a)|Viene aggiunta automaticamente dalla creazione di una vista materializzata.  Non è richiesta alcuna azione da parte dell'utente.|
|La funzione STDEV(a) viene specificata dagli utenti nell'elenco SELECT della definizione di una vista materializzata e 'a' è un'espressione.|SUM(a), COUNT_BIG(a), SUM(square(a))|Viene aggiunta automaticamente dalla creazione di una vista materializzata.  Non è richiesta alcuna azione da parte dell'utente. |
| | | |

Dopo la creazione, le viste materializzate sono visibili all'interno di SQL Server Management Studio nella cartella views dell'istanza di Azure SQL Data Warehouse.

Gli utenti possono eseguire [SP_SPACEUSED](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql?view=azure-sqldw-latest) e [DBCC PDW_SHOWSPACEUSED](/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql?view=azure-sqldw-latest) per determinare lo spazio usato da una vista materializzata.  

È possibile eliminare una vista materializzata tramite DROP VIEW.  È possibile usare ALTER MATERIALIZED VIEW per disabilitare o ricostruire una vista materializzata.   

EXPLAIN PLAN e il piano di esecuzione stimato grafico in SQL Server Management Studio possono indicare se una vista materializzata viene presa in considerazione da Query Optimizer per l'esecuzione delle query. Il piano di esecuzione stimato grafico in SQL Server Management Studio può indicare se una vista materializzata viene presa in considerazione da Query Optimizer per l'esecuzione delle query.

Per scoprire se un'istruzione SQL può trarre vantaggio da una nuova vista materializzata, eseguire il comando `EXPLAIN` con `WITH_RECOMMENDATIONS`.  Per informazioni dettagliate, vedere [EXPLAIN (Transact-SQL)](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest).

## <a name="permissions"></a>Autorizzazioni

Sono richieste l'autorizzazione CREATE VIEW per il database e l'autorizzazione ALTER per lo schema in cui viene creata la vista. 
  
## <a name="see-also"></a>Vedere anche

[Ottimizzazione delle prestazioni con vista materializzata](/azure/sql-data-warehouse/performance-tuning-materialized-views)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)      
[DROP VIEW](/sql/t-sql/statements/drop-view-transact-sql?view=azure-sqldw-latest)  
[EXPLAIN &#40;Transact-SQL&#41;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-column-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_mappings &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[Viste del catalogo di SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Viste di sistema supportate in Azure SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Istruzioni T-SQL supportate in Azure SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
