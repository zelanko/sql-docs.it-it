---
title: Contenuto data mining Model per i modelli Naive Bayes (Analysis Services - Data Mining) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cbfb701bf6c4a90cf285e4643377b38e51121dd3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68182697"
---
# <a name="mining-model-content-for-naive-bayes-models-analysis-services---data-mining"></a>Contenuto dei modelli di data mining per i modelli Naive Bayes (Analysis Services - Data mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In questo argomento viene descritto il contenuto dei modelli di data mining specifico dei modelli che utilizzano l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes. Per una spiegazione dell'interpretazione delle statistiche e della struttura condivise da tutti i tipi di modello e per definizioni generali dei termini relativi al contenuto dei modelli di data mining, vedere [Contenuto dei modelli di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
## <a name="understanding-the-structure-of-a-naive-bayes-model"></a>Informazioni sulla struttura di un modello Naive Bayes  
 La struttura di un modello Naive Bayes è data da un solo nodo padre, che rappresenta il modello e i metadati, e da un numero qualsiasi di alberi indipendenti che rappresentano gli attributi stimabili selezionati. Oltre agli alberi per gli attributi, ogni modello contiene un nodo delle statistiche marginali (NODE_TYPE = 26) che fornisce statistiche descrittive sul set di case di training. Per ulteriori informazioni, vedere [Informazioni nel nodo delle statistiche marginali](#bkmk_margstats).  
  
 Per ogni valore e attributo stimabile, il modello restituisce un albero che contiene informazioni che descrivono come le varie colonne di input abbiano influito sul risultato di quel particolare attributo stimabile. Ogni albero contiene l'attributo stimabile e il relativo valore (NODE_TYPE = 9), oltre a una serie di nodi che rappresentano gli attributi di input (NODE_TYPE = 10). Poiché gli attributi di input dispongono in genere di più valori, ogni attributo di input (NODE_TYPE = 10) può disporre di più nodi figlio (NODE_TYPE = 11), ognuno per uno stato specifico dell'attributo.  
  
> [!NOTE]  
>  Poiché un modello Naive Bayes non consente tipi di dati continui, tutti i valori delle colonne di input vengono considerati discreti o discretizzati. È possibile specificare il modo in cui un valore viene discretizzato. Per altre informazioni, vedere [Modificare la discretizzazione di una colonna in un modello di data mining](../../analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md).  
  
 ![struttura del contenuto del modello per Naive bayes](../../analysis-services/data-mining/media/modelcontentstructure-nb.gif "struttura del contenuto del modello per Naive bayes")  
  
## <a name="model-content-for-a-naive-bayes-model"></a>Contenuto di un modello Naive Bayes  
 In questa sezione vengono forniti dettagli ed esempi relativi unicamente alle colonne del contenuto dei modelli di data mining particolarmente importanti per i modelli Naive Bayes.  
  
 Per informazioni sulle colonne generiche del set di righe dello schema, ad esempio MODEL_CATALOG e MODEL_NAME, non descritte in questo argomento o per spiegazioni sulla terminologia dei modelli di data mining, vedere [Contenuto dei modelli di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
 MODEL_CATALOG  
 Nome del database in cui è archiviato il modello.  
  
 MODEL_NAME  
 Nome del modello.  
  
 ATTRIBUTE_NAME  
 Nomi degli attributi che corrispondono a questo nodo.  
  
 **Nodo radice del modello** Nome dell'attributo stimabile.  
  
 **Statistiche marginali** Non applicabile  
  
 **Attributo stimabile** Nome dell'attributo stimabile.  
  
 **Attributo di input** Nome dell'attributo di input.  
  
 **Stato attributo di input** Nome del solo attributo di input. Per ottenere lo stato, utilizzare MSOLAP_NODE_SHORT_CAPTION.  
  
 NODE_NAME  
 Nome del nodo.  
  
 In questa colonna è contenuto lo stesso valore di NODE_UNIQUE_NAME.  
  
 Per ulteriori informazioni sulle convenzioni di denominazione dei nodi, vedere [Utilizzo dei nomi e degli ID dei nodi](#bkmk_nodenames).  
  
 NODE_UNIQUE_NAME  
 Nome univoco del nodo. I nomi univoci vengono assegnati sulla base di una convenzione che fornisce informazioni sulle relazioni tra i nodi. Per ulteriori informazioni sulle convenzioni di denominazione dei nodi, vedere [Utilizzo dei nomi e degli ID dei nodi](#bkmk_nodenames).  
  
 NODE_TYPE  
 Un modello Naive Bayes restituisce i tipi di nodo seguenti:  
  
|ID tipo di nodo|Descrizione|  
|------------------|-----------------|  
|26 (NaiveBayesMarginalStatNode)|Contiene statistiche che descrivono il set intero di case di training per il modello.|  
|9 (Attributo stimabile)|Contiene il nome dell'attributo stimabile.|  
|10 (Attributo di input)|Contiene il nome di una colonna dell'attributo di input e i nodi figlio che contengono i valori dell'attributo.|  
|11 (Stato attributo di input)|Contiene i valori o i valori discretizzati di tutti gli attributi di input abbinati a un particolare attributo di output.|  
  
 NODE_CAPTION  
 Etichetta o didascalia associata al nodo. Questa proprietà viene utilizzata principalmente per scopi di visualizzazione.  
  
 **Nodo radice del modello** vuoto  
  
 **Statistiche marginali** vuoto  
  
 **Attributo stimabile** Nome dell'attributo stimabile.  
  
 **Attributo di input** Nome dell'attributo stimabile e dell'attributo di input corrente. Ad esempio:  
  
 Bike Buyer -> Age  
  
 **Stato attributo di input** Nome dell'attributo stimabile e dell'attributo di input corrente, più valore di input. Ad esempio:  
  
 Bike Buyer -> Age = Missing  
  
 CHILDREN_CARDINALITY  
 Numero di nodi figlio del nodo.  
  
 **Nodo radice del modello** Conteggio degli attributi stimabili nel modello più 1 per il nodo delle statistiche marginali.  
  
 **Statistiche marginali** Per definizione non dispongono di nodi figlio.  
  
 **Attributo stimabile**  Conteggio degli attributi di input correlati all'attributo stimabile corrente.  
  
 **Attributo di input** Conteggio dei valori discreti o discretizzati per l'attributo di input corrente.  
  
 **Stato attributo di input** Sempre 0.  
  
 PARENT_UNIQUE_NAME  
 Nome univoco del nodo padre. Per ulteriori informazioni sull'associazione di nodi padre e nodi figlio, vedere [Utilizzo dei nomi e degli ID dei nodi](#bkmk_nodenames).  
  
 NODE_DESCRIPTION  
 Equivale alla didascalia del nodo.  
  
 NODE_RULE  
 Rappresentazione XML della didascalia del nodo.  
  
 MARGINAL_RULE  
 Equivale alla regola del nodo.  
  
 NODE_PROBABILITY  
 Probabilità associata a questo nodo.  
  
 **Nodo radice del modello** Sempre 0.  
  
 **Statistiche marginali** Sempre 0.  
  
 **Attributo stimabile**  Sempre 1.  
  
 **Attributo di input** Sempre 1.  
  
 **Stato attributo di input** Numero decimale che rappresenta la probabilità del valore corrente. La somma dei valori di tutti gli stati dell'attributo di input sotto il nodo padre dell'attributo di input dà 1.  
  
 MARGINAL_PROBABILITY  
 Equivale alla probabilità del nodo.  
  
 NODE_DISTRIBUTION  
 Tabella contenente l'istogramma delle probabilità del nodo. Per altre informazioni, vedere [Tabella NODE_DISTRIBUTION](#bkmk_nodedist).  
  
 NODE_SUPPORT  
 Numero di case che supportano il nodo.  
  
 **Nodo radice del modello** Conteggio di tutti i case nei dati di training.  
  
 **Statistiche marginali** Sempre 0.  
  
 **Attributo stimabile** Conteggio di tutti i case nei dati di training.  
  
 **Attributo di input** Conteggio di tutti i case nei dati di training.  
  
 **Stato attributo di input** Conteggio dei case nei dati di training che contengono solo questo particolare valore.  
  
 MSOLAP_MODEL_COLUMN  
 Etichetta utilizzata a scopo di visualizzazione. Equivale in genere a ATTRIBUTE_NAME.  
  
 MSOLAP_NODE_SCORE  
 Rappresenta l'importanza dell'attributo o del valore all'interno del modello.  
  
 **Nodo radice del modello** Sempre 0.  
  
 **Statistiche marginali** Sempre 0.  
  
 **Attributo stimabile**  Sempre 0.  
  
 **Attributo di input** Punteggio di interesse per l'attributo di input corrente in relazione all'attributo stimabile corrente.  
  
 **Stato attributo di input** Sempre 0.  
  
 MSOLAP_NODE_SHORT_CAPTION  
 Stringa di testo che rappresenta il nome o il valore di una colonna.  
  
 **Nodo radice del modello** Vuoto  
  
 **Statistiche marginali** Vuoto  
  
 **Attributo stimabile**  Nome dell'attributo stimabile.  
  
 **Attributo di input** Nome dell'attributo di input.  
  
 **Stato attributo di input** Valore o valore discretizzato dell'attributo di input.  
  
##  <a name="bkmk_nodenames"></a> Utilizzo dei nomi e degli ID dei nodi  
 La denominazione dei nodi in un modello Naive Bayes fornisce informazioni aggiuntive sul tipo di nodo, per rendere più facile la comprensione delle relazioni tra le informazioni nel modello. Nella tabella seguente viene illustrata la convenzione per gli ID assegnati a diversi tipi di nodo.  
  
|Tipo di nodo|Convenzione per ID del nodo|  
|---------------|----------------------------|  
|Nodo radice del modello (1)|Sempre 0.|  
|Nodo delle statistiche marginali (26)|Valore ID arbitrario.|  
|Attributo stimabile (9)|Numero esadecimale che inizia con 10000000<br /><br /> Esempio: 100000001, 10000000b|  
|Attributo di input (10)|Numero esadecimale in due parti dove la prima parte è sempre 20000000 e la seconda inizia con l'identificatore esadecimale dell'attributo stimabile correlato.<br /><br /> Esempio: 20000000b00000000<br /><br /> In questo caso, l'attributo stimabile correlato è 10000000b.|  
|Stato attributo di input (11)|Numero esadecimale in tre parti dove la prima parte è sempre 30000000, la seconda parte inizia con l'identificatore esadecimale dell'attributo stimabile correlato e la terza rappresenta l'identificatore del valore.<br /><br /> Esempio: 30000000b00000000200000000<br /><br /> In questo caso, l'attributo stimabile correlato è 10000000b.|  
  
 È possibile utilizzare gli ID per correlare attributi di input e stati a un attributo stimabile. Ad esempio, la query seguente restituisce i nomi e le didascalie per nodi che rappresentano le possibili combinazioni di attributi di input e attributi stimabili per il modello, `TM_NaiveBayes`.  
  
```  
SELECT NODE_NAME, NODE_CAPTION  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 10  
```  
  
 Risultati previsti:  
  
|NODE_NAME|NODE_CAPTION|  
|----------------|-------------------|  
|20000000000000001|Bike Buyer -> Commute Distance|  
|20000000000000002|Bike Buyer -> English Education|  
|20000000000000003|Bike Buyer -> English Occupation|  
|20000000000000009|Bike Buyer -> Marital Status|  
|2000000000000000a|Bike Buyer -> Number Children At Home|  
|2000000000000000b|Bike Buyer -> Region|  
|2000000000000000c|Bike Buyer -> Total Children|  
  
 È quindi possibile utilizzare gli ID dei nodi padre per recuperare i nodi figlio. La query seguente recupera i nodi che contengono valori per l'attributo `Marital Status` , insieme alla probabilità di ciascun nodo.  
  
```  
SELECT NODE_NAME, NODE_CAPTION, NODE_PROBABILITY  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 11  
AND [PARENT_UNIQUE_NAME] = '20000000000000009'  
```  
  
> [!NOTE]  
>  Il nome della colonna, PARENT_UNIQUE_NAME, deve essere racchiuso tra parentesi quadre per distinguerlo dalla parola chiave riservata con lo stesso nome.  
  
 Risultati previsti:  
  
|NODE_NAME|NODE_CAPTION|NODE_PROBABILITY|  
|----------------|-------------------|-----------------------|  
|3000000000000000900000000|Bike Buyer -> Marital Status = Missing|0|  
|3000000000000000900000001|Bike Buyer -> Marital Status = S|0,457504004|  
|3000000000000000900000002|Bike Buyer -> Marital Status = M|0,542495996|  
  
##  <a name="bkmk_nodedist"></a> Tabella NODE_DISTRIBUTION  
 La colonna della tabella nidificata, NODE_DISTRIBUTION, contiene in genere le statistiche sulla distribuzione dei valori nel nodo. In un modello Naive Bayes questa tabella viene popolata solo per i nodi seguenti:  
  
|Tipo di nodo|Contenuto della tabella nidificata|  
|---------------|-----------------------------|  
|Nodo radice del modello (1)|Vuoto.|  
|Nodo delle statistiche marginali (24)|Contiene informazioni di riepilogo per tutti gli attributi stimabili e gli attributi di input, per l'intero set di dati di training.|  
|Attributo stimabile (9)|Vuoto.|  
|Attributo di input (10)|Vuoto.|  
|Stato attributo di input (11)|Contiene statistiche che descrivono la distribuzione di valori nei dati di training per questa particolare combinazione di un valore stimabile e di un valore dell'attributo di input.|  
  
 È possibile utilizzare gli ID o le didascalie dei nodi per recuperare maggiori livelli di dettaglio. Ad esempio, la query seguente recupera colonne specifiche dalla tabella NODE_DISTRIBUTION solo per quei nodi dell'attributo di input correlati al valore, `'Marital Status = S'`.  
  
```  
SELECT FLATTENED NODE_CAPTION,  
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT], [PROBABILITY], VALUETYPE  
FROM NODE_DISTRIBUTION) as t  
FROM TM_NaiveBayes.content  
WHERE NODE_TYPE = 11  
AND NODE_CAPTION = 'Bike Buyer -> Marital Status = S'  
```  
  
 Risultati previsti:  
  
|NODE_CAPTION|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|-------------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|Bike Buyer -> Marital Status = S|Bike Buyer|Missing|0|0|1|  
|Bike Buyer -> Marital Status = S|Bike Buyer|0|3783|0,472934117|4|  
|Bike Buyer -> Marital Status = S|Bike Buyer|1|4216|0,527065883|4|  
  
 In questi risultati il valore della colonna SUPPORT suggerisce il conteggio di clienti con lo stato civile specificato che hanno acquistato una bicicletta. La colonna PROBABILITY contiene la probabilità di ogni valore dell'attributo, calcolato solo per questo nodo. Per definizioni generali dei termini usati nella tabella NODE_DISTRIBUTION, vedere [Contenuto dei modelli di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
###  <a name="bkmk_margstats"></a> Informazioni nel nodo delle statistiche marginali  
 In un modello Naive Bayes la tabella nidificata per il nodo delle statistiche marginali contiene la distribuzione di valori per l'intero set di dati di training. Ad esempio, la tabella seguente contiene un elenco parziale delle statistiche della tabella NODE_DISTRIBUTION nidificata per il modello, `TM_NaiveBayes`:  
  
|ATTRIBUTE_NAME|ATTRIBUTE_VALUE|SUPPORT|PROBABILITY|VARIANCE|VALUETYPE|  
|---------------------|----------------------|-------------|-----------------|--------------|---------------|  
|Bike Buyer|Missing|0|0|0|1|  
|Bike Buyer|0|8869|0,507263784|0|4|  
|Bike Buyer|1|8615|0,492736216|0|4|  
|Marital Status|Missing|0|0|0|1|  
|Marital Status|S|7999|0,457504004|0|4|  
|Marital Status|M|9485|0,542495996|0|4|  
|Total Children|Missing|0|0|0|1|  
|Total Children|0|4865|0,278254404|0|4|  
|Total Children|3|2093|0,119709449|0|4|  
|Total Children|1|3406|0,19480668|0|4|  
  
 La colonna [Bike Buyer] viene inclusa poiché il nodo delle statistiche marginali contiene sempre una descrizione dell'attributo stimabile e dei valori relativi possibili. Tutte le altre colonne elencate rappresentano attributi di input, insieme ai valori utilizzati nel modello. I valori possono solo essere mancanti, discreti o discretizzati.  
  
 In un modello Naive Bayes non possono essere presenti attributi continui, pertanto tutti i dati numerici vengono rappresentati come discreti (VALUE_TYPE = 4) o discretizzati (VALUE_TYPE = 5).  
  
 Un valore **Missing** (VALUE_TYPE = 1) viene aggiunto a ogni attributo di input e di output per rappresentare i valori potenziali che non erano presenti nei dati di training. È necessario prestare attenzione alla distinzione tra "mancante" riferito a una stringa e il valore **Missing** predefinito. Per altre informazioni, vedere [Valori mancanti &#40; Analysis Services - Data mining&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Contenuto dei modelli di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)   
 [Visualizzatori modello di data mining](../../analysis-services/data-mining/data-mining-model-viewers.md)   
 [Query di data mining](../../analysis-services/data-mining/data-mining-queries.md)   
 [Algoritmo Microsoft Naive Bayes](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)  
  
  
