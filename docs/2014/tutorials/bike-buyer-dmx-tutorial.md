---
title: Esercitazione DMX Bike Buyer | Microsoft Docs
ms.custom: ''
ms.date: 10/19/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- DMX [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- statements [DMX], tutorials
- Data Mining Extensions [Analysis Services], tutorials
- tutorials [Data Mining]
ms.assetid: 4b634cc1-86dc-42ec-9804-a19292fe8448
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3cf9a0c9e6059330c0b8edbd8228f617ba093564
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63140539"
---
# <a name="bike-buyer-dmx-tutorial"></a>Esercitazione su DMX per Bike Buyer
  In questa esercitazione vengono descritte le procedure per la creazione, il training e l'esplorazione di modelli di data mining utilizzando il linguaggio di query DMX (Data Mining Extensions). Questi modelli di data mining verranno quindi utilizzati per la creazione di stime relative alla probabilità che un cliente acquisti una bicicletta.  
  
 I modelli di data mining verranno creati a partire dai dati contenuti nel database di esempio [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)], in cui sono memorizzati i dati relativi alla società fittizia [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] è una grande società multinazionale. che produce e vende biciclette in metallo e a struttura mista per i mercati di America del nord, Europa e Asia. La sede operativa si trova a Bothell, nello stato di Washington, in cui lavorano 290 dipendenti, e la società dispone di numerosi reparti vendite dislocati nelle diverse aree di mercato a livello internazionale.  
  
## <a name="tutorial-scenario"></a>Scenario dell'esercitazione  
 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] ha deciso di espandere la propria struttura di analisi dei dati creando un'applicazione personalizzata dotata di funzionalità di data mining. Gli obiettivi dell'applicazione personalizzata sono i seguenti:  
  
-   Utilizzare come input determinate caratteristiche di un potenziale cliente e stimare se tale cliente acquisterà una bicicletta.  
  
-   Utilizzare come input un elenco di potenziali clienti con le relative caratteristiche e stimare quali di essi acquisteranno una bicicletta.  
  
 Nel primo caso i dati dei clienti sono tratti da una pagina di registrazione dei clienti, mentre nel secondo caso l'elenco dei potenziali clienti viene fornito dal reparto marketing di [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)].  
  
 Il reparto marketing ha inoltre l'esigenza di raggruppare i clienti esistenti in categorie sulla base di caratteristiche quali il luogo di residenza, il numero di figli e la distanza dal luogo di lavoro per stabilire se tali gruppi possono essere utilizzati per la definizione di offerte mirate a specifiche tipologie di clientela. Questo richiederà un ulteriore modello di data mining.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]In    sono disponibili numerosi strumenti che possono essere utilizzati per eseguire queste attività:  
  
-   Il linguaggio di query DMX  
  
-   L' [algoritmo Microsoft Decision Trees](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md) e l' [algoritmo Microsoft Clustering](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md)  
  
-   L'editor di query in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]  
  
 DMX (Data Mining Extensions) è un linguaggio di query incluso in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che è possibile utilizzare per creare e gestire modelli di data mining. L'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Decision Trees consente di creare modelli che possono essere utilizzati per stimare se una persona acquisterà una bicicletta. Il modello risultante può utilizzare un singolo cliente o una tabella di clienti come input. L'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering consente di creare raggruppamenti di clienti in base a caratteristiche condivise. Lo scopo di questa esercitazione consiste nel fornire gli script DMX che verranno utilizzati nell'applicazione personalizzata.  
  
 **Per ulteriori informazioni:** [soluzioni di data mining](../../2014/analysis-services/data-mining/data-mining-solutions.md)  
  
