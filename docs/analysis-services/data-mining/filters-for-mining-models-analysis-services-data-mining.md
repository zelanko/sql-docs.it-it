---
title: Filtri per i modelli di Data Mining (Analysis Services - Data Mining) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 81592abc0224b2898b64d834857d23484750b326
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52410668"
---
# <a name="filters-for-mining-models-analysis-services---data-mining"></a>Filtri per i modelli di data mining (Analysis Services - Data mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  I filtri dei modelli basati sui dati consentono di creare modelli di data mining che utilizzano subset di dati in una struttura di data mining. I filtri garantiscono grande flessibilità per la progettazione di strutture di data mining e origini dati, poiché è possibile creare una sola struttura di data mining sulla base di una vista origine dati completa. Sarà quindi possibile creare filtri per utilizzare solo una parte dei dati per il training e il testing di una varietà di modelli, anziché compilare una struttura diversa e i relativi modelli per ciascun subset di dati.  
  
 Ad esempio, definire la vista origine dati nella tabella Customers e nelle tabelle correlate. Quindi, definire una sola struttura di data mining che include tutti i campi necessari. Infine, creare un modello filtrato su un determinato attributo del cliente, ad esempio la regione. È quindi possibile creare facilmente una copia di quel modello e modificare solo la condizione di filtro per generare un nuovo modello basato su una regione diversa.  
  
 Alcuni scenari reali in cui è possibile trarre vantaggio da questa funzionalità sono i seguenti:  
  
-   Creazione di modelli separati per valori discreti come ad esempio sesso, regione e così via. Ad esempio, un negozio di abbigliamento potrebbe utilizzare le informazioni demografiche sui clienti per compilare modelli separati per sesso, anche se i dati di vendita provengono da una sola origine dati per tutti i clienti.  
  
-   Esperimenti con i modelli tramite la creazione e il testing di più raggruppamenti degli stessi dati, ad esempio età 20-30 rispetto a età 20-40 ed età 20-25.  
  
-   Specifica di filtri complessi su contenuto di tabelle nidificate, ad esempio la richiesta di inclusione di un case nel modello solo se il cliente ha acquistato almeno due unità di un determinato articolo.  
  
 In questa sezione vengono descritti la compilazione, l'utilizzo e la gestione dei filtri sui modelli di data mining.  
  
## <a name="creating-model-filters"></a>Creazione di filtri dei modelli  
 È possibile creare e applicare filtri nei seguenti modi:  
  
-   Usando la scheda **Modelli di data mining** nella Progettazione modelli di data mining per compilare condizioni con l'aiuto delle finestre di dialogo dell'editor filtri.  
  
-   Digitando un'espressione di filtro direttamente nella proprietà **Filter** del modello di data mining.  
  
-   Impostando a livello di codice delle condizioni di filtro in un modello tramite AMO.  
  
### <a name="creating-model-filters-using-data-mining-designer"></a>Creazione di filtri dei modelli utilizzando la Progettazione modelli di data mining  
 Filtrare un modello nella Progettazione modelli di data mining modificando la proprietà **Filter** del modello di data mining. È possibile digitare direttamente un'espressione di filtro nel riquadro **Proprietà** oppure è possibile aprire una finestra di dialogo del filtro per compilare le condizioni.  
  
 Sono disponibili due finestre di dialogo del filtro. La prima consente di creare le condizioni applicate alla tabella del case. Se l'origine dati contiene più tabelle, selezionare in primo luogo una tabella, quindi selezionare una colonna e specificare gli operatori e le condizioni applicabili alla colonna. È possibile collegare più condizioni usando gli operatori **AND**/**OR** . Gli operatori disponibili per la definizione dei valori variano a seconda che la colonna contenga valori discreti o continui. Con i valori continui, ad esempio, è possibile usare gli operatori **maggiore di** e **minore di** . Per i valori discreti, tuttavia, è possibile usare soltanto gli operatori **= (uguale a)**, **!= (non uguale a)** e **is null** .  
  
> [!NOTE]  
>  La parola chiave **LIKE** non è supportata. Se si vuole includere più attributi discreti, è necessario creare condizioni distinte e collegarle usando l'operatore **OR** .  
  
 Se le condizioni sono complesse, è possibile aprire la seconda finestra di dialogo del filtro per utilizzare una tabella alla volta. Quando si chiude la seconda finestra di dialogo del filtro, l'espressione viene valutata e quindi combinata con le condizioni di filtro impostate nelle altre colonne nella tabella del case.  
  
### <a name="creating-filters-on-nested-tables"></a>Creazione di filtri nelle tabelle nidificate  
 Se la vista origine dati contiene tabelle nidificate, è possibile utilizzare la seconda finestra di dialogo del filtro per compilare condizioni sulle righe nelle tabelle nidificate.  
  
 Se, ad esempio, la tabella del case è riferita ai clienti e nella tabella nidificata vengono indicati i prodotti acquistati da un cliente, è possibile creare un filtro per i clienti che hanno acquistato determinati articoli usando la sintassi seguente nel filtro della tabella nidificata: `[ProductName]='Water Bottle' OR ProductName='Water Bottle Cage'`.  
  
 È possibile anche creare un filtro in base all'esistenza di un determinato valore usando la parola chiave **EXISTS** o **NOT EXISTS** e una sottoquery. Questo consente di creare condizioni come `EXISTS (SELECT * FROM Products WHERE ProductName='Water Bottle')`. `EXISTS SELECT(<subquery>)` restituisce **true** se la tabella nidificata contiene almeno una riga che include il valore `Water Bottle`.  
  
 È possibile combinare condizioni nella tabella del case con le condizioni nella tabella nidificata. Ad esempio, nella sintassi seguente è inclusa una condizione nella tabella del case (`Age > 30` ), una sottoquery nella tabella nidificata (`EXISTS (SELECT * FROM Products)`) e più condizioni nella tabella nidificata (`WHERE ProductName='Milk'  AND Quantity>2`)).  
  
