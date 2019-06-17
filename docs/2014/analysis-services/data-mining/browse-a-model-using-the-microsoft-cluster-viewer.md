---
title: Visualizzare un modello usando il visualizzatore Microsoft Clustering | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clusters [Analysis Services]
- discrimination [Analysis Services]
- names [Analysis Services], clusters
- Microsoft Cluster Viewer
- mining model content, viewing
- comparing clusters
- viewing clusters
- displaying clusters
- data mining [Analysis Services], clusters
- Cluster Viewer [Analysis Services]
- mining models [Analysis Services], clusters
ms.assetid: 591fe30b-d88f-4a71-94d4-4a3907fc275d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e13882cf6186632b893b18369aef263e6cdd6445
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086044"
---
# <a name="browse-a-model-using-the-microsoft-cluster-viewer"></a>Visualizzare un modello utilizzando il Visualizzatore Microsoft Clustering
  Il Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering disponibile in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consente di visualizzare i modelli di data mining compilati con l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering. L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering è un algoritmo di segmentazione da usare per l'esplorazione dei dati al fine di identificare eventuali anomalie e creare stime. Per altre informazioni su questo algoritmo, vedere [Algoritmo Microsoft Clustering](microsoft-clustering-algorithm.md).  
  
> [!NOTE]  
>  Per visualizzare informazioni dettagliate sulle equazioni utilizzate nel modello e sui modelli individuati, utilizzare il visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Generic Content Tree Viewer. Per altre informazioni, vedere [Visualizzare un modello usando Microsoft Generic Content Tree Viewer](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) o [Microsoft Generic Content Tree Viewer &#40;Data mining&#41;](../microsoft-generic-content-tree-viewer-data-mining.md).  
  
##  <a name="BKMK_ViewerTabs"></a> Schede del visualizzatore  
 Per la visualizzazione di un modello di data mining in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]viene utilizzato il visualizzatore appropriato nella scheda **Visualizzatore modello di data mining** di Progettazione modelli di data mining. Per l'esplorazione di modelli di data mining per il clustering, nel Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering sono disponibili le schede seguenti:  
  
-   [Diagramma dei cluster](#BKMK_Diagram)  
  
-   [Profili cluster](#BKMK_Profile)  
  
-   [Caratteristiche cluster](#BKMK_Characteristics)  
  
-   [Analisi discriminante tra cluster](#BKMK_Discrimination)  
  
###  <a name="BKMK_Diagram"></a> Diagramma dei cluster  
 Nella scheda **Diagramma dei cluster** del Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering vengono visualizzati tutti i cluster di un modello di data mining. L'ombreggiatura della linea che collega un cluster all'altro rappresenta il grado di somiglianza dei cluster. Se l'ombreggiatura è chiara o inesistente, il grado di somiglianza dei cluster è basso. Man mano che la linea diventa più scura, il grado di somiglianza dei collegamenti aumenta. È possibile modificare il numero di linee visualizzate regolando il dispositivo di scorrimento a destra dei cluster. Se si sposta il dispositivo di scorrimento verso il basso, vengono visualizzati solo i collegamenti più attendibili.  
  
 Per impostazione predefinita, l'ombreggiatura rappresenta la popolazione del cluster. Tramite il **Variabileombreggiatura** e **stato** opzioni, è possibile selezionare quale attributo e la coppia di stati è l'ombreggiatura rappresenta. Più scura è l'ombreggiatura, maggiore è la distribuzione dell'attributo per uno stato specifico. La distribuzione diminuisce man mano che l'ombreggiatura diventa più chiara.  
  
 Per rinominare un cluster, fare clic con il pulsante destro del mouse sul nodo corrispondente e scegliere **Rinomina cluster**. Il nuovo nome è persistente nel server.  
  
 Per copiare la sezione visibile del diagramma negli Appunti, fare clic su **Copia parte visibile del grafico**. Per copiare il diagramma completo, fare clic su **Copia grafico intero**. È anche possibile ingrandire o ridurre il diagramma tramite **Zoom avanti** e **Zoom indietro**oppure adattarlo alla schermata tramite **Ridimensiona e adatta il diagramma alla finestra**.  
  
 [Torna all'inizio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Profile"></a> Profili cluster  
 La scheda **Profili cluster** offre una vista globale dei cluster creati dall'algoritmo nel modello. Tale vista include ogni attributo, insieme alla relativa distribuzione in ogni cluster. In una finestra popup relativa a ogni cella vengono visualizzate le statistiche di distribuzione, mentre in una finestra popup relativa a ogni intestazione di colonna viene visualizzata la popolazione del cluster. Gli attributi discreti vengono visualizzati come barre colorate, mentre gli attributi continui vengono visualizzati come un grafico a rombi che rappresenta la deviazione media e standard in ogni cluster. L'opzione **Barre istogramma** consente di controllare il numero di barre visibili nell'istogramma. Se esiste un numero di barre superiore a quello che si sceglie di visualizzare, le barre più importanti vengono mantenute mentre le barre rimanenti vengono raggruppate in un bucket grigio.  
  
 È possibile modificare i nomi predefiniti dei cluster in modo da renderli più descrittivi. Per rinominare un cluster, fare clic con il pulsante destro del mouse sull'intestazione di colonna corrispondente e scegliere **Rinomina cluster**. È anche possibile nascondere i cluster selezionando **Nascondi colonna**.  
  
 Per aprire una finestra contenente una visualizzazione più grande e dettagliata dei cluster, fare doppio clic su una cella nella colonna **Stati** o su un istogramma nel visualizzatore.  
  
 Fare clic su un'intestazione di colonna per disporre gli attributi in ordine di importanza per il cluster. È inoltre possibile trascinare le colonne per riordinarle nel visualizzatore.  
  
 [Torna all'inizio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Characteristics"></a> Caratteristiche cluster  
 Per usare la scheda **Caratteristiche cluster** , selezionare un cluster dall'elenco **Cluster** . Dopo aver selezionato un cluster, è possibile esaminare le caratteristiche del cluster specifico. Gli attributi contenuti nel cluster sono elencati nelle colonne **Variabili** , mentre lo stato di ogni attributo è elencato nella colonna **Valori** . Gli stati degli attributi sono elencati in ordine di importanza, in base alla probabilità che vengano inclusi nel cluster. La probabilità è indicata nella colonna **Probabilità** .  
  
 [Torna all'inizio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Discrimination"></a> Analisi discriminante tra cluster  
 La scheda **Analisi discriminante tra cluster** consente di confrontare gli attributi di due cluster. Per selezionare i cluster da confrontare, usare gli elenchi **Cluster 1** e **Cluster 2** . Il visualizzatore determina le differenze più importanti tra i cluster e mostra gli stati degli attributi associati alle differenze, in ordine di importanza. Una barra a destra dell'attributo indica il cluster che lo stato predilige e le dimensioni della barra indicano, in proporzione, quanto lo predilige.  
  
 [Torna all'inizio](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmo Microsoft Clustering](microsoft-clustering-algorithm.md)   
 [Attività e procedure relative al visualizzatore modello di data mining](mining-model-viewer-tasks-and-how-tos.md)   
 [Attività e procedure relative al visualizzatore modello di data mining](mining-model-viewer-tasks-and-how-tos.md)   
 [Strumenti di data mining](data-mining-tools.md)   
 [Visualizzatori modello di data mining](data-mining-model-viewers.md)  
  
  
