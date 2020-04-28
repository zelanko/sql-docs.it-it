---
title: CREAZIONE DI UN MODELLO DI DATA MINING (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e7215f50705b593130a69cfe076f0878b0ac03d6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68889074"
---
# <a name="create-mining-model-dmx"></a>CREATE MINING MODEL (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Consente di creare sia un nuovo modello di data mining che una struttura di data mining nel database. Per creare un modello è possibile definirlo nell'istruzione oppure utilizzare il linguaggio PMML (Predictive Model Markup Language). La seconda soluzione è consigliata solo agli utenti esperti.  
  
 Il nome della struttura di data mining viene creato aggiungendo il suffisso "_structure" al nome del modello, per assicurare l'utilizzo di un nome univoco derivato dal nome del modello.  
  
 Per creare un modello di data mining per una struttura di data mining esistente, utilizzare l'istruzione [ALTER mining structure &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CREATE [SESSION] MINING MODEL <model>  
(  
    [(<column definition list>)]  
)  
USING <algorithm> [(<parameter list>)] [WITH DRILLTHROUGH]  
CREATE MINING MODEL <model> FROM PMML <xml string>  
```  
  
## <a name="arguments"></a>Argomenti  
 *model*  
 Nome univoco del modello.  
  
 *elenco delle definizioni di colonna*  
 Elenco delimitato da virgole contenente le definizioni delle colonne.  
  
 *algoritmo*  
 Nome di un algoritmo di data mining, secondo quanto definito dal provider corrente.  
  
> [!NOTE]  
>  È possibile recuperare un elenco degli algoritmi supportati dal provider corrente utilizzando [DMSCHEMA_MINING_SERVICES set di righe](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset). Per visualizzare gli algoritmi supportati nell'istanza corrente di, vedere [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]proprietà di [data mining](https://docs.microsoft.com/analysis-services/server-properties/data-mining-properties).  
  
 *elenco di parametri*  
 Facoltativa. Elenco delimitato da virgole dei parametri definiti dal provider per l'algoritmo.  
  
 *stringa XML*  
 (Solo per uso avanzato). Modello con codifica XML (PMML). La stringa deve essere racchiusa tra virgolette singole (').  
  
 La clausola **Session** consente di creare un modello di data mining che viene rimosso automaticamente dal server quando si chiude la connessione o si verifica il timeout della sessione. I modelli di data mining di **sessione** sono utili perché non richiedono che l'utente sia un amministratore di database e utilizzano solo spazio su disco per il periodo di tempo in cui la connessione è aperta.  
  
 La clausola **with drill-through** consente di eseguire il drill-through sul nuovo modello di data mining. È possibile attivare il drill-through solo al momento della creazione del modello. Per alcuni tipi di modello, il drill-through è necessario per esplorare il modello nel visualizzatore personalizzato. Il drill-through non è richiesto per stima o per esplorare il modello tramite Microsoft Generic Content Tree Viewer.  
  
 L'istruzione **create Mining Model** crea un nuovo modello di data mining basato sull'elenco di definizioni di colonna, sull'algoritmo e sull'elenco di parametri dell'algoritmo.  
  
### <a name="column-definition-list"></a>Elenco delle definizioni di colonna  
 Per definire la struttura di un modello che utilizza l'elenco delle definizioni di colonna, è necessario includere le informazioni seguenti per ogni colonna:  
  
-   Nome (obbligatorio)  
  
-   Tipo di dati (obbligatorio)  
  
-   Distribuzione  
  
-   Elenco dei flag di modellazione  
  
-   Tipo di contenuto (obbligatorio)  
  
-   Richiesta di stima, che indica all'algoritmo di stimare la colonna, indicata dalla clausola **Predict** o **PREDICT_ONLY**  
  
-   Relazione con una colonna Attribute (obbligatoria solo se applicabile), indicata dalla clausola **related to**  
  
 Per definire una singola colonna utilizzare la sintassi seguente nell'elenco delle definizioni di colonna:  
  
```  
<column name>    <data type>    [<Distribution>]    [<Modeling Flags>]    <Content Type>    [<prediction>]    [<column relationship>]   
```  
  
 Per definire una colonna di tabella nidificata utilizzare la sintassi seguente nell'elenco delle definizioni di colonna:  
  
```  
<column name>    TABLE    [<prediction>] ( <non-table column definition list> )  
```  
  
 Ad eccezione dei flag di modellazione, per definire una colonna non è possibile utilizzare più di una clausola di uno stesso gruppo. È invece possibile definire più flag di modellazione per una stessa colonna.  
  
 Per un elenco dei tipi di dati, dei tipi di contenuto, delle distribuzioni di colonna e dei flag di modellazione che è possibile utilizzare per definire una colonna, vedere gli argomenti seguenti:  
  
-   [Tipi di dati &#40;Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-types-data-mining)  
  
-   [Tipi di contenuto &#40;Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining)  
  
-   [Distribuzioni delle colonne &#40;Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/column-distributions-data-mining)  
  
-   [Flag di modellazione &#40;data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/modeling-flags-data-mining)  
  
 Per descrivere la relazione tra due colonne, è possibile aggiungere una clausola alla descrizione. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]supporta l'utilizzo della clausola> \<della relazione di colonna seguente.  
  
 **CORRELATO A**  
 Questa forma indica una gerarchia di valori. La destinazione di una colonna con clausola RELATED TO può essere una colonna chiave in una tabella nidificata, una colonna con valori discreti nella riga dei case oppure un'altra colonna con una clausola RELATED TO, che indica una gerarchia con più livelli.  
  
 Per descrivere la modalità di utilizzo della colonna di stima, utilizzare una clausola di stima. Nella tabella seguente vengono descritte le due clausole disponibili.  
  
|\<clausola> di stima|Descrizione|  
|---------------------------|-----------------|  
|**PREDICT**|Questa colonna può essere stimata dal modello e può essere specificata nei case di input per stimare il valore di altre colonne stimabili.|  
|**PREDICT_ONLY**|Questa colonna può essere stimata dal modello, ma i relativi valori non possono essere utilizzati nei case di input per stimare il valore di altre colonne stimabili.|  
  
### <a name="parameter-definition-list"></a>Elenco delle definizioni di parametro  
 È possibile utilizzare l'elenco dei parametri per regolare le prestazioni e le funzionalità di un modello di data mining. La sintassi dell'elenco dei parametri è la seguente:  
  
```  
[<parameter> = <value>, <parameter> = <value>,...]  
```  
  
 Per un elenco dei parametri associati a ogni algoritmo, vedere [algoritmi di data mining &#40;Analysis Services-&#41;di data mining ](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining).  
  
## <a name="remarks"></a>Osservazioni  
 Per creare un modello che dispone di un set di dati di testing incorporati, è necessario utilizzare l'istruzione CREATE MINING STRUCTURE seguita da ALTER MINING STRUCTURE. Tuttavia, non tutti i tipi di modello supportano un set di dati di controllo. Per altre informazioni, vedere [CREATE MINING STRUCTURE &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md).  
  
 Per una procedura dettagliata relativa alla creazione di un modello di data mining tramite l'istruzione CREATEMODEL, vedere l' [esercitazione su Time Series Prediction DMX](https://msdn.microsoft.com/library/38ea7c03-4754-4e71-896a-f68cc2c98ce2).  
  
## <a name="naive-bayes-example"></a>Esempio sull'algoritmo Naive Bayes  
 Nell'esempio seguente viene utilizzato l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes per creare un nuovo modello di data mining. La colonna Bike Buyer è definita come attributo stimabile.  
  
```  
CREATE MINING MODEL [NBSample]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE PREDICT  
)  
USING Microsoft_Naive_Bayes  
```  
  
## <a name="association-model-example"></a>Esempio sul modello Association Rules  
 Nell'esempio seguente viene utilizzato l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Association Rules per creare un nuovo modello di data mining. L'istruzione sfrutta la possibilità di nidificare una tabella nella definizione del modello tramite una colonna di tabella. Il modello viene modificato utilizzando i parametri *MINIMUM_PROBABILITY* e *MINIMUM_SUPPORT* .  
  
```  
CREATE MINING MODEL MyAssociationModel (  
    OrderNumber TEXT KEY,  
    [Products] TABLE PREDICT (  
        [Model] TEXT KEY  
    )  
)  
USING Microsoft_Association_Rules (Minimum_Probability = 0.1, MINIMUM_SUPPORT = 0.01)  
```  
  
## <a name="sequence-clustering-example"></a>Esempio sull'algoritmo Sequence Clustering  
 Nell'esempio seguente viene utilizzato l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Sequence Clustering per creare un nuovo modello di data mining. Per definire il modello vengono utilizzate due chiavi. La colonna OrderNumber viene utilizzata come chiave del case e specifica singoli ordini. La colonna LineNumber viene utilizzata come chiave della tabella nidificata e specifica la sequenza nella quale gli elementi sono aggiunti a un ordine.  
  
```  
CREATE MINING MODEL BuyingSequence (  
    [Order Number] TEXT KEY,  
    [Products] TABLE   
     (  
        [Line Number] LONG KEY SEQUENCE,  
        [Model] TEXT DISCRETE PREDICT  
    )  
)  
USING Microsoft_Sequence_Clustering  
```  
  
## <a name="time-series-example"></a>Esempio sull'algoritmo Time Series  
 Nell'esempio seguente viene utilizzato l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Times Series per creare un nuovo modello di data mining utilizzando l'algoritmo ARTxp. ReportingDate è la colonna chiave per la serie temporale e ModelRegion è la colonna chiave per la serie di dati. In questo esempio si presuppone che i dati abbiano una periodicità di 12 mesi. Pertanto, il parametro *PERIODICITY_HINT* è impostato su 12.  
  
> [!NOTE]  
>  È necessario specificare il parametro *PERIODICITY_HINT* usando caratteri di parentesi graffe. Inoltre, poiché il valore è una stringa, deve essere racchiuso tra virgolette singole: "{\<valore numerico>}".  
  
```  
CREATE MINING MODEL SalesForecast (  
        ReportingDate DATE KEY TIME,  
        ModelRegion TEXT KEY,  
        Amount LONG CONTINUOUS PREDICT,  
        Quantity LONG CONTINUOUS PREDICT  
)  
USING Microsoft_Time_Series (PERIODICITY_HINT = '{12}', FORECAST_METHOD = 'ARTXP')  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di definizione dei dati](../dmx/dmx-statements-data-definition.md)   
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
