---
title: ALTER MINING STRUCTURE (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5535428d89a0d14b60e3ac79d281f63b4c69bfb5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68889869"
---
# <a name="alter-mining-structure-dmx"></a>ALTER MINING STRUCTURE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Crea un nuovo modello di data mining basato su una struttura di data mining esistente.  Quando si utilizza l'istruzione **ALTER MINING STRUCTURE** per creare un nuovo modello di data mining, la struttura deve essere già esistente. Al contrario, quando si utilizza l'istruzione, [creare un modello di data mining &#40;&#41;DMX ](../dmx/create-mining-model-dmx.md), si crea un modello e si genera automaticamente la struttura di data mining sottostante.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ALTER MINING STRUCTURE <structure>  
ADD MINING MODEL <model>  
(  
    <column definition list>  
  [(<nested column definition list>) [WITH FILTER (<nested filter criteria>)]]  
)  
USING <algorithm> [(<parameter list>)]   
[WITH DRILLTHROUGH]  
[,FILTER(<filter criteria>)]  
```  
  
## <a name="arguments"></a>Argomenti  
 *struttura*  
 Nome della struttura di data mining a cui verrà aggiunto il modello di data mining.  
  
 *model*  
 Nome univoco del modello di data mining.  
  
 *elenco delle definizioni di colonna*  
 Elenco delimitato da virgole contenente le definizioni delle colonne.  
  
 *elenco di definizioni di colonne nidificate*  
 Elenco delimitato da virgole delle colonne di una tabella nidificata, se applicabile.  
  
 *criteri di filtro annidati*  
 Espressione di filtro applicata alle colonne di una tabella nidificata.  
  
 *algoritmo*  
 Nome di un algoritmo di data mining, definito dal provider.  
  
> [!NOTE]  
>  È possibile recuperare un elenco degli algoritmi supportati dal provider corrente utilizzando [DMSCHEMA_MINING_SERVICES set di righe](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset). Per visualizzare gli algoritmi supportati nell'istanza corrente di, vedere [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]proprietà di [data mining](https://docs.microsoft.com/analysis-services/server-properties/data-mining-properties).  
  
 *elenco di parametri*  
 Facoltativa. Elenco delimitato da virgole dei parametri definiti dal provider per l'algoritmo.  
  
 *criteri di filtro*  
 Espressione di filtro applicata alle colonne della tabella del case.  
  
## <a name="remarks"></a>Osservazioni  
 Se la struttura di data mining contiene chiavi composte, il modello di data mining dovrà includere tutte le colonne chiave definite nella struttura.  
  
 Se il modello non richiede una colonna stimabile, come ad esempio i modelli compilati utilizzando gli algoritmi [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering e [!INCLUDE[msCoName](../includes/msconame-md.md)] Sequence Clustering, non sarà necessario includere una definizione di colonna nell'istruzione. Tutti gli attributi nel modello risultante verranno gestiti come input.  
  
 Nella clausola **with** applicabile alla tabella del case è possibile specificare le opzioni per il filtro e il drill-through:  
  
-   Aggiungere la parola chiave **Filter** e una condizione di filtro. Il filtro si applica ai case nel modello di data mining.  
  
-   Aggiungere la parola chiave **drill-through** per consentire agli utenti del modello di data mining di eseguire il drill-down dai risultati del modello ai dati del case. In DMX (Data Mining Extensions) è possibile abilitare il drill-through solo al momento della creazione del modello.  
  
 Per utilizzare sia il filtro case che il drill-through, combinare le parole chiave in una singola clausola **with** usando la sintassi illustrata nell'esempio seguente:  
  
 `WITH DRILLTHROUGH, FILTER(Gender = 'Male')`  
  
## <a name="column-definition-list"></a>Elenco delle definizioni di colonna  
 Per definire la struttura di un modello, specificare un elenco delle definizioni di colonna che include le informazioni seguenti per ogni colonna:  
  
-   Nome (obbligatorio)  
  
-   Alias (facoltativo)  
  
-   Flag di modellazione  
  
-   Richiesta di stima, che indica all'algoritmo se la colonna contiene un valore stimabile, indicato dalla clausola **Predict** o **PREDICT_ONLY**  
  
 Per definire una singola colonna, utilizzare la sintassi seguente nell'elenco delle definizioni di colonna:  
  
```  
<structure column name>  [AS <model column name>]  [<modeling flags>]    [<prediction>]  
```  
  
### <a name="column-name-and-alias"></a>Nome e alias di colonna  
 Il nome di colonna utilizzato nell'elenco delle definizioni di colonna deve essere il nome della colonna così come viene utilizzato nella struttura di data mining. Tuttavia, è anche possibile definire un alias per rappresentare la colonna della struttura nel modello di data mining. È inoltre possibile creare più definizioni di colonna per la stessa colonna della struttura e assegnare un alias e un utilizzo di stima diversi a ogni copia della colonna. Per impostazione predefinita, il nome della colonna della struttura viene utilizzato se non viene definito un alias. Per altre informazioni, vedere [creare un alias per una colonna del modello](https://docs.microsoft.com/analysis-services/data-mining/create-an-alias-for-a-model-column).  
  
 Per le colonne della tabella nidificata, specificare il nome della tabella nidificata, specificare il tipo di dati come **tabella**, quindi fornire l'elenco delle colonne annidate da includere nel modello, racchiuse tra parentesi.  
  
 È possibile definire un'espressione di filtro che viene applicata alla tabella nidificata aggiungendo un'espressione di criteri di filtro dopo la definizione di colonna della tabella nidificata.  
  
### <a name="modeling-flags"></a>Flag di modellazione  
 
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] supporta i flag di modellazione seguenti per l'utilizzo nelle colonne del modello di data mining:  
  
> [!NOTE]  
>  Il flag di modellazione NOT_NULL si applica alla colonna della struttura di data mining. Per altre informazioni, vedere [CREATE MINING STRUCTURE &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md).  
  
|||  
|-|-|  
|Termine|Definizione|  
|**REGRESSORE**|Indica che l'algoritmo può utilizzare la colonna specificata nella formula di regressione degli algoritmi di regressione.|  
|**MODEL_EXISTENCE_ONLY**|Indica che i valori per la colonna di attributi sono meno importanti rispetto alla presenza dell'attributo.|  
  
 È invece possibile definire più flag di modellazione per una stessa colonna. Per ulteriori informazioni sull'utilizzo dei flag di modellazione, vedere [flag di modellazione &#40;&#41;DMX ](../dmx/modeling-flags-dmx.md).  
  
### <a name="prediction-clause"></a>Clausola di stima  
 La clausola di stima consente di descrivere la modalità di utilizzo della colonna di stima. Nella tabella seguente sono elencate le clausole possibili.  
  
|||  
|-|-|  
|**PREDICT**|Questa colonna può essere stimata dal modello e i relativi valori possono essere utilizzati come input per stimare il valore di altre colonne stimabili.|  
|**PREDICT_ONLY**|Questa colonna può essere stimata dal modello, ma i relativi valori non possono essere utilizzati nei case di input per stimare il valore di altre colonne stimabili.|  
  
## <a name="filter-criteria-expressions"></a>Espressioni di criteri di filtro  
 È possibile definire un filtro per limitare i case utilizzati nel modello di data mining. Il filtro può essere applicato alle colonne nella tabella del case, alle righe nella tabella nidificata o a entrambe.  
  
 Le espressioni di criteri di filtro sono predicati DMX semplificati, simili a una clausola WHERE. Le espressioni di filtro sono limitate a formule che utilizzano operatori matematici di base, valori scalari e nomi di colonna. L'operatore EXISTS, che restituisce true se per la sottoquery viene restituita almeno una riga, rappresenta un'eccezione. I predicati possono essere combinati utilizzando gli operatori logici comuni: AND, OR e NOT.  
  
 Per ulteriori informazioni sui filtri utilizzati con i modelli di data mining, vedere [filtri per i modelli di data mining &#40;Analysis Services-&#41;di data mining ](https://docs.microsoft.com/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining).  
  
> [!NOTE]  
>  Le colonne di un filtro devono essere colonne della struttura di data mining. Non è possibile creare un filtro su una colonna del modello o una colonna in forma di alias.  
  
 Per ulteriori informazioni sulla sintassi e sugli operatori DMX, vedere [colonne del modello di data mining](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns).  
  
## <a name="parameter-definition-list"></a>Elenco delle definizioni di parametro  
 È possibile modificare le prestazioni e le funzionalità di un modello aggiungendo parametri dell'algoritmo all'elenco di parametri. I parametri che è possibile utilizzare variano in base all'algoritmo specificato nella clausola USING. Per un elenco dei parametri associati a ogni algoritmo, vedere algoritmi di [data mining &#40;Analysis Services-&#41;di data mining ](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining).  
  
 La sintassi dell'elenco dei parametri è la seguente:  
  
```  
[<parameter> = <value>, <parameter> = <value>,...]  
```  
  
## <a name="example-1-add-a-model-to-a-structure"></a>Esempio 1: Aggiunta di un modello a una struttura  
 Nell'esempio seguente viene aggiunto un modello di data mining Naive Bayes alla nuova struttura di data mining **mailing** e viene limitato il numero massimo di stati degli attributi a 50.  
  
```  
ALTER MINING STRUCTURE [New Mailing]  
ADD MINING MODEL [Naive Bayes]  
(  
    CustomerKey,   
    Gender,  
    [Number Cars Owned],  
    [Bike Buyer] PREDICT  
)  
USING Microsoft_Naive_Bayes (MAXIMUM_STATES = 50)  
```  
  
## <a name="example-2-add-a-filtered-model-to-a-structure"></a>Esempio 2: Aggiunta di un modello filtrato a una struttura  
 Nell'esempio seguente viene aggiunto un modello `Naive Bayes Women`di data mining alla nuova struttura di data mining **mailing** . Il nuovo modello presenta la stessa struttura di base del modello di data mining aggiunto nell'esempio 1, ma i case della struttura di data mining sono limitati ai clienti di sesso femminile di età superiore a 50 anni.  
  
```  
ALTER MINING STRUCTURE [New Mailing]  
ADD MINING MODEL [Naive Bayes Women]  
(  
    CustomerKey,   
    Gender,  
    [Number Cars Owned],  
    [Bike Buyer] PREDICT  
)  
USING Microsoft_Naive_Bayes  
WITH FILTER([Gender] = 'F' AND [Age] >50)  
```  
  
## <a name="example-3-add-a-filtered-model-to-a-structure-with-a-nested-table"></a>Esempio 3: Aggiunta di un modello filtrato a una struttura con una tabella nidificata  
 Nell'esempio seguente viene aggiunto un modello di data mining a una versione modificata della struttura di data mining Market Basket. La struttura di data mining utilizzata nell'esempio è stata modificata per aggiungere una colonna **Region** , che contiene gli attributi per l'area Customer e una colonna del **gruppo Income** , che categorizza il reddito dei clienti usando i valori **High**, **moderate**o **low**.  
  
 La struttura di data mining include anche una tabella nidificata in cui sono elencati gli elementi acquistati dal cliente.  
  
 Poiché la struttura di data mining contiene una tabella nidificata, è possibile definire un filtro sulla tabella del case, sulla tabella nidificata o su entrambe. In questo esempio vengono combinati un filtro di case e un filtro di riga nidificata per limitare i case ai clienti europei abbienti che hanno acquistato uno dei modelli di pneumatici Road.  
  
```  
ALTER MINING STRUCTURE [Market Basket with Region and Income]  
ADD MINING MODEL [Decision Trees]  
(  
    CustomerKey,   
    Region,  
    [Income Group],  
    [Product] PREDICT (Model)   
WITH FILTER (EXISTS (SELECT * FROM [v Assoc Seq Line Items] WHERE   
 [Model] = 'HL Road Tire' OR  
 [Model] = 'LL Road Tire' OR  
 [Model] = 'ML Road Tire' )  
)  
) WITH FILTER ([Income Group] = 'High' AND [Region] = 'Europe')  
USING Microsoft_Decision Trees  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di definizione dei dati](../dmx/dmx-statements-data-definition.md)   
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