## <a name="mining-structure-and-mining-models"></a>Struttura e modelli di data mining  
 Prima di iniziare a creare istruzioni DMX, è importante comprendere gli oggetti principali utilizzati da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] per creare i modelli di data mining. Per struttura di data mining si intende una struttura di dati che definisce il dominio da cui vengono compilati i modelli di data mining. Una singola struttura di data mining può contenere più modelli di data mining che condividono lo stesso dominio. Un modello di data mining applica un algoritmo specifico ai dati rappresentati da una struttura di data mining.  
  
 Gli elementi di compilazione della struttura di data mining sono le relative colonne, che descrivono le informazioni contenute nell'origine dei dati. Tali colonne includono informazioni quali il tipo di dati, il tipo di contenuto e la modalità di distribuzione dei dati.  
  
 I modelli di data mining devono contenere la colonna chiave descritta nella struttura di data mining, nonché un subset delle colonne restanti. Il modello di data mining definisce l'utilizzo di ogni colonna e l'algoritmo utilizzato per creare il modello stesso. Ad esempio, in DMX è possibile specificare una colonna come colonna chiave o colonna PREDICT. Le colonne non specificate vengono considerate come colonne di input.  
  
 In DMX è possibile creare modelli di data mining in due modi, ovvero creando contemporaneamente una struttura di data mining e il modello di data mining associato mediante l'istruzione CREATE MINING MODEL oppure creando prima una struttura di data mining con l'istruzione CREATE MINING STRUCTURE e quindi aggiungendo un modello di data mining alla struttura mediante l'istruzione ALTER STRUCTURE. Questi metodi sono descritti nella tabella seguente.  
  
 CREATE MINING MODEL  
 Questa istruzione consente di creare contemporaneamente una struttura di data mining e il modello di data mining associato utilizzando lo stesso nome. Al nome del modello di data mining viene aggiunto il suffisso "Structure" per differenziarlo dalla struttura di data mining. Questa istruzione è utile quando si crea una struttura di data mining che conterrà un unico modello di data mining.  
  
 Per altre informazioni, vedere [CREATE MINING MODEL &#40;DMX&#41;](/sql/dmx/create-mining-model-dmx).  
  
 ALTER MINING STRUCTURE  
 Questa istruzione consente di aggiungere un modello di data mining a una struttura di data mining già esistente sul server. È utile se si desidera creare una struttura di data mining contenente più modelli di data mining. L'esigenza di aggiungere più modelli di data mining in un'unica struttura di data mining può essere dettata da numerose ragioni. È possibile ad esempio creare più modelli di data mining che utilizzano algoritmi diversi per stabilire quale algoritmo funziona meglio oppure creare più modelli di data mining che utilizzano lo stesso algoritmo, ma impostando un parametro in modo diverso in ogni modello per individuare l'impostazione ottimale per il parametro.  
  
 Per ulteriori informazioni, vedere [ALTER mining structure &#40;DMX&#41;](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016).  
  
 In questa esercitazione si utilizzerà il secondo metodo poiché si creerà una struttura di data mining contenente diversi modelli di data mining.  
  
 **Per ulteriori informazioni**  
  
 [Data Mining Extensions &#40;riferimento dmx&#41;](/sql/dmx/data-mining-extensions-dmx-reference), [informazioni sull'istruzione DMX SELECT, sulla](/sql/dmx/understanding-the-dmx-select-statement) [struttura e sull'utilizzo di query di stima](/sql/dmx/structure-and-usage-of-dmx-prediction-queries) DMX  
  
## <a name="what-you-will-learn"></a>Lezioni dell'esercitazione  
 L'esercitazione è suddivisa nelle lezioni seguenti:  
  
 [Lezione 1: Creazione della struttura di data mining Bike Buyer](../../2014/tutorials/lesson-1-creating-the-bike-buyer-mining-structure.md)  
 In questa lezione verranno illustrate le procedure per l'utilizzo dell'istruzione `CREATE` per creare strutture di data mining.  
  
 [Lezione 2: Aggiunta di modelli di data mining alla struttura di data mining Bike Buyer](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md)  
 In questa lezione verranno illustrate le procedure per l'utilizzo dell'istruzione `ALTER` per aggiungere modelli di data mining a una struttura di data mining.  
  
 [Lezione 3: Elaborazione della struttura di data mining Bike Buyer](../../2014/tutorials/lesson-3-processing-the-bike-buyer-mining-structure.md)  
 In questa lezione verranno illustrate le procedure per l'utilizzo dell'istruzione `INSERT INTO` per elaborare le strutture di data mining e i modelli di data mining ad esse associati.  
  
 [Lezione 4: Esplorazione dei modelli di data mining Bike Buyer](../../2014/tutorials/lesson-4-browsing-the-bike-buyer-mining-models.md)  
 In questa lezione verranno illustrate le procedure per l'utilizzo dell'istruzione `SELECT` per esplorare il contenuto dei modelli di data mining.  
  
 [Lezione 5: Esecuzione di query di stima](../../2014/tutorials/lesson-5-executing-prediction-queries.md)  
 In questa lezione verranno illustrate le procedure per l'utilizzo dell'istruzione `PREDICTION JOIN` per creare stime basate su modelli di data mining.  
  
## <a name="requirements"></a>Requisiti  
 Prima di eseguire l'esercitazione, verificare che sia installato quanto segue:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , [!INCLUDE[ssASversion10](../includes/ssasversion10-md.md)] [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   Database [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] . Per una maggiore sicurezza, i database di esempio non vengono installati per impostazione predefinita. Per installare i database di esempio [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]ufficiali per, visitare la pagina relativa ai [database di esempio di Microsoft SQL](https://go.microsoft.com/fwlink/?LinkId=88417) e selezionare i database che si desidera installare.  
  
> [!NOTE]  
>  Quando si esaminano le esercitazioni, è consigliabile aggiungere i pulsanti **argomento successivo** e **argomento precedente** alla barra degli strumenti del Visualizzatore di documenti.  
  
## <a name="see-also"></a>Vedi anche  
 [Esercitazione su Market basket DMX](../../2014/tutorials/market-basket-dmx-tutorial.md)   
 [Esercitazione di base sul data mining](../../2014/tutorials/basic-data-mining-tutorial.md)  
  
  
