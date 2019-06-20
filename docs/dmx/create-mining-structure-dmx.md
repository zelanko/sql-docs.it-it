---
title: CREARE LA STRUTTURA DI DATA MINING (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ea04b08f98385755f006c1a67125a87dc71e41f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62854337"
---
# <a name="create-mining-structure-dmx"></a>CREATE MINING STRUCTURE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Crea una nuova struttura di data mining in un database e facoltativamente definisce le partizioni di training e test. Dopo aver creato la struttura di data mining, è possibile usare la [ALTER MINING STRUCTURE &#40;DMX&#41; ](../dmx/alter-mining-structure-dmx.md) istruzione per aggiungere modelli alla struttura di data mining.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CREATE [SESSION] MINING STRUCTURE <structure>  
(  
    [(<column definition list>)]  
)  
[WITH HOLDOUT (<holdout-specifier> [OR <holdout-specifier>])]  
[REPEATABLE(<holdout seed>)]  
<holdout-specifier>::=  <holdout-maxpercent> PERCENT | <holdout-maxcases> CASES  
```  
  
## <a name="arguments"></a>Argomenti  
 *structure*  
 Nome univoco della struttura.  
  
 *elenco di definizioni di colonna*  
 Elenco delimitato da virgole contenente le definizioni delle colonne.  
  
 *holdout-maxpercent*  
 Valore intero tra 1 e 100 che indica la percentuale di dati accantonata per l'esecuzione di test.  
  
 *holdout-maxcases*  
 Valore intero che indica il numero massimo di case da utilizzare per l'esecuzione di test.  
  
 Se il valore massimo specificato per i case è maggiore del numero dei case di input, tutti i case di input sono utilizzati per l'esecuzione di test e viene generato un avviso.  
  
> [!NOTE]  
>  Se sono specificati entrambi, percentuale e numero massimo di case, viene utilizzato il più piccolo dei due limiti.  
  
 *valore di inizializzazione dei dati di controllo*  
 Valore intero utilizzato come valore di inizializzazione per avviare il partizionamento dei dati.  
  
 Se è impostato su 0, come valore di inizializzazione viene utilizzato l'hash del'ID della struttura di data mining.  
  
> [!NOTE]  
>  Per essere certi che una partizione sia riproducibile, è necessario specificare un valore di inizializzazione.  
  
 Impostazione predefinita: REPEATABLE(0)  
  
## <a name="remarks"></a>Note  
 Per definire una struttura di data mining è necessario specificare un elenco di colonne, specificando facoltativamente le relazioni gerarchiche tra le stesse e partizionando facoltativamente la struttura di data mining in set di dati di training e test.  
  
 La parola chiave SESSION facoltativa indica che si tratta di una struttura temporanea che è possibile utilizzare solo per la durata della sessione corrente. Al termine della sessione, la struttura e gli eventuali modelli basati su di essa verranno eliminati. Per creare modelli e strutture di data mining temporanei, è innanzitutto necessario impostare la proprietà del database AllowSessionMiningModels. Per altre informazioni, vedere [Proprietà di data mining](../analysis-services/server-properties/data-mining-properties.md).  
  
## <a name="column-definition-list"></a>Elenco delle definizioni di colonna  
 Per definire una struttura di data mining, è necessario includere le informazioni seguenti per ogni colonna dell'argomento column definition list:  
  
-   Nome (obbligatorio)  
  
-   Tipo di dati (obbligatorio)  
  
-   Distribuzione  
  
-   Elenco dei flag di modellazione  
  
-   Tipo di contenuto (obbligatorio)  
  
-   Relazione con una colonna attributo (obbligatoria solo se applicabile), indicata dalla clausola RELATED TO.  
  
 Per definire una singola colonna, utilizzare la sintassi seguente nell'elenco delle definizioni di colonna:  
  
```  
<column name>    <data type>    [<Distribution>]    [<Modeling Flags>]    <Content Type>    [<column relationship>]  
```  
  
 Per definire una colonna di tabella nidificata utilizzare la sintassi seguente nell'elenco delle definizioni di colonna:  
  
```  
<column name>    TABLE    ( <column definition list> )  
```  
  
 Per un elenco dei tipi di dati, dei tipi di contenuto, delle distribuzioni di colonna e dei flag di modellazione che è possibile utilizzare per definire le colonne di una struttura, vedere gli argomenti seguenti:  
  
-   [Tipi di dati &#40;Data mining&#41;](../analysis-services/data-mining/data-types-data-mining.md)  
  
-   [Tipi di contenuto &#40;Data mining&#41;](../analysis-services/data-mining/content-types-data-mining.md)  
  
-   [Distribuzioni delle colonne &#40;Data mining&#41;](../analysis-services/data-mining/column-distributions-data-mining.md)  
  
-   [Flag di modellazione &#40;data mining&#41;](../analysis-services/data-mining/modeling-flags-data-mining.md)  
  
 È possibile definire più valori dei flag di modellazione per una colonna. Tuttavia, è possibile disporre solo di un tipo di contenuto e di un tipo di dati per colonna.  
  
### <a name="column-relationships"></a>Relazioni tra colonne  
 Per descrivere la relazione tra due colonne, è possibile aggiungere una clausola a qualsiasi istruzione per la definizione di colonna. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] supporta l'utilizzo delle opzioni seguenti \<relazione a colonna > clausola.  
  
 **CORRELATI A**  
 Indica una gerarchia di valori. La destinazione di una colonna con clausola RELATED TO può essere una colonna chiave in una tabella nidificata, una colonna con valori discreti nella riga dei case oppure un'altra colonna con una clausola RELATED TO, che indica una gerarchia con più livelli.  
  
## <a name="holdout-parameters"></a>Parametri di controllo  
 Quando si specificano parametri di controllo, viene creata una partizione dei dati della struttura. La quantità specificata per il controllo è riservata per l'esecuzione di test, mentre i dati rimanenti sono utilizzati per il training. Se si crea una struttura di data mining utilizzando [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], per impostazione predefinita viene creata automaticamente una partizione di controllo contenente il 30% di dati per l'esecuzione di test e il 70% di dati di training. Per altre informazioni, vedere [Training and Testing Data Sets](../analysis-services/data-mining/training-and-testing-data-sets.md).  
  
 Se si crea una struttura di data mining mediante DMX (Data Mining Extensions), è necessario specificare manualmente che è stata creata una partizione di controllo.  
  
> [!NOTE]  
>  Il **ALTER MINING STRUCTURE** istruzione non supporta i dati di controllo.  
  
 È possibile specificare fino a tre parametri di controllo. Se si specifica sia un numero massimo di case di controllo sia una percentuale di controllo, viene riservata una percentuale di case fino al raggiungimento del limite massimo dei case. Specificare la percentuale di dati di controllo come valore intero seguito dal **percento** parola chiave e specificare il numero massimo di case come valore intero seguito dal **casi** (parola chiave). È possibile combinare le condizioni in qualsiasi ordine, come mostrato negli esempi seguenti:  
  
```  
WITH HOLDOUT (20 PERCENT)   
WITH HOLDOUT (2000 CASES)   
WITH HOLDOUT (20 PERCENT OR 2000 CASES)   
WITH HOLDOUT (2000 CASES OR 20 PERCENT)  
```  
  
 Il valore di inizializzazione di controllo controlla il punto iniziale del processo di assegnazione casuale dei case ai set di dati di training o test. Impostando un valore di inizializzazione di controllo, è possibile garantire che la partizione possa essere ripetuta. Se non viene specificato un valore di inizializzazione di controllo, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utilizza il nome della struttura di data mining per creare un valore di inizializzazione. Se si modifica il nome della struttura, il valore di inizializzazione cambierà. È possibile utilizzare il parametro del valore di inizializzazione di controllo con uno o entrambi gli altri parametri di controllo.  
  
> [!NOTE]  
>  Poiché le informazioni di partizione viene memorizzato nella cache con i dati di training, per utilizzare il controllo, è necessario assicurarsi che il **CacheMode** della struttura di data mining è impostata su **KeepTrainingData**. Si tratta dell'impostazione predefinita in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] per le strutture di data mining nuove. Modifica il **CacheMode** proprietà **ClearTrainingCases** su una struttura di data mining esistente che contiene un controllo partizione non influirà su qualsiasi modello di data mining è stati elaborati. Tuttavia, se <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> non è impostata su **KeepTrainingData**, parametri di controllo non ha alcun effetto. Ciò significa che tutti i dati di origine saranno utilizzati per il training e non sarà disponibile alcun set di test. La definizione della partizione è memorizzata nella cache con la struttura; se si cancella la cache dei case di training, verrà cancellata anche la cache dei dati di test e la definizione del controllo impostato.  
  
## <a name="examples"></a>Esempi  
 Negli esempi seguenti viene illustrato come creare una struttura di data mining con controllo mediante DMX.  
  
### <a name="example-1-adding-a-structure-with-no-training-set"></a>Esempio 1: Aggiunta di una struttura con alcun Set di Training  
 Nell'esempio seguente viene creata una nuova struttura di data mining denominata `New Mailing` senza creare alcun modello di data mining associato e senza utilizzare alcun controllo. Per informazioni su come aggiungere un modello di data mining alla struttura, vedere [ALTER MINING STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md).  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)  
```  
  
### <a name="example-2-specifying-holdout-percentage-and-seed"></a>Esempio 2: Valore di inizializzazione e specificando la percentuale di controllo  
 È possibile aggiungere la clausola seguente dopo l'elenco di definizioni di colonna per definire un set di dati da utilizzare per il test di tutti i modelli di data mining associati alla struttura di data mining. Con l'istruzione viene creato un set di test che corrisponde al 25% dei case di input totali, senza alcun limite nel numero massimo di case. Come valore di inizializzazione per la creazione della partizione è utilizzato 5000. Se si specifica un valore di inizializzazione, verranno scelti gli stessi case per il set di test ogni volta che la struttura di data mining viene elaborata, purché i dati sottostanti non cambino.  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)   
WITH HOLDOUT(25 PERCENT) REPEATABLE(5000)  
```  
  
### <a name="example-3-specifying-holdout-percentage-and-max-cases"></a>Esempio 3: Specifica di controllo percentuale e numero massimo di case  
 La clausola seguente consente di creare un set di test che corrisponde al 25% dei case di input totali o a 2000 case, a seconda del valore minore. Poiché come valore di inizializzazione è specificato 0, il nome della struttura di data mining è utilizzato per creare il valore di inizializzazione utilizzato per avviare il campionamento dei case di input.  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)   
WITH HOLDOUT(25 PERCENT OR 2000 CASES) REPEATABLE(0)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Le estensioni di Data Mining di dati &#40;DMX&#41; istruzioni di definizione dei dati](../dmx/dmx-statements-data-definition.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
