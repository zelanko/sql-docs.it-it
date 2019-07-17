---
title: Database OLAP WideWorldImporters - uso di SQL Server | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 313f85c5d5ec3590e231bdac4a746318c927a33a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104218"
---
# <a name="wideworldimportersdw-use-of-sql-server-features-and-capabilities"></a>WideWorldImportersDW sfrutta le funzionalità di SQL Server
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
WideWorldImportersDW è progettata per dimostrare molte delle funzionalità principali di SQL Server che sono adatte per il data warehousing e analitica. Di seguito è riportato un elenco di funzionalità di SQL Server e le funzionalità e una descrizione del modo in cui vengono utilizzati nelle WideWorldImportersDW.

## <a name="polybase"></a>PolyBase

[Si applica a SQL Server (2016 e versioni successive)]

PolyBase viene usato per combinare le informazioni di vendita da WideWorldImportersDW con un set di dati pubblico su dati demografici per comprendere quale città potrebbe rivelarsi interessante per l'ulteriore espansione delle vendite.

Per abilitare l'uso di PolyBase nel database di esempio, assicurarsi che sia installato ed eseguire la stored procedure seguente nel database:

    EXEC [Application].[Configuration_ApplyPolyBase]

Verrà creata una tabella esterna `dbo.CityPopulationStatistics` che fa riferimento a un set di dati pubblico che contiene i dati della popolazione delle città negli Stati Uniti, ospitato in archiviazione blob di Azure. Sono invitati a esaminare il codice della stored procedure per comprendere il processo di configurazione. Se si desidera ospitare i propri dati nell'archiviazione blob di Azure e garantirne la sicurezza da accesso pubblico generale, è necessario intraprendere ulteriori passaggi di configurazione. La query seguente restituisce i dati da tale set di dati esterno:

    SELECT CityID, StateProvinceCode, CityName, YearNumber, LatestRecordedPopulation FROM dbo.CityPopulationStatistics;

Per comprendere quale città potrebbe rivelarsi interessante per ulteriore espansione, esamina il tasso di crescita delle città, la query seguente e restituisce la più grandi città primi 100 con crescita significativa, e in cui Wide World Importers non ha una presenza di vendita. La query include un join tra la tabella remota `dbo.CityPopulationStatistics` e la tabella locale `Dimension.City`e un filtro che coinvolgono la tabella locale `Fact.Sales`.

    WITH PotentialCities
    AS
    (
        SELECT cps.CityName,
               cps.StateProvinceCode,
               MAX(cps.LatestRecordedPopulation) AS PopulationIn2016,
               (MAX(cps.LatestRecordedPopulation) - MIN(cps.LatestRecordedPopulation)) * 100.0
                   / MIN(cps.LatestRecordedPopulation) AS GrowthRate
        FROM dbo.CityPopulationStatistics AS cps
        WHERE cps.LatestRecordedPopulation IS NOT NULL
        AND cps.LatestRecordedPopulation <> 0
        GROUP BY cps.CityName, cps.StateProvinceCode
    ),
    InterestingCities
    AS
    (
        SELECT DISTINCT pc.CityName,
                        pc.StateProvinceCode,
                        pc.PopulationIn2016,
                        FLOOR(pc.GrowthRate) AS GrowthRate
        FROM PotentialCities AS pc
        INNER JOIN Dimension.City AS c
        ON pc.CityName = c.City
        WHERE GrowthRate > 2.0
        AND NOT EXISTS (SELECT 1 FROM Fact.Sale AS s WHERE s.[City Key] = c.[City Key])
    )
    SELECT TOP(100) CityName, StateProvinceCode, PopulationIn2016, GrowthRate
    FROM InterestingCities
    ORDER BY PopulationIn2016 DESC;

## <a name="clustered-columnstore-indexes"></a>Indici columnstore cluster

(Versione completa dell'esempio)

Gli indici Columnstore cluster (CCI) vengono utilizzati con tutte le tabelle dei fatti, per ridurre il footprint di archiviazione e migliorare le prestazioni delle query. Con l'utilizzo dell'indice ColumnStore cluster, l'archiviazione di base per le tabelle dei fatti Usa la compressione della colonna.

Gli indici non cluster vengono utilizzati nella parte superiore dell'indice columnstore cluster, per facilitare la chiave primaria e vincoli di chiave esterna. Questi vincoli sono stati aggiunti all'esterno di un'abbondanza di attenzione: il processo ETL origina i dati dal database WideWorldImporters, che presenta vincoli di integrità. Rimozione di vincoli di chiavi primarie ed esterne e i relativi indici supporti, consentirebbe di ridurre il footprint di memoria delle tabelle dei fatti.

**Dimensioni dei dati**

Il database di esempio ha limitato dimensioni dei dati, per renderlo semplice scaricare e installare il campione. Tuttavia, per visualizzare i vantaggi reali prestazioni degli indici columnstore, si usa un set di dati più grande.

È possibile eseguire l'istruzione seguente per aumentare le dimensioni del `Fact.Sales` tabella mediante l'inserimento di un altro 12 milioni di righe di dati di esempio. Questi sono tutti inserite righe per l'anno 2012, modo che non sia presente nessuna interferenza con il processo ETL.

    EXECUTE [Application].[Configuration_PopulateLargeSaleTable]

Questa istruzione richiederà circa 5 minuti per l'esecuzione. Per inserire più di 12 milioni di righe, passare il numero desiderato di righe da inserire come parametro a questa stored procedure.

Per confrontare le prestazioni delle query con e senza columnstore, è possibile eliminare e/o ricreare l'indice columnstore cluster.

Eliminare l'indice:

    DROP INDEX [CCX_Fact_Order] ON [Fact].[Order]

Per ricreare:

    CREATE CLUSTERED COLUMNSTORE INDEX [CCX_Fact_Order] ON [Fact].[Order]

## <a name="partitioning"></a>Partizionamento

(Versione completa dell'esempio)

Dimensioni dei dati in un Data Warehouse possono raggiungere dimensioni molto grandi. È pertanto consigliabile usare il partizionamento per gestire l'archiviazione delle tabelle nel database di grandi dimensioni.

Tutte le tabelle dei fatti più grandi vengono partizionate per anno. L'unica eccezione è `Fact.Stock Holdings`, che non è basato sulla data e ha dimensioni limitate di dati confrontata con le altre tabelle dei fatti.

Funzione di partizione utilizzata per le tabelle partizionate tutto viene `PF_Date`, e lo schema di partizione in uso è `PS_Date`.

## <a name="in-memory-oltp"></a>OLTP in memoria

(Versione completa dell'esempio)

WideWorldImportersDW Usa le tabelle ottimizzate per la memoria SCHEMA_ONLY per le tabelle di staging. Tutti i `Integration.` * `_Staging` le tabelle sono tabelle ottimizzate per la memoria SCHEMA_ONLY.

Il vantaggio di tabelle SCHEMA_ONLY è che non vengono registrate e non richiedono qualsiasi accesso al disco. Ciò migliora le prestazioni del processo ETL. Poiché tali tabelle non vengono registrate, i relativi contenuti vengono persi se si verifica un errore. Tuttavia, l'origine dati è ancora disponibile, pertanto è possibile riavviare il processo ETL è sufficiente se si verifica un errore.
