---
title: Contenuto dei modelli di data mining per i modelli di associazione (Analysis Services-Data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- itemsets [Analysis Services]
- association algorithms [Analysis Services]
- mining model content, association models
- rules [Data Mining]
- associations [Analysis Services]
ms.assetid: d5849bcb-4b8f-4f71-9761-7dc5bb465224
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1836cb414e8ea7f6e0bedbf0b4fb75cf0bfa264e
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84521587"
---
# <a name="mining-model-content-for-association-models-analysis-services---data-mining"></a>Contenuto dei modelli di data mining per i modelli di associazione (Analysis Services - Data mining)
  Questo argomento descrive il contenuto dei modelli di data mining specifico dei modelli che usano l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules. Per una spiegazione della terminologia generale e statistica relativa al contenuto dei modelli di data mining applicabile a tutti i tipi di modello, vedere [Contenuto dei modelli di data mining &#40;Analysis Services - Data mining&#41;](mining-model-content-analysis-services-data-mining.md).  
  
## <a name="understanding-the-structure-of-an-association-model"></a>Informazioni sulla struttura di un modello di associazione  
 Un modello di associazione ha una struttura semplice. Ogni modello include un singolo nodo padre che rappresenta il modello e i relativi metadati. Ciascun nodo padre è associato a un elenco semplice di set di elementi e regole. I set di elementi e le regole non sono organizzati in alberi, ma sono ordinati come illustrato nel diagramma seguente, ossia con i set di elementi seguiti dalle regole.  
  
 ![Struttura del contenuto del modello per i modelli di associazione](../media/modelcontentstructure-assoc.gif "Struttura del contenuto del modello per i modelli di associazione")  
  
 Ogni set di elementi è contenuto nel proprio nodo (NODE_TYPE = 7). Il *nodo* include la definizione del set di elementi, il numero di case che contengono il set di elementi e altre informazioni.  
  
 Anche ogni regola è contenuta nel proprio nodo (NODE_TYPE = 8). Una *regola* descrive un modello generale per la modalità di associazione degli elementi. È simile a un'istruzione IF-THEN. Il lato sinistro della regola indica una condizione o un set di condizioni esistente. Il lato destro indica l'elemento del set di dati solitamente associato alle condizioni riportate a sinistra.  
  
 **Nota** Se si vuole estrarre le regole o i set di elementi, è possibile usare una query che restituisca solo i tipi di nodo desiderati. Per altre informazioni, vedere [Esempi di query sul modello di associazione](association-model-query-examples.md).  
  
## <a name="model-content-for-an-association-model"></a>Contenuto di un modello di associazione  
 In questa sezione vengono forniti dettagli ed esempi relativi solo alle colonne del contenuto dei modelli di data mining pertinenti per i modelli di associazione.  
  
 Per informazioni sulle colonne generiche del set di righe dello schema, ad esempio MODEL_CATALOG e MODEL_NAME, vedere [Contenuto dei modelli di data mining &#40;Analysis Services - Data mining&#41;](mining-model-content-analysis-services-data-mining.md).  
  
 MODEL_CATALOG  
 Nome del database in cui è archiviato il modello.  
  
 MODEL_NAME  
 Nome del modello.  
  
 ATTRIBUTE_NAME  
 Nomi degli attributi che corrispondono a questo nodo.  
  
 NODE_NAME  
 Il nome del nodo. Per un modello di associazione, questa colonna contiene lo stesso valore di NODE_UNIQUE_NAME.  
  
 NODE_UNIQUE_NAME  
 Nome univoco del nodo.  
  
 NODE_TYPE  
 Un modello di associazione restituisce solo i tipi di nodo seguenti:  
  
|ID tipo di nodo|Tipo|  
|------------------|----------|  
|1 (Model)|Radice o nodo padre.|  
|7 (Itemset)|Set di elementi, ovvero raccolta di coppie attributo-valore. Esempi:<br /><br /> `Product 1 = Existing, Product 2 = Existing`<br /><br /> oppure<br /><br /> `Gender = Male`.|  
|8 (Rule)|Regola che definisce la modalità di correlazione tra gli elementi.<br /><br /> Esempio:<br /><br /> `Product 1 = Existing, Product 2 = Existing -> Product 3 = Existing`.|  
  
 NODE_CAPTION  
 Etichetta o didascalia associata al nodo.  
  
 **Nodo di set di elementi** Elenco di elementi delimitati da virgole.  
  
 **Nodo di regola** Contiene i lati sinistro e destro della regola.  
  
 CHILDREN_CARDINALITY  
 Indica il numero di figli del nodo corrente.  
  
 **Nodo padre** Indica il numero totale di set di elementi e regole.  
  
> [!NOTE]  
>  Per ottenere una suddivisione del conteggio relativo a set di elementi e regole, vedere NODE_DESCRIPTION per il nodo radice del modello.  
  
 **Nodo di set di elementi o di regola** Sempre 0.  
  
 PARENT_UNIQUE_NAME  
 Nome univoco dell'elemento padre del nodo.  
  
 **Nodo padre** Sempre NULL.  
  
 **Nodo di set di elementi o di regola** Sempre 0.  
  
 NODE_DESCRIPTION  
 Descrizione semplice del contenuto del nodo.  
  
 **Nodo padre** Include un elenco delimitato da virgole delle informazioni seguenti sul modello:  
  
|Elemento|Descrizione|  
|----------|-----------------|  
|ITEMSET_COUNT|Conteggio di tutti i set di elementi nel modello.|  
|RULE_COUNT|Conteggio di tutte le regole nel modello.|  
|MIN_SUPPORT|Supporto minimo individuato per ogni singolo set di elementi.<br /><br /> **Nota** Questo valore potrebbe essere diverso da quello impostato per il parametro *MINIMUM_SUPPORT* .|  
|MAX_SUPPORT|Supporto massimo individuato per ogni singolo set di elementi.<br /><br /> **Nota** Questo valore potrebbe essere diverso da quello impostato per il parametro *MAXIMUM_SUPPORT* .|  
|MIN_ITEMSET_SIZE|Dimensione del set di elementi più piccolo, rappresentata come conteggio di elementi.<br /><br /> Il valore 0 indica che lo stato `Missing` viene considerato come un elemento indipendente.<br /><br /> **Nota** Il valore predefinito del parametro *MINIMUM_ITEMSET_SIZE* è 1.|  
|MAX_ITEMSET_SIZE|Indica la dimensione del set di elementi più grande individuato.<br /><br /> **Nota** Questo valore è vincolato dal valore impostato per il parametro *MAX_ITEMSET_SIZE* durante la creazione del modello. Non può mai superare tale valore, ma può essere minore. Il valore predefinito è 3.|  
|MIN_PROBABILITY|Probabilità minima individuata per ogni singolo set di elementi o regola nel modello.<br /><br /> Esempio: 0,400390625<br /><br /> **Nota** Per i set di elementi, questo valore è sempre maggiore del valore impostato per il parametro *MINIMUM_PROBABILITY* durante la creazione del modello.|  
|MAX_PROBABILITY|Probabilità massima individuata per ogni singolo set di elementi o regola nel modello.<br /><br /> Esempio: 1<br /><br /> **Nota** Non esistono parametri che vincolano la probabilità massima dei set di elementi. Per eliminare gli elementi troppo frequenti, usare il parametro *MAXIMUM_SUPPORT* .|  
|MIN_LIFT|Livello minimo di accuratezza fornito dal modello per un set di elementi.<br /><br /> Esempio: 0,4309369632511<br /><br /> Nota: conoscendo questo valore, è possibile determinare se l'accuratezza è significativa per ogni singolo set di elementi.|  
|MAX_LIFT|Livello massimo di accuratezza fornito dal modello per ogni set di elementi.<br /><br /> Esempio: 1,95758227647523 **Nota** Conoscendo questo valore, è possibile determinare se l'accuratezza è significativa per ogni singolo set di elementi.|  
  
 **Nodo di set di elementi** I nodi di set di elementi contengono un elenco di elementi, visualizzato come stringa di testo delimitato da virgole.  
  
 Esempio:  
  
 `Touring Tire = Existing, Water Bottle = Existing`  
  
 Significa che i pneumatici Touring e le bottiglie di acqua sono stati acquistati insieme.  
  
 **Nodo di regola** I nodi di regola contengono i lati sinistro e destro della regola, separati da una freccia.  
  
 Esempio: `Touring Tire = Existing, Water Bottle = Existing -> Cycling cap = Existing`  
  
 Significa che chi ha acquistato un pneumatico Touring e una bottiglia d'acqua è probabile che abbia anche acquistato un berretto da ciclista.  
  
 NODE_RULE  
 Frammento XML che descrive la regola o il set di elementi incorporato nel nodo.  
  
 **Nodo padre** Vuoto.  
  
 **Nodo di set di elementi** Vuoto.  
  
 **Nodo di regola** Il frammento XML include informazioni utili aggiuntive sulla regola, come supporto, confidenza e numero di elementi, insieme all'ID del nodo che rappresenta il lato sinistro della regola.  
  
 MARGINAL_RULE  
 Vuoto.  
  
 NODE_PROBABILITY  
 Probabilità o punteggio di confidenza associato al set di elementi o alla regola.  
  
 **Nodo padre** Sempre 0.  
  
 **Nodo di set di elementi** Probabilità del set di elementi.  
  
 **Nodo di regola** Valore di confidenza per la regola.  
  
 MARGINAL_PROBABILITY  
 Uguale a NODE_PROBABILITY.  
  
 NODE_DISTRIBUTION  
 La tabella contiene informazioni molto diverse, a seconda che il nodo sia un set di elementi o una regola.  
  
 **Nodo padre** Vuoto.  
  
 **Nodo di set di elementi** Elenca ogni elemento del set di elementi insieme a un valore di probabilità e di supporto. Se ad esempio il set di elementi contiene due prodotti, viene riportato il nome di ogni prodotto insieme al conteggio dei case che lo includono.  
  
 **Nodo di regola** Contiene due righe. Nella prima riga è indicato l'attributo del lato destro della regola, ovvero l'elemento stimato, insieme a un punteggio di confidenza.  
  
 La seconda riga è univoca per i modelli di associazione. Contiene un puntatore al set di elementi sul lato destro della regola. Il puntatore è rappresentato nella colonna ATTRIBUTE_VALUE come ID del set di elementi che contiene solo l'elemento di destra.  
  
 Ad esempio, se la regola è `If {A,B} Then {C}`, la tabella contiene il nome dell'elemento `{C}`e l'ID del nodo che contiene il set di elementi per l'elemento C.  
  
 Questo puntatore è utile perché consente di determinare dal nodo di set di elementi la quantità complessiva di case che includono il prodotto del lato destro. I casi soggetti alla regola `If {A,B} Then {C}` sono un subset dei case elencati nel set di elementi per `{C}`.  
  
 NODE_SUPPORT  
 Numero di case che supportano il nodo.  
  
 **Nodo padre** Numero di case nel modello.  
  
 **Nodo di set di elementi** Numero di case che contengono tutti gli elementi del set di elementi.  
  
 **Nodo di regola** Numero di case che contengono tutti gli elementi inclusi nella regola.  
  
 MSOLAP_MODEL_COLUMN  
 Contiene informazioni diverse a seconda che il nodo sia un set di elementi o una regola.  
  
 **Nodo padre** Vuoto.  
  
 **Nodo di set di elementi** Vuoto.  
  
 **Nodo di regola** ID del set di elementi che contiene gli elementi nel lato sinistro della regola. Ad esempio, se la regola è `If {A,B} Then {C}`, questa colonna contiene l'ID del set di elementi che include solo `{A,B}`.  
  
 MSOLAP_NODE_SCORE  
 **Nodo padre** Vuoto.  
  
 **Nodo di set di elementi** Punteggio di priorità per il set di elementi.  
  
 **Nodo di regola** Punteggio di priorità per la regola.  
  
> [!NOTE]  
>  La priorità viene calcolata in modo diverso per i set di elementi e le regole. Per altre informazioni, vedere [Riferimento tecnico per l'algoritmo Microsoft Association Rules](microsoft-association-algorithm-technical-reference.md).  
  
 MSOLAP_NODE_SHORT_CAPTION  
 Vuoto.  
  
## <a name="see-also"></a>Vedere anche  
 [Contenuto del modello di data mining &#40;Analysis Services-&#41;di data mining](mining-model-content-analysis-services-data-mining.md)   
 [Algoritmo Microsoft Association](microsoft-association-algorithm.md)   
 [Esempi di query sul modello di associazione](association-model-query-examples.md)  
  
  
