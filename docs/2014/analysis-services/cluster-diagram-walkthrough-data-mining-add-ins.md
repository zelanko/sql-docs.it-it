---
title: Descrizione dettagliata del diagramma (componenti aggiuntivi Data Mining dei dati) del cluster | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Visio shapes, cluster
- diagram, cluster
- shapes, data mining
- shapes, cluster
- data mining layout toolbar
ms.assetid: 761bef6a-37d4-4b19-944e-f2aadc75a242
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ee4a7a09471078753589463c058ba5ea2e39c4d2
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52420005"
---
# <a name="cluster-diagram-walkthrough-data-mining-add-ins"></a>Descrizione dettagliata del diagramma cluster (componenti aggiuntivi Data mining)
  Dopo aver creato un modello di clustering, è possibile importarlo in Visio utilizzando la **Cluster** il data shaping e quindi continuare a personalizzare e migliorare il layout. Il **forme di Data Mining per Visio** includono i seguenti controlli personalizzati per l'uso di diagrammi di data mining:  
  
-   Controlli di rendering per il diagramma dei cluster  
  
     Queste opzioni fanno parte del **Creazione guidata Cluster** che viene avviata quando si rilascia una forma nell'area di lavoro di Visio.  
  
-   **Layout Data Mining** sulla barra degli strumenti  
  
     Queste opzioni vengono aggiunte all'area di lavoro di Visio per consentire di interagire con la forma di data mining. Le opzioni variano a seconda del tipo di modello di data mining utilizzato.  
  
## <a name="build-a-cluster-diagram"></a>Creazione del diagramma di un cluster  
 In questa procedura dettagliata viene illustrato come creare e personalizzare un diagramma di clustering in Visio.  
  
 Per proseguire, è necessario avere un modello di clustering già disponibile. Se non è un modello, usare il [Creazione guidata Cluster &#40;aggiuntivi di Data Mining per Excel&#41; ](cluster-wizard-data-mining-add-ins-for-excel.md) guidata e creare un modello usando il set di dati di Training nella cartella di lavoro di esempio, usando tutte le impostazioni predefinite.  
  
#### <a name="use-the-cluster-visio-shape-wizard"></a>Utilizzo della Procedura guidata Forma di Visio per cluster  
  
1.  Se non viene visualizzata **forme Microsoft Data Mining** nel **forme** fare clic su **più forme**, selezionare **Apri Stencil**e aprire la modello dal percorso di installazione predefinito.  
  
     \<unità >: \Programmi\Microsoft SQL Server 2012 DM Add-Ins  
  
2.  Trascinare il **Cluster** la forma nella pagina.  
  
3.  Nella pagina di benvenuto del **procedura guidata forma di Visio Cluster**, fare clic su **successivo**.  
  
4.  Nel **Vybrat Zdroj** pagina del **guidata Cluster**, scegliere una connessione a un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] server che contiene i modelli di data mining da visualizzare.  
  
5.  Selezionare un modello di data mining appropriato e fare clic su **successivo**.  
  
     Per assicurarsi di scegliere un modello di clustering, esaminare la descrizione nella finestra di **proprietà** riquadro.  
  
6.  Se la connessione ha esito positivo, nella pagina **opzioni per il diagramma cluster**, si decide quale tipo di diagramma dei cluster da includere nella presentazione di Visio:  
  
     **Mostra solo forme del cluster**  
     Questa opzione consente di creare un semplice diagramma dei cluster, dove ogni cluster è rappresentato da un rettangolo o un'altra forma scelta.  
  
     **Mostra cluster con grafico delle caratteristiche**  
     Questa opzione consente di creare lo stesso grafico precedente, ma all'interno delle forme sono presenti istogrammi in cui vengono descritte le caratteristiche del cluster.  
  
     ![Esempio di grafico delle caratteristiche del cluster in Visio](media/dm13-visio-cluster-samplecharshape.gif "esempio di grafico delle caratteristiche del cluster in Visio")  
  
     **Mostra cluster con grafico analisi discriminante**  
     Questa opzione consente di creare lo stesso grafico del diagramma dei cluster, ma anche di elencare le caratteristiche del cluster corrente che lo distinguono maggiormente dagli altri.  
  
     È possibile passare a un altro tipo di grafico dopo che è stato creato il diagramma tramite la procedura guidata, facendo clic con il pulsante destro del mouse su un cluster e selezionando un nuovo tipo di grafico. Per il momento, scegliere l'opzione **Mostra cluster con grafico delle caratteristiche**.  
  
