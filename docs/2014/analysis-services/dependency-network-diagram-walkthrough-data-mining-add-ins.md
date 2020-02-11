---
title: Procedura dettagliata relativa al diagramma della rete di dipendenze (componenti aggiuntivi Data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Visio shapes, dependency network
- shapes, data mining
- shapes, network
- dependencies
- diagram, dependency network
- data mining layout toolbar
- dependency network
ms.assetid: aac732a8-5262-4649-b7d7-3ccf6f9cfa8b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: db069b243a0d06c142651ab4dcadd68e1e06657f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081964"
---
# <a name="dependency-network-diagram-walkthrough-data-mining-add-ins"></a>Descrizione dettagliata del diagramma della rete di dipendenze (componenti aggiuntivi Data mining)
  In vari tipi differenti di modelli di data mining viene utilizzato un grafico della rete come modalità di esplorazione delle relazioni nei dati. È possibile importare questi modelli in Visio utilizzando la forma **rete di dipendenze** , quindi continuare a personalizzare e migliorare il layout. Nelle **forme di data mining per Visio** sono inclusi i seguenti controlli personalizzati per l'utilizzo di diagrammi di rete di dipendenze:  
  
-   Controlli di rendering per il grafico della rete  
  
     Queste opzioni fanno parte della procedura guidata che viene avviata quando si rilascia una forma nell'area di lavoro di Visio.  
  
-   Barra degli strumenti **Layout data mining**  
  
     Queste opzioni vengono aggiunte all'area di lavoro di Visio per consentire di interagire con il grafico della rete di dipendenze.  
  
## <a name="build-a-dependency-network-graph"></a>Compilazione di un grafico della rete di dipendenze  
 È possibile rilasciare una forma nella pagina Visio per avviare la **procedura guidata forma di Visio per la rete di dipendenze** e impostare le opzioni del diagramma.  
  
#### <a name="use-the-dependency-net-visio-shape-wizard"></a>Utilizzo della Procedura guidata Forma di Visio per rete di dipendenze  
  
1.  Se non vengono visualizzate le **forme di data mining di Microsoft** nell'elenco **forme** , fare clic su **altre forme**, selezionare **Apri stencil**e aprire il modello dal percorso di installazione predefinito.  
  
     \<unità>: \Program Files (X85) \Microsoft SQL Server 2012 DM Add-ins  
  
2.  Trascinare la forma **rete di dipendenze** nella pagina per avviare la procedura guidata. Fare clic su **Avanti**.  
  
3.  Nella pagina iniziale della **procedura guidata forma di Visio per rete di dipendenze**fare clic su **Avanti**.  
  
4.  Nella pagina **Selezione origine dati** della **procedura guidata forma di Visio per rete di dipendenze**scegliere una connessione a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] un server che disponga del modello che si desidera visualizzare.  
  
5.  Selezionare un modello di data mining appropriato e fare clic su **Avanti**.  
  
     Per selezionare un modello appropriato, è possibile esaminare il nome, la descrizione, le colonne e il tipo di dati nel riquadro **Proprietà** .  
  
     Questa forma supporta modelli creati tramite questi algoritmi:  
  
    -   Naive Bayes  
  
    -   Decision Trees  
  
    -   Regole di associazione  
  
