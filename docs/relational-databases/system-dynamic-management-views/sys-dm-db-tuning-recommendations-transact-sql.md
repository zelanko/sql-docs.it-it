---
title: sys.dm_db_tuning_recommendations (Transact-SQL) | Microsoft Docs
description: Informazioni su come trovare potenziali problemi di prestazioni e consigliate le correzioni apportate in SQL Server e Database SQL di Azure
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
ms.openlocfilehash: dbee7422bdf58d753c31c7aa57a81bc4b29d2568
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096232"
---
# <a name="sysdmdbtuningrecommendations-transact-sql"></a>sys.dm\_db\_tuning\_recommendations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Restituisce informazioni dettagliate sui suggerimenti di ottimizzazione.  
  
 In [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], le viste a gestione dinamica non possono esporre le informazioni che influenzerebbero l'indipendenza del database o le informazioni sugli altri database a cui l'utente dispone di accesso. Per evitare di esporre queste informazioni, ogni riga che contiene dati che non appartengono al tenant connesso viene filtrata.

| **Nome colonna** | **Tipo di dati** | **Descrizione** |
| --- | --- | --- |
| **name** | **nvarchar(4000)** | Nome univoco della raccomandazione. |
| **type** | **nvarchar(4000)** | Il nome dell'opzione ottimizzazione automatica che ha generato la raccomandazione, ad esempio, `FORCE_LAST_GOOD_PLAN` |
| **reason** | **nvarchar(4000)** | Motivo per cui è stata fornita questa raccomandazione. |
| **valido\_poiché** | **datetime2** | La prima volta che è stata generata da questa raccomandazione. |
| **ultimo\_Aggiorna** | **datetime2** | L'ora dell'ultima è stata generata questa raccomandazione. |
| **state** | **nvarchar(4000)** | Documento JSON che descrive lo stato della raccomandazione. Sono disponibili i seguenti campi:<br />-   `currentValue` -stato corrente della raccomandazione.<br />-   `reason` -(costante) che descrive il motivo per cui la raccomandazione è nello stato corrente.|
| **viene\_eseguibile\_azione** | **bit** | 1 = la raccomandazione possa essere eseguita sul database tramite [!INCLUDE[tsql_md](../../includes/tsql-md.md)] script.<br />0 = la raccomandazione non possa essere eseguita sul database (ad esempio: raccomandazione ripristinato o solo informazioni) |
| **viene\_revertable\_azione** | **bit** | 1 = la raccomandazione può essere monitorata e ripristinata dal motore di Database automaticamente.<br />0 = la raccomandazione non può essere monitorata e ripristinata automaticamente. La maggior parte degli &quot;eseguibile&quot; azioni saranno &quot;revertable&quot;. |
| **eseguire\_azione\_avviare\_ora** | **datetime2** | Data che la raccomandazione viene applicata. |
| **eseguire\_azione\_durata** | **time** | Durata dell'azione di esecuzione. |
| **eseguire\_azione\_avviato\_da** | **nvarchar(4000)** | `User` = Utente forzati manualmente piano nell'indicazione. <br /> `System` = Raccomandazione viene applicata automaticamente sistema. |
| **eseguire\_azione\_avviato\_ora** | **datetime2** | Data che la raccomandazione è stata applicata. |
| **REVERT\_azione\_avviare\_ora** | **datetime2** | Data che la raccomandazione è stata ripristinata. |
| **REVERT\_azione\_durata** | **time** | Durata dell'azione di annullamento. |
| **REVERT\_azione\_avviato\_da** | **nvarchar(4000)** | `User` = Piano consigliato manualmente forzatura utente. <br /> `System` = Sistema annullato automaticamente raccomandazione. |
| **REVERT\_azione\_avviato\_ora** | **datetime2** | Data che la raccomandazione è stata ripristinata. |
| **punteggio** | **int** | Previsto valore/o l'impatto di questa raccomandazione su 0-100 la scala (più grande è preferibile) |
| **Dettagli** | **nvarchar(max)** | Documento JSON che contiene altri dettagli sulla raccomandazione. Sono disponibili i seguenti campi:<br /><br />`planForceDetails`<br />-    `queryId` -query\_id della query regredite.<br />-    `regressedPlanId` -plan_id del piano regredito.<br />-   `regressedPlanExecutionCount` -Numero di esecuzioni della query con piano con regressione prima la regressione viene rilevato.<br />-    `regressedPlanAbortedCount` -Numero di errori rilevati durante l'esecuzione del piano regredito.<br />-    `regressedPlanCpuTimeAverage` -Tempo CPU medio utilizzato dalla query regredite prima che la regressione viene rilevata.<br />-    `regressedPlanCpuTimeStddev` -Deviazione Standard di tempo della CPU utilizzato dalla query regredite prima la regressione è stata rilevata.<br />-    `recommendedPlanId` -plan_id del piano che deve essere forzato.<br />-   `recommendedPlanExecutionCount`: Numero di esecuzioni della query con il piano che deve essere forzato prima che la regressione viene rilevata.<br />-    `recommendedPlanAbortedCount` : Numero di errori rilevati durante l'esecuzione del piano che deve essere forzato.<br />-    `recommendedPlanCpuTimeAverage` -Tempo CPU medio utilizzato dalla query eseguita con il piano che deve essere forzato (calcolato prima che la regressione viene rilevata).<br />-    `recommendedPlanCpuTimeStddev` Deviazione standard di tempo della CPU utilizzato dalla query regredite prima la regressione è stata rilevata.<br /><br />`implementationDetails`<br />-  `method` -Il metodo che deve essere usato per risolvere la regressione. Valore è sempre `TSql`.<br />-    `script` - [!INCLUDE[tsql_md](../../includes/tsql-md.md)] script da eseguire per forzare il piano consigliato. |
  
