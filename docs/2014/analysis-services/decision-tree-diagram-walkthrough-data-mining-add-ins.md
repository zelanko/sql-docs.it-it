---
title: Procedura dettagliata relativa al diagramma dell'albero delle decisioni (componenti aggiuntivi Data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
ms.openlocfilehash: ef951825144f381ab37a83526ec96321fe43cfec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66082275"
---
# <a name="decision-tree-diagram-walkthrough--data-mining-add-ins"></a>Procedura dettagliata relativa al diagramma dell'albero delle decisioni (componenti aggiuntivi Data mining)
  Se è stato creato un modello di albero delle decisioni, è possibile creare un diagramma personalizzato in Visio tramite la forma Albero delle decisioni o la forma Rete di dipendenze. In questo argomento vengono descritte le personalizzazioni che è possibile eseguire utilizzando la forma **albero delle decisioni** e i controlli seguenti:  
  
-   Controlli di rendering per il diagramma dell'albero delle decisioni  
  
     Queste opzioni fanno parte della **procedura guidata albero delle decisioni** avviata quando si rilascia una forma nell'area di lavoro di Visio.  
  
-   Barra degli strumenti **Layout data mining**  
  
     Queste opzioni vengono aggiunte all'area di lavoro di Visio per consentire di interagire con la forma.  
  
## <a name="build-a-decision-tree-diagram"></a>Compilazione di un diagramma dell'albero delle decisioni  
 È possibile rilasciare la forma albero delle decisioni nella pagina Visio per avviare la **procedura guidata forma di Visio** per l'albero delle decisioni e impostare le opzioni del diagramma.  
  
#### <a name="use-the-decision-tree-wizard"></a>Utilizzo della Procedura guidata Albero delle decisioni  
  
1.  Se non vengono visualizzate le **forme di data mining di Microsoft** nell'elenco **forme** , fare clic su **altre forme**, selezionare **Apri stencil**e aprire il modello dal percorso di installazione predefinito.  
  
     \<unità>: \Program Files (X85) \Microsoft SQL Server 2012 DM Add-ins  
  
2.  Trascinare la forma **albero delle decisioni** nella pagina.  
  
3.  Nella pagina iniziale della **procedura guidata forma di Visio**per l'albero delle decisioni fare clic su **Avanti**.  
  
4.  Nella pagina **Selezione origine dati** della **creazione guidata cluster**scegliere una connessione a un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] server in cui è presente il modello che si desidera visualizzare.  
  
5.  Selezionare un modello di data mining appropriato e fare clic su **Avanti**.  
  
     Questo tipo di diagramma supporta i modelli creati mediante l'algoritmo Decision Trees o Linear Regression.  
  
6.  Nella pagina **Seleziona albero delle decisioni** scegliere un singolo albero da visualizzare.  
  
     Un albero modella le interazioni che portano a un risultato specifico che è stato modellato; Pertanto, anche se il modello contiene più risultati, è possibile visualizzare solo un albero alla volta.  
  
7.  Nella finestra di dialogo **Seleziona albero delle decisioni** è inoltre possibile impostare queste opzioni di rendering:  
  
     **Profondità massima di rendering**  
     Utilizzare questa opzione per controllare il numero di nodi visualizzati.  
  
     Un albero delle decisioni potrebbe avere una gerarchia molto profonda, creando un diagramma che non rientra nella pagina. Utilizzare questo controllo per concentrarsi sui nodi più a sinistra, che sono i più importanti.  
  
     L'impostazione predefinita è tre livelli di nodi.  
  
     **Selezionare il colore e il testo da visualizzare per i valori**  
     Scegliere il colore che rappresenterà ognuno dei risultati. Se non si specificano i colori, questi vengono automaticamente generati utilizzando i colori del tema del video correnti.  
  
8.  Fare clic su **Avanzate** per personalizzare le opzioni seguenti per ogni nodo del diagramma dell'albero delle decisioni.  
  
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
 Dopo aver completato la **procedura guidata forma di Visio**per l'albero delle decisioni, in Visio viene creato un diagramma ad albero nella pagina che visualizza graficamente le regole che portano al risultato stimato.  
  
 È possibile continuare a modificare la forma utilizzando i seguenti controlli per i diagrammi dell'albero delle decisioni:  
  
#### <a name="using-the-decision-tree-option-menus"></a>Utilizzo dei menu delle opzioni dell'albero delle decisioni  
  
1.  Fare clic sulla barra multifunzione **componenti** aggiuntivi e quindi visualizzare una delle barre degli strumenti personalizzate utilizzate per l'utilizzo dei diagrammi data mining:  
  
     **Layout**  
     Consente di ottimizzare la disposizione dell'albero da adattare nella pagina corrente.  
  
     **Ridimensiona pagina**  
     Questo controllo è destinato alle versioni HTML precedenti. Utilizzare invece i controlli per il ridimensionamento della pagina di Visio.  
  
     **Descrizione**  
     Quando è selezionato un nodo dell'albero, fare clic su questa opzione per visualizzare i dettagli sui case nel nodo.  
  
2.  Utilizzare l'opzione **nuova pagina layout** nella barra multifunzione di **progettazione** di Visio per provare layout di struttura ad albero diversi.  
  
3.  Utilizzare l'opzione **connettori** nella scheda **progettazione** per modificare i connettori utilizzati tra i nodi dell'albero.  
  
4.  Utilizzare il controllo **Pan e zoom** , nell'area **riquadro attività** della barra multifunzione **visualizzazione** Visio, per concentrarsi su una particolare area del diagramma.  
  
5.  Fare clic con il pulsante destro del mouse su qualsiasi nodo dell'albero e scegliere tra queste opzioni del menu di scelta rapida specifiche dei diagrammi dell'albero delle decisioni:  
  
     **Ottimizza layout di pagina**  
     Consente di ripartire uniformemente i nodi nella pagina, nonché di modificare la visualizzazione della pagina in modo da includere tutti i nodi.  
  
     **Sposta figli in una nuova pagina**  
     Consente di spostare in una nuova pagina i nodi figlio del nodo attualmente selezionato.  
  
     **Comprimi nodi figlio**  
     Consente di nascondere i nodi figlio del nodo attualmente selezionato.  
  
     **Espandi nodi figlio**  
     Consente di visualizzare i nodi figlio del nodo attualmente selezionato.  
  
## <a name="see-also"></a>Vedere anche  
 [Risoluzione dei problemi relativi ai diagrammi di data mining di Visio &#40;componenti aggiuntivi Data mining di SQL Server&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
