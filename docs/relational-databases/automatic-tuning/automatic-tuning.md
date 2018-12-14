---
title: L'ottimizzazione automatica | Microsoft Docs
description: Informazioni sull'ottimizzazione automatica in SQL Server e Database SQL di Azure
ms.custom: ''
ms.date: 08/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- performance tuning [SQL Server]
ms.assetid: ''
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a196ef879c176fe731fe85b2de7962d70edff7b4
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52541170"
---
# <a name="automatic-tuning"></a>Ottimizzazione automatica
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

L'ottimizzazione automatica è una funzionalità di database che offre informazioni su potenziali problemi di prestazioni delle query, suggerisce soluzioni e corregge automaticamente i problemi rilevati.

L'ottimizzazione automatica nel [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] invia una notifica ogni volta che viene rilevato un potenziale problema di prestazioni e consente di applicare azioni correttive o consente il [!INCLUDE[ssde_md](../../includes/ssde_md.md)] risolvere automaticamente problemi di prestazioni.
L'ottimizzazione automatica nel [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] consente di identificare e risolvere i problemi di prestazioni causati da **le regressioni della scelta piano l'esecuzione di query**. L'ottimizzazione automatica nel [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] inoltre crea gli indici necessari e deve eliminare gli indici inutilizzati. Per altre informazioni sui piani di esecuzione di query, vedere [piani di esecuzione](../../relational-databases/performance/execution-plans.md).

Il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] monitoraggi, le query eseguite sul database e automaticamente migliora le prestazioni del carico di lavoro. Il [!INCLUDE[ssde_md](../../includes/ssde_md.md)] include un meccanismo di intelligence integrata che possa ottimizzare automaticamente e migliorare le prestazioni delle query, adattando in modo dinamico il database ai carichi di lavoro. Esistono due funzionalità di ottimizzazione automatica disponibili:

 -  **Correzione automatica dei piani** identifica query problematiche piani di esecuzione e corregge i problemi di prestazioni di piani di esecuzione della query. **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (A partire da [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
 -  **Gestione automatica degli indici** identifica gli indici che devono essere aggiunti nel database e gli indici che devono essere rimossi. **Si applica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

## <a name="why-automatic-tuning"></a>Il motivo per cui l'ottimizzazione automatica?

Tre delle principali attività di amministrazione classica dei database esegue il monitoraggio del carico di lavoro, che identifica critici [!INCLUDE[tsql_md](../../includes/tsql-md.md)] esegue una query, gli indici che devono essere aggiunte per migliorare le prestazioni e identificazione usata raramente. Il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] offre informazioni dettagliate per le query e gli indici che è necessario monitorare. Tuttavia, costantemente il monitoraggio di un database è un'attività complessa e tediosa, in particolare quando si lavora con molti database. Potrebbe essere impossibile in modo efficiente gestire un numero enorme di database. Invece di monitoraggio e ottimizzazione del database manualmente, è possibile delegare alcune del monitoraggio e le azioni di ottimizzazione di [!INCLUDE[ssde_md](../../includes/ssde_md.md)] usando funzionalità di ottimizzazione automatica.

### <a name="how-does-automatic-tuning-work"></a>Come funziona automatica ottimizzazione?

L'ottimizzazione automatica è un monitoraggio continuo e il processo di analisi che apprende continuamente le caratteristiche del carico di lavoro e identificare potenziali problemi e miglioramenti.

![Processo di ottimizzazione automatica](./media/tuning-process.png)

Questo processo consente database adattamento dinamico al carico di lavoro mediante la ricerca degli indici e i piani potrebbero migliorare le prestazioni dei carichi di lavoro e quali indici con effetti sui carichi di lavoro. Basato su questi risultati, l'ottimizzazione automatica applica le azioni di ottimizzazione che consentono di migliorare le prestazioni del carico di lavoro. Inoltre, database monitora continuamente le prestazioni dopo qualsiasi modifica apportata dall'ottimizzazione automatica per garantire che migliora le prestazioni del carico di lavoro. Qualsiasi azione che non introduce miglioramenti delle prestazioni viene annullata automaticamente. Questo processo di verifica è una funzionalità chiave che assicura che qualsiasi modifica apportata dall'ottimizzazione automatica non diminuisca le prestazioni del carico di lavoro.

## <a name="automatic-plan-correction"></a>Correzione automatica dei piani

Correzione automatica del piano è una funzionalità di ottimizzazione automatica che identifica **regressioni della scelta di piani di esecuzione** e risolvere automaticamente il problema, forzando l'ultimo piano adeguato noto. Per altre informazioni sui piani di esecuzione di query e query optimizer, vedere la [Guida sull'architettura di elaborazione Query](../../relational-databases/query-processing-architecture-guide.md).

