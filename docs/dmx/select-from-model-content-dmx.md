---
title: Selezionare da &lt; modello &gt; . CONTENUTO (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0fe7de8ce6ee6f40d0d50ce76a148dc3d000a808
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669595"
---
# <a name="select-from-ltmodelgtcontent-dmx"></a>Selezionare da &lt; modello &gt; . CONTENUTO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Restituisce il set di righe dello schema del modello di data mining per il modello di data mining specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.CONTENT   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argomenti  
 *n*  
 Facoltativa. Valore intero mediante il quale viene specificato il numero di righe da restituire.  
  
 *elenco di espressioni*  
 Elenco delimitato da virgole contenente colonne derivate dal set di righe dello schema relativo al contenuto.  
  
 *model*  
 Identificatore del modello.  
  
 *espressione della condizione*  
 Facoltativa. Condizione per limitare i valori restituiti dall'elenco di colonne.  
  
 *expression*  
 Facoltativa. Espressione che restituisce un valore scalare.  
  
## <a name="remarks"></a>Commenti  
 >**di selezione dal** _ \< modello _ **. **L'istruzione Content restituisce contenuto specifico per ogni algoritmo. È ad esempio possibile utilizzare le descrizioni di tutte le regole di un modello Association Rules in un'applicazione personalizzata. È possibile utilizzare una **selezione da \< modello>. Istruzione CONTENT** per restituire valori nella colonna NODE_RULE del modello.  
  
 Nella tabella seguente vengono elencate le colonne incluse nel contenuto del modello di data mining.  
  
> [!NOTE]  
>  Gli algoritmi possono interpretare le colonne in modo diverso al fine di rappresentarne correttamente il contenuto. Per una descrizione del contenuto del modello di data mining per ogni algoritmo e suggerimenti per l'interpretazione e l'esecuzione di query sul contenuto del modello di data mining per ogni tipo di modello, vedere [contenuto dei modelli di data mining &#40;Analysis Services-&#41;di data mining ](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-analysis-services-data-mining).  
  
|Colonna del set di righe relativo al contenuto|Descrizione|  
|---------------------------|-----------------|  
|MODEL_CATALOG|Nome di catalogo. Se il provider non supporta i cataloghi, ha valore NULL.|  
|MODEL_SCHEMA|Nome di schema non qualificato. Se il provider non supporta gli schemi, ha valore NULL.|  
|MODEL_NAME|Nome di modello. Questa colonna non può contenere valori NULL.|  
|ATTRIBUTE_NAME|Nome dell'attributo che corrisponde al nodo.|  
|NODE_NAME|Il nome del nodo.|  
|NODE_UNIQUE_NAME|Nome univoco del nodo all'interno del modello.|  
|NODE_TYPE|Valore intero che rappresenta il tipo del nodo. .|  
|NODE_GUID|GUID del nodo. Se il GUID non è presente, ha valore NULL.|  
|NODE_CAPTION|Etichetta o didascalia associata al nodo. Utilizzata principalmente a scopo di visualizzazione. Se non esiste una didascalia, verrà restituito NODE_NAME.|  
|CHILDREN_CARDINALITY|Numero di nodi figlio del nodo.|  
|PARENT_UNIQUE_NAME|Nome univoco dell'elemento padre del nodo.|  
|NODE_DESCRIPTION|Descrizione del nodo.|  
|NODE_RULE|Frammento XML che rappresenta la regola incorporata nel nodo. Il formato della stringa XML è basato sullo standard PMML.|  
|MARGINAL_RULE|Frammento XML che descrive il percorso dall'elemento padre al nodo.|  
|NODE_PROBABILITY|Probabilità del percorso di terminare nel nodo.|  
|MARGINAL_PROBABILITY|Probabilità di raggiungere il nodo dal nodo padre.|  
|NODE_DISTRIBUTION|Tabella contenente le statistiche che descrivono la distribuzione dei valori nel nodo.|  
|NODE_SUPPORT|Numero di case di supporto al nodo.|  
  
## <a name="examples"></a>Esempio  
 Nel codice seguente viene restituito l'ID del nodo padre per il modello di albero delle decisioni aggiunto alla struttura di data mining Targeted Mailing.  
  
```  
SELECT MODEL_NAME, NODE_NAME FROM [TM Decision Tree].CONTENT  
WHERE NODE_TYPE = 1  
```  
  
 Risultati previsti:  
  
|MODEL_NAME|NODE_NAME|  
|-----------------|----------------|  
|TM_DecisionTree|0|  
  
 Nella query seguente viene utilizzata la funzione **descendant** per restituire gli elementi figlio immediati del nodo restituito nella query precedente.  
  
> [!NOTE]  
>  Poiché il valore della NODE_NAME è una stringa, non è possibile utilizzare un'istruzione sub-SELECT per restituire l'NODE_ID come argomento della funzione **decrescente** .  
  
```  
SELECT NODE_NAME, NODETYPE, NODE_CAPTION   
FROM [TM Decision Tree].CONTENT  
WHERE ISDESCENDANT('0')  
```  
  
 Risultati previsti:  
  
 Poiché il modello è un modello di albero delle decisioni, i discendenti del nodo padre del modello includono un singolo nodo delle statistiche marginali, un nodo che rappresenta l'attributo stimabile e più nodi che contengono valori e attributi di input. Per altre informazioni, vedere [Contenuto dei modelli di data mining per i modelli di albero delle decisioni &#40;Analysis Services - Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining).  
  
## <a name="using-the-flattened-keyword"></a>Utilizzo della parola chiave FLATTENED  
 Il contenuto del modello di data mining contiene spesso informazioni interessanti sul modello presente nelle colonne della tabella nidificata. La parola chiave FLATTENED consente di recuperare i dati da una colonna della tabella nidificata senza utilizzare un provider che supporta i set di righe gerarchici.  
  
 Nella query seguente viene restituito un singolo nodo, il nodo delle statistiche marginali (NODE_TYPE = 26) da un modello Naive Bayes. Tuttavia, questo nodo contiene una tabella nidificata nella colonna NODE_DISTRIBUTION. Di conseguenza, la colonna della tabella nidificata viene resa bidimensionale e viene restituita una riga per ogni riga della tabella nidificata. Il valore della colonna scalare MODEL_NAME viene ripetuto per ogni riga della tabella nidificata.  
  
 Inoltre, se si specifica solo il nome della colonna della tabella nidificata, viene restituita una nuova colonna per ogni colonna della tabella nidificata. Per impostazione predefinita, il nome della tabella nidificata viene aggiunto come prefisso al nome di ogni colonna della tabella nidificata.  
  
```  
SELECT FLATTENED MODEL_NAME, NODE_DISTRIBUTION  
FROM [TM_NaiveBayes].CONTENT  
WHERE NODE_TYPE = 26  
```  
  
 Risultati dell'esempio:  
  
|MODEL_NAME|NODE_DISTRIBUTION.ATTRIBUTE_NAME|NODE_DISTRIBUTION.ATTRIBUTE_VALUE|NODE_DISTRIBUTION.SUPPORT|NODE_DISTRIBUTION.PROBABILITY|NODE_DISTRIBUTION.VARIANCE|NODE_DISTRIBUTION.VALUETYPE|  
|-----------------|----------------------------------------|-----------------------------------------|--------------------------------|------------------------------------|---------------------------------|----------------------------------|  
|TM_NaiveBayes|Bike Buyer|Missing|0|0|0|1|  
|TM_NaiveBayes|Bike Buyer|0|6556|0.506685215240745|0||  
|TM_NaiveBayes|Bike Buyer|1|6383|0.493314784759255|0||  
  
 Nell'esempio seguente viene illustrato come restituire solo alcune colonne dalla tabella nidificata mediante un'istruzione sub-SELECT. È possibile semplificare la visualizzazione specificando un alias per il nome della tabella nidificata.  
  
```  
SELECT MODEL_NAME,   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT] AS t  
FROM NODE_DISTRIBUTION)   
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 26  
```  
  
 Risultati dell'esempio:  
  
|MODEL_NAME|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|  
|-----------------|-----------------------|------------------------|---------------|  
|TM_NaiveBayes|Bike Buyer|Missing|0|  
|TM_NaiveBayes|Bike Buyer|0|6556|  
|TM_NaiveBayes|Bike Buyer|1|6383|  
  
## <a name="see-also"></a>Vedere anche  
 [SELEZIONARE &#40;DMX&#41;](../dmx/select-dmx.md)   
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
