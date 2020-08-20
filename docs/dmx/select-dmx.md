---
description: SELECT (DMX)
title: SELECT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1e44c7d2f4bf872a7629a48c305114f09f98ee66
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462045"
---
# <a name="select-dmx"></a>SELECT (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  L'istruzione **Select** in DMX (Data Mining Extensions) viene utilizzata per le seguenti attività in data mining:  
  
-   Visualizzazione del contenuto di un modello di data mining esistente  
  
-   Creazione di stime da un modello di data mining esistente.  
  
-   Creazione di una copia di un modello di data mining esistente.  
  
-   Visualizzazione della struttura di data mining  
  
 Sebbene la sintassi completa di questa istruzione sia complessa, le principali clausole utilizzate per la visualizzazione di un modello e della struttura sottostante possono essere riepilogate come segue:  
  
```  
SELECT [FLATTENED] [TOP <n>] <select list>  
FROM <model/structure>[.aspect]  
[WHERE <condition expression>]  
[ORDER BY <expression>[DESC|ASC]]  
```  
  
## <a name="flattened"></a>FLATTENED  
 Alcuni client di data mining non possono accettare set di risultati in formato gerarchico da un provider di data mining. Il client potrebbe non essere in grado di gestire una gerarchia o potrebbe essere necessario archiviare i risultati in una singola tabella denormalizzata. Per convertire i dati da tabelle nidificate in tabelle in formato flat, è necessario richiedere che i risultati della query siano convertiti in formato flat.  
  
 Per rendere flat i risultati della query, usare la sintassi **Select** con l'opzione **Flat** , come illustrato nell'esempio seguente:  
  
```  
SELECT FLATTENED <select list> FROM ...  
```  
  
## <a name="top-n-and-order-by"></a>TOP \<n> e order by  
 È possibile ordinare i risultati di una query utilizzando un'espressione e può restituire un subset dei risultati utilizzando una combinazione delle clausole **Order by** e **Top** . Questo è utile ad esempio in uno scenario di mailing diretto in cui si desidera inviare i risultati solo ai destinatari che hanno la maggiore probabilità di rispondere. È possibile ordinare i risultati di una query di stima mailing di destinazione in base alla probabilità di stima, quindi restituire solo i primi \<n> risultati.  
  
## <a name="select-list"></a>Elenco di selezione  
 *\<select list>* Può includere riferimenti a colonne scalari, funzioni di stima ed espressioni. Le opzioni disponibili variano in base all'algoritmo e ai contesti seguenti:  
  
-   È in corso l'esecuzione di una query su una struttura di data mining o su un modello di data mining  
  
-   È in corso l'esecuzione di una query sul contenuto o sui case  
  
-   L'origine dati è una tabella relazionale o un cubo  
  
-   È in corso l'esecuzione di stime  
  
 In molti casi, è possibile utilizzare alias o creare espressioni semplici basate sugli elementi nell'elenco di selezione. Nell'esempio seguente viene illustrata un'espressione nelle colonne del modello:  
  
```  
SELECT [CustomerID], [Last Name] + ', ' + [FirstName] AS FullName  
FROM <model>.CASES  
```  
  
 Nell'esempio seguente viene creato un alias per una colonna che contiene i risultati di una funzione di stima:  
  
```  
SELECT Predict([Column1], 'Value') as Column1Prediction  
FROM MyModel  
JOIN <source data query>  
```  
  
## <a name="where"></a>WHERE  
 È possibile limitare i case restituiti dalla query utilizzando una clausola **where** . La clausola **where** specifica che i riferimenti di colonna nell'espressione **where** devono avere la stessa semantica dei riferimenti di colonna in *\<select list>* dell'istruzione **Select** e possono restituire solo un'espressione booleana. La sintassi per la clausola **where** è la seguente:  
  
```  
WHERE < condition expression >  
```  
  
 L'elenco di selezione e la clausola **where** di un'istruzione **SELECT** devono rispettare le regole seguenti:  
  
-   L'elenco di selezione deve contenere un'espressione che non restituisce un risultato booleano. L'espressione può essere modificata, ma deve comunque restituire risultati non booleani.  
  
-   La clausola **where** deve contenere un'espressione che restituisce un risultato booleano. La clausola può essere modificata, ma deve comunque restituire un risultato booleano.  
  
## <a name="predictions"></a>Stime  
 Esistono due tipi di sintassi che è possibile utilizzare per la creazione di stime:  
  
-   [SELECT FROM &#60;Model&#62; PREDICtion JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
-   [Selezionare da &#60;modello&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)  
  
 Il primo tipo consente di creare stime complesse in tempo reale o in batch.  
  
 Il secondo consente di creare un prediction join vuoto su una colonna stimabile in un modello di data mining e restituisce lo stato più probabile della colonna. I risultati di questa query sono completamente basati sul contenuto del modello di data mining.  
  
 È possibile inserire un'istruzione SELECT nella query di origine di un'istruzione SELECT FROM PREDICtion JOIN utilizzando la sintassi seguente.  
  
```  
SELECT FROM PREDICTION JOIN (<SELECT statement>) AS t, WHERE <SELECT statement>  
```  
  
 Per ulteriori informazioni sulla creazione di query di stima, vedere [struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md).  
  
## <a name="clause-syntax"></a>Sintassi delle clausole  
 A causa della complessità dell'esplorazione con l'istruzione **Select** , gli elementi della sintassi e gli argomenti dettagliati sono descritti in base alla clausola. Per ulteriori informazioni su ciascuna clausola, fare clic su un argomento indicato nell'elenco seguente:  
  
 [Selezionare DISTINCT FROM &#60;Model &#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)  
  
 [Selezionare da &#60;modello&#62;. CONTENUTO &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)  
  
 [Selezionare da &#60;modello&#62;. CASI &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)  
  
 [Selezionare da &#60;modello&#62;. SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)  
  
 [Selezionare da &#60;modello&#62;. DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)  
  
 [SELECT FROM &#60;Model&#62; PREDICtion JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
 [Selezionare da &#60;modello&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)  
  
 [Selezionare una&#62; struttura &#60;. CASI](../dmx/select-from-structure-cases.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di definizione dei dati](../dmx/dmx-statements-data-definition.md)   
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)  
  
  
