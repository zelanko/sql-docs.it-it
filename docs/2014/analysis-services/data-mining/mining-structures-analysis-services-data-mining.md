---
title: Strutture di data mining (Analysis Services - Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [data mining]
- mining structures [Analysis Services], about mining structures
- mining structures [Analysis Services]
- data mining [Analysis Services], structure
- Analysis Services objects, data mining objects
- data mining [Analysis Services], models
- algorithms [data mining]
- data mining [Analysis Services], objects
- mining models [Analysis Services]
- mining models [Analysis Services], about data mining models
ms.assetid: 39748290-c32a-48e6-92a6-0c3a9223773a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5b370c8f3fb3c8a672f832c13ba89381f475733f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62733341"
---
# <a name="mining-structures-analysis-services---data-mining"></a>Strutture di data mining (Analysis Services – Data mining)
  La struttura di data mining definisce i dati in base ai quali vengono compilati i modelli di data mining: specifica la vista dell'origine dati, il numero e il tipo di colonne e una partizione facoltativa in set di training e di testing. Una singola struttura di data mining può supportare più modelli di data mining che condividono lo stesso dominio. Nel diagramma seguente viene illustrata la relazione della struttura di data mining con l'origine dati e con i modelli di data mining che la compongono.  
  
 ![L'elaborazione dei dati: origine-struttura al modello](../media/dmcon-modelarch.gif "l'elaborazione dei dati: origine-struttura al modello")  
  
 La struttura di data mining nel diagramma è basata su un'origine dati che contiene più tabelle o viste, unite in join nel campo CustomerID. Una tabella contiene informazioni sui clienti, ad esempio l'area geografica, l'età, il reddito e il sesso, mentre la tabella nidificata correlata contiene più righe di informazioni aggiuntive su ogni cliente, ad esempio i prodotti che il cliente ha acquistato. Nel diagramma viene evidenziato che è possibile compilare più modelli in una struttura di data mining e che i modelli possono utilizzare colonne diverse della struttura.  
  
 **Modello 1** Vengono utilizzati CustomerID, Income, Age, Region e filtrati i dati in base a Region.  
  
 **Modello 2** Vengono utilizzati CustomerID, Income, Age, Region e filtrati i dati in base ad Age.  
  
 **Modello 3** Vengono utilizzati CustomerID, Age, Gender e la tabella nidificata, senza filtro.  
  
 Poiché i modelli utilizzano colonne diverse per l'input e poiché due dei modelli limitano ulteriormente i dati utilizzati nel modello applicando un filtro, i modelli potrebbero produrre risultati molto diversi anche se basati sugli stessi dati. Si noti che la colonna CustomerID è obbligatoria in tutti i modelli poiché è l'unica colonna disponibile che può essere utilizzata come chiave del case.  
  
 In questa sezione viene illustrata l'architettura di base di strutture di data mining, ovvero come definire una struttura di data mining, come popolarla con i dati, nonché come utilizzarla per la creazione di modelli. Per altre informazioni su come gestire o esportare strutture di data mining esistenti, vedere [Gestione degli oggetti e delle soluzioni di data mining](management-of-data-mining-solutions-and-objects.md).  
  
## <a name="defining-a-mining-structure"></a>Definizione di una struttura di data mining  
 Per configurare una struttura di data mining effettuare i passaggi seguenti:  
  
-   Definire un'origine dati.  
  
-   Selezionare le colonne di dati da includere nella struttura (non tutte le colonne devono essere aggiunte al modello) e definire una chiave.  
  
-   Definire una chiave per la struttura, includendo la chiave per la tabella nidificata, se applicabile.  
  
-   Specificare se i dati di origine devono essere separati in un set di training e uno di testing. Questo passaggio è facoltativo.  
  
-   Elaborare la struttura.  
  
 Questi passaggi vengono descritti in modo più dettagliato nelle sezioni seguenti.  
  
### <a name="data-sources-for-mining-structures"></a>Origini dati per le strutture di data mining  
 Quando si definisce una struttura di data mining, si utilizzano colonne disponibili in una vista origine dati esistente. Una vista origine dati è un oggetto condiviso che consente di combinare più origini dati e di utilizzarle come un'unica origine. Le origini dati originali non sono visibili nelle applicazioni client; inoltre è possibile utilizzare le proprietà della vista origine dati per modificare i tipi di dati, creare le aggregazioni o le colonne alias.  
  
 Se si compilano più modelli di data mining dalla stessa struttura di data mining, nei modelli possono essere utilizzate colonne diverse della struttura. È possibile, ad esempio, creare una singola struttura, quindi compilare modelli di albero delle decisioni e di clustering separati a partire da essa, ognuno contenente colonne diverse e utilizzato per stimare attributi diversi.  
  
 Inoltre, in ogni modello le colonne della struttura possono essere utilizzate in modi diversi. Ad esempio, nella vista origine dati potrebbe essere contenuta una colonna relativa al reddito che può essere suddivisa in modi diversi per modelli differenti.  
  
 La struttura di data mining consente di archiviare la definizione dell'origine dati e le relative colonne sotto forma di *associazioni* all'origine dati. Per altre informazioni sulle associazioni alle origini dati, vedere [Origini dati e associazioni &#40;SSAS - multidimensionale&#41;](../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md). Tenere presente, tuttavia, che è anche possibile creare una struttura di data mining senza associarla a un'origine dati specifica tramite l'istruzione DMX [CREATE MINING STRUCTURE &#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx).  
  
### <a name="mining-structure-columns"></a>Colonne della struttura di data mining  
 Gli elementi di compilazione della struttura di data mining sono le relative colonne, che descrivono le informazioni contenute nell'origine dei dati. Tali colonne includono informazioni quali il tipo di dati, il tipo di contenuto e la modalità di distribuzione dei dati. La struttura di data mining non contiene informazioni sulla modalità di utilizzo delle colonne per un modello di data mining specifico o sul tipo di algoritmo utilizzato per compilare un modello. Tali informazioni vengono definite nel modello stesso.  
  
 Una struttura di data mining può contenere anche tabelle nidificate. Una tabella nidificata rappresenta una relazione uno-a-molti tra l'entità di un case e gli attributi correlati. Ad esempio, se le informazioni che descrivono i clienti sono contenute in una tabella mentre quelle relative agli acquisti dei clienti sono contenute in un'altra tabella, è possibile utilizzare le tabelle nidificate per combinare le informazioni in un singolo case. L'identificatore del cliente è l'entità, mentre gli acquisti sono gli attributi correlati. Per altre informazioni su quando usare le tabelle annidate, vedere [Tabelle annidate &#40;Analysis Services - Data mining&#41;](nested-tables-analysis-services-data-mining.md).  
  
 Per creare un modello di data mining in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], è necessario prima creare una struttura di data mining. La Creazione guidata modello di data mining guida l'utente attraverso il processo di creazione di una struttura di data mining, di scelta dei dati e di aggiunta di un modello di data mining.  
  
 Se si crea un modello di data mining tramite DMX (Data Mining Extensions), è possibile specificare il modello e le colonne in esso contenute in modo che DMX consenta di creare automaticamente la struttura di data mining necessaria. Per altre informazioni, vedere [CREATE MINING MODEL &#40;DMX&#41;](/sql/dmx/create-mining-model-dmx).  
  
 Per altre informazioni, vedere [Mining Structure Columns](mining-structure-columns.md).  
  
### <a name="dividing-the-data-into-training-and-testing-sets"></a>Suddivisione dei dati in set di training e di testing  
 Quando si definiscono i dati per la struttura di data mining, è anche possibile specificare che alcuni dei dati vengano utilizzati per il training e altri per il testing. Pertanto, non è più necessario suddividere i dati prima di creare una struttura di data mining. Invece, quando si crea il modello, è possibile specificare che una certa percentuale dei dati venga isolata per il testing e che il resto venga utilizzato per il training, oppure è possibile specificare un certo numero di case da utilizzare come set di dati di test. Le informazioni sui set di dati di training e testing vengono memorizzate nella cache con la struttura di data mining, pertanto è possibile utilizzare lo stesso set di test per tutti i modelli basati su tale struttura.  
  
 Per altre informazioni, vedere [Training and Testing Data Sets](training-and-testing-data-sets.md).  
  
### <a name="enabling-drillthrough"></a>Attivazione del drill-through  
 È possibile aggiungere colonne alla struttura di data mining anche se non si intende utilizzare la colonna in un modello di data mining specifico. Ciò si rivela utile se, ad esempio, si desidera recuperare gli indirizzi di posta elettronica dei clienti in un modello di clustering, senza utilizzare l'indirizzo di posta elettronica durante il processo di analisi. Per ignorare una colonna durante l'analisi e la fase di stima, è possibile aggiungerla alla struttura senza specificare un utilizzo per la colonna o impostare il flag di utilizzo su Ignora. I dati contrassegnati in questo modo possono comunque essere utilizzati nelle query se il drill-through è stato abilitato nel modello di data mining e se si dispone delle autorizzazioni necessarie. Ad esempio, è possibile verificare i cluster derivanti dall'analisi di tutti i clienti e, successivamente, utilizzare una query drill-through per ottenere i nomi e gli indirizzi di posta elettronica dei clienti di un cluster particolare, anche se tali colonne di dati non sono state utilizzate per compilare il modello.  
  
 Per altre informazioni, vedere [Query drill-through &#40;Data mining&#41;](drillthrough-queries-data-mining.md).  
  
### <a name="processing-mining-structures"></a>Elaborazione di strutture di data mining  
 Fino a quando non viene elaborata, una struttura di data mining è soltanto un contenitore di metadati. Quando si elabora una struttura di data mining, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene creata una cache locale per l'archiviazione delle statistiche relative ai dati, delle informazioni sul modo in cui vengono discretizzati gli eventuali attributi continui e di altre informazioni che verranno utilizzate successivamente dai modelli di data mining. Il modello di data mining non consente di archiviare queste informazioni di riepilogo, tuttavia permette di fare riferimento alle informazioni memorizzate nella cache quando è stata elaborata la struttura di data mining. Pertanto, non è necessario rielaborare la struttura ogni volta che si aggiunge un nuovo modello a una struttura esistente, bensì è sufficiente elaborare solo il modello.  
  
 È possibile scegliere di rimuovere questa cache dopo l'elaborazione, se la cache è molto grande o se si desidera rimuovere i dati dettagliati. Se non si desidera memorizzare i dati nella cache, è possibile modificare la proprietà `CacheMode` della struttura di data mining in `ClearAfterProcessing`. In questo modo, la cache verrà distrutta dopo l'elaborazione dei modelli. Impostando la proprietà `CacheMode` su `ClearAfterProcessing` verrà disabilitato il drill-through dal modello di data mining.  
  
 Tuttavia, dopo aver eliminato la cache, non sarà possibile aggiungere nuovi modelli alla struttura di data mining. Se si aggiunge un nuovo modello di data mining alla struttura o si modificano le proprietà dei modelli esistenti, sarebbe necessario innanzitutto rielaborare la struttura di data mining. Per altre informazioni, vedere [Requisiti e considerazioni sull'elaborazione &#40;data mining&#41;](processing-requirements-and-considerations-data-mining.md).  
  
### <a name="viewing-mining-structures"></a>Visualizzazione delle strutture di data mining  
 Non è possibile utilizzare visualizzatori per esplorare i dati in una struttura di data mining. Tuttavia, in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]è possibile utilizzare la scheda **Struttura di data mining** nella Progettazione modelli di data mining per visualizzare le colonne della struttura e le relative definizioni. Per altre informazioni, vedere [Data Mining Designer](data-mining-designer.md).  
  
 Se si desidera esaminare i dati nella struttura di data mining, è possibile creare query utilizzando DMX (Data Mining Extensions). Ad esempio, l'istruzione `SELECT * FROM <structure>.CASES` restituisce tutti i dati presenti nella struttura di data mining. Per recuperare queste informazioni, è necessario che la struttura di data mining sia stata elaborata e che i risultati dell'elaborazione vengano memorizzati nella cache.  
  
 L'istruzione `SELECT * FROM <model>.CASES` restituisce le stesse colonne, ma solo per i case di quel modello specifico. Per altre informazioni, vedere [SELECT FROM &#60;structure&#62;.CASES](/sql/dmx/select-from-structure-cases) e [SELECT FROM &#60;model&#62;.CASES &#40;DMX&#41;](/sql/dmx/select-from-model-content-dmx).  
  
## <a name="using-data-mining-models-with-mining-structures"></a>Utilizzo dei modelli di data mining con le strutture di data mining  
 Un modello di data mining applica un algoritmo specifico ai dati rappresentati da una struttura di data mining. Un modello di data mining è un oggetto che appartiene a una determinata struttura di data mining ed eredita tutti i valori delle proprietà definite dalla struttura. Nel modello possono essere utilizzate tutte le colonne contenute nella struttura di data mining o un subset delle colonne. È possibile aggiungere più copie di una colonna della struttura a una struttura. È anche possibile aggiungere più copie di una colonna della struttura a un modello e quindi assegnare nomi o *alias*diversi a ogni colonna della struttura nel modello. Per altre informazioni sulle colonne della struttura di alias, vedere [Creare un alias per una colonna di un modello](create-an-alias-for-a-model-column.md) e [Proprietà dei modelli di data mining](mining-model-properties.md).  
  
 Per altre informazioni sull'architettura dei modelli di data mining, vedere [Mining Models &#40;Analysis Services - Data Mining&#41;](mining-models-analysis-services-data-mining.md).  
  
## <a name="related-tasks"></a>Attività correlate  
 Utilizzare i collegamenti forniti di seguito per ottenere ulteriori informazioni sulla definizione, sulla gestione e sull'utilizzo delle strutture di data mining.  
  
|Attività|Collegamenti|  
|-----------|-----------|  
|Utilizzare le strutture di data mining relazionali|[Creare una nuova struttura di data mining relazionale](create-a-new-relational-mining-structure.md)<br /><br /> [Aggiungere una tabella nidificata a una struttura di data mining](add-a-nested-table-to-a-mining-structure.md)|  
|Utilizzare le strutture di data mining basate su cubi OLAP|[Creare una nuova struttura di data mining OLAP](create-a-new-olap-mining-structure.md)<br /><br /> [Filtrare il cubo di origine per una struttura di data mining](../filter-the-source-cube-for-a-mining-structure.md)|  
|Utilizzare le colonne in una struttura di data mining|[Aggiungere colonne a una struttura di data mining](add-columns-to-a-mining-structure.md)<br /><br /> [Rimuovere colonne da una struttura di data mining](remove-columns-from-a-mining-structure.md)|  
|Eseguire una query sulle proprietà e sui dati della struttura di data mining o modificarli|[Modificare le proprietà di una struttura di data mining](change-the-properties-of-a-mining-structure.md)|  
|Utilizzare le origini dati sottostanti e aggiornare i dati di origine|[Modificare la vista origine dati usata per una struttura di data mining](edit-the-data-source-view-used-for-a-mining-structure.md)<br /><br /> [Elaborare una struttura di data mining](process-a-mining-structure.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetti di database &#40;Analysis Services - Dati multidimensionali&#41;](../multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [Modelli di data mining &#40;Analysis Services - Data mining&#41;](mining-models-analysis-services-data-mining.md)  
  
  
