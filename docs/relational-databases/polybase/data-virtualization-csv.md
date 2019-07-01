---
title: Virtualizzare i dati esterni in SQL Server 2019 CTP 2.0 | Microsoft Docs
description: Questa pagina illustra i passaggi per l'uso della procedura guidata di creazione di una tabella esterna per un file CSV
author: Abiola
ms.author: aboke
ms.reviewer: jroth
manager: craigg
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: polybase
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 0a0a609d2581230418df2a7c1ae1e990a04e41ae
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/25/2019
ms.locfileid: "67388857"
---
# <a name="use-the-external-table-wizard-with-csv-files"></a>Usare la procedura guidata di creazione di una tabella esterna per i file CSV

SQL Server 2019 offre inoltre la possibilità di virtualizzare i dati da un file CSV in HDFS.  Questo processo consente ai dati di rimanere nella posizione originale, ma è possibile **virtualizzare** i dati in un'istanza di SQL Server in modo da poter eseguire query nella versione virtualizzata come per qualsiasi altra tabella in SQL Server. Con questa funzionalità sarà possibile ridurre al minimo la necessità di ricorrere a processi ETL (estrazione, trasformazione e caricamento). Ciò è possibile grazie all'uso di connettori Polybase. Per altre informazioni sulla virtualizzazione dei dati, vedere il documento [Introduzione a PolyBase](polybase-guide.md).

## <a name="prerequisite"></a>Prerequisiti

A partire da CTP 2.4, le origini dati esterne del pool di dati e del pool di archiviazione non vengono più create per impostazione predefinita nel cluster Big Data. Prima di usare la procedura guidata, creare l'origine dati esterna **SqlStoragePool** predefinita nel database di destinazione con la query Transact-SQL seguente. Verificare di aver prima cambiato il contesto della query sul database di destinazione.

```sql
-- Create default data sources for SQL Big Data Cluster
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
    CREATE EXTERNAL DATA SOURCE SqlDataPool
    WITH (LOCATION = 'sqldatapool://controller-svc/default');

IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
    CREATE EXTERNAL DATA SOURCE SqlStoragePool
    WITH (LOCATION = 'sqlhdfs://controller-svc/default');
```

## <a name="launch-the-external-table-wizard"></a>Avviare la procedura guidata Tabella esterna

Connettersi alla cartella radice di HDFS specificando l'indirizzo IP. Espandere gli elementi in Esplora oggetti. Selezionare quindi uno dei file CSV di cui si vogliono virtualizzare i dati in un'istanza di SQL Server esistente. Fare clic con il pulsante destro del mouse sul file e quindi scegliere **Create External Table From CSV File** (Crea tabella esterna da file CSV) dal menu di scelta rapida. È anche possibile creare tabelle esterne da file CSV di una cartella in HDFS a patto che i file nella cartella seguano lo stesso schema. Ciò consentirebbe di eseguire la virtualizzazione dei dati a livello di cartella evitando di elaborare i singoli file e di ottenere un set di risultati unito in join che copre tutti i dati combinati. Verrà avviata la procedura guidata Virtualize Data (Virtualizza dati). È anche possibile avviare la procedura guidata Virtualize Data (Virtualizza dati) dal riquadro comandi digitando CTRL+MAIUSC+P (in Windows) e Comando+Maiuscole+P (in Mac).

![Procedura guidata Virtualize Data (Virtualizza dati)](media/data-virtualization/csv-virtualize-data-wizard.png)

## <a name="connect-to-a-sql-server-master-instance"></a>Connettersi a un'istanza principale di SQL Server

È anche possibile specificare a quale istanza principale di SQL connettersi usando le informazioni IP, porta e credenziali. Le connessioni salvate in precedenza sono accessibili tramite la casella di riepilogo a discesa **Active SQL Server connections** (Connessioni attive di SQL Server). 
> [!NOTE]
>Se si usa una connessione salvata, gli altri campi verranno bloccati


![Selezione un'origine dati](media/data-virtualization/csv-connect-to-master.png)

Fare clic su Avanti per andare al passaggio successivo della procedura guidata che consente di impostare la chiave master del database.

## <a name="select-destination-database"></a>Selezionare il database di destinazione

In questo passaggio si sceglierà il database di destinazione all'interno del quale virtualizzare i dati. Il campo di riepilogo a discesa conterrà tutti i database accettabili nell'istanza principale di SQL specificata nella schermata precedente. Qui è anche possibile assegnare un nome alla nuova tabella esterna e vedere lo schema che verrà usato.

![Creare una chiave master del database](media/data-virtualization/csv-select-destination.png)


## <a name="preview-data"></a>Anteprima dei dati

In questa finestra sarà possibile vedere un'anteprima delle prime 50 righe del file CSV per la convalida.

Al termine della visualizzazione dell'anteprima, fare clic su "Avanti" per continuare

![Credenziali dell'origine dati esterna](media/data-virtualization/csv-preview-data.png)

## <a name="modify-columns"></a>Modificare le colonne

Nella finestra successiva sarà possibile modificare le colonne della tabella esterna che si intende creare. È possibile modificare il nome della colonna, modificare il tipo di dati, nonché consentire che le righe ammettano valori null. 

![Credenziali dell'origine dati esterna](media/data-virtualization/csv-modify-columns.png)


## <a name="summary"></a>Riepilogo

Questo passaggio visualizza un riepilogo delle selezioni. Indica l'istanza principale di SQL e informazioni sulla tabella esterna proposta. In questo passaggio è possibile scegliere **"Genera script"** per generare uno script con sintassi T-SQL per creare l'origine dati esterna o **Crea** per creare l'oggetto origine dati esterna.

![Schermata Riepilogo](media/data-virtualization/csv-virtualize-data-summary.png)

Se si fa clic su "Crea" sarà possibile vedere la tabella esterna creata nel database di destinazione.

![Origini dati esterne](media/data-virtualization/csv-external-data-sources.png)

Se si fa clic su **Genera script** verrà visualizzata la query T-SQL generata per la creazione dell'oggetto origine dati esterna.

![Genera script](media/data-virtualization/csv-generated-script.png)

> [!NOTE]
> Il pulsante Genera script deve essere visibile solo nell'ultima pagina della procedura guidata. Attualmente viene visualizzato in tutte le pagine.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data di SQL Server e gli scenari correlati, vedere [What is SQL Server Big Data Cluster?](../../big-data-cluster/big-data-cluster-overview.md) (Che cos'è un cluster Big Data di SQL Server?).
