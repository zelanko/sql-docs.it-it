---
title: Contenuto dei modelli di data mining (Analysis Services - Data Mining) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5fe10a98910f54e4317d0191753d40b9b6b0b94f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62736082"
---
# <a name="mining-model-content-analysis-services---data-mining"></a>Mining Model Content (Analysis Services - Data Mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In seguito alla progettazione e all'elaborazione di un modello di data mining mediante i dati della struttura di data mining sottostante, il modello di data mining è completo e contiene il *contenuto del modello di data mining*. È possibile utilizzare questo contenuto per eseguire stime o analisi di dati.  
  
 Il contenuto del modello di data mining include i metadati relativi al modello, statistiche sui dati e modelli individuati dall'algoritmo di data mining. A seconda dell'algoritmo utilizzato, il contenuto del modello può includere formule di regressione, le definizioni di regole e set di elementi, o pesi e altre statistiche.  
  
 Il contenuto del modello di data mining viene visualizzato in una struttura standard a prescindere dall'algoritmo utilizzato. È possibile esplorare la struttura tramite Microsoft Generic Content Tree Viewer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]e quindi passare a un visualizzatore personalizzato per visualizzare il modo in cui le informazioni sono interpretate e visualizzate graficamente per ogni tipo di modello. È inoltre possibile creare query sul contenuto del modello di data mining con un client che supporti il set di righe dello schema MINING_MODEL_CONTENT. Per altre informazioni, vedere [Attività e procedure relative alle query di data mining](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md).  
  
 In questa sezione viene illustrata la struttura di base del contenuto per tutti i tipi di modelli di data mining. Vengono descritti i tipi di nodo comuni al contenuto del modello di data mining e fornite istruzioni sull'interpretazione delle informazioni.  
  
 [Struttura del contenuto del modello di data mining](#bkmk_Structure)  
  
 [Nodi nel contenuto del modello](#bkmk_Nodes)  
  
 [Contenuto del modello di data mining in base al tipo di algoritmo](#bkmk_AlgoType)  
  
 [Strumenti per la visualizzazione del contenuto di un modello di data mining](#bkmk_Viewing)  
  
 [Strumenti per l'esecuzione di query sul contenuto di un modello di data mining](#bkmk_Querying)  
  
##  <a name="bkmk_Structure"></a> Struttura del contenuto del modello di data mining  
 Il contenuto di ciascun modello viene presentato come una serie di *nodi*. Un nodo è un oggetto all'interno di un modello di data mining che contiene i metadati e le informazioni su una parte del modello. I nodi sono disposti in una gerarchia e la loro disposizione esatta, nonché il significato della gerarchia, dipende dall'algoritmo utilizzato. Se ad esempio si crea un modello di albero delle decisioni, il modello può contenere più alberi collegati al nodo radice del modello; se si crea un modello di rete neurale, il modello può contenere una o più reti e un nodo di statistiche.  
  
 Il primo nodo di ogni modello è denominato *nodo radice*o nodo *padre del modello* . Ogni modello dispone di un nodo radice (NODE_TYPE = 1). Il nodo radice contiene in genere alcuni metadati relativi al modello e il numero di nodi figlio, ma poche informazioni aggiuntive sui modelli individuati dal modello.  
  
 Il numero di nodi figlio presenti nel nodo radice varia a seconda dell'algoritmo utilizzato per creare il modello. I nodi figlio hanno significati diversi e contengono contenuto diverso, a seconda dell'algoritmo e della profondità e complessità dei dati.  
  
##  <a name="bkmk_Nodes"></a> Nodi nel contenuto del modello di data mining  
 In un modello di data mining, un nodo è un contenitore generico in cui sono archiviate informazioni riguardanti tutto il modello o una parte di esso. La struttura di ogni nodo è sempre la stessa e contiene le colonne definite dal set di righe dello schema di data mining. Per altre informazioni, vedere [Set di righe DMSCHEMA_MINING_MODEL_CONTENT](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset).  
  
 Ogni nodo include i relativi metadati, tra cui un identificatore univoco all'interno di ciascun modello, l'ID del nodo padre e il numero di nodi figlio presenti. I metadati identificano il modello di appartenenza del nodo e il catalogo del database in cui è archiviato quel modello specifico. Il contenuto aggiuntivo presente nel nodo varia in base al tipo di algoritmo utilizzato per creare il modello e potrebbe includere gli elementi seguenti:  
  
-   Conteggio dei case nei dati di training che supporta un determinato valore stimato.  
  
-   Statistiche, quali media, deviazione standard o varianza.  
  
-   Coefficienti e formule.  
  
-   Definizione di regole e puntatori secondari.  
  
-   Frammenti XML che descrivono una parte del modello.  
  
### <a name="list-of-mining-content-node-types"></a>Elenco di tipi di nodo del contenuto di data mining  
 Nella tabella seguente sono elencati i diversi tipi di nodo restituiti nei modelli di data mining. Poiché ogni algoritmo elabora in modo diverso le informazioni, ciascun modello genera solo alcuni tipi specifici di nodi. Modificando l'algoritmo, il tipo di nodo potrebbe cambiare. Il contenuto di ogni nodo potrebbe inoltre cambiare se si rielabora il modello.  
  
> [!NOTE]  
>  Se si usa un servizio di data mining, o se si creano algoritmi plug-in, i tipi di nodo personalizzati aggiuntivi potrebbero essere disponibili.  
  
|ID NODE_TYPE|Etichetta del nodo|Contenuto del nodo|  
|-------------------|----------------|-------------------|  
|1|Modello|Metadati e nodo di contenuto radice. Si applica a tutti i tipi di modello.|  
|2|Tree|Nodo radice di un albero di classificazione. Si applica ai modelli di albero delle decisioni.|  
|3|Interior|Nodo interno di divisione in un albero. Si applica ai modelli di albero delle decisioni.|  
|4|Distribuzione|Nodo finale di un albero. Si applica ai modelli di albero delle decisioni.|  
|5|Cluster|Cluster rilevato dall'algoritmo. Si applica ai modelli di clustering e ai modelli Sequence Clustering.|  
|6|Unknown|Tipo di nodo sconosciuto.|  
|7|ItemSet|Set di elementi rilevato dall'algoritmo. Si applica ai modelli di associazione o ai modelli Sequence Clustering.|  
|8|AssociationRule|Regola di associazione rilevata dall'algoritmo. Si applica ai modelli di associazione o ai modelli Sequence Clustering.|  
|9|PredictableAttribute|Attributo stimabile. Si applica a tutti i tipi di modello.|  
|10|InputAttribute|Attributo di input. Si applica ai modelli di alberi delle decisioni e Naive Bayes.|  
|11|InputAttributeState|Statistiche relative agli stati di un attributo di input. Si applica ai modelli di alberi delle decisioni e Naive Bayes.|  
|13|Sequenza|Nodo di livello superiore per un componente del modello Markov di un cluster di sequenza. Si applica ai modelli Sequence Clustering.|  
|14|Transition|Matrice di transizione Markov. Si applica ai modelli Sequence Clustering.|  
|15|TimeSeries|Nodo non radice di un albero di serie temporali. Si applica solo ai modelli Time Series.|  
|16|TsTree|Nodo radice di un albero di serie temporali corrispondente a una serie temporale stimabile. Si applica ai modelli Time Series e solo se il modello è stato creato utilizzando il parametro MIXED.|  
|17|NNetSubnetwork|Subnet. Si applica ai modelli di rete neurale.|  
|18|NNetInputLayer|Gruppo che contiene i nodi del livello di input. Si applica ai modelli di rete neurale.|  
|19|NNetHiddenLayer|Gruppi contenenti i nodi che descrivono il livello nascosto. Si applica ai modelli di rete neurale.|  
|21|NNetOutputLayer|Gruppi che contengono i nodi del livello di output. Si applica ai modelli di rete neurale.|  
|21|NNetInputNode|Nodo nel livello di input che corrisponde a un attributo di input con gli stati corrispondenti. Si applica ai modelli di rete neurale.|  
|22|NNetHiddenNode|Nodo nel livello nascosto. Si applica ai modelli di rete neurale.|  
|23|NNetOutputNode|Nodo nel livello di output. Questo nodo di solito corrisponde a un attributo di output e agli stati corrispondenti. Si applica ai modelli di rete neurale.|  
|24|NNetMarginalNode|Statistiche marginali sul set di training. Si applica ai modelli di rete neurale.|  
|25|RegressionTreeRoot|Nodo radice di un albero di regressione. Si applica ai modelli di regressione lineare e ai modelli di albero delle decisioni che contengono attributi continui di input.|  
|26|NaiveBayesMarginalStatNode|Statistiche marginali sul set di training. Si applica ai modelli Naive Bayes.|  
|27|ArimaRoot|Nodo radice di un modello ARIMA. Si applica solo ai modelli Time Series che utilizzano l'algoritmo ARIMA.|  
|28|ArimaPeriodicStructure|Struttura periodica in un modello ARIMA. Si applica solo ai modelli Time Series che utilizzano l'algoritmo ARIMA.|  
|29|ArimaAutoRegressive|Coefficiente autoregressivo per un singolo termine in un modello ARIMA.<br /><br /> Si applica solo ai modelli Time Series che utilizzano l'algoritmo ARIMA.|  
|30|ArimaMovingAverage|Coefficiente di media mobile per un singolo termine in un modello ARIMA. Si applica solo ai modelli Time Series che utilizzano l'algoritmo ARIMA.|  
|1000|CustomBase|Punto iniziale dei tipi di nodo personalizzati. I tipi di nodo personalizzati devono essere Integer maggiori di questa costante. Si applica ai modelli creati tramite algoritmi plug-in personalizzati.|  
  
### <a name="node-id-name-caption-and-description"></a>ID, nome, didascalia e descrizione dei nodi  
 Il valore dell'ID univoco,**NODE_UNIQUE_NAME**, del nodo radice di qualsiasi modello è sempre uguale a 0. Tutti gli ID dei nodi vengono assegnati automaticamente da Analysis Services e non possono essere modificati.  
  
 Il nodo radice di ogni modello contiene anche i metadati di base relativi al modello. Tra i metadati sono inclusi il database di Analysis Services in cui viene archiviato il modello (**MODEL_CATALOG**), lo schema (**MODEL_SCHEMA)** e il nome del modello (**MODEL_NAME)** . Queste informazioni sono ripetute in tutti i nodi del modello, pertanto non è necessario eseguire query sul nodo radice per ottenere i metadati.  
  
 Oltre al nome usato come identificatore univoco, ogni nodo dispone di un *nome* ,**NODE_NAME**, che viene creato automaticamente dall'algoritmo a scopo di visualizzazione e non può essere modificato.  
  
> [!NOTE]  
>  L'algoritmo Microsoft Clustering consente di assegnare nomi descrittivi a ogni cluster. Questi nomi descrittivi, tuttavia, non vengono salvati in modo permanente sul server e se si rielabora il modello l'algoritmo genera nuovi nomi per i cluster.  
  
 La *didascalia* e la *descrizione* relative a ogni nodo sono generate automaticamente dall'algoritmo e fungono da etichette per conoscere il contenuto del nodo. Il testo generato per ogni campo dipende dal tipo di modello. A volte il nome, la didascalia e la descrizione contengono esattamente la stessa stringa, ma in alcuni modelli la descrizione può contenere informazioni aggiuntive. Per informazioni dettagliate sull'implementazione, vedere l'argomento relativo al singolo tipo di modello.  
  
> [!NOTE]  
>  Il server Analysis Services supporta la ridenominazione dei nodi solo se i modelli vengono compilati tramite un algoritmo plug-in personalizzato che implementa la ridenominazione. Per abilitare la ridenominazione, è necessario eseguire l'override dei metodi durante la creazione dell'algoritmo plug-in.  
  
### <a name="node-parents-node-children-and-node-cardinality"></a>Padri, figli e cardinalità dei nodi  
 La relazione tra nodi padre e nodi figlio in una struttura ad albero è determinata dal valore della colonna PARENT_UNIQUE_NAME. Questo valore è archiviato nel nodo figlio e indica l'ID del nodo padre. Di seguito sono riportati alcuni esempi delle modalità di utilizzo di queste informazioni:  
  
-   Se il valore della colonna PARENT_UNIQUE_NAME è NULL, il nodo è il nodo di livello superiore del modello.  
  
-   Se il valore di PARENT_UNIQUE_NAME è 0, il nodo deve essere un discendente diretto del nodo di livello superiore del modello. Il valore dell'ID del nodo radice infatti è sempre 0.  
  
-   È possibile individuare discendenti o padri di un determinato nodo utilizzando funzioni in query DMX (Data Mining Extensions). Per altre informazioni sull'utilizzo di funzioni nelle query, vedere [Query di data mining](../../analysis-services/data-mining/data-mining-queries.md).  
  
 Il termine*cardinalità* fa riferimento al numero di elementi contenuti in un set. Nel contesto di un modello di data mining elaborato, la cardinalità indica il numero di figli di uno specifico nodo. Ad esempio, in presenza di un modello di albero delle decisioni con un nodo [Yearly Income] che dispone a sua volta di due nodi figlio, uno per la condizione [Yearly Income] = High e uno per la condizione [Yearly Income] = Low, il valore di CHILDREN_CARDINALITY per il nodo [Yearly Income] è uguale a 2.  
  
> [!NOTE]  
>  In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], durante il calcolo della cardinalità di un nodo vengono contati solo i nodi figlio immediati. Tuttavia, se si crea un algoritmo plug-in personalizzato, è possibile eseguire l'overload di CHILDREN_CARDINALITY per contare la cardinalità in modo diverso. L'operazione può essere utile, ad esempio, per contare il numero complessivo di discendenti, non solo i figli immediati.  
  
 Sebbene la cardinalità sia contata nello stesso modo per tutti i modelli, la modalità di interpretazione o utilizzo del valore della cardinalità varia in base al tipo di modello. In un modello di clustering, ad esempio, la cardinalità del nodo di livello superiore indica il numero di transizioni trovate. In altri tipi di modello, il valore della cardinalità può sempre essere impostato a seconda del tipo di nodo. Per ulteriori informazioni sull'interpretazione della cardinalità, vedere l'argomento relativo al singolo tipo di modello.  
  
> [!NOTE]  
>  Alcuni modelli, quali quelli creati dall'algoritmo Microsoft Neural Network, contengono inoltre uno speciale tipo di nodo che fornisce statistiche descrittive sui dati di training per l'intero modello. Per definizione, questi nodi non dispongono mai di nodi figlio.  
  
### <a name="node-distribution"></a>node distribution  
 Nella colonna NODE_DISTRIBUTION è contenuta una tabella nidificata che fornisce importanti e dettagliate informazioni sui modelli individuati dall'algoritmo per molti nodi. Le statistiche esatte fornite nella tabella variano a seconda del tipo di modello, della posizione del nodo nell'albero e del fatto che l'attributo stimabile sia un valore numerico continuo o un valore discreto; possono tuttavia includere i valori minimo e massimo di un attributo, i pesi assegnati ai valori, il numero di case presenti in un nodo, i coefficienti utilizzati in una formula di regressione e misure statistiche quali deviazione standard e varianza. Per ulteriori informazioni su come interpretare la distribuzione dei nodi, vedere l'argomento relativo al tipo specifico di modello utilizzato.  
  
> [!NOTE]  
>  A seconda del tipo di nodo, la tabella NODE_DISTRIBUTION può essere vuota. Alcuni nodi ad esempio hanno esclusivamente lo scopo di organizzare una raccolta di nodi figlio e sono i nodi figlio a contenere le statistiche dettagliate.  
  
 Nella tabella nidificata NODE_DISTRIBUTION sono contenute sempre le colonne riportate di seguito. Il contenuto di ciascuna colonna varia a seconda del tipo di modello. Per ulteriori informazioni su tipi di modello specifici, vedere [Contenuto del modello di data mining in base al tipo di algoritmo](#bkmk_AlgoType).  
  
 ATTRIBUTE_NAME  
 Il contenuto varia in base all'algoritmo. Può essere il nome di una colonna, ad esempio un attributo stimabile, una regola, un set di elementi o un'informazione interna all'algoritmo come la porzione di una formula.  
  
 Questa colonna può contenere inoltre una coppia attributo-valore.  
  
 ATTRIBUTE_VALUE  
 Valore dell'attributo specificato in ATTRIBUTE_NAME.  
  
 Se il nome dell'attributo è una colonna, nel caso più semplice ATTRIBUTE_VALUE contiene uno dei valori discreti per la colonna.  
  
 A seconda dei valori elaborati dall'algoritmo, nella colonna ATTRIBUTE_VALUE può essere presente anche un flag che indica se esiste un valore per l'attributo (**Existing**) o se il valore è Null (**Missing**).  
  
 Ad esempio, se il modello è configurato per la ricerca dei clienti che hanno acquistato almeno una volta un determinato elemento, nella colonna ATTRIBUTE_NAME potrebbe essere contenuta la coppia attributo-valore che definisce l'elemento di interesse, ad esempio `Model = 'Water bottle'`, e nella colonna ATTRIBUTE_VALUE solo la parola chiave **Existing** o **Missing**.  
  
 SUPPORT  
 Conteggio dei case che dispongono di questa coppia attributo-valore o che contengono questo set di elementi o regola.  
  
 In generale, il valore di supporto per ogni nodo indica quanti case del set di training sono inclusi nel nodo corrente. Nella maggior parte dei tipi di modelli il supporto rappresenta il conteggio esatto dei case. I valori di supporto sono utili perché consentono di visualizzare la distribuzione dei dati all'interno dei case di training senza che sia necessario eseguire una query sui dati di training. Questi valori vengono inoltre utilizzati dal server Analysis Services per confrontare la probabilità archiviata con la probabilità precedente in modo da determinare se l'inferenza è forte o debole.  
  
 In un albero di classificazione, ad esempio, il valore di supporto indica il numero di case che dispongono della combinazione di attributi descritta.  
  
 In un albero delle decisioni, la somma del supporto in ciascun livello dell'albero ammonta al supporto del nodo padre. Ad esempio, se un modello che contiene 1200 case viene diviso equamente per genere e quindi suddiviso equamente per tre valori per i nodi di reddito basso, medio e alto, il figlio del nodo (2), che costituiscono nodi (4), (5) e (6), ammontano sempre allo stesso numero di case come nodo (2).  
  
|ID e attributi del nodo|Conteggio del supporto|  
|---------------------------------|-------------------|  
|(1) Model root|1200|  
|(2) Gender = Male<br /><br /> (3) Gender = Female|600<br /><br /> 600|  
|(4) Gender = Male e Income = High<br /><br /> (5) Gender = Male e Income = Medium<br /><br /> (6) Gender = Male e Income = Low|200<br /><br /> 200<br /><br /> 200|  
|(7) Gender = Female e Income = High<br /><br /> (8) Gender = Female e Income = Medium<br /><br /> (9) Gender = Female e Income = Low|200<br /><br /> 200<br /><br /> 200|  
  
 Per un modello di clustering, è possibile ponderare il numero di supporto in modo da includere le probabilità di appartenenza a più cluster. L'appartenenza a più cluster costituisce il metodo di clustering predefinito. In questo scenario, poiché ogni case non appartiene necessariamente a un unico cluster, il supporto in questi modelli potrebbe non raggiungere il 100% in tutti i cluster.  
  
 PROBABILITY  
 Indica la probabilità per il nodo specificato all'interno dell'intero modello.  
  
 La probabilità rappresenta generalmente il supporto per questo determinato valore, diviso per il totale dei case all'interno del nodo (NODE_SUPPORT).  
  
 La probabilità è tuttavia leggermente adattata per eliminare distorsioni provocate da valori mancanti nei dati.  
  
 Ad esempio, se i valori correnti per [Total Children] sono 1 e 2, si desidera evitare di creare un modello che stimi che è impossibile non avere figli oppure avere tre figli. Per assicurarsi che i valori mancanti siano improbabili ma non impossibili, l'algoritmo aggiunge sempre 1 al conteggio dei valori effettivi per qualsiasi attributo.  
  
 Esempio:  
  
 Probabilità per [Total Children = 1] = [Conteggio dei case in cui Total Children è uguale a 1] + 1/[Conteggio di tutti i case] + 3  
  
 Probabilità per [Total Children = 2] = [Conteggio dei case in cui Total Children è uguale a 2] + 1/[Conteggio di tutti i case] + 3  
  
> [!NOTE]  
>  Il valore 3 dell'adattamento è calcolato aggiungendo 1 al numero complessivo di valori n esistenti.  
  
 Dopo l'adattamento le probabilità per tutti i valori sono ancora uguali a 1. La probabilità per il valore senza dati (in questo esempio, [Total Children = '0', '3' o un altro valore]), inizia da un livello molto basso diverso da zero e aumenta lentamente man mano che vengono aggiunti altri case.  
  
 variance  
 Indica la varianza dei valori all'interno del nodo. Per definizione, la varianza dei valori discreti è sempre 0. Se il modello supporta valori continui, la varianza viene calcolata come σ (sigma), usando il denominatore n o il numero di case presenti nel nodo.  
  
 In generale, la deviazione standard,**StDev**, viene rappresentata tramite due definizioni: un metodo per il calcolo della deviazione standard prende in considerazione la distorsione, mentre l'altro calcola la deviazione standard senza utilizzare la distorsione. In generale, gli algoritmi di data mining di Microsoft non utilizzano la distorsione durante il calcolo della deviazione standard.  
  
 Il valore visualizzato nella tabella NODE_DISTRIBUTION costituisce il valore effettivo per gli attributi discreti e discretizzati e la media per i valori continui.  
  
 VALUE_TYPE  
 Indica il tipo di dati del valore o attributo e l'utilizzo del valore. Determinati tipi di valore si applicano solo a determinati tipi di modello:  
  
|ID VALUE_TYPE|Valore dell'etichetta|Nome del tipo di valore|  
|--------------------|-----------------|---------------------|  
|1|Missing|Indica che i dati del case non contengono un valore per questo attributo. Lo stato **Missing** è calcolato separatamente dagli attributi con valori.|  
|2|Existing|Indica che i dati del case contengono un valore per questo attributo.|  
|3|Continuo|Indica che il valore dell'attributo è un valore numerico continuo che può pertanto essere rappresentato da una media, insieme alle varianza e deviazione standard.|  
|4|Discrete|Indica che un valore di testo o numerico viene trattato come discreto.<br /><br /> **Nota** i valori discreti possono anche essere mancanti; tuttavia, vengono gestiti in modo diverso durante l'esecuzione dei calcoli. Per informazioni, vedere [Valori mancanti &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md).|  
|5|Discretizzato|Indica che l'attributo contiene valori numerici discretizzati. Il valore sarà una stringa formattata che descrive i bucket di discretizzazione.|  
|6|Existing|Indica che l'attributo dispone di valori numerici continui e che i valori sono stati forniti nei dati, a fronte di valori mancanti o derivati.|  
|7|Coefficiente|Indica un valore numerico che rappresenta un coefficiente.<br /><br /> Un coefficiente è un valore che viene applicato durante il calcolo della variabile dipendente. Ad esempio, se il modello crea una formula di regressione che stima il reddito in base all'età, il coefficiente viene utilizzato nella formula di correlazione dell'età al reddito.|  
|8|Miglioramento punteggio|Indica un valore numerico che rappresenta il miglioramento del punteggio di un attributo.|  
|9|Statistiche|Indica un valore numerico che rappresenta una statistica per un regressore.|  
|10|Nome univoco nodo|Indica che il valore non deve essere gestito come valore numerico o stringa, ma come l'identificatore univoco di un altro nodo di contenuto del modello.<br /><br /> In un modello di rete neurale, ad esempio, gli ID forniscono puntatori dai nodi presenti nel livello di output ai nodi nel livello nascosto, e dai nodi presenti nel livello nascosto ai nodi nel livello di input.|  
|11|Intercetta|Indica un valore numerico che rappresenta l'intercetta in una formula di regressione.|  
|12|Periodicità|Indica che il valore denota una struttura periodica nel modello.<br /><br /> Si applica solo a modelli Time Series che contengono un modello ARIMA.<br /><br /> Nota: L'algoritmo Microsoft Time Series rileva automaticamente le strutture periodiche basate sui dati di training. pertanto le periodicità del modello finale possono includere valori di periodicità che non sono stati forniti come parametri durante la creazione del modello.|  
|13|Ordine autoregressivo|Indica che il valore rappresenta il numero di serie autoregressive.<br /><br /> Si applica a modelli Time Series che utilizzano l'algoritmo ARIMA.|  
|14|Ordine media mobile|Rappresenta un valore che indica il numero di medie mobili in una serie.<br /><br /> Si applica a modelli Time Series che utilizzano l'algoritmo ARIMA.|  
|15|Ordine delle differenze|Rappresenta un valore che indica il numero di volte in cui viene differenziata la serie.<br /><br /> Si applica a modelli Time Series che utilizzano l'algoritmo ARIMA.|  
|16|Boolean|Rappresenta un tipo booleano.|  
|17|Altro|Rappresenta un valore personalizzato definito dall'algoritmo.|  
|18|Stringa visualizzabile|Rappresenta un valore personalizzato che viene visualizzato come stringa dall'algoritmo. Non è stata applicata alcuna formattazione dal modello a oggetti.|  
  
 I tipi di valore derivano dall'enumerazione ADMOMD.NET. Per altre informazioni, vedere <xref:Microsoft.AnalysisServices.AdomdServer.MiningValueType>.  
  
### <a name="node-score"></a>Punteggio del nodo  
 Il significato del punteggio del nodo varia a seconda del tipo di modello e può anche essere specifico del tipo di nodo. Per informazioni sulla modalità di calcolo di NODE_SCORE per ogni modello e tipo di nodo, vedere [Contenuto del modello di data mining in base al tipo di algoritmo](#bkmk_AlgoType).  
  
### <a name="node-probability-and-marginal-probability"></a>Probabilità del nodo e probabilità marginale  
 Nel set di righe dello schema del modello di data mining sono incluse le colonne NODE_PROBABILITY e MARGINAL_PROBABILITY per tutti i tipi di modello. Queste colonne contengono valori solo nei nodi che hanno un valore significativo di probabilità. Il nodo radice di un modello, ad esempio, non contiene mai un punteggio di probabilità.  
  
 Nei nodi che forniscono punteggi di probabilità, la probabilità del nodo e le probabilità marginali costituiscono calcoli diversi.  
  
-   La**probabilità marginale** indica la probabilità di raggiungere il nodo dal padre.  
  
-   La**probabilità del nodo** indica la probabilità di raggiungere il nodo dalla radice.  
  
-   La**probabilità del nodo** è sempre minore o uguale alla **probabilità marginale**.  
  
 Ad esempio, se il popolamento di tutti i clienti in un albero delle decisioni è suddiviso equamente per genere e nessun valore è mancante, la probabilità dei nodi figlio sarà uguale a 0,5. Tuttavia, si supponga che ognuno dei nodi di genere venga equamente diviso per i livelli di reddito-High, Medium e Low. In questo caso il punteggio di MARGINAL_PROBABILITY di ciascun nodo figlio deve essere sempre 0,33, ma il valore di NODE_PROBABILTY sarà il prodotto di tutte le probabilità che conducono a quel nodo e pertanto sarà sempre inferiore al valore di MARGINAL_PROBABILITY.  
  
|Livello e valore del nodo/attributo|probabilità marginale|probabilità del nodo|  
|----------------------------------------|--------------------------|----------------------|  
|Nodo radice del modello<br /><br /> Tutti i clienti di destinazione|1|1|  
|Clienti di destinazione suddivisi per genere|.5|.5|  
|Clienti di destinazione suddivisi per genere, quindi suddivisi nuovamente in tre modi in base al reddito|.33|.5 * .33 = .165|  
  
### <a name="node-rule-and-marginal-rule"></a>Regola del nodo e regola marginale  
 Nel set di righe dello schema del modello di data mining sono inoltre incluse le colonne NODE_RULE e MARGINAL_RULE per tutti i tipi di modello. Queste colonne contengono frammenti XML che è possibile utilizzare per serializzare un modello o rappresentare parti della sua struttura. In presenza di valori non significativi le colonne di alcuni nodi possono essere vuote.  
  
 I due tipi di regole XML fornite sono simili ai due tipi di valori di probabilità. Il frammento XML in MARGINAL_RULE definisce l'attributo e il valore del nodo corrente, laddove il frammento XML in NODE_RULE descrive il percorso al nodo corrente dal nodo radice del modello.  
  
##  <a name="bkmk_AlgoType"></a> Contenuto del modello di data mining in base al tipo di algoritmo  
 Ogni algoritmo archivia tipi diversi di informazioni come parte dello schema di contenuto. L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering, ad esempio, genera una moltitudine di nodi figlio, ognuno dei quali rappresenta un possibile cluster. Ogni nodo del cluster contiene regole che descrivono caratteristiche condivise dagli elementi presenti nel cluster. L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression non contiene invece nodi figlio e il nodo padre del modello contiene l'equazione che descrive la relazione lineare individuata dall'analisi.  
  
 Nella tabella seguente vengono forniti collegamenti agli argomenti disponibili per ogni tipo di algoritmo.  
  
-   **Argomenti sul contenuto del modello:** Viene illustrato il significato di ogni tipo di nodo per ogni tipo di algoritmo e fornire informazioni aggiuntive su quali nodi sono di particolare interesse in un determinato tipo di modello.  
  
-   **L'esecuzione di query argomenti:** Vengono forniti esempi di query su un particolare tipo di modello e istruzioni su come interpretare i risultati.  
  
|Tipo di modello o di algoritmo|model content|Esecuzione di query sui modelli di data mining|  
|-----------------------------|-------------------|----------------------------|  
|Modelli Association Rules|[Contenuto dei modelli di data mining per i modelli di associazione &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)|[Esempi di query sul modello di associazione](../../analysis-services/data-mining/association-model-query-examples.md)|  
|Modelli di clustering|[Contenuto dei modelli di data mining per i modelli di albero delle decisioni &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)|[Esempi di query sul modello di clustering](../../analysis-services/data-mining/clustering-model-query-examples.md)|  
|Modelli di albero delle decisioni|[Contenuto dei modelli di data mining per i modelli di albero delle decisioni &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)|[Esempi di query sul modello di alberi delle decisioni](../../analysis-services/data-mining/decision-trees-model-query-examples.md)|  
|Modelli di regressione lineare|[Contenuto dei modelli di data mining per i modelli di regressione lineare &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)|[Esempi di query sul modello di regressione lineare](../../analysis-services/data-mining/linear-regression-model-query-examples.md)|  
|Modelli di regressione logistica|[Contenuto dei modelli di data mining per i modelli di regressione logistica &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)|[Esempi di query sul modello di regressione lineare](../../analysis-services/data-mining/linear-regression-model-query-examples.md)|  
|Modelli Naive Bayes|[Contenuto dei modelli di data mining per i modelli Naive Bayes &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)|[Naive Bayes Model Query Examples](../../analysis-services/data-mining/naive-bayes-model-query-examples.md)|  
|Modelli di rete neurale|[Contenuto dei modelli di data mining per i modelli di rete neurale &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)|[Esempi di query sul modello di rete neurale](../../analysis-services/data-mining/neural-network-model-query-examples.md)|  
|Sequence Clustering|[Contenuto dei modelli di data mining per i modelli Sequence Clustering &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)|[Sequence Clustering Model Query Examples](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)|  
|Modelli Time Series|[Contenuto dei modelli di data mining per i modelli Time Series &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)|[Esempi di query sui modelli Time Series](../../analysis-services/data-mining/time-series-model-query-examples.md)|  
  
##  <a name="bkmk_Viewing"></a> Strumenti per la visualizzazione del contenuto di un modello di data mining  
 Quando si esplora un modello in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], è possibile visualizzare le informazioni in **Microsoft Generic Content Tree Viewer**, disponibile sia in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] che in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 In [!INCLUDE[msCoName](../../includes/msconame-md.md)] Generic Content Viewer vengono visualizzati elementi quali colonne, regole, proprietà, attributi, nodi e altro contenuto del modello utilizzando le informazioni disponibili nel set di righe dello schema relativo al contenuto del modello di data mining. Il set di righe dello schema relativo al contenuto è un framework generico per la presentazione di informazioni dettagliate sul contenuto di un modello di data mining. È possibile visualizzare il contenuto del modello in un client che supporti i set di righe gerarchici. Il visualizzatore di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] presenta le informazioni in un visualizzatore di tabelle HTML che rappresenta tutti i modelli in un formato coerente e semplifica la comprensione della struttura dei modelli creati. Per altre informazioni, vedere [Visualizzare un modello utilizzando Microsoft Generic Content Tree Viewer](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).  
  
##  <a name="bkmk_Querying"></a> Strumenti per l'esecuzione di query sul contenuto di un modello di data mining  
 Per recuperare il contenuto di un modello di data mining, è necessario creare una query sul modello di data mining.  
  
 Il modo più semplice per creare una query sul contenuto consiste nell'eseguire l'istruzione DMX seguente in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:  
  
```  
SELECT * FROM [<mining model name>].CONTENT  
```  
  
 Per altre informazioni, vedere [Query di data mining](../../analysis-services/data-mining/data-mining-queries.md).  
  
 È anche possibile eseguire una query sul contenuto del modello di data mining utilizzando i set di righe dello schema di data mining. Un set di righe dello schema è una struttura standard utilizzata dai client per individuare, esplorare ed eseguire query sulle informazioni relative a strutture e modelli di data mining. È possibile eseguire query sui set di righe dello schema tramite istruzioni XMLA, Transact-SQL o DMX.  
  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]è inoltre possibile accedere alle informazioni sui set di righe dello schema di data mining stabilendo una connessione all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ed eseguendo query sulle tabelle di sistema. Per altre informazioni, vedere [Set di righe dello schema di data mining &#40;SSAS&#41;](../../analysis-services/data-mining/data-mining-schema-rowsets-ssas.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Microsoft Generic Content Tree Viewer &#40;Data mining&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)   
 [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
  
