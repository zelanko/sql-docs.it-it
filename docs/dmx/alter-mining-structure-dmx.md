---
title: MODIFICARE LA STRUTTURA DI DATA MINING (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 487fb5c04d623f2a4ef408cf35784dd57b067f4f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913843"
---
# <a name="alter-mining-structure-dmx"></a>ALTER MINING STRUCTURE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Crea un nuovo modello di data mining basato su una struttura di data mining esistente.  Quando si usa la **ALTER MINING STRUCTURE** istruzione per creare un nuovo modello di data mining, la struttura deve esistere già. Al contrario, quando si usa l'istruzione [CREATE MINING MODEL &#40;DMX&#41;](../dmx/create-mining-model-dmx.md), si crea un modello e di generare automaticamente la struttura di data mining sottostante nello stesso momento.  
  
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
  
 *elenco di definizioni di colonna*  
 Elenco delimitato da virgole contenente le definizioni delle colonne.  
  
 *elenco di definizioni di colonne nidificati*  
 Elenco delimitato da virgole delle colonne di una tabella nidificata, se applicabile.  
  
 *criteri di filtro annidati*  
 Espressione di filtro applicata alle colonne di una tabella nidificata.  
  
 *algorithm*  
 Nome di un algoritmo di data mining, definito dal provider.  
  
> [!NOTE]  
>  Un elenco degli algoritmi supportati dal provider corrente può essere recuperato tramite [set di righe DMSCHEMA_MINING_SERVICES](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset). Per visualizzare gli algoritmi supportati nell'istanza corrente di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], vedere [proprietà di Data Mining](../analysis-services/server-properties/data-mining-properties.md).  
  
 *elenco di parametri*  
 facoltativo. Elenco delimitato da virgole dei parametri definiti dal provider per l'algoritmo.  
  
 *criteri di filtro*  
 Espressione di filtro applicata alle colonne della tabella del case.  
  
## <a name="remarks"></a>Note  
 Se la struttura di data mining contiene chiavi composte, il modello di data mining dovrà includere tutte le colonne chiave definite nella struttura.  
  
 Se il modello non richiede una colonna stimabile, come ad esempio i modelli compilati utilizzando gli algoritmi [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering e [!INCLUDE[msCoName](../includes/msconame-md.md)] Sequence Clustering, non sarà necessario includere una definizione di colonna nell'istruzione. Tutti gli attributi nel modello risultante verranno gestiti come input.  
  
 Nel **WITH** clausola che si applica alla tabella del case, è possibile specificare opzioni per il filtro e il drill-through:  
  
-   Aggiungere il **filtro** (parola chiave) e una condizione di filtro. Il filtro si applica ai case nel modello di data mining.  
  
-   Aggiungere il **drill-through** parola chiave per consentire agli utenti del modello di data mining di eseguire il drill-dai risultati del modello per i dati del case. In DMX (Data Mining Extensions) è possibile abilitare il drill-through solo al momento della creazione del modello.  
  
 Per usare case sia il filtro drill-through, si combinano le parole chiave in un unico **WITH** clausola usando la sintassi illustrata nell'esempio seguente:  
  
 `WITH DRILLTHROUGH, FILTER(Gender = 'Male')`  
  
## <a name="column-definition-list"></a>Elenco delle definizioni di colonna  
 Per definire la struttura di un modello, specificare un elenco delle definizioni di colonna che include le informazioni seguenti per ogni colonna:  
  
-   Nome (obbligatorio)  
  
-   Alias (facoltativo)  
  
-   Flag di modellazione  
  
-   Richiesta di stima, che indica all'algoritmo se la colonna contiene un valore stimabile, indicato dal **PREDICT** oppure **PREDICT_ONLY** clausola  
  
 Per definire una singola colonna, utilizzare la sintassi seguente nell'elenco delle definizioni di colonna:  
  
```  
<structure column name>  [AS <model column name>]  [<modeling flags>]    [<prediction>]  
```  
  
### <a name="column-name-and-alias"></a>Nome e alias di colonna  
 Il nome di colonna utilizzato nell'elenco delle definizioni di colonna deve essere il nome della colonna così come viene utilizzato nella struttura di data mining. Tuttavia, è anche possibile definire un alias per rappresentare la colonna della struttura nel modello di data mining. È inoltre possibile creare più definizioni di colonna per la stessa colonna della struttura e assegnare un alias e un utilizzo di stima diversi a ogni copia della colonna. Per impostazione predefinita, il nome della colonna della struttura viene utilizzato se non viene definito un alias. Per altre informazioni, vedere [creare un Alias per una colonna del modello](../analysis-services/data-mining/create-an-alias-for-a-model-column.md).  
  
 Per le colonne della tabella nidificata, specificare il nome della tabella nidificata, specificare il tipo di dati **tabella**e quindi specificare l'elenco delle colonne nidificate da includere nel modello, racchiuso tra parentesi.  
  
 È possibile definire un'espressione di filtro che viene applicata alla tabella nidificata aggiungendo un'espressione di criteri di filtro dopo la definizione di colonna della tabella nidificata.  
  
### <a name="modeling-flags"></a>Flag di modellazione  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] supporta i flag di modellazione seguenti per l'utilizzo nelle colonne del modello di data mining:  
  
> [!NOTE]  
>  Il flag di modellazione NOT_NULL si applica alla colonna della struttura di data mining. Per altre informazioni, vedere [CREATE MINING STRUCTURE &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md).  
  
|||  
|-|-|  
|Nome|Definizione|  
|**REGRESSOR**|Indica che l'algoritmo può utilizzare la colonna specificata nella formula di regressione degli algoritmi di regressione.|  
|**MODEL_EXISTENCE_ONLY**|Indica che i valori per la colonna di attributi sono meno importanti rispetto alla presenza dell'attributo.|  
  
 È invece possibile definire più flag di modellazione per una stessa colonna. Per altre informazioni su come usare i flag di modellazione, vedere [flag di modellazione &#40;DMX&#41;](../dmx/modeling-flags-dmx.md).  
  
### <a name="prediction-clause"></a>Clausola di stima  
 La clausola di stima consente di descrivere la modalità di utilizzo della colonna di stima. Nella tabella seguente sono elencate le clausole possibili.  
  
|||  
|-|-|  
|**PREDICT**|Questa colonna può essere stimata dal modello e i relativi valori possono essere utilizzati come input per stimare il valore di altre colonne stimabili.|  
|**PREDICT_ONLY**|Questa colonna può essere stimata dal modello, ma i relativi valori non possono essere utilizzati nei case di input per stimare il valore di altre colonne stimabili.|  
  
## <a name="filter-criteria-expressions"></a>Espressioni di criteri di filtro  
 È possibile definire un filtro per limitare i case utilizzati nel modello di data mining. Il filtro può essere applicato alle colonne nella tabella del case, alle righe nella tabella nidificata o a entrambe.  
  
 Le espressioni di criteri di filtro sono predicati DMX semplificati, simili a una clausola WHERE. Le espressioni di filtro sono limitate a formule che utilizzano operatori matematici di base, valori scalari e nomi di colonna. L'operatore EXISTS, che restituisce true se per la sottoquery viene restituita almeno una riga, rappresenta un'eccezione. I predicati possono essere combinati utilizzando gli operatori logici comuni: AND, OR e non.  
  
 Per altre informazioni sui filtri utilizzati con modelli di data mining, vedere [filtri per i modelli di Data Mining &#40;Analysis Services - Data Mining&#41;](../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  Le colonne di un filtro devono essere colonne della struttura di data mining. Non è possibile creare un filtro su una colonna del modello o una colonna in forma di alias.  
  
 Per altre informazioni sulla sintassi e gli operatori DMX, vedere [colonne del modello di Data Mining](../analysis-services/data-mining/mining-model-columns.md).  
  
## <a name="parameter-definition-list"></a>Elenco delle definizioni di parametro  
 È possibile modificare le prestazioni e le funzionalità di un modello aggiungendo parametri dell'algoritmo all'elenco di parametri. I parametri che è possibile utilizzare variano in base all'algoritmo specificato nella clausola USING. Per un elenco di parametri che sono associati a ogni algoritmo, vedere [algoritmi di Data Mining &#40;Analysis Services - Data Mining&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
 La sintassi dell'elenco dei parametri è la seguente:  
  
```  
[<parameter> = <value>, <parameter> = <value>,...]  
```  
  
## <a name="example-1-add-a-model-to-a-structure"></a>Esempio 1: Aggiungere un modello a una struttura  
 L'esempio seguente aggiunge un modello di data mining Naive Bayes per la **New Mailing** struttura di data mining e i limiti il numero massimo di attributi indica fino a 50.  
  
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
  
## <a name="example-2-add-a-filtered-model-to-a-structure"></a>Esempio 2: Aggiungere un modello filtrato a una struttura  
 L'esempio seguente aggiunge un modello di data mining `Naive Bayes Women`, per il **New Mailing** struttura di data mining. Il nuovo modello presenta la stessa struttura di base del modello di data mining aggiunto nell'esempio 1, ma i case della struttura di data mining sono limitati ai clienti di sesso femminile di età superiore a 50 anni.  
  
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
  
## <a name="example-3-add-a-filtered-model-to-a-structure-with-a-nested-table"></a>Esempio 3: Aggiungere un modello filtrato a una struttura con una tabella nidificata  
 Nell'esempio seguente viene aggiunto un modello di data mining a una versione modificata della struttura di data mining Market Basket. Struttura di data mining usata nell'esempio è stata modificata per aggiungere un **regione** colonna che contiene gli attributi per l'area del cliente, e un **Income Group** colonna che vengono suddivisi in categorie di reddito del cliente usando i valori **elevata**, **moderato**, o **bassa**.  
  
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
 [Le estensioni di Data Mining di dati &#40;DMX&#41; istruzioni di definizione dei dati](../dmx/dmx-statements-data-definition.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
