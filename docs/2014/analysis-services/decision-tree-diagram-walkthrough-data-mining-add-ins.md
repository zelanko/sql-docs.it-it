---
title: Decision Trees descrizione dettagliata del diagramma dell'albero (componenti aggiuntivi Data Mining dei dati) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- shapes, data mining
- diagram, decision tree
- Visio shapes, decision tree
- decision tree [data mining]
ms.assetid: 9566f6a2-c750-4125-ba5e-42c7251a78c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 55bdeb41ed62fd727a6e5eb637734a67d21660fe
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62732434"
---
# <a name="decision-tree-diagram-walkthrough--data-mining-add-ins"></a>Descrizione dettagliata del diagramma dell'albero delle decisioni (componenti aggiuntivi Data Mining dei dati)
  Se è stato creato un modello di albero delle decisioni, è possibile creare un diagramma personalizzato in Visio tramite la forma Albero delle decisioni o la forma Rete di dipendenze. In questo argomento descrive le personalizzazioni è possibile eseguire utilizzando la **albero delle decisioni** questi controlli e forme:  
  
-   Controlli di rendering per il diagramma dell'albero delle decisioni  
  
     Queste opzioni fanno parte del **procedura guidata albero delle decisioni** che viene avviata quando si rilascia una forma nell'area di lavoro di Visio.  
  
-   **Layout Data Mining** sulla barra degli strumenti  
  
     Queste opzioni vengono aggiunte all'area di lavoro di Visio per consentire di interagire con la forma.  
  
## <a name="build-a-decision-tree-diagram"></a>Compilazione di un diagramma dell'albero delle decisioni  
 Si rilascia la forma albero delle decisioni nella pagina di Visio per avviare il **procedura guidata forma Visio per albero delle decisioni** e impostare le opzioni del diagramma.  
  
#### <a name="use-the-decision-tree-wizard"></a>Utilizzo della Procedura guidata Albero delle decisioni  
  
1.  Se non viene visualizzata **forme Microsoft Data Mining** nel **forme** fare clic su **più forme**, selezionare **Apri Stencil**e aprire la modello dal percorso di installazione predefinito.  
  
     \<unità >: \Programmi file (x85) \Microsoft SQL Server 2012 DM Add-Ins  
  
2.  Trascinare il **albero delle decisioni** la forma nella pagina.  
  
3.  Nella pagina di benvenuto del **procedura guidata forma Visio per albero delle decisioni**, fare clic su **successivo**.  
  
4.  Nel **Vybrat Zdroj** pagina del **guidata Cluster**, scegliere una connessione a un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] server che contiene il modello da visualizzare.  
  
5.  Selezionare un modello di data mining appropriato e fare clic su **successivo**.  
  
     Questo tipo di diagramma supporta i modelli creati mediante l'algoritmo Decision Trees o Linear Regression.  
  
6.  Nel **selezione albero delle decisioni** pagina, scegliere un singolo albero da visualizzare.  
  
     Un albero vengono modellate le interazioni che portano un risultato specifico modellato; Pertanto, anche se il modello contiene più risultati, è possibile visualizzare solo un albero alla volta.  
  
7.  Nel **selezione albero delle decisioni** nella finestra di dialogo è inoltre possibile impostare queste opzioni di rendering:  
  
     **Profondità massima di Rendering**  
     Utilizzare questa opzione per controllare il numero di nodi visualizzati.  
  
     Un albero delle decisioni potrebbe avere una gerarchia molto profonda, creando un diagramma che non rientra nella pagina. Utilizzare questo controllo per concentrarsi sui nodi più a sinistra, che sono i più importanti.  
  
     L'impostazione predefinita è tre livelli di nodi.  
  
     **Selezionare il colore e visualizzare il testo per i valori**  
     Scegliere il colore che rappresenterà ognuno dei risultati. Se non si specificano i colori, questi vengono automaticamente generati utilizzando i colori del tema del video correnti.  
  
