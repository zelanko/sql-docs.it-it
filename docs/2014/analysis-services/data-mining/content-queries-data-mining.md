---
title: Query sul contenuto (data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c4f4a5a8-a230-4222-bece-9d563501f65f
author: minewiskan
ms.author: owend
ms.openlocfilehash: 44b162c34f5f505462a713205d8434484473afa4
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84524057"
---
# <a name="content-queries-data-mining"></a>Query sul contenuto (Data mining)
  Una query sul contenuto consente di estrarre informazioni sulle statistiche interne e sulla struttura del modello di data mining. Talvolta una query sul contenuto può fornire dettagli che non sono immediatamente disponibili nel visualizzatore. I risultati di una query sul contenuto possono essere utilizzati anche per estrarre a livello di codice informazioni per altri utilizzi.  
  
 In questa sezione vengono fornite informazioni generali sui tipi di informazioni che è possibile recuperare tramite una query sul contenuto, nonché la sintassi DMX generale per le query sul contenuto.  
  
 [Query sul contenuto di base](#bkmk_ContentQuery)  
  
-   [Query sulla struttura e sui dati del case](#bkmk_Structure)  
  
-   [Query sugli schemi del modello](#bkmk_Patterns)  
  
 [esempi](#bkmk_Examples)  
  
-   [Query sul contenuto su un modello di associazione](#bkmk_Assoc)  
  
-   [Query sul contenuto su un modello Decision Trees](#bkmk_DecTree)  
  
 [Utilizzo dei risultati delle query](#bkmk_Results)  
  
##  <a name="basic-content-queries"></a><a name="bkmk_ContentQuery"></a>Query sul contenuto di base  
 È possibile creare query sul contenuto tramite il generatore delle query di stima, utilizzare i modelli di query sul contenuto DMX disponibili in SQL Server Management Studio o scrivere query direttamente in DMX. A differenza delle query di stima, non è necessario unire in join i dati esterni, pertanto le query sul contenuto sono facili da scrivere.  
  
 In questa sezione viene fornita una panoramica dei tipi di query sul contenuto che è possibile creare.  
  
-   Le query sulla struttura di data mining o sui dati del case consentono di visualizzare i dati dettagliati utilizzati per il training.  
  
-   Le query sul modello possono restituire modelli, elenchi di attributi, formule e così via.  
  
###  <a name="queries-on-structure-and-case-data"></a><a name="bkmk_Structure"></a> Query sulla struttura e sui dati del case  
 DMX supporta le query sui dati memorizzati nella cache utilizzati per compilare strutture e modelli di data mining. Per impostazione predefinita, questa cache viene creata quando si definisce la struttura di data mining e viene popolata quando si elabora la struttura o il modello.  
  
> [!WARNING]  
>  Questa cache non può essere cancellata o eliminata se è necessario separare i dati in set di training e di testing. Se la cache viene cancellata, non è possibile eseguire una query sui dati del case.  
  
 Negli esempi seguenti vengono mostrati i modelli comuni utilizzati per la creazione di query sui dati del case o query sui dati nella struttura di data mining:  
  
 **Ottenere tutti i case per un modello**  
 `SELECT FROM <model>.CASES`  
  
 Utilizzare questa istruzione per recuperare colonne specifiche dai dati del case utilizzati per compilare un modello. È necessario disporre delle autorizzazioni drill-through sul modello per eseguire questa query.  
  
 **Visualizzare tutti i dati inclusi nella struttura**  
 `SELECT FROM <structure>.CASES`  
  
 Utilizzare questa istruzione per visualizzare tutti i dati presenti nella struttura, incluse le colonne non comprese in un determinato modello di data mining. Per recuperare i dati dalla struttura di data mining, è necessario disporre delle autorizzazioni drill-through sul modello e sulla struttura.  
  
 **Ottenere l'intervallo di valori**  
 `SELECT DISTINCT RangeMin(<column>), RangeMax(<column>) FROM <model>`  
  
 Utilizzare questa istruzione per individuare i valori minimo e massimo e la media di una colonna continua o dei bucket di una colonna DISCRETIZED.  
  
 **Ottenere valori distinct**  
 `SELECT DISTINCT <column>FROM <model>`  
  
 Utilizzare questa istruzione per recuperare tutti i valori di una colonna DISCRETE.  Non utilizzare questa istruzione per le colonne DISCRETIZED, ma utilizzare le funzioni `RangeMin` e `RangeMax`.  
  
 **Individuare i case utilizzati per il training di un modello o di una struttura**  
 `SELECT  FROM <mining structure.CASES WHERE IsTrainingCase()`  
  
 Utilizzare questa istruzione per ottenere il set di dati completo utilizzato per il training di un modello.  
  
 **Individuare i case utilizzati per il testing di un modello o di una struttura**  
 `SELECT  FROM <mining structure.CASES WHERE IsTestingCase()`  
  
 Utilizzare questa istruzione per ottenere i dati riservati per il testing dei modelli di data mining correlati a una struttura specifica.  
  
 **Eseguire il drill-through da uno schema del modello specifico ai dati del case sottostanti**  
 `SELECT FROM <model>.CASESWHERE IsTrainingCase() AND IsInNode(<node>)`  
  
 Utilizzare questa istruzione per recuperare dati del case dettagliati da un modello sottoposto a training. È necessario specificare un determinato nodo, ad esempio è necessario conoscere l'ID del nodo del cluster, il ramo specifico di un albero delle decision, e così via. Inoltre, è necessario disporre delle autorizzazioni drill-through sul modello per eseguire questa query.  
  
###  <a name="queries-on-model-patterns-statistics-and-attributes"></a><a name="bkmk_Patterns"></a>Query su modelli di modello, statistiche e attributi  
 Il contenuto di un modello di data mining è utile per molti scopi. Con una query sul contenuto del modello, è possibile:  
  
-   Estrarre formule o probabilità per effettuare i calcoli.  
  
-   Per un modello di associazione, recuperare le regole utilizzate per generare una stima.  
  
-   Recuperare le descrizioni di regole specifiche in modo da poter utilizzare le regole in un'applicazione personalizzata.  
  
-   Visualizzare le medie mobili rilevate da un modello Time Series.  
  
-   Ottenere la formula di regressione per alcuni segmenti della linea di tendenza.  
  
-   Recuperare informazioni utilizzabili sui clienti identificati come facenti parte di un cluster specifico.  
  
 Negli esempi seguenti vengono mostrati alcuni dei modelli comuni per la creazione di query sul contenuto del modello:  
  
 **Ottenere schemi dal modello**  
 `SELECT FROM <model>.CONTENT`  
  
 Utilizzare questa istruzione per recuperare informazioni dettagliate su nodi specifici del modello. A seconda del tipo di algoritmo, nel nodo possono essere contenute regole e formule, statistiche sul supporto e sulla varianza e così via.  
  
 **Recuperare attributi utilizzati in un modello sottoposto a training**  
 `CALL System.GetModelAttributes(<model>)`  
  
 Utilizzare questa stored procedure per recuperare l'elenco di attributi utilizzati da un modello. Queste informazioni sono utili per determinare gli attributi eliminati, ad esempio, in seguito alla selezione delle caratteristiche.  
  
 **Recuperare il contenuto archiviato in una dimensione di data mining**  
 `SELECT FROM <model>.DIMENSIONCONTENT`  
  
 Utilizzare questa istruzione per recuperare i dati da una dimensione di data mining.  
  
 Questo tipo di query è destinato principalmente a uso interno. Tuttavia, non tutti gli algoritmi supportano questa funzionalità. Il supporto è indicato da un flag nel set di righe dello schema MINING_SERVICES.  
  
 Se si sviluppa un proprio algoritmo plug-in, è possibile utilizzare questa istruzione per verificare il contenuto del modello per il testing.  
  
 **Ottenere la rappresentazione PMML di un modello**  
 `SELECT * FROM <model>.PMML`  
  
 Consente di ottenere un documento XML che rappresenta il modello in formato PMML. Non sono supportati tutti i tipi di modello.  
  
##  <a name="examples"></a><a name="bkmk_Examples"></a> Esempi  
 Sebbene alcuni contenuti dei modelli siano standard nei diversi algoritmi, alcune parti del contenuto variano significativamente a seconda dell'algoritmo utilizzato per compilare il modello. Pertanto, quando si crea una query sul contenuto, è necessario identificare le informazione del modello che sono utili per il modello specifico in uso.  
  
 Alcuni esempi vengono forniti in questa sezione per illustrare come la scelta di algoritmo influisca sul tipo di informazioni archiviato nel modello. Per altre informazioni sul contenuto del modello di data mining e sul contenuto specifico per ogni tipo di modello, vedere [Contenuto del modello di data mining &#40;Analysis Services - Data Mining&#41;](mining-model-content-analysis-services-data-mining.md).  
  
###  <a name="example-1-content-query-on-an-association-model"></a><a name="bkmk_Assoc"></a> Esempio 1: Query sul contenuto su un modello di associazione  
 Tramite l'istruzione, `SELECT FROM <model>.CONTENT`, vengono restituiti tipi diversi di informazioni, a seconda del tipo di modello su cui si esegue una query. Per un modello di associazione, un'informazione chiave è il *tipo di nodo*. I nodi sono come contenitori per le informazioni nel contenuto del modello. In un modello di associazione, i nodi che rappresentano regole hanno un valore NODE_TYPE pari a 8, mentre i nodi che rappresentano i set di elementi hanno un valore NODE_TYPE pari a 7.  
  
 Pertanto, tramite la query seguente vengono restituiti i primi 10 set di elementi, classificati per supporto (ordinamento predefinito).  
  
```  
SELECT TOP 10 NODE_DESCRIPTION, NODE_PROBABILITY, SUPPORT  
FROM <model>.CONTENT WHERE NODE_TYPE = 7  
```  
  
 La query seguente consente di compilare su queste informazioni. La query restituisce tre colonne: l'ID del nodo, la regola completa e il prodotto sul lato destro del set di elementi, ovvero il prodotto stimato per essere associato ad altri prodotti come parte di un set di elementi.  
  
```  
SELECT FLATTENED NODE_UNIQUE_NAME, NODE_DESCRIPTION,  
     (SELECT RIGHT(ATTRIBUTE_NAME, (LEN(ATTRIBUTE_NAME)-LEN('Association model name')))   
FROM NODE_DISTRIBUTION  
WHERE LEN(ATTRIBUTE_NAME)>2  
)   
AS RightSideProduct  
FROM [<Association model name>].CONTENT  
WHERE NODE_TYPE = 8   
ORDER BY NODE_SUPPORT DESC  
```  
  
 La parola chiave FLATTENED indica che il set di righe nidificato deve essere convertito in una tabella bidimensionale. L'attributo che rappresenta il prodotto sul lato destro della regola è contenuto nella tabella NODE_DISTRIBUTION; pertanto, si recupera solo la riga che contiene un nome di attributo aggiungendo un requisito in base al quale la lunghezza deve essere maggiore di 2.  
  
 Per rimuovere il nome del modello dalla terza colonna viene utilizzata una semplice funzione stringa. Generalmente il nome del modello viene aggiunto come prefisso ai valori delle colonne nidificate.  
  
 La clausola WHERE consente di specificare che il valore di NODE_TYPE deve essere 8, per recuperare solo le regole.  
  
 Per altri esempi, vedere [Esempi di query sul modello di associazione](association-model-query-examples.md).  
  
###  <a name="example-2-content-query-on-a-decision-trees-model"></a><a name="bkmk_DecTree"></a> Esempio 2: Query sul contenuto su un modello di alberi delle decisioni  
 Un modello di albero delle decisioni può essere utilizzato per la stima, nonché per la classificazione.  In questo esempio si presuppone l'utilizzo del modello per la stima di un risultato, ma si desidera scoprire anche quali fattori o regole possono essere utilizzate per classificare il risultato.  
  
 In un modello di albero delle decisioni, i nodi sono utilizzati per rappresentare sia alberi sia nodi foglia. Nella didascalia per ogni nodo è contenuta la descrizione del percorso fino al risultato. Pertanto, per tracciare il percorso per qualsiasi particolare risultato, è necessario identificare il nodo in cui è contenuto e ottenere i dettagli per tale nodo.  
  
 Nella query di stima si aggiunge la funzione di stima [PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx) per ottenere l'ID del nodo correlato, come mostrato nell'esempio seguente:  
  
```  
SELECT  Predict([Bike Buyer]), PredictNodeID([Bike Buyer])   
FROM [<decision tree model name>]  
PREDICTION JOIN   
<input rowset>   
```  
  
 Una volta ottenuto l'ID del nodo contenente il risultato, è possibile recuperare la regola o il percorso tramite cui viene spiegata la stima creando una query sul contenuto in cui sia incluso NODE_CAPTION, come illustrato di seguito:  
  
```  
SELECT NODE_CAPTION  
FROM [<decision tree model name>]   
WHERE NODE_UNIQUE_NAME= '<node id>'  
```  
  
 Per altri esempi, vedere [Esempi di query sul modello di alberi delle decisioni](decision-trees-model-query-examples.md).  
  
##  <a name="working-with-the-query-results"></a><a name="bkmk_Results"></a>Utilizzo dei risultati della query  
 Come dimostrato negli esempi, tramite le query sul contenuto vengono restituiti soprattutto set di righe tabulari, tuttavia possono essere incluse anche informazioni sulle colonne nidificate. È possibile rendere bidimensionale il set di righe restituito, tuttavia, in questo modo, l'utilizzo dei risultati può risultare più complesso. Il contenuto del nodo NODE_DISTRIBUTION in particolare è nidificato, ma in esso sono contenute informazioni molto interessanti sul modello.  
  
 Per ulteriori informazioni sull'utilizzo di set di righe gerarchici, vedere la specifica OLE DB su MSDN.  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sull'istruzione DMX SELECT](/sql/dmx/understanding-the-dmx-select-statement)   
 [Query di data mining](data-mining-queries.md)  
  
  
