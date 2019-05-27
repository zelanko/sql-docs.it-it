---
title: Sequence Clustering scheda Analisi discriminante tra Cluster (Visualizzatore modello di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.discrimination.f1
ms.assetid: 7dd16479-2633-4f4b-83bf-cf55972a2241
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 914629fca09d4bcffb5ac931316331bbb7e7eebe
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66069141"
---
# <a name="sequence-clustering-cluster-discrimination-tab-mining-model-viewer"></a>Scheda Analisi discriminante tra cluster di Sequence Clustering (Visualizzatore modello di data mining)
  La scheda **Analisi discriminante tra cluster** in **Visualizzatore Microsoft Sequence Clustering** consente di confrontare i cluster selezionati in un modello Sequence Clustering.  
  
 Utilizzare questa vista di un modello Sequence Clustering per confrontare due cluster e vedere quali stati e transizioni sono diversi.  
  
 **Per altre informazioni:** [Algoritmo Microsoft Sequence Clustering](data-mining/microsoft-sequence-clustering-algorithm.md), [visualizzare un modello usando il visualizzatore Microsoft Sequence Clustering](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>Opzioni  
 **Aggiorna contenuto visualizzatore**  
 Consente di ricaricare il modello di data mining nel visualizzatore.  
  
 **Modello di data mining**  
 Fare clic su un modello di data mining da visualizzare contenuto nella struttura di data mining corrente. Il modello di data mining verrà aperto nel visualizzatore associato.  
  
 **Visualizzatore**  
 Consente di scegliere un visualizzatore da utilizzare per l'esplorazione del modello di data mining selezionato. È possibile utilizzare il visualizzatore personalizzato o **Microsoft Generic Content Tree Viewer**. Se disponibili, è anche possibile utilizzare i visualizzatori plug-in.  
  
 **Cluster 1**  
 Consente di selezionare un cluster tra quelli presenti nel modello.  
  
 **Cluster 2**  
 Consente di selezionare un secondo cluster nel modello di data mining per il confronto con **Cluster 1**.  
  
 Se non si seleziona un altro cluster, per impostazione predefinita il cluster selezionato viene confrontato con il complemento, ovvero tutti i case nel modello che non sono presenti in Cluster 1.  
  
 **Punteggi dell'analisi discriminante per \<cluster 1 > e \<2 del cluster >**  
 In questo grafico è disponibile il confronto dettagliato tra i cluster selezionati. In generale, un modello di clustering consente raramente di assegnare stati o valori esclusivamente a un singolo cluster. Pertanto, il visualizzatore indica solo che un attributo o uno stato particolare *predilige* un determinato cluster.  
  
 In generale, in un determinato cluster potrebbero essere contenuti più stati, ad esempio uno stato comune potrebbe essere l'acquisto in sequenza di una bottiglia di acqua e di un relativo contenitore. Tuttavia, la sequenza potrebbe essere presente in altri cluster che dispongono di caratteristiche di definizione più importanti. Ad esempio, un altro cluster potrebbe essere caratterizzato da tempi di transazione molto brevi e un'analisi rivelerebbe che gli elementi [Water Bottle e Water] sono posizionati in modo da essere raggruppati generalmente in questo cluster, ma non sempre.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Variabili**|Un attributo nel modello di data mining.|  
|**Valori**|Uno stato dell'attributo contenuto nell'elenco **Variabili**.|  
|**Predilige \<1 del cluster >**|È contenuta una barra ombreggiata che indica il livello di predilezione dell'attributo e dello stato elencati in **Variabili** e **Valore** per il cluster selezionato in **Cluster 1**.|  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizzatori modello di data mining &#40;Progettazione modelli di data mining&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizzatori modello di data mining](data-mining/data-mining-model-viewers.md)  
  
  