### <a name="what-is-execution-plan-choice-regression"></a>Che cos'è regressioni della scelta del piano esecuzione?

Il [!INCLUDE[ssdenoversion_md](../../includes/ssdenoversion_md.md)] può utilizzare piani di esecuzione diversi per eseguire il [!INCLUDE[tsql_md](../../includes/tsql-md.md)] le query. I piani di query variano in base ad altri fattori, indici e le statistiche. Il piano ottimale da usare per eseguire alcune [!INCLUDE[tsql_md](../../includes/tsql-md.md)] query potrebbero essere modificate nel corso del tempo. In alcuni casi, il nuovo piano non sia migliore rispetto a quello precedente e il nuovo piano potrebbe causare una regressione delle prestazioni.

 ![Regressioni della scelta del piano l'esecuzione di query](media/plan-choice-regression.png "regressioni della scelta del piano l'esecuzione di Query") 

Ogni volta che si verificano le regressioni della scelta del piano, è necessario trovare alcuni validi precedenti piano e lo forza anziché corrente usando uno `sp_query_store_force_plan` procedure.
[!INCLUDE[ssde_md](../../includes/ssde_md.md)] in [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] fornisce informazioni sulle query regredite piani e le azioni correttive consigliate.
È inoltre [!INCLUDE[ssde_md](../../includes/ssde_md.md)] consente di automatizzare questo processo e consentire completamente [!INCLUDE[ssde_md](../../includes/ssde_md.md)] correggere gli eventuali problemi riscontrati relativi per le modifiche apportate al piano.

### <a name="automatic-plan-choice-correction"></a>Correzione automatica del piano

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] può passare automaticamente all'ultimo piano adeguato noto ogni volta che viene rilevata la regressione della scelta del piano.

![Correzione scelta del piano di esecuzione di query](media/force-last-good-plan.png "correzione scelta del piano di esecuzione di Query") 

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] rileva automaticamente le regressioni della scelta del piano potenziali incluso il piano che deve essere usato al posto del piano errato.
Quando il [!INCLUDE[ssde_md](../../includes/ssde_md.md)] verrà applicata l'ultima nota piano appropriato, monitora automaticamente le prestazioni del piano forzato. Se il piano forzato non è migliore del piano regredito, il nuovo piano sarà forzatura e [!INCLUDE[ssde_md](../../includes/ssde_md.md)] verrà compilato un nuovo piano. Se il [!INCLUDE[ssde_md](../../includes/ssde_md.md)] verifica che il piano forzato è migliore del piano regredito, il piano forzato viene mantenuto anche se è preferibile rispetto al piano regredito, fino a quando non si verifica una ricompilazione (ad esempio, nella successiva statistiche update modifica dello schema o).

> [!NOTE]
> Qualsiasi automaticamente i piani di esecuzione forzato non sono persistenti tra riavvii del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza.

### <a name="enabling-automatic-plan-choice-correction"></a>Abilitazione della correzione automatica del piano

È possibile abilitare l'ottimizzazione automatica per ogni database e specificare che il miglior piano più recente deve essere forzato ogni volta in cui viene rilevata una regressione della modifica del piano. L'ottimizzazione automatica viene abilitata con il comando seguente:

```sql   
ALTER DATABASE current
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON ); 
```

Dopo aver abilitato questa opzione, il [!INCLUDE[ssde_md](../../includes/ssde_md.md)] automaticamente forzare una raccomandazione in cui il miglioramento di CPU stimato è maggiore di 10 secondi o il numero di errori nel nuovo piano è maggiore del numero di errori del piano consigliato e verificare che il piano forzato è migliore rispetto a quella corrente.

