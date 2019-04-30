---
title: Statistiche automatiche (sistema di piattaforma Analitica)
description: Vengono descritte funzionalità statistiche automatico introdotta in AU7 sistema di piattaforma Analitica.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: e48d40d78c25431fd6e5592dacfa410723b31f82
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63057064"
---
# <a name="configure-auto-statistics"></a>Configurare automaticamente le statistiche

Informazioni su come configurare Parallel Data Warehouse per l'uso automatico statistiche per creare e aggiornare automaticamente le statistiche.  Usare questa funzionalità per migliorare i piani di query e pertanto migliorare le prestazioni delle query.

**Si applica a:** AP (a partire da 2016 AU7)

## <a name="what-are-statistics"></a>Quali sono le statistiche?
Le statistiche di ottimizzazione delle query sono oggetti che contengono informazioni statistiche sulla distribuzione dei valori in una o più colonne di una tabella. Query optimizer Usa queste statistiche per stimare la cardinalità o numero di righe, nella query. Queste stime della cardinalità consentono a query optimizer creare un piano di query di alta qualità. Ad esempio, in punti di accesso, la MPP query optimizer Usa le stime della cardinalità per scegliere di riprodurre in modo casuale o replicare il meno elevato tra due tabelle utilizzate in una clausola join e in questo modo le prestazioni delle query.  Per altre informazioni, vedere [statistiche](../relational-databases/statistics/statistics.md) e [DBCC SHOW_STATISTICS](../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)

## <a name="what-are-auto-statistics"></a>Quali sono le statistiche automatico?
Statistiche automatiche sono statistiche che query optimizer vengono create e aggiornate automaticamente per migliorare il piano di query. Le statistiche possono diventare non aggiornate dopo il caricamento, lo inserisce, aggiornano e le operazioni di eliminazione. Senza statistiche automatico, è necessario eseguire la propria analisi per comprendere le colonne necessarie statistiche e quando le statistiche dovranno essere aggiornati.

Statistiche automatico includono le tre impostazioni seguenti: 

### <a name="autocreatestatistics"></a>AUTO_CREATE_STATISTICS
Quando l'opzione per la creazione automatica delle statistiche, AUTO_CREATE_STATISTICS, è impostata su ON, Query Optimizer crea le statistiche necessarie per colonne singole nel predicato di query, per migliorare le stime della cardinalità per il piano di query. Queste statistiche di colonna singola vengono create in colonne che ancora non dispongono di un istogramma in un oggetto statistiche esistente.

### <a name="autoupdatestatistics"></a>AUTO_UPDATE_STATISTICS 
Quando l'opzione per l'aggiornamento automatico delle statistiche, AUTO_UPDATE_STATISTICS, è impostata su ON, Query Optimizer determina se le statistiche potrebbero non essere aggiornate, quindi ne esegue l'aggiornamento qualora vengano utilizzate tramite una query. Le statistiche diventano obsolete in seguito a operazioni di inserimento, aggiornamento, eliminazione o unione che modificano la distribuzione dei dati nella tabella o nella vista indicizzata. Query Optimizer determina che le statistiche potrebbero non essere aggiornate contando il numero di modifiche apportate ai dati dopo l'ultimo aggiornamento delle statistiche e confrontando il numero di modifiche con una soglia basata sul numero di righe nella tabella o nella vista indicizzata.

### <a name="autoupdatestatisticsasync"></a>AUTO_UPDATE_STATISTICS_ASYNC
L'opzione relativa all'aggiornamento asincrono delle statistiche, AUTO_UPDATE_STATISTICS_ASYNC, determina se Query Optimizer usa gli aggiornamenti sincroni o asincroni delle statistiche. Per i punti di accesso, l'opzione relativa all'aggiornamento asincrono delle statistiche è impostata su ON per impostazione predefinita e Query Optimizer Aggiorna le statistiche in modo asincrono. L'opzione AUTO_UPDATE_STATISTICS_ASYNC si applica a oggetti statistiche creati per indici, colonne singole nei predicati di query e statistiche create con l'istruzione CREATE STATISTICS.

## <a name="configuration-settings-for-system-administrators"></a>Impostazioni di configurazione per gli amministratori di sistema
Dopo l'aggiornamento a AU7 APS, statistiche automatico sono abilitata per impostazione predefinita. L'amministratore di sistema può abilitare o disabilitare le statistiche automatico con il [opzione della funzionalità](appliance-feature-switch.md) opzione in Gestione configurazione di Appliance.  Una volta abilitata, gli utenti possono modificare le impostazioni delle statistiche per ogni database.
La modifica dei valori di parametro funzionalità richiede un riavvio del servizio sui punti di accesso.

## <a name="change-auto-statistics-settings-on-a-database"></a>Modificare le impostazioni delle statistiche automatico in un database
Quando le statistiche automatico sono abilitata dall'amministratore di sistema, è possibile usare [ALTER DATABASE (Parallel Data Warehouse)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) per modificare le impostazioni delle statistiche in un database. Se l'opzione della funzionalità delle statistiche automatico è abilitato dall'amministratore di sistema, i nuovi database creati dopo l'aggiornamento a AU7 avrà statistiche automatico abilitate. Tutti i database esistenti prima dell'aggiornamento a AU7 presentano statistiche automatico disabilitate. L'esempio seguente Abilita le statistiche automatiche per myPDW il database esistente.

```sql
ALTER DATABASE myPDW SET AUTO_CREATE_STATISTICS ON
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS ON 
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS_ASYNC ON
```
 
Opzione AUTO_UPDATE STATISTICS_ASYNC funziona solo se la proprietà AUTO_UPDATE_STATISTICS è impostata su ON.  Di conseguenza, le statistiche non vengono aggiornate quando AUTO_UPDATE_STATISTICS è impostata su OFF e AUTO_UPDATE_STATISTICS_ASYNC è ON. 

### <a name="error-messages"></a>Messaggi di errore
Si potrebbe ricevere il messaggio di errore "questa opzione non è supportata in PDW".  Questo errore si verifica quando l'amministratore di sistema non ha abilitato le statistiche automatiche, e si tenta di impostare uno qualsiasi dei automatica opzioni relative alle statistiche in ALTER DATABASE. 

### <a name="limitations-and-restrictions"></a>Limitazioni e restrizioni
Statistiche automatico non funziona per le tabelle esterne. 

### <a name="check-the-current-values"></a>Controllare i valori correnti
La query seguente restituisce i valori correnti delle impostazioni delle statistiche automatico per tutti i database.

```sql
SELECT NAME
    , IS_AUTO_CREATE_STATS_ON 
    , IS_AUTO_UPDATE_STATS_ON
    , IS_AUTO_UPDATE_STATS_ASYNC_ON
FROM
    sys.databases;
```

È un valore restituito pari a 1 indica che le impostazioni di in e 0 indica che l'impostazione è disattivata. 

## <a name="next-steps"></a>Passaggi successivi
Per prestazioni delle query, vedere [monitoraggio delle query attive](monitoring-active-queries.md)
