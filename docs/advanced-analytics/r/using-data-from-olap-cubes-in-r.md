---
title: Uso dei dati dai cubi OLAP in R - servizi di SQL Server Machine Learning
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: fc7158ca426b02a9275ea2142f3e97e771dbfd1e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962381"
---
# <a name="using-data-from-olap-cubes-in-r"></a>Uso dei dati dai cubi OLAP in R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Il **olapR** pacchetto è un pacchetto R, fornito da Microsoft per l'uso con Machine Learning Server e SQL Server, che ti permette di eseguire query MDX per ottenere dati dai cubi OLAP. Con questo pacchetto, non è necessario creare server collegati o pulire i set di righe bidimensionali; è possibile ottenere dati OLAP direttamente da R.

Questo articolo descrive l'API, insieme a una panoramica di OLAP e MDX per gli utenti di R che potrebbero essere nuovi per database di cubi multidimensionali.

> [!IMPORTANT]
> Un'istanza di Analysis Services può supportare convenzionali cubi multidimensionali o modelli tabulari, ma un'istanza non può supportare entrambi i tipi di modelli. Pertanto, prima di provare a compilare una query MDX su un cubo, verificare che l'istanza di Analysis Services contenente modelli multidimensionali.

## <a name="what-is-an-olap-cube"></a>Che cos'è un cubo OLAP?

OLAP è l'acronimo di elaborazione analitica in linea. Soluzioni OLAP vengono ampiamente usate per l'acquisizione e l'archiviazione dei dati aziendali critici nel tempo. I dati OLAP vengono utilizzati per l'analisi aziendale da un'ampia gamma di strumenti, dashboard e visualizzazioni. Per altre informazioni, vedere [elaborazione analitica in linea](https://en.wikipedia.org/wiki/Online_analytical_processing).

Microsoft fornisce [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services), che consente di progettare, distribuire ed eseguire query sui dati OLAP nel formato _cubi_ oppure _i modelli tabulari_. Un cubo è un database multidimensionale. _Dimensioni_ sono come facet dei dati, o fattori in r: le dimensioni si utilizzano per identificare un subset specifico dei dati che si desidera riepilogare o analizzare. Ad esempio, ora è una dimensione di importante, molto altro in modo che le soluzioni OLAP molti includono più calendari definiti per impostazione predefinita, da utilizzare durante il sezionamento e riepilogo dei dati. 

Per motivi di prestazioni, un database OLAP spesso consente di calcolare i riepiloghi (o _aggregazioni_) in anticipo e quindi li archivia per il recupero più veloce. Si basano *misure*, che rappresentano le formule che possono essere applicate ai dati numerici. Si vengono utilizzate le dimensioni per definire un subset di dati e quindi calcola la misura su quei dati. Ad esempio, si utilizzerà una misura per calcolare le vendite totali per una determinata linea di prodotto nel corso dei trimestri più meno imposte, per segnalare i costi di spedizione medio per un particolare fornitore, year-to-date annua cumulativo a pagamento e così via.

MDX, acronimo di espressioni MDX, è il linguaggio utilizzato per eseguire query sui cubi. Una query MDX in genere contiene una definizione di dati che include una o più dimensioni e almeno una misura, anche se le query MDX possono ottenere notevolmente più complesse e includono windows in sequenza, cumulative medie, somme, ranghi o percentili. 

Ecco alcune altre condizioni che possono risultare utili quando si avvia la creazione di query MDX:

+ *Il sezionamento* considera un subset del cubo utilizzando i valori da una singola dimensione.

+ *Estrazione* crea un sottocubo specificando un intervallo di valori in più dimensioni.

+ *Drill-down* passa da un riepilogo alle informazioni dettagliate.

+ *Drill-up* passa dalle informazioni dettagliate a un livello superiore di aggregazione.

+ *Rollup* riepiloga i dati in una dimensione.

+ *Pivot* ruota il cubo o la selezione di dati.

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>Come usare olapR per creare query MDX

L'articolo seguente fornisce esempi dettagliati della sintassi per la creazione o l'esecuzione di query su un cubo:

+ [Come creare query MDX con R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>olapR API

Il pacchetto **olapR** supporta due metodi per la creazione di query MDX:

- **Utilizzare il Generatore MDX.** Usare le funzioni R del pacchetto per generare una semplice query MDX, scegliendo un cubo, e quindi impostando gli assi e filtri dei dati. Questo è un modo semplice per compilare una query MDX valida se si dispone di accesso agli strumenti OLAP tradizionali o non ha una profonda conoscenza del linguaggio MDX.

    Non tutte le query MDX possono create utilizzando questo metodo, in quanto MDX può essere complessa. Tuttavia, questa API supporta la maggior parte delle operazioni più comuni e utili, tra cui sezioni, dice, drill-down, rollup e pivot nelle dimensioni N.

+ **Copiare e incollare il MDX ben formato.** Creare manualmente e quindi incollare una query MDX. Questa opzione è la migliore se si dispone di query MDX esistenti che si desidera riutilizzare o se è troppo complessa per la query da compilare **olapR** da gestire.

    Dopo aver compilato il codice MDX con qualsiasi utilità client, ad esempio SQL Server Management Studio o Excel, salvare la stringa di query. Fornire questa stringa MDX come argomento per il *gestore di query SSAS* nel **olapR** pacchetto. Il provider invia la query al server Analysis Services specificato e passati nuovamente i risultati a R. 

Per esempi di come compilare un MDX eseguire una query o eseguire una query MDX esistente, vedere [come creare query MDX con R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md).

## <a name="known-issues"></a>Problemi noti

Questa sezione sono elencati alcuni problemi noti e domande frequenti sui **olapR** pacchetto.

### <a name="tabular-model-support"></a>Supporto del modello tabulare

Se ci si connette a un'istanza di Analysis Services che contiene un modello tabulare, il `explore` funzione segnala l'esito positivo con valore restituito true. Tuttavia, gli oggetti del modello tabulare sono diversi dagli oggetti multidimensionali e la struttura di un database multidimensionale è diversa da quello di un modello tabulare.

Benché DAX (analisi dei dati Expressions) è la lingua in genere utilizzata con i modelli tabulari, è possibile progettare query MDX valide su un modello tabulare, se si ha già familiarità con MDX. È possibile usare i costruttori di olapR per compilare query MDX valide su un modello tabulare.

Tuttavia, le query MDX sono un modo inefficiente per recuperare dati da un modello tabulare. Se è necessario ottenere dati da un modello tabulare per l'uso in R, considerare invece questi metodi:

+ Abilitare DirectQuery nel modello e aggiungere il server come server collegato in SQL Server. 
+ Se il modello tabulare è stato creato in un data mart relazionale, è possibile ottenere i dati direttamente dall'origine.

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>Come determinare se un'istanza contiene modelli tabulari o multidimensionali

Una singola istanza di Analysis Services può contenere un solo tipo di modello, anche se può contenere più modelli. Il motivo è che esistono differenze fondamentali tra i modelli tabulari e i modelli multidimensionali che controllano il modo i dati vengono archiviati ed elaborati. Ad esempio, i modelli tabulari vengono archiviati in memoria e sfruttano gli indici columnstore per eseguire calcoli molto veloci. Nei modelli multidimensionali, i dati vengono archiviati su disco e le aggregazioni vengono definite in precedenza e recuperate tramite query MDX.

Se ci si connette ad Analysis Services Usa un client, ad esempio SQL Server Management Studio, è possibile stabilire immediatamente il tipo di modello supportato, esaminando l'icona per il database.

È anche possibile visualizzare ed eseguire query per determinare quale tipo di modello l'istanza supporta le proprietà del server. Il **modalità Server** proprietà supporta i due valori: _multidimensionali_ oppure _tabulare_.

Vedere l'articolo seguente per informazioni generali sui due tipi di modelli:

+ [Confronto di modelli multidimensionali e tabulari](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

Vedere l'articolo seguente per informazioni sull'esecuzione di query le proprietà del server:

+ [Set di righe dello schema OLE DB per OLAP](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>Il writeback non è supportato

Non è possibile eseguire il writeback i risultati dei calcoli R personalizzati per il cubo.

In generale, anche quando un cubo è abilitato per il writeback, sono supportate solo le operazioni limitate e potrà essere necessaria una configurazione aggiuntiva. È consigliabile utilizzare MDX per tali operazioni.

+ [Dimensioni abilitate per scrittura](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [Partizioni abilitate per scrittura](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [Impostare l'accesso personalizzato ai dati delle celle](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>Query MDX con esecuzione prolungata blocca l'elaborazione del cubo

Anche se il **olapR** pacchetto esegue solo operazioni di lettura, query MDX possono creare i blocchi che impediscono l'elaborazione del cubo con esecuzione prolungata. Testare sempre le query MDX in anticipo in modo da sapere la quantità di dati devono essere restituiti.

Se si prova a connettersi a un cubo che è stato bloccato, si potrebbe ottenere un errore che non è possibile raggiungere il data warehouse di SQL Server. Le risoluzioni consigliate includono l'abilitazione di connessioni remote, controllare il server o nome dell'istanza e così via; Tuttavia, prendere in considerazione la possibilità di una connessione aperta precedente.

Un amministratore SSAS può impedire problemi di blocco identificando e terminare le sessioni aperte. Una proprietà di timeout può essere applicata anche alle query MDX a livello di server per forzare la terminazione di tutte le query con esecuzione prolungata.

## <a name="resources"></a>Risorse

Se si ha familiarità con OLAP o per le query MDX, vedere questi articoli di Wikipedia: 

+ [Cubi OLAP](https://en.wikipedia.org/wiki/OLAP_cube)
+ [Query MDX](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