### <a name="alternative---manual-plan-choice-correction"></a>Opzione alternativa: correzione scelta del piano manuale

Senza l'ottimizzazione automatica, gli utenti devono monitorare il sistema periodicamente e cercare le query regredite. Se qualsiasi piano regredito, utente dovrebbe trovare alcuni validi precedenti piano e lo forza anziché corrente usando uno `sp_query_store_force_plan` procedure. La procedura consigliata, è possibile forzare l'ultimo piano valido noto, poiché i piani precedenti potrebbero non essere validi a causa di modifiche di indice o statistica. L'utente che forza l'ultimo piano adeguato noto deve monitorare le prestazioni della query viene eseguita usando il piano forzato e verificare che il piano forzato funziona come previsto. A seconda dei risultati dell'analisi e monitoraggio, è necessario forzare il piano o utente deve trovare un altro modo per ottimizzare la query.
Piani forzati manualmente dovrebbero non essere forzati all'infinito, perché il [!INCLUDE[ssde_md](../../includes/ssde_md.md)] deve essere in grado di applicare i piani ottimali. L'utente o amministratore di database deve alla fine Annulla forzatura piano tramite il `sp_query_store_unforce_plan` procedure e consentono la [!INCLUDE[ssde_md](../../includes/ssde_md.md)] trovare il piano ottimale. 

> [!TIP]
> Alternativelly, usare il **le query con piani forzato** visualizzazione di Query Store per individuare e Annulla forzatura piani.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce tutte le viste necessarie e procedure necessarie per monitorare le prestazioni e risolvere i problemi in Query Store.

In [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], è possibile trovare le regressioni della scelta piano utilizzo delle viste di sistema di Query Store. Nella [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], il [!INCLUDE[ssde_md](../../includes/ssde_md.md)] rileva e visualizza le regressioni della scelta piano potenziali e le azioni consigliate che devono essere applicate nella [DM db_tuning_recommendations &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md) visualizzazione. La visualizzazione Mostra informazioni sul problema, l'importanza del problema e i dettagli, ad esempio la query identificato, l'ID del piano regredito, l'ID del piano che è stato usato come base per il confronto e il [!INCLUDE[tsql_md](../../includes/tsql-md.md)] istruzione che può essere eseguito per correggere il c'è problema.

| Tipo | description | DATETIME | score | dettagli | ... |
| --- | --- | --- | --- | --- | --- |
| `FORCE_LAST_GOOD_PLAN` | Modificato da 4 ms a 14 ms di tempo di CPU | 3/17/2017 | 83 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |
| `FORCE_LAST_GOOD_PLAN` | Tempo di CPU modificato da 37 ms e ms 84 | 3/16/2017 | 26 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |

Alcune colonne da questa visualizzazione sono descritti nell'elenco seguente:
 - Tipo di azione consigliata: `FORCE_LAST_GOOD_PLAN`
 - Descrizione che contiene il motivo per cui le informazioni [!INCLUDE[ssde_md](../../includes/ssde_md.md)] ritiene che la modifica del piano è una regressione delle prestazioni potenziali
 - Data/ora quando viene rilevata una regressione il potenziale
 - Punteggio della raccomandazione
 - Dettagli sui problemi, ad esempio ID del piano rilevato, ID del piano regredito, ID del piano che per risolvere il problema, è necessario forzare [!INCLUDE[tsql_md](../../includes/tsql-md.md)] script che potrebbe essere applicato per risolvere il problema e così via. I dettagli vengono archiviati in [formato JSON](../../relational-databases/json/index.md)

Usare la query seguente per ottenere uno script che corregge il problema e informazioni aggiuntive sulle stimati ottenere:

```sql   
SELECT reason, score,
      script = JSON_VALUE(details, '$.implementationDetails.script'),
      planForceDetails.*,
      estimated_gain = (regressedPlanExecutionCount+recommendedPlanExecutionCount)
                  *(regressedPlanCpuTimeAverage-recommendedPlanCpuTimeAverage)/1000000,
      error_prone = IIF(regressedPlanErrorCount>recommendedPlanErrorCount, 'YES','NO')
FROM sys.dm_db_tuning_recommendations
  CROSS APPLY OPENJSON (Details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            [current plan_id] int '$.regressedPlanId',
            [recommended plan_id] int '$.recommendedPlanId',

            regressedPlanErrorCount int,
            recommendedPlanErrorCount int,

            regressedPlanExecutionCount int,
            regressedPlanCpuTimeAverage float,
            recommendedPlanExecutionCount int,
            recommendedPlanCpuTimeAverage float

          ) as planForceDetails;
```