## <a name="remarks"></a>Note  
 Le informazioni restituite da `sys.dm_db_tuning_recommendations` viene aggiornato quando identifica potenziali regressione delle prestazioni di query motore di database e non è persistente. Le raccomandazioni vengono mantenute solo fino al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene riavviato. Gli amministratori di database devono eseguire periodicamente copie di backup di indicazione di ottimizzazione se desiderano mantenere dopo il riciclo del server. 

 `currentValue` campo di `state` colonna potrebbe disporre i valori seguenti:
 
 | Stato | Descrizione |
 |--------|-------------|
 | `Active` | Raccomandazione è attiva e non ancora applicato. Utente può eseguire script indicazioni ed eseguirlo manualmente. |
 | `Verifying` | La raccomandazione viene applicata da [!INCLUDE[ssde_md](../../includes/ssde_md.md)] e processo di verifica interne vengono confrontate le prestazioni del piano forzato con il piano con regressione. |
 | `Success` | Raccomandazione viene applicata correttamente. |
 | `Reverted` | Raccomandazioni verranno annullate perché non esistono Nessun miglioramenti significativi delle prestazioni. |
 | `Expired` | Raccomandazione è scaduto e non può essere applicata più. |

Documento JSON in `state` colonna contiene il motivo per cui viene descritto il motivo per cui è l'indicazione dello stato corrente. I valori del campo motivo potrebbero essere: 

| `Reason` | Descrizione |
|--------|-------------|
| `SchemaChanged` | Raccomandazione è scaduta perché lo schema di una tabella cui viene fatto riferimento viene modificato. |
| `StatisticsChanged`| Indicazione scaduto a causa della modifica di statistiche in una tabella cui viene fatto riferimento. |
| `ForcingFailed` | Non è possibile forzare il piano consigliato su una query. Trovare il `last_force_failure_reason` nella [Sys. query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) vista per individuare il motivo dell'errore. |
| `AutomaticTuningOptionDisabled` | `FORCE_LAST_GOOD_PLAN` opzione è disabilitata dall'utente durante il processo di verifica. Abilitare `FORCE_LAST_GOOD_PLAN` opzione usando [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) istruzione o forzare il piano manualmente usando lo script nel `[details]` colonne. |
| `UnsupportedStatementType` | Non è possibile forzare il piano della query. Esempi di query non supportati sono i cursori e `INSERT BULK` istruzione. |
| `LastGoodPlanForced` | Raccomandazione viene applicata correttamente. |
| `AutomaticTuningOptionNotEnabled`| [!INCLUDE[ssde_md](../../includes/ssde_md.md)] identificare potenziali regressione delle prestazioni, ma il `FORCE_LAST_GOOD_PLAN` opzione non è abilitata, vedere la [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md). Raccomandazione applicata manualmente o abilitare `FORCE_LAST_GOOD_PLAN` opzione. |
| `VerificationAborted`| Processo di verifica viene interrotta a causa del riavvio o pulizia di Query Store. |
| `VerificationForcedQueryRecompile`| Query viene ricompilata in quanto non vi è alcun miglioramento significativo delle prestazioni. |
| `PlanForcedByUser`| Utente forzati manualmente usando il piano [sp_query_store_force_plan &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md) routine. |
| `PlanUnforcedByUser` | Utente manualmente annullare la forzatura del piano tramite [sp_query_store_unforce_plan &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md) routine. |

 Statistiche nella colonna dei dettagli non vengono visualizzate le statistiche di runtime piano (ad esempio, tempo CPU corrente). I dettagli delle raccomandazioni vengono eseguiti al momento del rilevamento di regressione e una descrizione per questo motivo [!INCLUDE[ssde_md](../../includes/ssde_md.md)] identificato regressione delle prestazioni. Uso `regressedPlanId` e `recommendedPlanId` alla query [viste del catalogo di Query Store](../../relational-databases/performance/how-query-store-collects-data.md) per trovare le statistiche di runtime esatta piano.

## <a name="examples-of-using-tuning-recommendations-information"></a>Esempi di utilizzo le informazioni relative indicazioni di ottimizzazione  

### <a name="example-1"></a>Esempio 1
Ottiene il generato quanto segue [!INCLUDE[tsql](../../includes/tsql-md.md)] script che forza una pianificazione valida per una determinata query:  
 
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
Ottiene il generato quanto segue [!INCLUDE[tsql](../../includes/tsql-md.md)] script che forza una pianificazione valida per qualsiasi query specificata e informazioni aggiuntive sul miglioramento stimato:

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
Ottiene il generato quanto segue [!INCLUDE[tsql](../../includes/tsql-md.md)] script che forza una pianificazione valida per qualsiasi query specificata e informazioni aggiuntive che include il testo della query e piani di query archiviati in Query Store:

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

Per altre informazioni sulle funzioni JSON che può essere utilizzato per i valori di query nella visualizzazione di indicazioni, vedere [and JSON Support](../../relational-databases/json/index.md) in [!INCLUDE[ssde_md](../../includes/ssde_md.md)].
  
## <a name="permissions"></a>Permissions  

È necessario `VIEW SERVER STATE` l'autorizzazione per [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].   
Richiede la `VIEW DATABASE STATE` l'autorizzazione per il database in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].   

## <a name="see-also"></a>Vedere anche  
 [L'ottimizzazione automatica](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [sys.database_automatic_tuning_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)   
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Supporto JSON](../../relational-databases/json/index.md)
 