8.  Fare clic su **avanzate** per personalizzare le opzioni seguenti per ogni nodo nel diagramma dell'albero delle decisioni.  
  
     **Variabile ombreggiatura** e **stato**  
     Scegliere il risultato di destinazione che si desidera visualizzare nel diagramma dell'albero.  
  
     **Mostra istogramma**  
     Consente di aggiungere un grafico a ogni nodo in cui vengono visualizzate le regole che definiscono tale nodo.  
  
     **Mostra etichetta**  
     Consente di aggiungere i nomi di colonna all'istogramma.  
  
     **Mostra probabilità**  
     Consente di visualizzare la probabilità di ogni valore.  
  
     **Mostra supporto**  
     Consente di visualizzare il supporto per ogni valore.  
  
     **Mostra piè di pagina**  
     Consente di aggiungere un piè di pagina in cui vengono sommati tutti i valori visualizzati.  
  
     **Mostra intestazione**  
     Consente di aggiungere intestazioni di colonna.  
  
     **Mostra stati con supporto zero**  
     Consente di visualizzare i valori mancanti.  
  
9. Fare clic su **fine** per creare il grafico.  
  
    > [!WARNING]  
    >  In alcuni ambienti, i connettori nel grafico potrebbero non riuscire a eseguire il rendering in Office 2013.  
  
## <a name="explore-and-modify-the-finished-diagram"></a>Esplorazione e modifica del diagramma completato  
 Dopo aver completato la **procedura guidata forma Visio per albero delle decisioni**, Visio consente di creare un diagramma dell'albero nella pagina in cui vengono visualizzati graficamente le regole che portano il risultato stimato.  
  
 È possibile continuare a modificare la forma utilizzando i seguenti controlli per i diagrammi dell'albero delle decisioni:  
  
#### <a name="using-the-decision-tree-option-menus"></a>Utilizzo dei menu delle opzioni dell'albero delle decisioni  
  
1.  Scegliere il **Add-Ins** della barra multifunzione e quindi visualizzare una delle barre degli strumenti personalizzate utilizzate per l'uso di diagrammi di data mining:  
  
     **Layout**  
     Consente di ottimizzare la disposizione dell'albero da adattare nella pagina corrente.  
  
     **Ridimensiona pagina**  
     Questo controllo è destinato alle versioni HTML precedenti. Utilizzare invece i controlli per il ridimensionamento della pagina di Visio.  
  
     **Descrizione**  
     Quando è selezionato un nodo dell'albero, fare clic su questa opzione per visualizzare i dettagli sui case nel nodo.  
  
2.  Usare la **nuovo Layout pagina** opzione in Visio **progettazione** della barra multifunzione per provare layout dell'albero differenti.  
  
3.  Usare la **connettori** opzione il **progettazione** pressione di tab per modificare i connettori utilizzati tra i nodi dell'albero.  
  
4.  Usare la **panoramica e Zoom** controllo la **riquadro attività** area di Visio **visualizzazione** barra multifunzione per concentrarsi su una determinata area del diagramma.  
  
5.  Fare clic con il pulsante destro del mouse su qualsiasi nodo dell'albero e scegliere tra queste opzioni del menu di scelta rapida specifiche dei diagrammi dell'albero delle decisioni:  
  
     **Ottimizza Layout di pagina**  
     Consente di ripartire uniformemente i nodi nella pagina, nonché di modificare la visualizzazione della pagina in modo da includere tutti i nodi.  
  
     **Sposta figli in una nuova pagina**  
     Consente di spostare in una nuova pagina i nodi figlio del nodo attualmente selezionato.  
  
     **Comprimere i nodi figlio**  
     Consente di nascondere i nodi figlio del nodo attualmente selezionato.  
  
     **Espandere i nodi figlio**  
     Consente di visualizzare i nodi figlio del nodo attualmente selezionato.  
  
## <a name="see-also"></a>Vedere anche  
 [Risoluzione dei problemi di diagrammi di Visio Data Mining &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
