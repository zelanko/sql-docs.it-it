---
title: Esercitazione su Market basket DMX | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- DMX [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- statements [DMX], tutorials
- Data Mining Extensions [Analysis Services], tutorials
- market basket analysis [Analysis Services]
- tutorials [Data Mining]
- tutorials [DMX]
ms.assetid: 6e262a1d-c89e-4033-8368-46cf25168ef5
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: fe12f1c4ca1c0946572c61e89f4f4edb8ba9a762
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63185648"
---
# <a name="market-basket-dmx-tutorial"></a>Esercitazione su DMX per Market Basket
  In questa esercitazione vengono descritte le procedure per la creazione, il training e l'esplorazione dei modelli di data mining utilizzando il linguaggio di query DMX (Data Mining Extensions). Questi modelli di data mining verranno quindi utilizzati per la creazione di stime che indicano quali prodotti tendono a essere acquistati contemporaneamente.  
  
 I modelli di data mining verranno creati a partire dai dati contenuti nel database di esempio [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)], in cui sono memorizzati i dati relativi alla società fittizia [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] è una grande società multinazionale. che produce e vende biciclette in metallo e a struttura mista per i mercati di America del nord, Europa e Asia. La sede operativa si trova a Bothell, nello stato di Washington, in cui lavorano 290 dipendenti, e la società dispone di numerosi reparti vendite dislocati nelle diverse aree di mercato a livello internazionale.  
  
## <a name="tutorial-scenario"></a>Scenario dell'esercitazione  
 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] ha deciso di creare un'applicazione personalizzata dotata di funzionalità di data mining per stimare quali tipi di prodotti i clienti tendono ad acquistare contemporaneamente. L'obiettivo dell'applicazione personalizzata consiste nella possibilità di specificare un set di prodotti e di stimare quali prodotti aggiuntivi verranno acquistati insieme a quelli specificati. Queste informazioni verranno quindi utilizzate da [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] per aggiungere una caratteristica di suggerimento nel sito Web e ottimizzare la presentazione delle informazioni alla clientela.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in sono disponibili diversi strumenti che possono essere utilizzati per completare questa [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] attività:  
  
-   Il linguaggio di query DMX  
  
-   [Algoritmo Microsoft Association](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)  
  
-   L'editor di query in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]  
  
 DMX (Data Mining Extensions) è un linguaggio di query incluso in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che è possibile utilizzare per creare e gestire modelli di data mining. L' [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Association crea modelli in grado di prevedere i prodotti che probabilmente verranno acquistati insieme.  
  
 Lo scopo di questa esercitazione consiste nel fornire le query DMX che verranno utilizzate nell'applicazione personalizzata.  
  
 **Per ulteriori informazioni:** [soluzioni di data mining](../../2014/analysis-services/data-mining/data-mining-solutions.md)  
  
