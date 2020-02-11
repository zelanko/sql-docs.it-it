---
title: Set di dati di training e di testing | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- testing mining models
- holdout [data mining]
- testing data mining models
- accuracy testing [data mining]
ms.assetid: 5798fa48-ef3c-4e97-a17c-38274970fccd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 34aefc2895057c499e54c572340ca63dc28ed68f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66082741"
---
# <a name="training-and-testing-data-sets"></a>Set di dati di training e di testing
  La separazione dei dati in set di training e set di testing rappresenta una parte importante della valutazione dei modelli di data mining. In genere, quando si separa un set di dati in un set di training e un set di testing, la maggior parte dei dati viene utilizzata per il training e una parte più piccola per il testing. 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esegue un campionamento casuale dei dati per assicurare che i set di testing e i training set siano simili. Utilizzando dati simili per il training e il testing, è possibile ridurre al minimo gli effetti delle discrepanze di dati e comprendere meglio le caratteristiche del modello.  
  
 Dopo aver elaborato il modello tramite il set di training, il modello viene testato eseguendo stime sul set di test. Poiché nei dati nel set di testing sono contenuti già valori noti per l'attributo di cui si desidera eseguire la stima, la correttezza delle ipotesi del modello può essere determinata facilmente.  
  
## <a name="creating-test-and-training-sets-for-data-mining-structures"></a>Creazione di set di testing e di training per strutture di data mining  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]il set di dati originale viene separato al livello della struttura di data mining. Le informazioni sulle dimensioni dei training set e set di dati di test e su quale riga appartiene a un set vengono archiviate con la struttura, e tutti i modelli basati su tale struttura possono utilizzare i set di training e di testing.  
  
 È possibile definire un set di dati di testing in una struttura di data mining nelle modalità seguenti:  
  
-   Utilizzando la Creazione guidata modello di data mining per dividere la struttura di data mining durante la relativa creazione.  
  
-   Modificando le proprietà della struttura nella scheda **Struttura di data mining** di Progettazione modelli di data mining.  
  
-   Creando e modificando a livello di codice le strutture utilizzando librerie AMO (Analysis Management Objects) o XML DDL (Data Definition Language).  
  
### <a name="using-the-data-mining-wizard-to-divide-a-mining-structure"></a>Utilizzo della Creazione guidata modelli di data mining per dividere una struttura di data mining  
 Per impostazione predefinita, dopo aver definito le origini dati per una struttura di data mining, mediante la Creazione guidata modelli di data mining i dati verranno divisi in due set: uno contenente il 70% e un altro il 30% dei dati di origine, rispettivamente per il training e il testing del modello. Questa impostazione predefinita è stata scelta in quanto un rapporto 70-30 viene spesso usato nel data mining, ma con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è possibile modificarlo secondo le proprie necessità.  
  
 È anche possibile configurare la procedura guidata per impostare un numero massimo di case di training oppure combinare i limiti per consentire una percentuale massima di case che rappresenti un numero massimo di case specificato. Quando si specifica sia una percentuale massima che un numero massimo di case, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizza il più piccolo dei due limiti come dimensione del set di test. Ad esempio, se si specifica il 30% di controllo per i case del testing e 1000 come numero massimo di test case, la dimensione del set di test non supererà mai i 1000 case. Questa condizione può essere utile se si desidera assicurare che le dimensioni del set di test rimangano coerenti anche se vengono aggiunti ulteriori dati di training al modello.  
  
 Se si utilizza la stessa vista origine dati per strutture di data mining diverse e si desidera assicurare che i dati vengano divisi approssimativamente nello stesso modo per tutte le strutture di data mining e i relativi modelli, è necessario specificare il valore di inizializzazione utilizzato per inizializzare il campionamento casuale. Quando si specifica un valore per `HoldoutSeed`, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizzerà quel valore per iniziare il campionamento. In caso contrario, per creare il valore di inizializzazione viene utilizzato un algoritmo di hash sul nome della struttura di data mining.  
  
