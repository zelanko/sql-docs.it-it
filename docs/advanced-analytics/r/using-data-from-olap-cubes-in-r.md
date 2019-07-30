---
title: Uso di dati da cubi OLAP in R
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: c8ac0827ba6bfbb2c35e594967925d16d4730915
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469869"
---
# <a name="using-data-from-olap-cubes-in-r"></a>Uso di dati da cubi OLAP in R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Il  pacchetto olapr è un pacchetto R, fornito da Microsoft per l'uso con Machine Learning Server e SQL Server, che consente di eseguire query MDX per ottenere dati da cubi OLAP. Con questo pacchetto non è necessario creare server collegati o pulire i set di righe bidimensionali; è possibile ottenere dati OLAP direttamente da R.

Questo articolo descrive l'API, oltre a una panoramica di OLAP e MDX per gli utenti R che potrebbero non essere nuovi per i database di cubi multidimensionali.

> [!IMPORTANT]
> Un'istanza di Analysis Services può supportare i cubi multidimensionali convenzionali o i modelli tabulari, ma un'istanza di non è in grado di supportare entrambi i tipi di modelli. Pertanto, prima di tentare di compilare una query MDX su un cubo, verificare che l'istanza di Analysis Services contenga modelli multidimensionali.

## <a name="what-is-an-olap-cube"></a>Che cos'è un cubo OLAP?

OLAP è breve per l'elaborazione analitica online. Le soluzioni OLAP sono ampiamente usate per l'acquisizione e l'archiviazione di dati aziendali critici nel tempo. I dati OLAP vengono utilizzati per l'analisi aziendale da un'ampia gamma di strumenti, dashboard e visualizzazioni. Per ulteriori informazioni, vedere [elaborazione analitica in linea](https://en.wikipedia.org/wiki/Online_analytical_processing).

Microsoft fornisce [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services), che consente di progettare, distribuire ed eseguire query sui dati OLAP sotto forma di _cubi_ o _modelli tabulari_. Un cubo è un database multidimensionale. Le _dimensioni_ sono simili ai facet dei dati o ai fattori in R: si usano le dimensioni per identificare alcuni subset di dati specifici che si desidera riepilogare o analizzare. Ad esempio, l'ora è una dimensione importante, quindi molte soluzioni OLAP includono più calendari definiti per impostazione predefinita, da usare durante il sezionamento e il riepilogo dei dati. 

Per motivi di prestazioni, un database OLAP spesso calcola i riepiloghi (o aggregazioni) in anticipo e li archivia per un recupero più rapido. I riepiloghi sono basati su *misure*, che rappresentano formule che possono essere applicate ai dati numerici. Si utilizzano le dimensioni per definire un subset di dati, quindi si calcola la misura su tali dati. È ad esempio possibile utilizzare una misura per calcolare le vendite totali per una determinata linea di prodotti in più trimestri meno le imposte, per segnalare i costi di spedizione medi per uno specifico fornitore, i salari cumulativi da inizio anno a pagamento e così via.

MDX, short for Multidimensional Expressions, è il linguaggio utilizzato per l'esecuzione di query sui cubi. Una query MDX contiene in genere una definizione dei dati che include una o più dimensioni e almeno una misura, sebbene le query MDX possano essere notevolmente più complesse e includano finestre in sequenza, medie cumulative, somme, rango o percentile. 

Di seguito sono riportati alcuni altri termini che possono risultare utili quando si inizia a creare query MDX:

+ Il sezionamento accetta un subset del cubo utilizzando i valori di una singola dimensione.

+ *Estrazione* crea un sottocubo specificando un intervallo di valori in più dimensioni.

+ *Drill-down* passa da un riepilogo alle informazioni dettagliate.

+ *Drill-up* passa dalle informazioni dettagliate a un livello superiore di aggregazione.

+ *Rollup* riepiloga i dati in una dimensione.

+ *Pivot* ruota il cubo o la selezione di dati.

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>Come usare olapr per creare query MDX

Nell'articolo seguente vengono forniti esempi dettagliati della sintassi per la creazione o l'esecuzione di query su un cubo:

+ [Come creare query MDX con R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>API olapr

Il pacchetto **olapR** supporta due metodi per la creazione di query MDX:

- **Utilizzare il Generatore MDX.** Usare le funzioni R nel pacchetto per generare una semplice query MDX, scegliendo un cubo e quindi impostando gli assi e i filtri dei dati. Si tratta di un modo semplice per compilare una query MDX valida se non si ha accesso agli strumenti OLAP tradizionali o se non si ha una conoscenza approfondita del linguaggio MDX.

    Non è possibile creare tutte le query MDX utilizzando questo metodo, perché MDX può essere complesso. Questa API supporta tuttavia la maggior parte delle operazioni più comuni e utili, tra cui Slice, dadi, drill-down, rollup e pivot in N dimensioni.

+ **MDX ben formato per la copia e incolla.** Creare e incollare manualmente una query MDX. Questa opzione è ottimale se si dispone di query MDX esistenti che si desidera riutilizzare o se la query da compilare è troppo complessa per la gestione di **olapr** .

    Dopo aver compilato l'MDX usando qualsiasi utilità client, ad esempio SSMS o Excel, salvare la stringa di query. Fornire questa stringa MDX come argomento al gestore di *query SSAS* nel pacchetto **olapr** . Il provider invia la query al server Analysis Services specificato e restituisce i risultati a R. 

Per esempi su come compilare una query MDX o eseguire una query MDX esistente, vedere [come creare query MDX con R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md).

## <a name="known-issues"></a>Problemi noti

In questa sezione vengono elencati alcuni problemi noti e le domande  comuni sul pacchetto olapr.

### <a name="tabular-model-support"></a>Supporto di modelli tabulari

Se ci si connette a un'istanza di Analysis Services contenente un modello tabulare, `explore` la funzione segnala l'esito positivo con un valore restituito true. Tuttavia, gli oggetti modello tabulare sono diversi dagli oggetti multidimensionali e la struttura di un database multidimensionale è diversa da quella di un modello tabulare.

Anche se DAX (Data Analysis Expressions) è il linguaggio usato in genere con i modelli tabulari, è possibile progettare query MDX valide su un modello tabulare, se si ha già familiarità con MDX. Non è possibile utilizzare i costruttori olapr per compilare query MDX valide su un modello tabulare.

Tuttavia, le query MDX non sono un modo efficiente per recuperare dati da un modello tabulare. Se è necessario ottenere dati da un modello tabulare per l'uso in R, prendere in considerazione questi metodi:

+ Abilitare DirectQuery sul modello e aggiungere il server come server collegato in SQL Server. 
+ Se il modello tabulare è stato compilato in un data mart relazionale, ottenere i dati direttamente dall'origine.

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>Come determinare se un'istanza contiene modelli tabulari o multidimensionali

Una singola istanza di Analysis Services può contenere un solo tipo di modello, anche se può contenere più modelli. Il motivo è che esistono differenze fondamentali tra i modelli tabulari e i modelli multidimensionali che controllano il modo in cui i dati vengono archiviati ed elaborati. I modelli tabulari, ad esempio, vengono archiviati in memoria e sfruttano gli indici columnstore per eseguire calcoli molto veloci. Nei modelli multidimensionali i dati vengono archiviati su disco e le aggregazioni sono definite in anticipo e recuperate tramite query MDX.

Se ci si connette a Analysis Services usando un client, ad esempio SQL Server Management Studio, è possibile stabilire immediatamente quale tipo di modello è supportato, esaminando l'icona del database.

È inoltre possibile visualizzare ed eseguire query sulle proprietà del server per determinare il tipo di modello supportato dall'istanza. La proprietà **modalità server** supporta due valori: _multidimensionale_ o _tabulare_.

Per informazioni generali sui due tipi di modelli, vedere l'articolo seguente:

+ [Confronto tra modelli multidimensionali e tabulari](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

Per informazioni sull'esecuzione di query sulle proprietà del server, vedere l'articolo seguente:

+ [Set di righe dello schema OLE DB per OLAP](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>Il writeback non è supportato

Non è possibile scrivere nuovamente i risultati dei calcoli R personalizzati nel cubo.

In generale, anche quando un cubo è abilitato per il writeback, sono supportate solo le operazioni limitate e potrebbe essere necessaria una configurazione aggiuntiva. Si consiglia di utilizzare MDX per operazioni di questo tipo.

+ [Dimensioni abilitate per la scrittura](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [Partizioni abilitate per la scrittura](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [Impostare l'accesso personalizzato ai dati delle celle](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>Query MDX con esecuzione prolungata blocco elaborazione cubi

Sebbene il  pacchetto olapr esegua solo le operazioni di lettura, le query MDX con esecuzione prolungata possono creare blocchi che impediscono l'elaborazione del cubo. Testare sempre le query MDX in anticipo in modo da conoscere la quantità di dati da restituire.

Se si tenta di connettersi a un cubo bloccato, è possibile che venga ricevuto un errore che indica che non è possibile raggiungere il SQL Server data warehouse. Le soluzioni suggerite includono l'abilitazione di connessioni remote, il controllo del nome del server o dell'istanza e così via. Tuttavia, si consideri la possibilità di una connessione aperta precedente.

Un amministratore di SSAS può impedire problemi di blocco identificando e terminando le sessioni aperte. Una proprietà timeout può essere applicata anche a query MDX a livello di server per forzare la terminazione di tutte le query con esecuzione prolungata.

## <a name="resources"></a>Risorse

Se non si ha familiarità con OLAP o con query MDX, vedere gli articoli di Wikipedia seguenti: 

+ [Cubi OLAP](https://en.wikipedia.org/wiki/OLAP_cube)
+ [Query MDX](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
