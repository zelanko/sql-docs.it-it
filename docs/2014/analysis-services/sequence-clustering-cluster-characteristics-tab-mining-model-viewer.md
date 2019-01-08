---
title: Sequence Clustering scheda caratteristiche Cluster (Visualizzatore modello di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.characteristics.f1
ms.assetid: 3a9e8a0c-7d03-47cc-8625-e68d73a8c947
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 156bd83662b9b6fa42eb99e8e5810bb4fc71d51a
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52414850"
---
# <a name="sequence-clustering-cluster-characteristics-tab-mining-model-viewer"></a>Scheda Caratteristiche cluster di Microsoft Sequence Clustering (Visualizzatore modello di data mining)
  Nella scheda **Caratteristiche cluster** in **Visualizzatore Microsoft Sequence Clustering** è disponibile un elenco dettagliato delle caratteristiche che definiscono un cluster di sequenza. In tali caratteristiche possono essere incluse semplici coppie attributo-valore, nonché transizioni tra stati.  
  
 Utilizzare questa vista di un modello Sequence Clustering per eseguire il drill-down nel contenuto del cluster e visualizzare le sequenze rappresentative di un cluster.  
  
 **Per altre informazioni:** [Algoritmo Microsoft Sequence Clustering](data-mining/microsoft-sequence-clustering-algorithm.md), [visualizzare un modello usando il visualizzatore Microsoft Sequence Clustering](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>Opzioni  
 **Aggiorna contenuto visualizzatore**  
 Consente di ricaricare il modello di data mining nel visualizzatore.  
  
 **Modello di data mining**  
 Fare clic su un modello di data mining da visualizzare contenuto nella struttura di data mining corrente. Il modello di data mining verrà aperto nel visualizzatore associato.  
  
 **Visualizzatore**  
 Consente di scegliere un visualizzatore da utilizzare per l'esplorazione del modello di data mining selezionato. È possibile utilizzare il visualizzatore personalizzato o **Microsoft Generic Content Tree Viewer**. Se disponibili, è anche possibile utilizzare i visualizzatori plug-in.  
  
 **Cluster**  
 Consente di scegliere il cluster che si desidera visualizzare.  
  
 **Caratteristiche per \<Cluster >**  
 In questa tabella è disponibile un elenco delle sequenze assegnate al cluster corrente, ordinate per probabilità. Si tenga presente che una sequenza è fondamentalmente una coppia attributo-valore, seguita da una o più coppie attributo-valore aggiuntive. La combinazione di sequenze e le relative probabilità sono le caratteristiche di definizione di ogni cluster.  
  
 Ad esempio, in un modello Sequence Clustering basato su Market basket analysis un cluster potrebbe disporre, come caratteristica principale, di un cliente che sceglie l'elemento di vendita e successivamente termina la transazione senza acquistare nient'altro. In un modello Sequence Clustering che consente di cercare di analizzare gli errori del server, le caratteristiche principali di un cluster potrebbero essere una serie di eventi di errore di frequenza elevata.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Variabile**|In questa colonna viene indicato se la caratteristica è un valore o una transizione.<br /><br /> Se la caratteristica è un valore, il **variabile** colonna contiene il nome dell'attributo.<br /><br /> Se la caratteristica rappresenta una transizione di stato, il **variabile** colonna contiene il testo "Transizioni".|  
|**Valori**|Il valore di questa colonna varia a seconda che la caratteristica sia una semplice coppia attributo-valore o una transizione di stato che rappresenta una sequenza comune di elementi o eventi.<br /><br /> Se la caratteristica è un valore, il **valore** colonna contiene lo stato.<br /><br /> Se la caratteristica rappresenta una transizione di stato, il **valore** colonna contiene la descrizione della transizione di stato.|  
|**Probabilità**|In questa colonna viene visualizzata una barra tramite cui viene indicata la probabilità relativa che questa caratteristica (una semplice coppia attributo-valore o una combinazione di stati) sia membro del cluster corrente.<br /><br /> È possibile posizionare il mouse sulla coppia per visualizzare il valore di frequenza della caratteristica.|  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizzatori modello di data mining &#40;Progettazione modelli di data mining&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizzatori modello di data mining](data-mining/data-mining-model-viewers.md)  
  
  