[!INCLUDE[ssresult-md](../../includes/ssresult-md.md)]     

| reason | score | script | query\_id | piano corrente\_id | piano consigliato\_id | stimato\_ottenere | errore\_soggetta a
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Modificato da 3 ms a 46 ms di tempo di CPU | 36 | EXEC sp\_query\_archiviare\_forzare\_piano di 12, 17; | 12 | 28 | 17 | 11.59 | 0

`estimated_gain` rappresenta il numero stimato di secondi che verrebbero salvate se viene eseguito il piano consigliato anziché il piano corrente. Se il miglioramento è maggiore di 10 secondi, è necessario forzare il piano consigliato anziché il piano corrente. Se sono presenti più errori (ad esempio, i timeout o esecuzioni interrotte) nel piano corrente più in consigliata prevede, la colonna `error_prone` verrebbe impostato sul valore `YES`. Piano soggette a errore è un altro motivo perché è necessario forzare il piano consigliato invece di quello corrente.

Sebbene [!INCLUDE[ssde_md](../../includes/ssde_md.md)] fornisce tutte le informazioni necessarie per identificare le regressioni della scelta piano; continuo di monitoraggio e risoluzione dei problemi di prestazioni potrebbero essere un'operazione laboriosa. L'ottimizzazione automatica, questo processo diventa molto più semplice.

> [!NOTE]
> I dati nel DM db_tuning_recommendations DMV non sono persistente tra riavvii del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza.

## <a name="automatic-index-management"></a>Gestione automatica degli indici

Nelle [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], la gestione degli indici è semplice perché [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] apprende il carico di lavoro e assicura che i dati vengono indicizzati sempre in modo ottimale. La progettazione di indici appropriato è fondamentale per ottenere prestazioni ottimali del carico di lavoro e gestione automatica degli indici può consentire di ottimizzare gli indici. Gestione automatica degli indici possibile risolvere i problemi di prestazioni nei database indicizzati in modo non corretto, oppure mantenere e migliorare gli indici nello schema del database esistente. L'ottimizzazione automatica nel [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] esegue le azioni seguenti:

 - Identifica gli indici che potrebbero migliorare le prestazioni dei [!INCLUDE[tsql_md](../../includes/tsql-md.md)] le query che leggono dati dalle tabelle.
 - Identifica gli indici ridondanti o gli indici non utilizzati in un periodo più lungo di tempo in cui è stato possibile rimuovere. Rimozione di indici non necessari migliora le prestazioni delle query che aggiornano i dati nelle tabelle.

### <a name="why-do-you-need-index-management"></a>Il motivo per cui è necessario gestione degli indici?

Gli indici di velocizzare alcune delle query che leggono dati dalle tabelle; Tuttavia, possono rallentare le query che aggiornano i dati. È necessario valutare con attenzione quando creare un indice e delle colonne della tabella è necessario includere nell'indice. Alcuni indici potrebbero non essere necessario qualche minuto. Pertanto, è necessario individuare ed eliminare gli indici che non portano alcun vantaggio periodicamente. Se si ignorano gli indici inutilizzati, le prestazioni delle query che aggiornano i dati potrebbero risultare ridotte, senza alcun vantaggio per le query che leggono i dati. Gli indici inutilizzati influisce anche sulle prestazioni complessive del sistema perché aggiornamenti aggiuntivi richiedono operazioni di registrazione superflue.

Individuare il set ottimale di indici che consentono di migliorare le prestazioni delle query che leggono dati dalle tabelle di e avere un impatto minimo sugli aggiornamenti potrebbero richiedere l'analisi continue e complesse.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] Usa funzionalità di intelligence integrata e regole avanzate per l'analisi delle query, identificare gli indici che sarebbero ottimali per carichi di lavoro correnti e gli indici potrebbero essere rimossa. Database SQL di Azure consente di disporre di un set minimo necessario di indici che ottimizzano le query che leggono i dati, con un impatto minimo sulle altre query.