```  
(Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName='Milk'  AND Quantity>2) )  
```  
  
 Quando la compilazione del filtro è terminata, il testo del filtro viene valutato da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], tradotto a un'espressione DMX e quindi salvato con il modello.  
  
 Per istruzioni sull'uso delle finestre di dialogo del filtro in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], vedere [Applicare un filtro a un modello di data mining](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md).  
  
## <a name="managing-mining-model-filters"></a>Gestione dei filtri dei modelli di data mining  
 I filtri dei modelli basati sui dati semplificano in modo significativo la gestione delle strutture e dei modelli di data mining, in quanto consentono di creare con facilità più modelli basati sulla stessa struttura. È inoltre possibile creare rapidamente copie di modelli di data mining esistenti e quindi modificare solo la condizione di filtro. Tuttavia, i filtri possono causare confusione.  
  
 Di seguito vengono riportate alcune domande frequenti su come gestire e interpretare i filtri nei modelli di data mining:  
  
### <a name="how-can-i-tell-whether-a-filter-is-being-used"></a>Com'è possibile stabilire se viene utilizzato un filtro?  
 Esistono più modalità per determinare se è stato applicato un filtro a un modello:  
  
-   Nella finestra di progettazione fare clic sulla scheda **Modelli di data mining** , aprire **Proprietà**e visualizzare la proprietà **Filter** del modello di data mining.  
  
-   La DMV, DMSCHEMA_MINING_MODELS, restituisce una colonna che contiene il testo del filtro. È possibile utilizzare la query seguente in una DMV per restituire i nomi di modelli e i relativi filtri:  
  
    ```  
    SELECT MODEL_NAME, [FILTER]   
    FROM $SYSTEM.DMSCHEMA_MINING_MODELS  
  
    ```  
  
-   È possibile ottenere il valore della proprietà Filter dell'oggetto MiningModel in AMO o esaminare l'elemento Filter in XMLA.  
  
 Si potrebbe anche definire una convenzione di denominazione affinché i modelli riflettano il contenuto del filtro. semplificando il riconoscimento di modelli correlati.  
  
### <a name="how-can-i-save-a-filter"></a>Com'è possibile salvare un filtro?  
 L'espressione di filtro viene salvata come script che viene a sua volta archiviato con il modello di data mining o la tabella nidificata associati. Se si elimina il testo del filtro, tale testo può essere ripristinato solo ricreando manualmente l'espressione di filtro. Pertanto, se si creano espressioni di filtro complesse, è necessario creare una copia di backup del testo del filtro.  
  
### <a name="why-cant-i-see-any-effects-from-the-filter"></a>Il motivo per cui non vengono visualizzati tutti gli effetti del filtro?  
 Ogni volta che si modifica o si aggiunge un'espressione di filtro, è necessario rielaborare la struttura e il modello prima che sia possibile visualizzare gli effetti del filtro.  
  
### <a name="why-do-i-see-filtered-attributes-in-prediction-query-results"></a>Perché sono presenti attributi filtrati nei risultati della query di stima?  
 Quando si applica un filtro a un modello, tale operazione interessa solo la selezione di casi utilizzati per il training del modello. Il filtro non influisce sugli attributi noti al modello né modifica o elimina i dati presenti nell'origine dati. Di conseguenza, le query eseguite sul modello possono restituire stime per altri tipi di casi e gli elenchi a discesa di valori utilizzati dal modello potrebbero mostrare valori di attributi esclusi dal filtro.  
  
 Ad esempio, si supponga di eseguire il training del modello [Bike Buyer] utilizzando solo i casi che riguardano donne di età compresa tra 20 e 30 anni. È comunque possibile eseguire una query di stima per definire la probabilità che ha un uomo di acquistare una bicicletta o stimare il risultato per una donna di età compresa tra 30 e 40 anni. Questo si verifica perché gli attributi e i valori presenti nell'origine dati definiscono cosa è teoricamente possibile, mentre i casi definiscono le occorrenze utilizzate per il training. Tuttavia, queste query restituiscono probabilità molto ridotte perché i dati di training non contengono alcun caso con i valori di destinazione.  
  
 Se è necessario nascondere o anonimizzare completamente i valori di attributi nel modello, esistono diverse opzioni:  
  
-   Filtrare i dati in entrata come parte della definizione della vista origine dati o nell'origine dati relazionale.  
  
-   Nascondere o codificare il valore di attributo.  
  
-   Comprimere i valori esclusi in una categoria come parte della definizione della struttura di data mining.  
  
## <a name="related-resources"></a>Risorse correlate  
 Per altre informazioni sulla sintassi dei filtri e per esempi delle espressioni di filtro, vedere [Sintassi ed esempi di filtri dei modelli &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md).  
  
 Per informazioni sull'uso di filtri dei modelli quando si esegue il test di un modello di data mining, vedere [Scegliere un tipo di grafico di accuratezza e impostare le opzioni del grafico](../../analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Sintassi ed esempi di filtri dei modelli &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)   
 [Test e convalida &#40;Data mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  
