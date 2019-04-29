---
title: Esempi di Query del modello di regressione logistica | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 78a89577c35f1effe00fe35685640c229811860d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63020602"
---
# <a name="logistic-regression-model-query-examples"></a>Esempi di query sul modello di regressione logistica
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Quando si crea una query su un modello di data mining, è possibile creare una query sul contenuto, che fornisce dettagli sui criteri individuati durante l'analisi, oppure una query di stima, che utilizza i criteri presenti nel modello di data mining per eseguire stime utilizzando nuovi dati.  
  
 In questa sezione viene illustrato come creare entrambi i tipi di query per i modelli basati sull'algoritmo Microsoft Logistic Regression.  
  
 **Query sul contenuto**  
  
 [Recupero di parametri di modello tramite un set di righe dello schema di data mining](#bkmk_Query1)  
  
 [Ricerca di dettagli aggiuntivi sul modello tramite DMX](#bkmk_Query2)  
  
 **Query di stima**  
  
 [Esecuzione di stime per un valore continuo](#bkmk_Query3)  
  
 [Esecuzione di stime per un valore discreto](#bkmk_Query4)  
  
##  <a name="bkmk_top"></a> Acquisizione di informazioni sul modello di regressione logistica  
 I modelli di regressione logistica vengono creati utilizzando l'algoritmo Microsoft Neural Network con un particolare set di parametri. In un modello di regressione logistica sono pertanto contenute alcune delle informazioni presenti in un modello di rete neurale, ma in forma meno complessa. Per comprendere la struttura del contenuto del modello e i tipi di informazioni archiviati dai diversi tipi di nodo, vedere [Mining Model Content for Logistic Regression Models &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md).  
  
 Per proseguire negli scenari di query, è possibile creare un modello di regressione logistica come descritto nella sezione seguente dell'esercitazione intermedia sul Data Mining dei dati: [Lezione 5: Creazione di reti neurali e modelli di regressione logistica &#40;esercitazione intermedia sul Data Mining&#41;](http://msdn.microsoft.com/library/42c3701a-1fd2-44ff-b7de-377345bbbd6b).  
  
 È possibile usare anche la struttura di data mining, Targeted Mailing, da [Esercitazione di base sul data mining](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
```  
ALTER MINING STRUCTURE [Targeted Mailing]  
ADD MINING MODEL [TM_Logistic Regression]  
([Customer Key],  
[Age],  
[Bike Buyer] PREDICT,  
[Yearly Income] PREDICT,  
[Commute Distance],  
[English Education],  
Gender,  
[House Owner Flag],  
[Marital Status],  
[Number Cars Owned],  
[Number Children At Home],  
[Region],  
[Total Children]  
)  
USING Microsoft_Logistic_Regression  
```  
  
###  <a name="bkmk_Query1"></a> Esempio di Query 1: Recupero di parametri di modello tramite un set di righe dello schema di data mining  
 L'esecuzione di una query sul set di righe dello schema di data mining consente di trovare i metadati relativi al modello, ad esempio la data e l'ora di creazione, la data e l'ora dell'ultima elaborazione, il nome della struttura di data mining su cui si basa il modello e il nome della colonna utilizzata come attributo stimabile. Nell'esempio seguente vengono restituiti i parametri utilizzati quando è stato creato il modello, il nome e il tipo di modello e la relativa data di creazione.  
  
```  
SELECT MODEL_NAME, SERVICE_NAME, DATE_CREATED, MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Call Center_LR'  
```  
  
 Risultati dell'esempio:  
  
|MODEL_NAME|SERVICE_NAME|DATE_CREATED|MINING_PARAMETERS|  
|-----------------|-------------------|-------------------|------------------------|  
|Call Center_LR|Microsoft_Logistic_Regression|04/07/2009 20:38:33|HOLDOUT_PERCENTAGE=30, HOLDOUT_SEED=1, MAXIMUM_INPUT_ATTRIBUTES=255, MAXIMUM_OUTPUT_ATTRIBUTES=255, MAXIMUM_STATES=100, SAMPLE_SIZE=10000|  
  
###  <a name="bkmk_Query2"></a> Esempio di Query 2: Ricerca di dettagli aggiuntivi sul modello tramite DMX  
 Nella query seguente vengono restituite informazioni di base sul modello di regressione logistica. Si tenga presente che un modello di regressione logistica è per molti aspetti simile a un modello di rete neurale, inclusa la presenza di un nodo delle statistiche marginali (NODE_TYPE = 24) che descrive i valori utilizzati come input. In questa query di esempio viene utilizzato il modello di mailing diretto e i valori di tutti gli input vengono recuperati dalla tabella nidificata, NODE_DISTRIBUTION.  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION AS t  
FROM [TM_Logistic Regression].CONTENT   
```  
  
 Risultati parziali:  
  
|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|Age|Missing|0|0|0|1|  
|Age|45.43491192|17484|1|126.9544114|3|  
|Bike Buyer|Missing|0|0|0|1|  
|Bike Buyer|0|8869|0,507263784|0|4|  
|Bike Buyer|1|8615|0,492736216|0|4|  
|Commute Distance|Missing|0|0|0|1|  
|Commute Distance|5-10 Miles|3033|0.173472889|0|4|  
  
 Tramite la query effettiva vengono restituite molte più righe, tuttavia in questo esempio viene illustrato il tipo di informazioni fornite sugli input. Per gli input discreti, nella tabella viene elencato ogni valore possibile. Poiché per gli input con valore continuo, ad esempio Age, è impossibile fornire un elenco completo, l'input viene discretizzato come media. Per altre informazioni su come usare le informazioni nel nodo delle statistiche marginali, vedere [Contenuto dei modelli di data mining per i modelli di regressione logistica &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md).  
  
> [!NOTE]  
>  I risultati sono stati resi bidimensionali per consentirne una visualizzazione più immediata, ma è possibile restituire la tabella nidificata in una sola colonna, se il provider supporta set di righe gerarchici.  
  
## <a name="prediction-queries-on-a-logistic-regression-model"></a>Query di stima per un modello di regressione logistica  
 È possibile usare la funzione [Predict &#40;DMX&#41;](../../dmx/predict-dmx.md) con ogni tipo di modello di data mining per fornire nuovi dati al modello ed eseguire stime in base ai nuovi valori. Sono inoltre disponibili funzioni che consentono di restituire informazioni aggiuntive sulla stima, ad esempio la probabilità che una stima sia corretta. In questa sezione vengono forniti alcuni esempi di query di stima su un modello di regressione logistica.  
  
###  <a name="bkmk_Query3"></a> Esempio di Query 3: Esecuzione di stime per un valore continuo  
 Poiché la regressione logistica supporta anche l'utilizzo di attributi continui sia per l'input sia per la stima, è facile creare modelli che correlano i vari fattori nei dati. È possibile utilizzare query di stima per esplorare la relazione fra questi fattori.  
  
 Nell'esempio di query riportato di seguito, basato sul modello di call center tratto dall'esercitazione intermedia, viene creata una query singleton che stima il livello di servizio per il turno del venerdì mattina. Tramite la funzione [PredictHistogram (DMX)](../../dmx/predicthistogram-dmx.md) viene restituita una tabella annidata che contiene statistiche importanti per comprendere la validità del valore stimato.  
  
```  
SELECT  
  Predict([Call Center_LR].[Service Grade]) as Predicted ServiceGrade,  
  PredictHistogram([Call Center_LR].[Service Grade]) as [Results],  
FROM  
  [Call Center_LR]  
NATURAL PREDICTION JOIN  
(SELECT 'Friday' AS [Day Of Week],  
  'AM' AS [Shift]) AS t  
```  
  
 Risultati dell'esempio:  
  
|Livello di servizio stimato|Service Grade|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|-----------------------------|-------------------|--------------|------------------|--------------------------|---------------|------------|  
|0.102601830123659|0.102601830123659|83.0232558139535|0.988372093023256|0|0.00120552660600087|0.034720694203902|  
|||0.976744186046512|0.0116279069767442|0.0116279069767442|0|0|  
  
 Per altre informazioni su probabilità, supporto e deviazione standard di valori nella tabella NODE_DISTRIBUTION nidificata, vedere [Contenuto dei modelli di data mining per i modelli di regressione logistica &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md).  
  
###  <a name="bkmk_Query4"></a> Esempio di Query 4: Esecuzione di stime per un valore discreto  
 La regressione logistica viene in genere utilizzata negli scenari nei quali si desidera analizzare i fattori che contribuiscono a un risultato binario. Anche se tramite il modello usato nell'esercitazione viene stimato un valore continuo, **ServiceGrade**, in uno scenario reale è necessario configurare il modello per stimare se il livello di servizio ha soddisfatto un valore target discretizzato. In alternativa, è possibile restituire le stime usando un valore continuo, ma in un secondo momento è necessario raggruppare i risultati stimati in **Buono**, **Discreto**o **Scarso**.  
  
 Nell'esempio riportato di seguito viene illustrato come modificare la modalità di raggruppamento dell'attributo stimabile. A tale scopo, creare una copia della struttura di data mining, quindi modificare il metodo di discretizzazione della colonna di destinazione in modo che i valori siano raggruppati anziché continui.  
  
 La procedura seguente illustra come modificare il raggruppamento di valori del livello di servizio nei dati del call center.  
  
##### <a name="to-create-a-discretized-version-of-the-call-center-mining-structure-and-models"></a>Per creare una versione discretizzata della struttura di data mining del call center e dei modelli  
  
1.  In Esplora soluzioni di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]espandere **Strutture di data minin**.  
  
2.  Fare clic con il pulsante destro del mouse su Call Center.dmm e scegliere **Copia**.  
  
3.  Fare clic con il pulsante destro del mouse su **Strutture di data mining** e scegliere **Incolla**. Viene aggiunta una nuova struttura di data mining, denominata Call Center 1.  
  
4.  Fare clic con il pulsante destro del mouse sulla nuova struttura di data mining e scegliere **Rinomina**. Digitare il nuovo nome, **Call center discretizzato**.  
  
5.  Fare doppio clic sulla nuova struttura di data mining per aprirla nella finestra di progettazione. Si noti che sono stati copiati anche tutti i modelli di data mining, tutti con estensione 1. Per il momento, lasciare i nomi invariati.  
  
6.  Nella scheda **Struttura di data mining** fare clic con il pulsante destro del mouse sulla colonna per il livello di servizio e selezionare **Proprietà**.  
  
7.  Modificare il valore della proprietà **Content** da **Continuo** a **Discretizzato**. Modifica la proprietà **DiscretizationMethod** in **Cluster**. Per il conteggio dei bucket di discretizzazione digitare **3**.  
  
    > [!NOTE]  
    >  Questi parametri vengono utilizzati solo per illustrare il processo, non producono necessariamente un modello valido.  
  
8.  Scegliere **Elabora struttura di data mining e tutti i modelli** dal menu **Modello di data mining**.  
  
 Nella query di esempio seguente, basata su questo modello discretizzato, viene stimato il livello di servizio per il giorno della settimana specificato, insieme alle probabilità per ogni risultato stimato.  
  
```  
SELECT  
  (PredictHistogram([Call Center_LR 1].[Service Grade])) as [Predictions]  
FROM  
  [Call Center_LR 1]  
NATURAL PREDICTION JOIN  
(SELECT 'Saturday' AS [Day Of Week]) AS t    
```  
  
 Risultati previsti:  
  
 **Stime:**  
  
|Service Grade|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|-------------------|--------------|------------------|--------------------------|---------------|------------|  
|0.10872718383125|35.7246504770641|0.425293458060287|0.0170168360030293|0|0|  
|0.05855769230625|31.7098880800703|0.377498667619885|0.020882020060454|0|0|  
|0.170169491525|15.6109159883202|0.185844237956192|0.0661386571386049|0|0|  
||0.954545454545455|0.0113636363636364|0.0113636363636364|0|0|  
  
 Si noti che i risultati stimati sono stati raggruppati in tre categorie come specificato; tuttavia i raggruppamenti sono basati sul clustering di valori effettivi nei dati, non valori arbitrari che è possibile impostare come obiettivi aziendali.  
  
## <a name="list-of-prediction-functions"></a>Elenco delle funzioni di stima  
 Tutti gli algoritmi [!INCLUDE[msCoName](../../includes/msconame-md.md)] supportano un set comune di funzioni. L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Logistic Regression tuttavia supporta le funzioni aggiuntive elencate nella tabella seguente.  
  
|||  
|-|-|  
|Funzione di stima|Uso|  
|[IsDescendant &#40;DMX&#41;](../../dmx/isdescendant-dmx.md)|Viene determinato se un nodo è figlio di un altro nodo nel modello.|  
|[PredictAdjustedProbability &#40;DMX&#41;](../../dmx/predictadjustedprobability-dmx.md)|Viene restituita la probabilità adattata dello stato specificato.|  
|[PredictHistogram &#40;DMX&#41;](../../dmx/predicthistogram-dmx.md)|Viene restituito un valore, o un set di valori, stimato per una colonna specificata.|  
|[PredictProbability &#40;DMX&#41;](../../dmx/predictprobability-dmx.md)|Viene restituita la probabilità per uno stato specificato.|  
|[PredictStdev &#40;DMX&#41;](../../dmx/predictstdev-dmx.md)|Viene restituita la deviazione standard per il valore stimato.|  
|[PredictSupport &#40;DMX&#41;](../../dmx/predictsupport-dmx.md)|Viene restituito il valore di supporto per uno stato specificato.|  
|[PredictVariance &#40;DMX&#41;](../../dmx/predictvariance-dmx.md)|Restituisce la varianza di una colonna specificata.|  
  
 Per un elenco delle funzioni comuni a tutti gli algoritmi di [!INCLUDE[msCoName](../../includes/msconame-md.md)], vedere [Funzioni di stima correlate &#40;DMX&#41;](../../dmx/general-prediction-functions-dmx.md). Per la sintassi di funzioni specifiche, vedere [Guida di riferimento alle funzioni DMX &#40;Data Mining Extensions&#41;](../../dmx/data-mining-extensions-dmx-function-reference.md).  
  
> [!NOTE]  
>  Per i modelli di reti neurali e di regressione logistica la funzione [PredictSupport &#40;DMX&#41;](../../dmx/predictsupport-dmx.md) restituisce un solo valore che rappresenta la dimensione del set di training per l'intero modello.  
  
## <a name="see-also"></a>Vedere anche  
 [Query di data mining](../../analysis-services/data-mining/data-mining-queries.md)   
 [Algoritmo Microsoft Logistic Regression](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)   
 [Riferimento tecnico per l'algoritmo Microsoft Logistic Regression](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)   
 [Contenuto dei modelli di data mining per i modelli di regressione logistica &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)   
 [Lezione 5: Creazione di reti neurali e modelli di regressione logistica &#40;esercitazione intermedia sul Data Mining&#41;](http://msdn.microsoft.com/library/42c3701a-1fd2-44ff-b7de-377345bbbd6b)  
  
  