### <a name="automatic-index-management"></a>Gestione automatica degli indici

Oltre a rilevamento, [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] può applicare automaticamente le raccomandazioni identificate. Se si ritiene che le regole predefinite migliorare le prestazioni del database, è possibile delegare [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] gestione automatica degli indici.

Per abilitare l'ottimizzazione automatica nel [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e consentire la funzionalità di ottimizzazione automatica gestire il carico di lavoro, vedere completamente [abilitare l'ottimizzazione automatica nel Database SQL di Azure usando il portale di Azure](/azure/sql-database/sql-database-automatic-tuning-enable).

Quando il [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] viene applicata una raccomandazione CREATE INDEX o DROP INDEX, monitora automaticamente le prestazioni delle query che sono interessati dall'indice. Nuovo indice verrà conservate solo se sono possibile ottimizzare le prestazioni delle query interessate. L'indice rimosso verrà ricreato automaticamente se sono presenti alcune query eseguite più lentamente a causa dell'assenza dell'indice.

### <a name="automatic-index-management-considerations"></a>Considerazioni sulla gestione automatica dell'indice

Le azioni necessarie per creare gli indici necessari in [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] potrebbe utilizzare risorse e influire temporaneamente sulle prestazioni del carico di lavoro. Per ridurre al minimo l'impatto della creazione dell'indice sulle prestazioni del carico di lavoro, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] rileva che l'intervallo di tempo appropriato per qualsiasi operazione di gestione dell'indice. Azione di ottimizzazione viene posticipata se il database necessita di risorse per l'esecuzione del carico di lavoro e avviato quando il database dispone di sufficienti risorse inutilizzate che possono essere usate per l'attività di manutenzione. Una funzionalità importante nella gestione automatica degli indici è una verifica delle azioni. Quando [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] crea o Elimina indice, un processo di monitoraggio analizza le prestazioni del carico di lavoro per verificare che l'azione migliori effettivamente le prestazioni. Se non introduce miglioramenti significativi - l'azione viene annullata immediatamente. In questo modo, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] assicura che le azioni automatiche non influire negativamente sulle prestazioni del carico di lavoro. Gli indici creati tramite l'ottimizzazione automatica sono trasparenti per l'operazione di manutenzione sullo schema sottostante. Le modifiche dello schema, ad esempio eliminazione o ridenominazione delle colonne non siano bloccate dalla presenza di indici creati automaticamente. Gli indici creati automaticamente da [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] vengono eliminati immediatamente al correlate le colonne o una tabella viene eliminata.

### <a name="alternative---manual-index-management"></a>Opzione alternativa: gestione dell'indice di manuali

Senza gestione automatica degli indici, sarebbe necessario eseguire manualmente una query utente [DM db_missing_index_details &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md) vista per individuare gli indici che potrebbero migliorare le prestazioni, creare indici con i dettagli disponibili in questa vista e manualmente monitorare le prestazioni della query. Per trovare gli indici che devono essere eliminati, gli utenti devono monitorare le statistiche di utilizzo operativa degli indici per gli indici di ricerca usata raramente.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] semplifica questo processo. [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] Analizza il carico di lavoro, identifica le query che potrebbero essere eseguite più velocemente con un nuovo indice e identifica gli indici inutilizzati o duplicati. Trovare altre informazioni sull'identificazione degli indici che devono essere modificati in [trovare indicazioni relative agli indici nel portale di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-advisor-portal).

## <a name="see-also"></a>Vedere anche  
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_automatic_tuning_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)  
 [sys.dm_db_tuning_recommendations &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)     
 [sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)           
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Funzioni JSON](../../relational-databases/json/index.md)    
 [Piani di esecuzione](../../relational-databases/performance/execution-plans.md)    
 [Monitoraggio e ottimizzazione delle prestazioni](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [Strumenti per il monitoraggio e l'ottimizzazione delle prestazioni](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [Monitoraggio delle prestazioni con Archivio query](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
 [Assistente di ottimizzazione query](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)