7.  Lasciare l'opzione **numero di righe nel grafico**, pari a 5.  
  
     Questa opzione non modifica il numero di cluster nel modello. limita semplicemente il numero di attributi che possono essere visualizzati come caratteristiche di ogni cluster.  
  
     Tuttavia, l'opzione agisce come un filtro sui dati del grafico, in modo che non è possibile aumentare il numero di elementi in un secondo momento.  
  
8.  Fare clic su **Avanzate**.  
  
     Il **opzioni Cluster** nella finestra di dialogo è possibile personalizzare l'aspetto visivo delle forme utilizzate nel diagramma. È possibile modificare i colori utilizzati nel grafico e la forma utilizzata per i cluster.  
  
     Il **variabile ombreggiatura** controllo non funziona in Office 2013.  
  
     ![Fare clic su Avanzate per scegliere i colori delle forme](media/dm13-visio-clusteroptions-advanced.gif "fare clic su Avanzate per scegliere i colori delle forme")  
  
     **Suggerimento:** Alcuni colori possono essere modificati in un secondo momento usando i temi di Visio e i controlli di modifica della forma. Tuttavia, i temi di Visio sostituiranno anche alcune di queste selezioni dei colori, pertanto è consigliabile iniziare con colori predefiniti e gradualmente applicare le modifiche.  
  
9. Fare clic su **fine** per creare il grafico.  
  
     La procedura guidata consente di recuperare le informazioni dal modello di data mining, eseguire il rendering delle forme e popolare ciascun cluster con attributi e valori.  
  
     ![una rete di dipendenze](media/dm13-visiodepnet-defaultgraph.gif "una rete di dipendenze")  
  
## <a name="explore-and-modify-the-finished-diagram"></a>Esplorazione e modifica del diagramma completato  
 Dopo che il diagramma è stato completato, è possibile continuare a personalizzare l'aspetto utilizzando i controlli di Visio, come illustrato nell'esempio seguente.  
  
 ![diagramma dei cluster personalizzato mediante Visio](media/dm13-visio-clustercomplete1.gif "diagramma dei cluster personalizzato mediante Visio")  
  
 Tutte le forme di base del cluster vengono generate dalla procedura guidata; utilizzare gli strumenti seguenti per aggiornare e personalizzare il diagramma:  
  
1.  Trascinare il dispositivo di scorrimento **opzioni Cluster** controllo, per filtrare le relazioni meno attendibili e semplificare il diagramma.  
  
2.  Utilizzare Visio **nuovo Layout pagina** opzione per provare layout di cluster diverso.  
  
3.  Usare la **connettori** opzione il **progettazione** pressione di tab per modificare lo stile del connettore per impedire alle righe di incrociare i cluster.  
  
4.  Scegliere il **Add-Ins** della barra multifunzione e quindi visualizzare una delle barre degli strumenti personalizzate utilizzate per l'uso di diagrammi di data mining:  
  
     **Layout**  
     Consente di ottimizzare la disposizione dei cluster da adattare nella pagina corrente.  
  
     **Ridimensiona pagina**  
     Questo controllo è destinato alle versioni HTML precedenti. Utilizzare invece i controlli per il ridimensionamento della pagina di Visio.  
  
     **Descrizione**  
     Se viene selezionato un cluster, fare clic su questa opzione per visualizzare i dettagli sul cluster.  
  
     ![Fare clic su descrizione per ottenere i dettagli relativi al cluster](media/dm13-visio-cluster-description-control.gif "fare clic su descrizione per informazioni dettagliate sul cluster")  
  
     **Livello attendibilità bordo**  
     Consente di visualizzare i punteggi di confidenza sulle linee che connettono i cluster.  
  
     Tuttavia, se si applica una qualsiasi formattazione speciale diversa da quella predefinita generata dalla procedura guidata, inclusi alcuni sfondi, questi numeri potrebbero non essere visibili.  
  
     **Dispositivo di scorrimento**  
     Consente di filtrare le linee tra i cluster. Spostando il dispositivo di scorrimento verso l'alto vengono rimosse tutte le associazioni tranne quelle più importanti.  
  
     **Ombreggiatura**  
     Questo controllo non funziona in Office 2013.  
  
5.  Usare la **panoramica e Zoom** controllo la **riquadro attività** area di Visio **visualizzazione** della barra multifunzione, per concentrarsi su un set di cluster e spostarsi nel diagramma.  
  
6.  Fare clic con il pulsante destro del mouse su un qualsiasi cluster per visualizzare le opzioni specifiche della forma del cluster:  
  
    -   Modificare lo stile del grafico.  
  
    -   Aggiungere un grafico delle caratteristiche del cluster.  
  
    -   Aggiungere un grafico dell'analisi discriminante del cluster.  
  
## <a name="see-also"></a>Vedere anche  
 [Risoluzione dei problemi di diagrammi di Visio Data Mining &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
