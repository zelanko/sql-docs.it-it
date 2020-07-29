---
title: Uso dei dati dai cubi OLAP in R
description: Questo articolo descrive l'API olapR, oltre a una panoramica di OLAP e MDX per gli utenti R che potrebbero non essere esperti di database per cubi multidimensionali.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 04/15/2018
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f27866a242cb03839a67a8f68478bc786222aa64
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "86968022"
---
# <a name="using-data-from-olap-cubes-in-r"></a>Uso dei dati dai cubi OLAP in R
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Il pacchetto **olapR** è un pacchetto R, fornito da Microsoft per l'uso con Machine Learning Server e SQL Server, che consente di eseguire query MDX per ottenere dati da cubi OLAP. Con questo pacchetto, non è necessario creare server collegati o ripulire set di righe bidimensionali, ma è possibile ottenere i dati OLAP direttamente da R.

Questo articolo descrive l'API, oltre a una panoramica di OLAP e MDX per gli utenti R che potrebbero non essere esperti di database per cubi multidimensionali.

> [!IMPORTANT]
> Un'istanza di Analysis Services può supportare i cubi multidimensionali convenzionali o i modelli tabulari, ma non entrambi i tipi di modelli. Pertanto, prima di tentare di creare una query MDX su un cubo, verificare che l'istanza di Analysis Services contenga modelli multidimensionali.

## <a name="what-is-an-olap-cube"></a>Che cos'è un cubo OLAP?

OLAP è l'acronimo di Online Analytical Processing, ovvero elaborazione analitica online. Le soluzioni OLAP sono ampiamente usate per l'acquisizione e l'archiviazione dei dati aziendali critici nel tempo. I dati OLAP vengono utilizzati per l'analisi aziendale da un'ampia gamma di strumenti, dashboard e visualizzazioni. Per altre informazioni, vedere [Online analytical processing](https://en.wikipedia.org/wiki/Online_analytical_processing) (Elaborazione analitica online).

Microsoft offre [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services), che consente di progettare, distribuire ed eseguire query sui dati OLAP sotto forma di _cubi_ o _modelli tabulari_. Un cubo è un database multidimensionale. Le _dimensioni_ sono simili a facet dei dati o ai fattori in R: si usano le dimensioni per identificare alcuni subset di dati particolari da riepilogare o analizzare. Ad esempio, il tempo rappresenta una dimensione importante, quindi molte soluzioni OLAP includono più calendari definiti per impostazione predefinita, da usare durante il sezionamento e il riepilogo dei dati. 

Per motivi di prestazioni, un database OLAP spesso calcola i riepiloghi (o _aggregazioni_) in anticipo e li archivia per un recupero più rapido. I riepiloghi sono basati sulle *misure*, che rappresentano le formule che possono essere applicate ai dati numerici. Si usano le dimensioni per definire un subset di dati, quindi si calcola la misura su tali dati. È ad esempio possibile usare una misura per calcolare le vendite totali per una determinata linea di prodotti in più trimestri a netto delle imposte, per creare report dei costi di spedizione medi per uno specifico fornitore, per calcolare il totale delle retribuzioni corrisposte fino a una determinata data e così via.

MDX, acronimo di Multidimensional Expression ovvero espressione MDX, è il linguaggio usato per l'esecuzione di query sui cubi. Una query MDX contiene in genere una definizione dei dati che include una o più dimensioni e almeno una misura, sebbene le query MDX possano diventare notevolmente più complesse e includere finestre mobili, medie cumulative, somme, ranghi o percentili. 

Di seguito sono riportati alcuni altri termini che possono risultare utili quando si inizia a creare query MDX:

+ Il *sezionamento* consente di creare un subset del cubo usando valori da una singola dimensione.

+ *Estrazione* crea un sottocubo specificando un intervallo di valori in più dimensioni.

+ *Drill-down* passa da un riepilogo alle informazioni dettagliate.

+ *Drill-up* passa dalle informazioni dettagliate a un livello superiore di aggregazione.

+ *Rollup* riepiloga i dati in una dimensione.

+ *Pivot* ruota il cubo o la selezione di dati.

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>Come usare olapR per creare query MDX

Nell'articolo seguente vengono forniti esempi dettagliati della sintassi per la creazione o l'esecuzione di query su un cubo:

