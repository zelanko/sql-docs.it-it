---
title: Visualizzare un modello usando il Visualizzatore Microsoft Decision Trees | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Tree Viewer [Analysis Services]
- predictions [Analysis Services], discrete attributes
- mining model content, viewing
- predictions [Analysis Services], continuous attributes
- mining legend [Analysis Services]
- discrete attributes [Analysis Services]
- Microsoft Decision Trees algorithm [Analysis Services]
- decision tree algorithms [Analysis Services]
- Microsoft Tree Viewer
- decision trees [Analysis Services]
- dependencies [Analysis Services]
- continuous attributes
ms.assetid: 0c96d518-ed20-40b7-8d62-b26ad6244287
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5f7ac483e0883386f620a654d6257a49fa8baf52
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66085943"
---
# <a name="browse-a-model-using-the-microsoft-tree-viewer"></a>Visualizzare un modello utilizzando il Visualizzatore Microsoft Decision Trees
  Il [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visualizzatore dell'albero [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in Visualizza gli alberi delle decisioni compilati con l' [!INCLUDE[msCoName](../../includes/msconame-md.md)] algoritmo Decision Trees. L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees è un algoritmo dell'albero delle decisioni ibrido che supporta classificazione e regressione. È anche possibile pertanto usare il visualizzatore per visualizzare modelli basati sull'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression. L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees viene usato per la modellazione predittiva di attributi discreti e continui. Per altre informazioni su questo algoritmo, vedere [Algoritmo Microsoft Decision Trees](microsoft-decision-trees-algorithm.md).  
  
> [!NOTE]  
>  Per visualizzare informazioni dettagliate sulle equazioni utilizzate nel modello e sui modelli individuati, utilizzare il visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Generic Content Tree Viewer. Per altre informazioni, vedere [Visualizzare un modello usando Microsoft Generic Content Tree Viewer](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) o [Microsoft Generic Content Tree Viewer &#40;Data mining&#41;](../microsoft-generic-content-tree-viewer-data-mining.md).  
  
##  <a name="BKMK_TabsPanes"></a>Schede del Visualizzatore  
 Per la visualizzazione di un modello di data mining in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]viene utilizzato il visualizzatore appropriato nella scheda **Visualizzatore modello di data mining** di Progettazione modelli di data mining. Il Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees include le schede e i riquadri seguenti:  
  
-   [Albero delle decisioni](#BKMK_DecisionTree)  
  
-   [Rete di dipendenze](#BKMK_DependencyNetwork)  
  
-   [Legenda data mining](#BKMK_MiningLegend)  
  
###  <a name="BKMK_DecisionTree"></a>Albero delle decisioni  
 Quando si compila un modello di albero delle decisioni, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene compilato un albero separato per ogni attributo stimabile. È possibile visualizzare un singolo albero selezionandolo dall'elenco **Albero** nella scheda **Albero delle decisioni** del visualizzatore.  
  
 Un albero delle decisioni è costituito da una serie di divisioni di cui la più importante, determinata dall'algoritmo, si trova a sinistra del visualizzatore nel nodo **Tutto** . Le altre divisioni si trovano a destra. La divisione nel nodo **Tutto** è la più importante in quanto contiene l'espressione condizionale più attendibile tra quelle che causano la divisione nel set di dati e, di conseguenza, ha causato la prima divisione.  
  
 È possibile espandere o comprimere singoli nodi dell'albero per visualizzare o nascondere le divisioni che ricorrono dopo ogni nodo. È anche possibile usare le opzioni della scheda **Albero delle decisioni** per determinare la modalità di visualizzazione dell'albero. Per modificare il numero di livelli visualizzati nell'albero, usare il dispositivo di scorrimento **Mostra livello** . Per impostare il numero predefinito di livelli visualizzati per tutti gli alberi del modello, usare **Espansione predefinita** .  
  
#### <a name="predicting-discrete-attributes"></a>Stima di attributi discreti  
 Se un albero è stata compilato con un attributo stimabile discreto, in ogni nodo dell'albero verranno visualizzati gli elementi seguenti:  
  
-   La condizione che ha causato la divisione.  
  
-   Un istogramma che rappresenta la distribuzione degli stati dell'attributo stimabile, ordinati in base alla diffusione.  
  
 Per modificare il numero di stati visualizzati negli istogrammi dell'albero, usare l'opzione **Istogramma** . Tale opzione è utile se l'attributo stimabile include molti stati. Gli stati vengono visualizzati nell'istogramma in ordine di diffusione da sinistra a destra. Se il numero di stati che si sceglie di visualizzare è inferiore al numero totale di stati dell'attributo, gli stati meno frequenti vengono visualizzati collettivamente in grigio. Per ottenere il conteggio esatto relativo a ogni stato di un nodo, posizionare il puntatore sul nodo per visualizzare una finestra popup oppure selezionare il nodo per visualizzare i relativi dettagli nella **Legenda data mining**.  
  
 Il colore di sfondo di ogni nodo rappresenta la concentrazione di case dello stato specifico dell'attributo selezionato tramite l'opzione **Sfondo** . Tale opzione consente di evidenziare i nodi che contengono la destinazione specifica desiderata.  
  
#### <a name="predicting-continuous-attributes"></a>Stima di attributi continui  
 Se un albero è stato generato con un attributo stimabile continuo, verrà visualizzato un grafico a rombi, anziché un istogramma, per ogni nodo dell'albero. Il grafico a rombi include una linea che rappresenta l'intervallo dell'attributo. Il rombo è posizionato in corrispondenza della media del nodo e lo spessore del rombo rappresenta la varianza dell'attributo in tale nodo. Un rombo con spessore minore indica che il nodo può creare una stima più accurata. Viene inoltre visualizzata l'equazione di regressione, utilizzata per determinare la divisione nel nodo.  
  
#### <a name="additional-decision-tree-display-options"></a>Opzioni di visualizzazione aggiuntive per l'albero delle decisioni  
 Se si attiva il drill-through per un modello di albero delle decisioni, è possibile accedere ai case di training che supportano un nodo facendo clic con il pulsante destro del mouse sul nodo dell'albero e selezionando **Drill-through**. Per attivare il drill-through, usare la Creazione guidata modello di data mining oppure modificare la proprietà del drill-through sul modello di data mining nella scheda **Modelli di data mining** .  
  
 È possibile ingrandire o ridurre un albero tramite le opzioni di zoom della scheda **Albero delle decisioni** oppure adattare l'intero modello alla schermata del visualizzatore tramite l'opzione **Adatta** . Se un albero è troppo grande per adattarlo alla schermata, è possibile spostarsi all'interno dell'albero tramite l'opzione **Navigazione**. Se si fa clic sull'opzione **Navigazione** , verrà aperta una finestra di navigazione separata che consente di selezionare le sezioni del modello da visualizzare.  
  
 È inoltre possibile copiare l'immagine della visualizzazione albero negli Appunti in modo da poterla incollare nei documenti o nel software per la modifica di immagini. Usare **Copia parte visibile del grafico** per copiare solo la sezione dell'albero visibile nel visualizzatore, oppure usare **Copia grafico intero** per visualizzare tutti i nodi espansi nell'albero.  
  
 [Torna all'inizio](#BKMK_TabsPanes)  
  
###  <a name="BKMK_DependencyNetwork"></a>Rete di dipendenze  
 Nella scheda **Rete di dipendenze** vengono visualizzate le dipendenze tra gli attributi di input e gli attributi stimabili del modello. Il dispositivo di scorrimento a sinistra del visualizzatore svolge la funzione di filtro correlato ai livelli di attendibilità delle dipendenze. Se si sposta il dispositivo di scorrimento verso il basso, vengono visualizzati solo i collegamenti più attendibili.  
  
 Quando si seleziona un nodo, nel visualizzatore vengono evidenziate le dipendenze specifiche del nodo. Se ad esempio si sceglie un nodo stimabile, nel visualizzatore verrà inoltre evidenziato ogni nodo che contribuisce alla stima del nodo stimabile.  
  
 Se il visualizzatore contiene un numero elevato di nodi, è possibile cercare nodi specifici tramite il pulsante **Trova nodo** . Se si fa clic sul pulsante **Trova nodo** , verrà visualizzata la finestra di dialogo **Trova nodo** , che consente di cercare e selezionare nodi specifici mediante un filtro.  
  
 La legenda nella parte inferiore del visualizzatore consente di individuare le corrispondenze tra i colori e i tipi di dipendenza rappresentati nel grafico. Ad esempio, quando si seleziona un nodo stimabile, a quest'ultimo viene applicata un'ombreggiatura turchese mentre ai nodi utilizzati per la stima del nodo selezionato viene applicata un'ombreggiatura arancione.  
  
 [Torna all'inizio](#BKMK_TabsPanes)  
  
###  <a name="BKMK_MiningLegend"></a>Legenda data mining  
 Quando si seleziona un nodo nel modello di albero delle decisioni, in **Legenda data mining** vengono visualizzate le informazioni seguenti:  
  
-   Il numero di case nel nodo, suddivisi in base agli stati dell'attributo stimabile  
  
-   La probabilità di ogni case dell'attributo stimabile per il nodo  
  
-   Un istogramma che include un conteggio per ogni stato dell'attributo stimabile  
  
-   Le condizioni necessarie per raggiungere un nodo specifico, note anche come *percorso del nodo*.  
  
-   Per i modelli di regressione lineare, la formula di regressione.  
  
 È possibile ancorare e usare la **Legenda data mining** in modo analogo a Esplora soluzioni.  
  
 [Torna all'inizio](#BKMK_TabsPanes)  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmo Microsoft Decision Trees](microsoft-decision-trees-algorithm.md)   
 [Visualizzatori modello di data mining &#40;Progettazione modelli di data mining&#41;](../mining-model-viewers-data-mining-model-designer.md)   
 [Attività e procedure relative al Visualizzatore modello di data mining](mining-model-viewer-tasks-and-how-tos.md)   
 [Strumenti di data mining](data-mining-tools.md)   
 [Visualizzatori modello di data mining](data-mining-model-viewers.md)  
  
  