## <a name="mining-structure-and-mining-models"></a>Struttura e modelli di data mining  
 Prima di iniziare a creare istruzioni DMX, è importante comprendere gli oggetti principali utilizzati da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] per creare i modelli di data mining. La *struttura* di data mining è una struttura di dati che definisce il dominio dei dati dal quale vengono compilati i modelli di data mining. Una singola struttura di data mining può contenere più *modelli di data mining* che condividono lo stesso dominio. Un modello di data mining applica un algoritmo specifico ai dati rappresentati da una struttura di data mining.  
  
 Gli elementi di compilazione della struttura di data mining sono le relative colonne, che descrivono le informazioni contenute nell'origine dei dati. Tali colonne includono informazioni quali il tipo di dati, il tipo di contenuto e la modalità di distribuzione dei dati.  
  
 I modelli di data mining devono contenere la colonna chiave descritta nella struttura di data mining, nonché un subset delle colonne restanti. Il modello di data mining definisce l'utilizzo di ogni colonna e l'algoritmo utilizzato per creare il modello stesso. Ad esempio, in DMX è possibile specificare una colonna come colonna chiave o colonna PREDICT. Le colonne non specificate vengono considerate come colonne di input.  
  
 In DMX è possibile creare modelli di data mining in due modi, ovvero creando contemporaneamente una struttura di data mining e il modello di data mining associato mediante l'istruzione `CREATE MINING MODEL` oppure creando prima una struttura di data mining con l'istruzione `CREATE MINING STRUCTURE` e quindi aggiungendo un modello di data mining alla struttura mediante l'istruzione `ALTER STRUCTURE`. Questi metodi sono descritti di seguito.  
  
 `CREATE MINING MODEL`  
 Questa istruzione consente di creare contemporaneamente una struttura di data mining e il modello di data mining associato utilizzando lo stesso nome. Al nome del modello di data mining viene aggiunto il suffisso "Structure" per differenziarlo dalla struttura di data mining.  
  
 Questa istruzione è utile quando si crea una struttura di data mining che conterrà un unico modello di data mining.  
  
 Per altre informazioni, vedere [CREATE MINING MODEL &#40;DMX&#41;](/sql/dmx/create-mining-model-dmx).  
  
 CREATE MINING STRUCTURE  
 Utilizzare questa istruzione per creare una nuova struttura di data mining senza modelli.  
  
 Quando si utilizza CREATE MINING STRUCTURE, è inoltre possibile creare un set di dati di controllo che può essere utilizzato per il testing dei modelli basati sulla stessa struttura di data mining.  
  
 Per altre informazioni, vedere [CREATE MINING STRUCTURE &#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx).  
  
 `ALTER MINING STRUCTURE`  
 Questa istruzione consente di aggiungere un modello di data mining a una struttura di data mining già esistente sul server.  
  
 L'esigenza di aggiungere più modelli di data mining in un'unica struttura di data mining può essere dettata da numerose ragioni. È possibile ad esempio creare più modelli di data mining con algoritmi diversi per stabilire quale di essi funziona meglio oppure creare più modelli di data mining che utilizzano lo stesso algoritmo, ma impostando un parametro in modo diverso in ogni modello per individuare l'impostazione ottimale per il parametro.  
  
 Per ulteriori informazioni, vedere [ALTER mining structure &#40;DMX&#41;](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016).  
  
 In questa esercitazione si utilizzerà il secondo metodo poiché si creerà una struttura di data mining contenente diversi modelli di data mining.  
  
 **Per ulteriori informazioni**  
  
 [Data Mining Extensions &#40;riferimento dmx&#41;](/sql/dmx/data-mining-extensions-dmx-reference), [informazioni sull'istruzione DMX SELECT, sulla](/sql/dmx/understanding-the-dmx-select-statement) [struttura e sull'utilizzo di query di stima](/sql/dmx/structure-and-usage-of-dmx-prediction-queries) DMX  
  
## <a name="what-you-will-learn"></a>Lezioni dell'esercitazione  
 L'esercitazione è suddivisa nelle lezioni seguenti:  
  
 [Lezione 1: Creazione della struttura di data mining Market Basket](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md)  
 In questa lezione verranno illustrate le procedure per l'utilizzo dell'istruzione `CREATE` per creare strutture di data mining.  
  
 [Lezione 2: Aggiunta di modelli di data mining alla struttura di data mining Market Basket](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)  
 In questa lezione verranno illustrate le procedure per l'utilizzo dell'istruzione `ALTER` per aggiungere modelli di data mining a una struttura di data mining.  
  
 [Lezione 3: Elaborazione della struttura di data mining Market Basket](../../2014/tutorials/lesson-3-processing-the-market-basket-mining-structure.md)  
 In questa lezione verranno illustrate le procedure per l'utilizzo dell'istruzione `INSERT INTO` per elaborare le strutture di data mining e i modelli di data mining ad esse associati.  
  
 [Lezione 4: Esecuzione delle stime relative a Market Basket](../../2014/tutorials/lesson-4-executing-market-basket-predictions.md)  
 In questa lezione verranno illustrate le procedure per l'utilizzo dell'istruzione `PREDICTION JOIN` per creare stime basate su modelli di data mining.  
  
## <a name="requirements"></a>Requisiti  
 Prima di eseguire l'esercitazione, verificare che sia installato quanto segue:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   Il database [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]  
  
 Per una maggiore sicurezza, i database di esempio non vengono installati per impostazione predefinita. Per installare i database di esempio ufficiali [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]per, vedere [http://www.CodePlex.com/MSFTDBProdSamples](https://go.microsoft.com/fwlink/?LinkId=88417) o nel Microsoft SQL Server esempi e progetti della community Home page nella sezione Microsoft SQL Server esempi di prodotti. Fare clic su **database**, quindi fare clic sulla scheda **releases** e selezionare i database desiderati.  
  
> [!NOTE]  
>  Quando si esaminano le esercitazioni, è consigliabile aggiungere i pulsanti **argomento successivo** e **argomento precedente** alla barra degli strumenti del Visualizzatore di documenti.  
  
## <a name="see-also"></a>Vedi anche  
 [Esercitazione DMX Bike Buyer](../../2014/tutorials/bike-buyer-dmx-tutorial.md)   
 [Esercitazione di base sul data mining](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Lezione 3: Compilazione di uno scenario Market Basket &#40;Esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
  
