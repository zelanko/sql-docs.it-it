---
title: Configurare le impostazioni per Data Migration Assistant
description: Informazioni su come configurare le impostazioni per il Data Migration Assistant aggiornando i valori nel file di configurazione
ms.custom: seo-lt-2019
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: fc280fa541e2a6b5ea984086d694ffdd3f7c39a8
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056546"
---
# <a name="configure-settings-for-data-migration-assistant"></a>Configurare le impostazioni per Data Migration Assistant

È possibile ottimizzare determinati comportamenti di Data Migration Assistant impostando i valori di configurazione nel file DMA. exe. config. Questo articolo descrive i valori di configurazione principali.

È possibile trovare il file DMA. exe. config per l'applicazione desktop Data Migration Assistant e l'utilità da riga di comando, nelle cartelle seguenti del computer.

- Applicazione desktop

  % ProgramFiles%\\Microsoft Data Migration Assistant\\DMA. exe. config

- Utilità della riga di comando

  % ProgramFiles%\\Microsoft Data Migration Assistant\\dmacmd. exe. config 

Assicurarsi di salvare una copia del file di configurazione originale prima di apportare qualsiasi modifica. Dopo aver apportato le modifiche, riavviare Data Migration Assistant per rendere effettivi i nuovi valori di configurazione.

## <a name="number-of-databases-to-assess-in-parallel"></a>Numero di database da valutare in parallelo

Data Migration Assistant valuta più database in parallelo. Durante la valutazione Data Migration Assistant estrae l'applicazione livello dati (dacpac) per comprendere lo schema del database. Questa operazione può determinare il timeout se vengono valutati in parallelo più database nello stesso server. 

A partire da Data Migration Assistant v 2.0, è possibile controllarlo impostando il valore di configurazione parallelDatabases. Il valore predefinito è 8.

```
<advisorGroup>

<workflowSettings>

<assessment parallelDatabases="8" />

</workflowSettings>

</advisorGroup>
```




## <a name="number-of-databases-to-migrate-in-parallel"></a>Numero di database di cui eseguire la migrazione in parallelo

Data Migration Assistant esegue la migrazione di più database in parallelo, prima di eseguire la migrazione degli account di accesso. Durante la migrazione, Data Migration Assistant eseguirà il backup del database di origine, copierà facoltativamente il backup e quindi lo ripristinerà nel server di destinazione. È possibile che si verifichino errori di timeout quando sono selezionati più database per la migrazione. 

A partire da Data Migration Assistant v 2.0, se si verifica questo problema, è possibile ridurre il valore di configurazione parallelDatabases. È possibile aumentare il valore per ridurre il tempo di migrazione globale.

```
<advisorGroup>

<workflowSettings>

<migration parallelDatabases="8″ />

</workflowSettings>

</advisorGroup>
```


## <a name="dacfx-settings"></a>Impostazioni DacFX

Durante la valutazione, Data Migration Assistant estrae l'applicazione livello dati (dacpac) per comprendere lo schema del database. Questa operazione può avere esito negativo con timeout per database di dimensioni molto grandi o se il server è sotto carico. A partire dalla migrazione dei dati v 1.0, è possibile modificare i valori di configurazione seguenti per evitare errori. 

> [!NOTE]
> Per impostazione predefinita, l'intera voce &lt;DACFx&gt; è impostata come commento. Rimuovere i commenti e quindi modificare il valore in base alle esigenze.

- commandTimeout

   Questo parametro imposta la proprietà IDbCommand. CommandTimeout in *secondi*. (Valore predefinito = 60)

- databaseLockTimeout

   Questo parametro equivale a impostare il timeout di timeout [\_\_di blocco](../t-sql/statements/set-lock-timeout-transact-sql.md) , espresso in *millisecondi*. (Valore predefinito = 5000)

- maxDataReaderDegreeOfParallelism

  Questo parametro imposta il numero di connessioni del pool di connessioni SQL da utilizzare. (Valore predefinito = 8)

```
<advisorGroup>

<advisorSettings>

<dacFx  commandTimeout="60" databaseLockTimeout="5000"
maxDataReaderDegreeOfParallelism="8"/>

</advisorSettings>

</advisorGroup>
```

## <a name="stretch-database-recommendation-threshold"></a>Stretch Database: soglia di raccomandazione

Con [SQL Server stretch database](https://docs.microsoft.com/sql/sql-server/stretch-database/stretch-database)è possibile estendere dinamicamente i dati transazionali caldi e freddi da Microsoft SQL Server 2016 ad Azure. Stretch Database è destinato a database transazionali con grandi quantità di dati a freddo. La raccomandazione Stretch Database, in base alle indicazioni sulle funzionalità di archiviazione, identifica innanzitutto le tabelle che ritiene trarranno vantaggio da questa funzionalità e quindi identifica le modifiche che devono essere apportate per abilitare la tabella per questa funzionalità.

A partire da Data Migration Assistant v 2.0, è possibile controllare questa soglia affinché una tabella sia idonea per la funzionalità Stretch Database usando il valore di configurazione recommendedNumberOfRows. Il valore predefinito è 100.000 righe. Se si desidera analizzare le funzionalità di estensione per le tabelle ancora più piccole, ridurre il valore di conseguenza.

```
<advisorGroup>

<advisorSettings>

<stretchDBAdvisor  recommendedNumberOfRows="100000" />

</advisorSettings>

</advisorGroup>
```


## <a name="sql-connection-timeout"></a>Timeout connessione SQL

È possibile controllare il timeout della [connessione SQL](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectiontimeout(v=vs.110).aspx) per le istanze di origine e di destinazione durante l'esecuzione di una valutazione o una migrazione, impostando il valore di timeout della connessione su un numero di secondi specificato. Il valore predefinito è 15 secondi.

```
<appSettings>

<add key="ConnectionTimeout" value="15" />

</appSettings>
```

## <a name="ignore-error-codes"></a>Ignora codici di errore

Nel titolo di ogni regola è presente un codice di errore. Se non sono necessarie regole e si vuole ignorarle, usare la proprietà ignoreErrorCodes. È possibile specificare di ignorare un solo errore o più errori. Per ignorare più errori, utilizzare un punto e virgola, ad esempio ignoreErrorCodes = "46010; 71501". Il valore predefinito è 71501, associato a riferimenti non risolti identificati quando un oggetto fa riferimento a oggetti di sistema, ad esempio procedure, viste e così via.

```
<workflowSettings>

<assessment parallelDatabases="8" ignoreErrorCodes="71501" />

</workflowSettings>
```

## <a name="see-also"></a>Vedere anche

[Download Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)