> [!NOTE]  
>  Se si crea una copia della struttura di data mining utilizzando le istruzioni `EXPORT` e `IMPORT`, la nuova struttura di data mining avrà gli stessi training set e set di dati di test, in quanto mediante il processo di esportazione viene creato un nuovo ID, ma viene utilizzato lo stesso nome. Tuttavia, se in due strutture di data mining viene utilizzata la stessa origine dati sottostante ma tali strutture hanno nomi diversi, i set creati per ogni struttura di data mining saranno diversi.  
  
### <a name="modifying-structure-properties-to-create-a-test-data-set"></a>Modifica delle proprietà di una struttura per creare un set di dati di test  
 Se si crea ed elabora una struttura di data mining, e in un secondo momento si desidera riservare un set di dati di test, è possibile modificare le proprietà della struttura di data mining. Per modificare la modalità di partizionamento dei dati, modificare le proprietà seguenti:  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|`HoldoutMaxCases`|Specifica il numero massimo di case da includere nel set di testing.|  
|`HoldoutMaxPercent`|Specifica il numero di case da includere nel set di testing come percentuale del set di dati completo. Se non sono presenti set di dati, specificare 0.|  
|`HoldoutSeed`|Specifica un valore intero da utilizzare come valore di inizializzazione quando si selezionano in modo casuale i dati per le partizioni. Questo valore non influisce sul numero di case nel set di training. Invece, assicura che la partizione possa essere ripetuta.|  
  
 Se si aggiunge o modifica un set di dati di test in una struttura esistente, è necessario rielaborare la struttura e tutti i modelli associati. Inoltre, poiché la divisione dei dati di origine causa l'esecuzione del training del modello in un subset di dati differente, si possono ottenere risultati diversi dal modello.  
  
### <a name="specifying-holdout-programmatically"></a>Specifica a livello di codice dei dati di controllo  
 È possibile definire training set e set di dati di testing in una struttura di data mining tramite istruzioni DMX, AMO o XML DDL. L'istruzione ALTER MINING STRUCTURE non supporta l'utilizzo di parametri di controllo.  
  
-   **DMX** nel linguaggio DMX (Data Mining Extensions), l'istruzione CREATE MINING STRUCTURE è stata estesa per includere una clausola with di dati di attesa.  
  
