---
title: SELECT FROM &lt;modello&gt; PREDICTION JOIN (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f0778a104383f54cf2798c0d6f51f082926b1fd4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62658953"
---
# <a name="select-from-ltmodelgt-prediction-join-dmx"></a>SELECT FROM &lt;modello&gt; PREDICTION JOIN (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Utilizza un modello di data mining per stimare gli stati delle colonne in un'origine dati esterna. Il **PREDICTION JOIN** istruzione corrisponde a ogni case dalla query di origine per il modello.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <select expression list>   
FROM <model> | <sub select> [NATURAL] PREDICTION JOIN   
<source data query> [ON <join mapping list>]   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argomenti  
 *n*  
 Facoltativo. Valore intero mediante il quale viene specificato il numero di righe da restituire.  
  
 *elenco di espressioni SELECT*  
 Elenco delimitato da virgole contenente espressioni e identificatori di colonna derivati dal modello di data mining.  
  
 *model*  
 Identificatore del modello.  
  
 *Selezionare Sub*  
 Istruzione SELECT incorporata.  
  
 *query sull'origine dati*  
 Query di origine.  
  
 *elenco mapping dei join*  
 Facoltativo. Espressione logica che confronta le colonne del modello con quelle della query di origine.  
  
 *espressione della condizione*  
 Facoltativo. Condizione per limitare i valori restituiti dall'elenco di colonne.  
  
 *expression*  
 Facoltativo. Espressione che restituisce un valore scalare.  
  
## <a name="remarks"></a>Note  
 La clausola ON definisce il mapping tra le colonne della query di origine e quelle del modello di data mining. Tale mapping viene utilizzato per dirigere le colonne dalla query di origine alle colonne nel modello di data mining, di modo che possano essere utilizzate come input durante la creazione delle stime. Colonne di \< *elenco mapping dei join*> sono correlate tramite un segno di uguale (=), come illustrato nell'esempio seguente:  
  
```  
[MiningModel].ColumnA = [source data query].Column1 AND   
[MiningModel].ColumnB = [source data query].Column2 AND  
...  
```  
  
 Quando si associa una tabella nidificata nella clausola ON, è necessario associare la colonna chiave a una colonna non chiave qualsiasi, di modo che l'algoritmo possa identificare correttamente a quale case appartiene il record della colonna nidificata.  
  
 La query di origine del PREDICTION JOIN può essere una query singleton o di tabella.  
  
 È possibile specificare funzioni di stima che non restituiscono un'espressione di tabella nel \< *elenco di espressioni select*> e il \< *espressione condizione*>.  
  
 **NATURAL PREDICTION JOIN** esegue automaticamente il mapping tra loro i nomi di colonna dalla query di origine corrispondano ai nomi di colonna nel modello. Se si usa **NATURAL PREDICTION**, è possibile omettere la clausola ON.  
  
 La condizione WHERE può essere applicata solo a colonne stimabili o colonne correlate.  
  
 La clausola ORDER BY può accettare solo una singola colonna come argomento; ovvero, non è possibile eseguire l'ordinamento in base a più colonne.  
  
## <a name="example-1-singleton-query"></a>Esempio 1: Query singleton  
 Nell'esempio seguente viene illustrato come creare una query per stimare in tempo reale la probabilità che una persona specifica acquisti una bicicletta. In questa query i dati non vengono archiviati in una tabella o in un'altra origine dati, ma vengono immessi direttamente nella query. La query si riferisce a una persona con il profilo seguente:  
  
-   35 anni  
  
-   Possiede una casa  
  
-   Possiede due automobili  
  
-   Ha due figli  
  
 Usa il modello di data mining TM Decision Tree e le caratteristiche note sull'oggetto, la query restituisce un valore booleano che indica se la persona ha acquistato la bicicletta e un set di valori tabulari, restituiti dai [PredictHistogram &#40;DMX &#41; ](../dmx/predicthistogram-dmx.md) (funzione), che descrivono come è stata effettuata la stima.  
  
```  
SELECT  
  [TM Decision Tree].[Bike Buyer],  
  PredictHistogram([Bike Buyer])  
FROM  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 35 AS [Age],  
  '5-10 Miles' AS [Commute Distance],  
  '1' AS [House Owner Flag],  
  2 AS [Number Cars Owned],  
  2 AS [Total Children]) AS t  
```  
  
## <a name="example-2-using-openquery"></a>Esempio 2: Tramite la funzione OPENQUERY  
 Nell'esempio seguente viene illustrato come creare una query di stima batch utilizzando un elenco di clienti potenziali archiviato in un set di dati esterno. Poiché la tabella fa parte di una vista origine dati che è stata definita in un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], la query può usare [OPENQUERY](../dmx/source-data-query-openquery.md) per recuperare i dati. Poiché i nomi delle colonne nella tabella sono diversi da quelli nel modello di data mining, il **via** clausola deve essere utilizzata per le colonne nella tabella vengono mappati alle colonne nel modello.  
  
 La query restituisce il nome e il cognome di ogni persona presente nella tabella, oltre a una colonna booleana che indica la probabilità che la persona acquisti una bicicletta, dove 0 indica "è improbabile che acquisti una bicicletta" e 1 indica "è probabile che acquisti una bicicletta". L'ultima colonna contiene la probabilità per il risultato stimato.  
  
```  
SELECT  
  t.[LastName],  
  t.[FirstName],  
  [TM Decision Tree].[Bike Buyer],  
  PredictProbability([Bike Buyer])  
From  
  [TM Decision Tree]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT  
      [LastName],  
      [FirstName],  
      [MaritalStatus],  
      [Gender],  
      [YearlyIncome],  
      [TotalChildren],  
      [NumberChildrenAtHome],  
      [Education],  
      [Occupation],  
      [HouseOwnerFlag],  
      [NumberCarsOwned]  
    FROM  
      [dbo].[ProspectiveBuyer]  
    ') AS t  
ON  
  [TM Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
  [TM Decision Tree].[Gender] = t.[Gender] AND  
  [TM Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
  [TM Decision Tree].[Total Children] = t.[TotalChildren] AND  
  [TM Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
  [TM Decision Tree].[Education] = t.[Education] AND  
  [TM Decision Tree].[Occupation] = t.[Occupation] AND  
  [TM Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
  [TM Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
```  
  
 Per limitare il set di dati solo ai clienti stimati come acquirenti di una bicicletta e quindi ordinare l'elenco in base al nome del cliente, è possibile aggiungere una clausola WHERE e una clausola ORDER BY all'esempio precedente:  
  
```  
WHERE [BIKE Buyer]  
ORDER BY [LastName] ASC  
```  
  
## <a name="example-3-predicting-associations"></a>Esempio 3: Stima delle associazioni  
 Nell'esempio seguente viene illustrato come creare una stima utilizzando un modello compilato in base all'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Association Rules. Le stime su un modello di associazione possono essere utilizzate per consigliare prodotti correlati. La query seguente restituisce ad esempio i tre prodotti che hanno la maggiore probabilità di essere acquistati insieme:  
  
-   Mountain Bottle Cage  
  
-   Mountain Tire Tube  
  
-   Mountain-200  
  
 Il [Predict &#40;DMX&#41; ](../dmx/predict-dmx.md) funzione è polimorfica e può essere utilizzata con tutti i tipi di modello. Viene utilizzato value3 come argomento della funzione per limitare il numero di articoli restituiti dalla query. Il **seleziona** elencate di seguito la clausola NATURAL PREDICTION JOIN fornisce i valori da utilizzare come input per la stima.  
  
```  
SELECT FLATTENED  
  PREDICT([Association].[v Assoc Seq Line Items], 3)  
FROM  
  [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
  UNION SELECT 'Mountain Tire Tube' AS [Model]  
  UNION SELECT 'Mountain-200' AS [Model]) AS [v Assoc Seq Line Items ]) AS t  
```  
  
 Risultati dell'esempio:  
  
|Expression.Model|  
|----------------------|  
|HL Mountain Tire|  
|Water Bottle|  
|Fender Set - Mountain|  
  
 Poiché la colonna che contiene l'attributo stimabile, `[v Assoc Seq Line Items]`, è una colonna della tabella, la query restituisce una singola colonna contenente una tabella nidificata. Per impostazione predefinita, la colonna della tabella nidificata viene denominata `Expression`. Se il provider non supporta set di righe gerarchici, è possibile usare la **FLATTENED** (parola chiave) come illustrato in questo esempio per rendere più semplice visualizzare i risultati.  
  
## <a name="see-also"></a>Vedere anche  
 [SELECT &#40;DMX&#41;](../dmx/select-dmx.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; istruzioni di definizione dei dati](../dmx/dmx-statements-data-definition.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
