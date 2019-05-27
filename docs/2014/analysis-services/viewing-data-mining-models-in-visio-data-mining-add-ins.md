---
title: Visualizzazione di modelli di Data Mining in Visio (componenti aggiuntivi Data Mining dei dati) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- diagram, modifying
- templates [Visio]
- shapes, data mining
- diagram
ms.assetid: 5841adea-6650-4fae-8526-26af33edbede
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c287e840c07d11a527e980f9f07fb39fb3852739
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66065516"
---
# <a name="viewing-data-mining-models-in-visio-data-mining-add-ins"></a>Visualizzazione di modelli di data mining in Visio (componenti aggiuntivi Data mining)
  Le forme di Visio per il data mining consentono di connettersi a un server e creare un diagramma che rappresenta un modello di data mining esistente. I diagrammi possono quindi essere personalizzati utilizzando i controlli di Visio, ma è anche possibile eseguire il drill-down nei dati, esporre alcune delle statistiche sottostanti e utilizzare il modello sottostante.  
  
## <a name="building-a-model-diagram"></a>Compilazione di un diagramma del modello  
 Quando si apre il file contenente le forme di Visio per il data mining, il **forme** riquadro sono elencate le forme seguenti.  
  
 Se all'apertura di Visio le forme di data mining non sono visibili, aprire il file modello dalla cartella di installazione.  
  
 ![DM](media/dm-stencil.gif "DM")  
  
 Per utilizzare una forma, trascinarla nella pagina. Con ogni forma viene aperta una procedura guidata diversa, che consente di selezionare i dati di origine, di impostare opzioni per il tipo di diagramma specifico e di specificare l'ombreggiatura e altre opzioni di visualizzazione.  
  
 Nella tabella seguente sono elencati i tipi di modelli che è possibile utilizzare con ogni tipo di diagramma.  
  
|Forma di Visio|Modelli supportati|  
|-----------------|----------------------|  
|Albero delle decisioni|Utilizzare questa forma per modelli basati sugli algoritmi di regressione lineare o dell'albero delle decisioni.|  
|Rete di dipendenze|Utilizzare questa forma per modelli basati su uno qualsiasi degli algoritmi seguenti: Naive Bayes, Decision Trees o Association Rules.|  
|Cluster|Utilizzare questa forma per modelli basati su algoritmi di clustering.|  
  
 Le opzioni disponibili nella procedura guidata variano a seconda del tipo di dati del modello di data mining. Ad esempio, le colonne contenenti numeri continui vengono visualizzate in modo diverso rispetto alle variabili di categoria.  
  
## <a name="working-with-completed-shapes"></a>Utilizzo delle forme completate  
 Dopo il completamento è possibile utilizzare il diagramma per esplorare il modello di data mining o migliorarlo per l'utilizzo nelle presentazioni.  
  
### <a name="visio-menus"></a>Menu di Visio  
 In Visio vengono forniti diversi controlli di rendering, temi e menu di scelta rapida per migliorare un diagramma.  
  
-   Utilizzare i temi di Visio per modificare i colori del diagramma.  
  
-   Modificare i connettori o il layout del diagramma.  
  
### <a name="data-mining-menus"></a>Menu di data mining  
 Queste barre degli strumenti e voci di menu vengono fornite dai componenti aggiuntivi specifici di ogni tipo di modello o forma.  
  
-   Ogni tipo di diagramma contiene un menu di scelta rapida per la forma che consente di accedere alle opzioni speciali. Benché molte delle opzioni di tale menu siano comuni a tutte le forme di Visio, alcune opzioni sono univoche nei modelli di data mining.  
  
     In un diagramma dell'albero delle decisioni ad esempio è possibile fare clic su un nodo e quindi comprimere i nodi figlio per semplificare la consultazione del diagramma oppure spostare i nodi figlio in una pagina a parte.  
  
-   Poiché la forma è associata ai dati del modello, è inoltre possibile eseguire alcune attività di esplorazione utilizzando il diagramma:  
  
     Filtrare i nodi visualizzati oppure modificare il livello dell'albero o la profondità del grafico.  
  
     Eseguire lo zoom avanti in sezioni specifiche, cercare i nodi che contengono un determinato attributo o filtrare un grafico delle dipendenze in base ai bordi (probabilità).  
  
## <a name="walkthroughs"></a>Procedure dettagliate  
 Per esempi di come utilizzare e interpretare un diagramma completato, vedere i seguenti argomenti:  
  
 [Descrizione dettagliata del diagramma dei cluster](cluster-diagram-walkthrough-data-mining-add-ins.md)  
  
 [Descrizione dettagliata di diagramma della rete di dipendenze](dependency-network-diagram-walkthrough-data-mining-add-ins.md)  
  
 [Descrizione dettagliata del diagramma dell'albero delle decisioni](decision-tree-diagram-walkthrough-data-mining-add-ins.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esplorazione di modelli in Excel &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