-   **ASSL** È possibile creare una nuova struttura di data mining o aggiungere un set di dati di testing a una struttura di data mining [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esistente utilizzando il linguaggio ASSL (Scripting Language).  
  
-   **Amo** È anche possibile visualizzare e modificare i set di dati di dati di dati di dati di dati di dati di Data Analysis  
  
 È possibile visualizzare informazioni sul set di dati di controllo in una struttura di data mining esistente eseguendo query sul set di righe dello schema di data mining. A tale scopo, effettuare una chiamata a DISCOVER ROWSET o utilizzare una query DMX.  
  
## <a name="retrieving-information-about-holdout-data"></a>Recupero delle informazioni sui dati di controllo  
 Tutte le informazioni sui training set e set di dati di test vengono memorizzati per impostazione predefinita nella cache per consentire l'utilizzo dei dati esistenti per il training e il test di nuovi modelli. È anche possibile definire i filtri da applicare ai dati di controllo memorizzati nella cache, in modo da poter valutare il modello in subset di dati.  
  
 La suddivisione dei case in training set e set di dati di test dipende dalla modalità di configurazione dei dati di controllo e dai dati forniti. Se si desidera determinare il numero dei case utilizzato per il training o per il testing o se si desidera trovare dettagli aggiuntivi sui case inclusi nei set di training e di test, è possibile eseguire una query sulla struttura del modello creando una query DMX. Ad esempio, nella query seguente vengono restituiti i case utilizzati nel set di training del modello.  
  
```  
SELECT * from <structure>.CASES WHERE IsTrainingCase()  
```  
  
 Per recuperare solo i test case e quindi filtrarli in una delle colonne nella struttura di data mining, utilizzare la sintassi seguente:  
  
```  
SELECT * from <structure>.CASES WHERE IsTestCase() AND <structure column name> = '<value>'  
```  
  
## <a name="limitations-on-the-use-of-holdout-data"></a>Limitazioni sull'utilizzo dei dati di controllo  
  
-   Per utilizzare i dati di controllo, è necessario impostare la proprietà <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> della struttura di data mining sul valore predefinito, `KeepTrainingCases`. Se si imposta la proprietà `CacheMode` su `ClearAfterProcessing` e si elabora quindi la struttura di data mining, la partizione andrà persa.  
  
-   Non è possibile rimuovere dati da un modello Time Series; pertanto, non è possibile separare i dati di origine in set di training e di testing. Se si comincia a creare una struttura di data mining e un modello e si sceglie l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series, l'opzione per creare un set di dati di controllo viene disabilitata. Viene inoltre disabilitato l'utilizzo dei dati di controllo se nella struttura di data mining è contenuta una colonna KEY TIME al livello del case o della tabella nidificata.  
  
-   È possibile configurare inavvertitamente il set di dati di controllo in modo che venga utilizzato l'intero set di dati per il testing senza lasciare alcun dato per il training. Tuttavia, in tal caso, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verrà generato un errore in modo che sia possibile correggere il problema. 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Inoltre, viene generato un avviso quando la struttura viene elaborata se più del 50% dei dati viene controllato per il testing.  
  
-   Nella maggior parte dei casi, il valore di controllo predefinito di 30 fornisce un buon bilanciamento tra dati di training e dati di testing. Non esiste un modo semplice per determinare le dimensioni del set di dati al fine di garantire un training sufficiente o il livello di supporto del tipo sparse da parte del set di training per evitare l'overfitting. Dopo aver compilato un modello, è tuttavia possibile utilizzare la convalida incrociata per stimare il set di dati rispetto a un determinato modello.  
  
-   Oltre alle proprietà elencate nella tabella precedente, in AMO e XML DDL viene fornita una proprietà di sola lettura, `HoldoutActualSize`. Tuttavia, poiché la dimensione effettiva di una partizione non può essere determinata accuratamente finché non viene elaborata la struttura, è necessario controllare se il modello è stato elaborato prima di recuperare il valore della proprietà `HoldoutActualSize`.  
  
## <a name="related-content"></a>Contenuto correlato  
  
|Argomenti|Collegamenti|  
|------------|-----------|  
|Viene descritto come i filtri in un modello interagiscono con i training set e set di dati di test.|[Filtri per i modelli di data mining &#40;Analysis Services-&#41;di data mining](mining-models-analysis-services-data-mining.md)|  
|Viene descritto come l'utilizzo dei dati di training e di testing influiscono sulla convalida incrociata.|[Convalida incrociata &#40;Analysis Services-&#41;di data mining](cross-validation-analysis-services-data-mining.md)|  
|Vengono fornite informazioni sulle interfacce di programmazione per l'utilizzo di training set e set di testing in una struttura di data mining.|[Modello a oggetti AMO e concetti relativi](https://docs.microsoft.com/bi-reference/amo/amo-concepts-and-object-model)<br /><br /> [Elemento MiningStructure &#40;&#41;ASSL](https://docs.microsoft.com/bi-reference/assl/objects/miningstructure-element-assl)|  
|Viene fornita la sintassi DMX per la creazione di set di dati di controllo.|[CREA STRUTTURA DI DATA MINING &#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx)|  
|Vengono recuperate informazioni sui case nei set di training e di testing.|[Set di righe dello schema di data mining](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)<br /><br /> [Esecuzione di query sui set di righe dello schema di data mining &#40;Analysis Services-Data mining&#41;](data-mining-schema-rowsets-ssas.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti di data mining](data-mining-tools.md)   
 [Concetti relativi al data mining](data-mining-concepts.md)   
 [Soluzioni di data mining](data-mining-solutions.md)   
 [Test e convalida &#40;&#41;di data mining](testing-and-validation-data-mining.md)  
  
  
