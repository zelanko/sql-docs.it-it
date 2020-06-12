---
title: Procedura dettagliata relativa al diagramma dei cluster (componenti aggiuntivi Data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
ms.openlocfilehash: 578b5b8e55fd3ae660db985eed2e608667dc768b
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527487"
---
# <a name="cluster-diagram-walkthrough-data-mining-add-ins"></a>Descrizione dettagliata del diagramma cluster (componenti aggiuntivi Data mining)
  Dopo aver creato un modello di clustering, è possibile importarlo in Visio utilizzando la forma **cluster** e quindi continuare a personalizzare e migliorare il layout. Nelle **forme di data mining per Visio** sono inclusi i seguenti controlli personalizzati per l'utilizzo di diagrammi data mining:  
  
-   Controlli di rendering per il diagramma dei cluster  
  
     Queste opzioni fanno parte della **procedura guidata cluster** avviata quando si rilascia una forma nell'area di lavoro di Visio.  
  
-   Barra degli strumenti **Layout data mining**  
  
     Queste opzioni vengono aggiunte all'area di lavoro di Visio per consentire di interagire con la forma di data mining. Le opzioni variano a seconda del tipo di modello di data mining utilizzato.  
  
## <a name="build-a-cluster-diagram"></a>Creazione del diagramma di un cluster  
 In questa procedura dettagliata viene illustrato come creare e personalizzare un diagramma di clustering in Visio.  
  
 Per proseguire, è necessario avere un modello di clustering già disponibile. Se non si dispone di un modello, utilizzare la [procedura guidata Cluster &#40;componenti aggiuntivi Data mining per la procedura guidata&#41;di Excel](cluster-wizard-data-mining-add-ins-for-excel.md) e creare un modello utilizzando il set di dati di training nella cartella di lavoro di esempio, utilizzando tutte le impostazioni predefinite.  
  
#### <a name="use-the-cluster-visio-shape-wizard"></a>Utilizzo della Procedura guidata Forma di Visio per cluster  
  
1.  Se non vengono visualizzate le **forme di data mining di Microsoft** nell'elenco **forme** , fare clic su **altre forme**, selezionare **Apri stencil**e aprire il modello dal percorso di installazione predefinito.  
  
     \<drive>: \Programmi\Microsoft SQL Server 2012 DM Add-ins  
  
2.  Trascinare la forma **cluster** nella pagina.  
  
3.  Nella pagina iniziale della **procedura guidata forma di Visio per cluster**fare clic su **Avanti**.  
  
4.  Nella pagina **Selezione origine dati** della **creazione guidata cluster**scegliere una connessione a un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] server contenente i modelli di data mining che si desidera visualizzare.  
  
5.  Selezionare un modello di data mining appropriato e fare clic su **Avanti**.  
  
     Per assicurarsi di scegliere un modello di clustering, esaminare la descrizione nel riquadro **Proprietà** .  
  
6.  Se la connessione ha esito positivo, nella pagina **Opzioni per diagramma cluster**si decide il tipo di diagramma del cluster da includere nella presentazione di Visio:  
  
     **Mostra solo forme del cluster**  
     Questa opzione consente di creare un semplice diagramma dei cluster, dove ogni cluster è rappresentato da un rettangolo o un'altra forma scelta.  
  
     **Mostra cluster con grafico delle caratteristiche**  
     Questa opzione consente di creare lo stesso grafico precedente, ma all'interno delle forme sono presenti istogrammi in cui vengono descritte le caratteristiche del cluster.  
  
     ![Esempio di grafico delle caratteristiche del cluster in Visio](media/dm13-visio-cluster-samplecharshape.gif "Esempio di grafico delle caratteristiche del cluster in Visio")  
  
     **Mostra cluster con grafico analisi discriminante**  
     Questa opzione consente di creare lo stesso grafico del diagramma dei cluster, ma anche di elencare le caratteristiche del cluster corrente che lo distinguono maggiormente dagli altri.  
  
     È possibile passare a un altro tipo di grafico dopo che è stato creato il diagramma tramite la procedura guidata, facendo clic con il pulsante destro del mouse su un cluster e selezionando un nuovo tipo di grafico. Per il momento, scegliere l'opzione **Mostra cluster con grafico delle caratteristiche**.  
  
7.  Lasciare l'opzione, **numero di righe nel grafico**, come 5.  
  
     Questa opzione non consente di modificare il numero di cluster nel modello. limita semplicemente il numero di attributi che possono essere visualizzati come funzionalità di ogni cluster.  
  
     Tuttavia, l'opzione funge da filtro sui dati del grafico, pertanto non è possibile aumentare il numero di elementi in un secondo momento.  
  
8.  Fare clic su **Avanzate**.  
  
     La finestra di dialogo **Opzioni cluster** consente di personalizzare l'aspetto visivo delle forme utilizzate nel diagramma. È possibile modificare i colori utilizzati nel grafico e la forma utilizzata per i cluster.  
  
     Il controllo **Variabile ombreggiatura** non funziona in Office 2013.  
  
     ![Fare clic su Avanzate per scegliere i colori delle forme](media/dm13-visio-clusteroptions-advanced.gif "Fare clic su Avanzate per scegliere i colori delle forme")  
  
     **Suggerimento:** Alcuni colori possono essere modificati in un secondo momento usando i temi di Visio e i controlli di modifica della forma. Tuttavia, i temi di Visio sostituiranno anche alcune di queste selezioni dei colori, pertanto è consigliabile iniziare con colori predefiniti e gradualmente applicare le modifiche.  
  
9. Fare clic su **fine** per creare il grafico.  
  
     La procedura guidata consente di recuperare le informazioni dal modello di data mining, eseguire il rendering delle forme e popolare ciascun cluster con attributi e valori.  
  
     ![Rete di dipendenze](media/dm13-visiodepnet-defaultgraph.gif "Rete di dipendenze")  
  
## <a name="explore-and-modify-the-finished-diagram"></a>Esplorazione e modifica del diagramma completato  
 Dopo che il diagramma è stato completato, è possibile continuare a personalizzare l'aspetto utilizzando i controlli di Visio, come illustrato nell'esempio seguente.  
  
 ![Diagramma dei cluster personalizzato mediante Visio](media/dm13-visio-clustercomplete1.gif "Diagramma dei cluster personalizzato mediante Visio")  
  
 Tutte le forme di base del cluster vengono generate dalla procedura guidata; utilizzare gli strumenti seguenti per aggiornare e personalizzare il diagramma:  
  
1.  Trascinare il dispositivo di scorrimento nel controllo delle **Opzioni del cluster** per filtrare le relazioni più vulnerabili e semplificare il diagramma.  
  
2.  Usare l'opzione **rilayout della pagina** di Visio per provare i diversi layout del cluster.  
  
3.  Utilizzare l'opzione **connettori** nella scheda **progettazione** per modificare lo stile del connettore in modo da evitare che le linee attraversino i cluster.  
  
4.  Fare clic sulla barra multifunzione **componenti** aggiuntivi e quindi visualizzare una delle barre degli strumenti personalizzate utilizzate per l'utilizzo dei diagrammi data mining:  
  
     **Layout**  
     Consente di ottimizzare la disposizione dei cluster da adattare nella pagina corrente.  
  
     **Ridimensiona pagina**  
     Questo controllo è destinato alle versioni HTML precedenti. Utilizzare invece i controlli per il ridimensionamento della pagina di Visio.  
  
     **Descrizione**  
     Se viene selezionato un cluster, fare clic su questa opzione per visualizzare i dettagli sul cluster.  
  
     ![Fare clic su Descrizione per informazioni dettagliate sul cluster](media/dm13-visio-cluster-description-control.gif "Fare clic su Descrizione per informazioni dettagliate sul cluster")  
  
     **Livello attendibilità bordo**  
     Consente di visualizzare i punteggi di confidenza sulle linee che connettono i cluster.  
  
     Tuttavia, se si applica una qualsiasi formattazione speciale diversa da quella predefinita generata dalla procedura guidata, inclusi alcuni sfondi, questi numeri potrebbero non essere visibili.  
  
     **Dispositivo di scorrimento**  
     Consente di filtrare le linee tra i cluster. Spostando il dispositivo di scorrimento verso l'alto vengono rimosse tutte le associazioni tranne quelle più importanti.  
  
     **Ombreggiatura**  
     Questo controllo non funziona in Office 2013.  
  
5.  Utilizzare il controllo **Pan e zoom** , nell'area **riquadro attività** della barra multifunzione **visualizzazione** Visio, per concentrarsi su un set di cluster e spostarsi intorno al diagramma.  
  
6.  Fare clic con il pulsante destro del mouse su un qualsiasi cluster per visualizzare le opzioni specifiche della forma del cluster:  
  
    -   Modificare lo stile del grafico.  
  
    -   Aggiungere un grafico delle caratteristiche del cluster.  
  
    -   Aggiungere un grafico dell'analisi discriminante del cluster.  
  
## <a name="see-also"></a>Vedere anche  
 [Risoluzione dei problemi relativi ai diagrammi di data mining di Visio &#40;componenti aggiuntivi Data mining di SQL Server&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
