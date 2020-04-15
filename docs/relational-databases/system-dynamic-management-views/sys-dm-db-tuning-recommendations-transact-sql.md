---
title: metodo sys.dm_db_tuning_recommendations (Transact-SQL) Documenti Microsoft
description: Informazioni su come trovare potenziali problemi di prestazioni e correzioni consigliate in SQL Server e nel database SQL di Azure
ms.custom: ''
ms.date: 07/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_tuning_recommendations
- dm_db_tuning_recommendations
- sys.dm_db_tuning_recommendations_TSQL
- dm_db_tuning_recommendations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database tuning recommendations feature [SQL Server], sys.dm_db_tuning_recommendations dynamic management view
- sys.dm_db_tuning_recommendations dynamic management view
ms.assetid: ced484ae-7c17-4613-a3f9-6d8aba65a110
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e8c18ce07ba5e36dcbdb5750db77edf17495c7b9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285491"
---
# <a name="sysdm_db_tuning_recommendations-transact-sql"></a>sys.dm\_\_suggerimenti\_per l'ottimizzazione dei database (Transact-SQL)Sys.dm db tuning recommendations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Restituisce informazioni dettagliate sui suggerimenti per l'ottimizzazione.  
  
 In [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], le viste a gestione dinamica non possono esporre le informazioni che influenzerebbero l'indipendenza del database o le informazioni sugli altri database a cui l'utente dispone di accesso. Per evitare di esporre queste informazioni, ogni riga che contiene dati che non appartengono al tenant connesso viene filtrata.

| **Nome colonna** | **Tipo di dati** | **Descrizione** |
| --- | --- | --- |
| **name** | **nvarchar(4000)** | Nome univoco della raccomandazione. |
| **type** | **nvarchar(4000)** | Il nome dell'opzione di sintonizzazione automatica che ha prodotto la raccomandazione, ad esempio,`FORCE_LAST_GOOD_PLAN` |
| **reason** | **nvarchar(4000)** | Motivo per cui è stata fornita questa raccomandazione. |
| **valido\_dal momento che** | **datetime2** | La prima volta che è stata generata questa raccomandazione. |
| **ultimo\_aggiornamento** | **datetime2** | L'ultima volta che è stata generata questa raccomandazione. |
| **Stato** | **nvarchar(4000)** | Documento JSON che descrive lo stato della raccomandazione. Sono disponibili i seguenti campi:<br />-   `currentValue`- stato attuale della raccomandazione.<br />-   `reason`- costante che descrive il motivo per cui la raccomandazione è nello stato corrente.|
| **è\_\_un'azione eseguibile** | **bit** | 1 - La raccomandazione può essere [!INCLUDE[tsql_md](../../includes/tsql-md.md)] eseguita sul database tramite script.<br />0 - La raccomandazione non può essere eseguita sul database (ad esempio: solo informazioni o raccomandazione annullata) |
| **è\_un'azione ripristinabile\_** | **bit** | 1 - La raccomandazione può essere monitorata e ripristinata automaticamente dal motore di database.<br />0 - La raccomandazione non può essere monitorata e ripristinata automaticamente. La &quot;&quot; maggior parte &quot;delle&quot;azioni eseguibili sarà ripristinabile. |
| **ora\_\_di\_inizio dell'azione di esecuzione** | **datetime2** | Data di applicazione della raccomandazione. |
| **durata\_\_dell'azione di esecuzione** | **time** | Durata dell'azione di esecuzione. |
| **eseguire\_\_l'azione avviata\_da** | **nvarchar(4000)** | `User`- Piano forzato manualmente dall'utente nella raccomandazione. <br /> `System`- Raccomandazione applicata automaticamente dal sistema. |
| **eseguire\_\_l'azione tempo di inizio\_** | **datetime2** | Data in cui è stata applicata la raccomandazione. |
| **ripristinare\_\_l'ora di inizio\_dell'azione** | **datetime2** | Data in cui la raccomandazione è stata annullata. |
| **ripristinare\_\_la durata dell'azione** | **time** | Durata dell'azione di ripristino. |
| **\_annullare\_\_l'azione avviata da** | **nvarchar(4000)** | `User`- Piano consigliato se non forzato dall'utente. <br /> `System`- Raccomandazione ripristinata automaticamente dal sistema. |
| **tempo\_\_di\_avvio dell'azione di ripristino** | **datetime2** | Data in cui la raccomandazione è stata annullata. |
| **Punteggio** | **Int** | Valore/impatto stimato per questa raccomandazione sulla scala 0-100 (maggiore è è il migliore) |
| **Dettagli** | **nvarchar(max)** | Documento JSON che contiene ulteriori dettagli sulla raccomandazione. Sono disponibili i seguenti campi:<br /><br />`planForceDetails`<br />-    `queryId`-\_ID query della query regredita.<br />-    `regressedPlanId`- plan_id del piano regredito.<br />-   `regressedPlanExecutionCount`- Numero di esecuzioni della query con piano regredito prima che venga rilevata la regressione.<br />-    `regressedPlanAbortedCount`- Numero di errori rilevati durante l'esecuzione del piano regredito.<br />-    `regressedPlanCpuTimeAverage`- Tempo medio CPU (in micro secondi) utilizzato dalla query regredita prima che venga rilevata la regressione.<br />-    `regressedPlanCpuTimeStddev`- Deviazione standard del tempo CPU utilizzata dalla query regredita prima che venga rilevata la regressione.<br />-    `recommendedPlanId`- plan_id del piano che dovrebbe essere forzato.<br />-   `recommendedPlanExecutionCount`- Numero di esecuzioni della query con il piano che deve essere forzato prima che venga rilevata la regressione.<br />-    `recommendedPlanAbortedCount`- Numero di errori rilevati durante l'esecuzione del piano che deve essere forzato.<br />-    `recommendedPlanCpuTimeAverage`- Tempo medio CPU (in micro secondi) utilizzato dalla query eseguita con il piano che deve essere forzato (calcolato prima che venga rilevata la regressione).<br />-    `recommendedPlanCpuTimeStddev`Deviazione standard del tempo CPU utilizzata dalla query regredita prima che venga rilevata la regressione.<br /><br />`implementationDetails`<br />-  `method`- Il metodo che deve essere utilizzato per correggere la regressione. Il valore `TSql`è sempre .<br />-    `script` - [!INCLUDE[tsql_md](../../includes/tsql-md.md)]script che deve essere eseguito per forzare il piano consigliato. |
  