+ [Come creare query MDX con R](../../machine-learning/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>API olapR

Il pacchetto **olapR** supporta due metodi per la creazione di query MDX:

- **Usare il Generatore MDX.** Usare le funzioni R nel pacchetto per generare una semplice query MDX, scegliendo un cubo e quindi impostando gli assi e i filtri dei dati. Questo è un modo semplice per creare query MDX valide anche se non si ha accesso agli strumenti OLAP tradizionali o in mancanza di conoscenze approfondite del linguaggio MDX.

    Non è possibile creare tutte le query MDX usando questo metodo, perché il linguaggio MDX può essere complesso. Tuttavia, questa API supporta tutte le operazioni più comuni e utili, tra cui sezionamento, estrazione, drill-down, rollup e pivot nelle dimensioni N.

+ **Copiare e incollare codice MDX ben formato.** È possibile creare manualmente e quindi incollare qualsiasi espressione in una query MDX. Questo metodo è ottimale se sono disponibili query MDX esistenti da riutiizzare o se la query che si vuole creare è troppo complessa per la gestione con **olapR**.

    Dopo aver creato l'espressione MDX usando qualsiasi utilità client, ad esempio SSMS o Excel, salvare la stringa di query. Fornire questa stringa MDX come argomento al *gestore di query SSAS* nel pacchetto di **olapR**. Il provider invia la query al server di Analysis Services specificato e restituisce i risultati a R. 

Per esempi su come creare una query MDX o eseguire una query MDX esistente, vedere [Come creare query MDX con R](../../machine-learning/r/how-to-create-mdx-queries-using-olapr.md).

## <a name="known-issues"></a>Problemi noti

In questa sezione vengono elencati alcuni problemi noti e domande comuni sul pacchetto **olapR**.

### <a name="tabular-model-support"></a>Supporto di modelli tabulari

Se ci si connette a un'istanza di Analysis Services contenente un modello tabulare, la funzione `explore` segnala l'esito positivo con il valore restituito TRUE. Tuttavia, gli oggetti modello tabulare sono diversi dagli oggetti multidimensionali e la struttura di un database multidimensionale è diversa da quella di un modello tabulare.

Anche se DAX (Data Analysis Expression) è il linguaggio usato in genere con i modelli tabulari, è possibile progettare query MDX valide su un modello tabulare, se si ha già familiarità con MDX. Non è possibile usare i costruttori olapR per creare query MDX valide su un modello tabulare.

Tuttavia, le query MDX non sono un modo efficiente per recuperare dati da un modello tabulare. Se è necessario ottenere dati da un modello tabulare per l'uso in R, prendere invece in considerazione questi metodi:

+ Abilitare DirectQuery per il modello e aggiungere il server come server collegato in SQL Server. 
+ Se il modello tabulare è stato compilato su un data mart relazionale, ottenere i dati direttamente dall'origine.

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>Come determinare se un'istanza contiene modelli tabulari o multidimensionali

Una singola istanza di Analysis Services può contenere un solo tipo di modello, anche se può contenere più modelli. Il motivo è che esistono differenze fondamentali tra i modelli tabulari e i modelli multidimensionali dalle quali dipende la modalità di archiviazione ed elaborazione dei dati. I modelli tabulari, ad esempio, vengono archiviati in memoria e sfruttano gli indici columnstore per eseguire calcoli molto veloci. Nei modelli multidimensionali i dati vengono archiviati su disco e le aggregazioni vengono definite in anticipo e recuperate tramite query MDX.

Se ci si connette ad Analysis Services usando un client, ad esempio SQL Server Management Studio, è possibile stabilire immediatamente quale tipo di modello è supportato, esaminando l'icona del database.

È anche possibile visualizzare ed eseguire query sulle proprietà del server per determinare il tipo di modello supportato dall'istanza. La proprietà **Modalità server** supporta due valori: _multidimensionale_ o _tabulare_.

Per informazioni generali sui due tipi di modelli, vedere l'articolo seguente:

+ [Confronto tra modelli multidimensionali e tabulari](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

Per informazioni sull'esecuzione di query sulle proprietà del server, vedere l'articolo seguente:

+ [Set di righe dello schema OLE DB per OLAP](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/ms126079(v=sql.110))

### <a name="writeback-is-not-supported"></a>Il writeback non è supportato

Non è possibile scrivere nuovamente i risultati dei calcoli R personalizzati nel cubo.

In generale, anche quando un cubo è abilitato per il writeback, sono supportate solo operazioni limitate e potrebbero essere necessari interventi di configurazione aggiuntivi. Si consiglia di usare MDX per operazioni di questo tipo.

+ [Dimensioni abilitate per la scrittura](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [Partizioni abilitate per la scrittura](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [Impostare l'accesso personalizzato ai dati delle celle](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>Le query MDX con esecuzione prolungata bloccano l'elaborazione dei cubi

Sebbene il pacchetto **olapR** esegua solo operazioni di lettura, le query MDX con esecuzione prolungata possono creare blocchi che impediscono l'elaborazione del cubo. Testare sempre le query MDX in anticipo in modo da conoscere la quantità di dati da restituire.

Se si tenta di connettersi a un cubo bloccato, è possibile che venga segnalato un errore che indica che non è possibile raggiungere il data warehouse di SQL Server. Le soluzioni suggerite includono l'abilitazione di connessioni remote, il controllo del nome del server o dell'istanza e così via. Tuttavia, si consideri la possibilità di una connessione aperta precedente.

Un amministratore di SSAS può impedire problemi di blocco identificando e terminando le sessioni aperte. È anche possibile applicare una proprietà di timeout a query MDX a livello di server per forzare la terminazione di tutte le query con esecuzione prolungata.

## <a name="resources"></a>Risorse

Se non si ha familiarità con OLAP o le query MDX, vedere questi articoli di Wikipedia: 

+ [Cubi OLAP](https://en.wikipedia.org/wiki/OLAP_cube)
+ [Query MDX](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