6.  Nella pagina selezionare i **nodi di cui eseguire il rendering**, personalizzare le dimensioni del grafico e, facoltativamente, applicare un filtro in modo da includere solo determinati nodi.  
  
     Con un set di dati di grandi dimensioni, un grafico delle dipendenze può diventare grande e contenere molti oggetti correlati, rappresentati come *nodi*. Tramite questa finestra di dialogo, è possibile creare un grafico della rete personalizzato in cui sono inclusi solo i nodi di interesse.  
  
     [segnaposto artistico]  
  
     **Numero di nodi da recuperare**  
     Se nel modello sono contenuti meno nodi rispetto al numero specificato, questa impostazione non avrà effetto. Se nel modello sono contenuti più nodi rispetto al numero specificato, verranno visualizzati solo i nodi più attendibili.  
  
     **Contenuto del nome**  
     Lasciare vuota questa casella e fare clic sulla freccia verde per recuperare tutti i nodi del modello.  
  
     In alternativa, digitare una stringa e fare clic sulla freccia verde per restituire solo i nodi contenenti la stringa specificata.  
  
     La maggior parte dei modelli che è possibile creare con i dati di esempio non è grande, pertanto per questo esempio, aumentare il numero di nodi a 10, quindi fare clic sulla freccia verde per eseguire una query e ottenere un elenco di tutti i nodi.  
  
7.  Fare clic su **Avanzate** per impostare le opzioni di ombreggiatura e forma per il grafico.  
  
8.  Fare clic su **Chiudi** per uscire dalla finestra di dialogo Opzioni **Avanzate** e quindi fare clic su **fine** per creare il grafico.  
  
## <a name="explore-and-modify-the-finished-diagram"></a>Esplorazione e modifica del diagramma completato  
 Dopo aver creato in Visio il grafico della rete di dipendenze, è possibile continuare a modificare e migliorare il grafico utilizzando le funzionalità di Visio.  
  
 Nel grafico seguente viene mostrato il layout predefinito di un grafico della rete di dipendenze.  
  
 [segnaposto artistico]  
  
1.  Utilizzare il controllo **Pan e zoom** , nell'area **riquadro attività** della barra multifunzione **visualizzazione** Visio, per concentrarsi su una sezione del grafico e spostarsi intorno al diagramma.  
  
2.  Provare a usare layout di grafico diversi forniti dall'opzione di **pagina nuovo layout** di Visio.  
  
3.  Fare clic sulla barra multifunzione **componenti** aggiuntivi e quindi visualizzare una delle barre degli strumenti personalizzate utilizzate per l'utilizzo dei diagrammi data mining:  
  
     **Layout**  
     Consente di ottimizzare il layout dei nodi nella pagina, nonché di modificare la visualizzazione in modo da includere tutti i nodi.  
  
     **Ridimensiona pagina**  
     Consente di modificare le dimensioni della pagina in modo da visualizzare tutti i nodi.  
  
     **Livello attendibilità bordo**  
     Consente di attivare e disattivare la visualizzazione del livello di attendibilità bordo per l'intero grafico. Un bordo è un collegamento tra nodi. È possibile utilizzare il controllo dispositivo di scorrimento per escludere tramite filtro i collegamenti non attendibili.  
  
     **Dispositivo di scorrimento**  
     Il **dispositivo di scorrimento** consente di controllare il livello di attendibilità delle relazioni visualizzate nel diagramma della rete di dipendenze.  
  
     Ogni nodo del grafico rappresenta uno stato. Una freccia rappresenta una transizione tra due stati e la probabilità associata alla transizione. Per ridurre il numero di nodi nel grafico, spostare il dispositivo di scorrimento verso l'alto.  
  
     Per aumentare il numero di nodi del grafico, spostare il dispositivo di scorrimento verso il basso.  
  
     **Aggiungi elementi**  
     Apre la finestra di dialogo **Seleziona nodi per il rendering** , in modo che sia possibile selezionare nuovi nodi da aggiungere al grafico.  
  
4.  È possibile rendere i grafici semplici o elaborati come desiderato e aggiungere annotazioni, rimanendo connessi al modello.  
  
     [segnaposto immagine]  
  
> [!WARNING]  
>  L'evidenziazione di nodi dipendenti e altre opzioni del menu di scelta rapida disponibili nelle versioni precedenti dei componenti aggiuntivi non funzionano in Office 2013.  
  
## <a name="see-also"></a>Vedere anche  
 [Risoluzione dei problemi relativi ai diagrammi di data mining di Visio &#40;componenti aggiuntivi Data mining di SQL Server&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