## <a name="remarks"></a>Osservazioni  
 Le informazioni `sys.dm_db_tuning_recommendations` restituite da vengono aggiornate quando il motore di database identifica la potenziale regressione delle prestazioni delle query e non viene mantenuta. Le raccomandazioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono mantenute solo fino al riavvio. Gli amministratori di database devono eseguire periodicamente copie di backup della raccomandazione di ottimizzazione se desiderano mantenerla dopo il riciclo del server. 

 `currentValue`nella `state` colonna potrebbe avere i seguenti valori:
 
 | Stato | Descrizione |
 |--------|-------------|
 | `Active` | La raccomandazione è attiva e non ancora applicata. L'utente può prendere script di raccomandazione ed eseguirlo manualmente. |
 | `Verifying` | Il consiglio [!INCLUDE[ssde_md](../../includes/ssde_md.md)] viene applicato e il processo di verifica interno confronta le prestazioni del piano forzato con il piano regredito. |
 | `Success` | La raccomandazione è stata applicata correttamente. |
 | `Reverted` | La raccomandazione viene annullata perché non sono presenti miglioramenti significativi delle prestazioni. |
 | `Expired` | La raccomandazione è scaduta e non può più essere applicata. |

Il documento `state` JSON nella colonna contiene il motivo che descrive il motivo per cui è la raccomandazione nello stato corrente. I valori nel campo del motivo potrebbero essere: 

| Motivo | Descrizione |
|--------|-------------|
| `SchemaChanged` | Consiglio scaduto perché lo schema di una tabella di riferimento viene modificato. Se viene rilevata una nuova regressione del piano di query nel nuovo schema, verrà creata una nuova raccomandazione. |
| `StatisticsChanged`| La raccomandazione è scaduta a causa della modifica statistica in una tabella di riferimento. Se viene rilevata una nuova regressione del piano di query in base a nuove statistiche, verrà creata una nuova raccomandazione. |
| `ForcingFailed` | Il piano consigliato non può essere forzato in una query. Trovare `last_force_failure_reason` il nella vista [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) per trovare il motivo dell'errore. |
| `AutomaticTuningOptionDisabled` | `FORCE_LAST_GOOD_PLAN`è disabilitata dall'utente durante il processo di verifica. Abilitare l'opzione `FORCE_LAST_GOOD_PLAN` utilizzando [ALTER DATABASE SET AUTOMATIC_TUNING &#40;'istruzione Transact-SQLTransact-SQL&#41;o](../../t-sql/statements/alter-database-transact-sql-set-options.md) forzare il piano manualmente utilizzando lo script nella `[details]` colonna. |
| `UnsupportedStatementType` | Impossibile forzare il piano nella query. Esempi di query non supportate sono cursori e `INSERT BULK` istruzioni. |
| `LastGoodPlanForced` | La raccomandazione è stata applicata correttamente. |
| `AutomaticTuningOptionNotEnabled`| [!INCLUDE[ssde_md](../../includes/ssde_md.md)]identificato la regressione `FORCE_LAST_GOOD_PLAN` delle prestazioni potenziale, ma l'opzione non è abilitata - vedere [ALTER DATABASE SET AUTOMATIC_TUNING &#40;&#41;Transact-SQL ](../../t-sql/statements/alter-database-transact-sql-set-options.md). Applicare la raccomandazione manualmente o l'opzione di abilitazione. `FORCE_LAST_GOOD_PLAN` |
| `VerificationAborted`| Il processo di verifica viene interrotto a causa del riavvio o della pulizia dell'archivio query. |
| `VerificationForcedQueryRecompile`| La query viene ricompilata perché non vi sono miglioramenti significativi delle prestazioni. |
| `PlanForcedByUser`| L'utente ha forzato manualmente il piano utilizzando sp_query_store_force_plan &#40;procedura [Transact-SQLTransact-SQL&#41;.](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md) Motore di database non applicherà la raccomandazione se l'utente ha deciso esplicitamente di forzare un piano. |
| `PlanUnforcedByUser` | Utente manualmente non forzato il piano utilizzando sp_query_store_unforce_plan &#40;procedura [Transact-SQLSql&#41;.](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md) Poiché l'utente ha ripristinato in modo esplicito il piano consigliato, motore di database continuerà a usare il piano corrente e genererà una nuova raccomandazione se si verifica una regressione del piano in futuro. |

 Statistiche nella colonna dei dettagli non mostrano le statistiche del piano di runtime (ad esempio, il tempo corrente della CPU). I dettagli della raccomandazione vengono acquisiti [!INCLUDE[ssde_md](../../includes/ssde_md.md)] al momento del rilevamento della regressione e descrivono il motivo per cui è stata identificata la regressione delle prestazioni. Usare `regressedPlanId` `recommendedPlanId` e per eseguire una query sulle viste del catalogo di [Query Store](../../relational-databases/performance/how-query-store-collects-data.md) per trovare le statistiche esatte del piano di runtime.

## <a name="examples-of-using-tuning-recommendations-information"></a>Esempi di utilizzo delle informazioni sulle raccomandazioni di ottimizzazioneExamples of using tuning recommendations information  

### <a name="example-1"></a>Esempio 1
Di seguito viene [!INCLUDE[tsql](../../includes/tsql-md.md)] ottenuto lo script generato che forza un piano valido per una determinata query:The following gets the generated script that forces a good plan for any query given query:  
 
```sql
SELECT name, reason, score,
    JSON_VALUE(details, '$.implementationDetails.script') AS script,
    details.* 
FROM sys.dm_db_tuning_recommendations
CROSS APPLY OPENJSON(details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            regressed_plan_id int '$.regressedPlanId',
            last_good_plan_id int '$.recommendedPlanId') AS details
WHERE JSON_VALUE(state, '$.currentValue') = 'Active';
```
### <a name="example-2"></a>Esempio 2
Di seguito viene [!INCLUDE[tsql](../../includes/tsql-md.md)] ottenuto lo script generato che impone un buon piano per una determinata query e informazioni aggiuntive sul guadagno stimato:

```sql
SELECT reason, score,
      script = JSON_VALUE(details, '$.implementationDetails.script'),
      planForceDetails.*,
      estimated_gain = (regressedPlanExecutionCount + recommendedPlanExecutionCount)
                  *(regressedPlanCpuTimeAverage - recommendedPlanCpuTimeAverage)/1000000,
      error_prone = IIF(regressedPlanErrorCount > recommendedPlanErrorCount, 'YES','NO')
FROM sys.dm_db_tuning_recommendations
CROSS APPLY OPENJSON (Details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            regressedPlanId int '$.regressedPlanId',
            recommendedPlanId int '$.recommendedPlanId',
            regressedPlanErrorCount int,
            recommendedPlanErrorCount int,
            regressedPlanExecutionCount int,
            regressedPlanCpuTimeAverage float,
            recommendedPlanExecutionCount int,
            recommendedPlanCpuTimeAverage float
          ) AS planForceDetails;
```

### <a name="example-3"></a>Esempio 3
Di seguito viene [!INCLUDE[tsql](../../includes/tsql-md.md)] ottenuto lo script generato che impone un piano valido per una determinata query e informazioni aggiuntive che includono il testo della query e i piani di query archiviati nell'archivio query:

```sql
WITH cte_db_tuning_recommendations
AS (SELECT reason,
        score,
        query_id,
        regressedPlanId,
        recommendedPlanId,
        current_state = JSON_VALUE(state, '$.currentValue'),
        current_state_reason = JSON_VALUE(state, '$.reason'),
        script = JSON_VALUE(details, '$.implementationDetails.script'),
        estimated_gain = (regressedPlanExecutionCount + recommendedPlanExecutionCount)
                * (regressedPlanCpuTimeAverage - recommendedPlanCpuTimeAverage)/1000000,
        error_prone = IIF(regressedPlanErrorCount > recommendedPlanErrorCount, 'YES','NO')
    FROM sys.dm_db_tuning_recommendations
    CROSS APPLY OPENJSON(Details, '$.planForceDetails')
    WITH ([query_id] int '$.queryId',
        regressedPlanId int '$.regressedPlanId',
        recommendedPlanId int '$.recommendedPlanId',
        regressedPlanErrorCount int,    
        recommendedPlanErrorCount int,
        regressedPlanExecutionCount int,
        regressedPlanCpuTimeAverage float,
        recommendedPlanExecutionCount int,
        recommendedPlanCpuTimeAverage float
        )
    )
SELECT qsq.query_id,
    qsqt.query_sql_text,
    dtr.*,
    CAST(rp.query_plan AS XML) AS RegressedPlan,
    CAST(sp.query_plan AS XML) AS SuggestedPlan
FROM cte_db_tuning_recommendations AS dtr
INNER JOIN sys.query_store_plan AS rp ON rp.query_id = dtr.query_id
    AND rp.plan_id = dtr.regressedPlanId
INNER JOIN sys.query_store_plan AS sp ON sp.query_id = dtr.query_id
    AND sp.plan_id = dtr.recommendedPlanId
INNER JOIN sys.query_store_query AS qsq ON qsq.query_id = rp.query_id
INNER JOIN sys.query_store_query_text AS qsqt ON qsqt.query_text_id = qsq.query_text_id;
```

Per altre informazioni sulle funzioni JSON che possono essere usate per [!INCLUDE[ssde_md](../../includes/ssde_md.md)]eseguire query sui valori nella visualizzazione dei suggerimenti, vedere Supporto [JSON](../../relational-databases/json/index.md) in .
  
## <a name="permissions"></a>Autorizzazioni  

Richiede `VIEW SERVER STATE` l'autorizzazione in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].   
Richiede `VIEW DATABASE STATE` l'autorizzazione per [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]il database in .   

## <a name="see-also"></a>Vedere anche  
 [Sintonizzazione automatica](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [&#40;transact-SQLdi sys.database_automatic_tuning_options&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)   
 [&#41;Transact-SQLdi sys.&#40;database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Supporto JSON](../../relational-databases/json/index.md)
 
