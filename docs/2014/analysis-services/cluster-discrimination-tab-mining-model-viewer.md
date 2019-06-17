---
title: Scheda Analisi discriminante (Visualizzatore modello di Data Mining) del cluster | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.clustering.discrimination.f1
ms.assetid: ae7cfff7-ab1c-4cf5-9a91-97b21d15d85f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1d55f61d9255d19f22fffb7380785a2ada1a2763
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087903"
---
# <a name="cluster-discrimination-tab-mining-model-viewer"></a>Scheda Analisi discriminante tra cluster (Visualizzatore modello di data mining)
  Usare la scheda **Analisi discriminante tra cluster** per confrontare due cluster esistenti in un modello di clustering. È possibile vedere la modalità di rappresentazione di combinazioni diverse di attributi e valori all'interno dei cluster.  
  
 **Per altre informazioni:** [Algoritmo Microsoft Clustering](data-mining/microsoft-clustering-algorithm.md), [visualizzare un modello usando il visualizzatore Microsoft Clustering](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
## <a name="options"></a>Opzioni  
 **Aggiorna contenuto visualizzatore**  
 Consente di ricaricare il modello di data mining nel visualizzatore.  
  
 **Modello di data mining**  
 Consente di scegliere un modello di data mining tra quelli presenti nella struttura di data mining corrente. Il modello di data mining verrà aperto nel visualizzatore associato.  
  
 **Visualizzatore**  
 Consente di scegliere un visualizzatore da utilizzare per l'esplorazione del modello di data mining selezionato. È possibile usare il visualizzatore personalizzato per i modelli di data mining o il Visualizzatore contenuto di data mining [!INCLUDE[msCoName](../includes/msconame-md.md)] . Se disponibili, è anche possibile utilizzare i visualizzatori plug-in.  
  
 **Cluster 1**  
 Consente di selezionare un cluster per poter confrontarlo con un altro cluster.  
  
 **Cluster 2**  
 Consente di selezionare un secondo cluster dal relativo elenco nel modello di data mining per il confronto con **Cluster 1**. È inoltre possibile confrontare un cluster con il complemento, ovvero con tutti i case del modello eccetto quelli presenti nel cluster selezionato.  
  
 **Punteggi dell'analisi discriminante per \<cluster 1 > e \<2 del cluster >**  
 Nelle colonne del grafico vengono fornite informazioni sulle modalità di correlazione tra ogni coppia attributo-valore e i due cluster selezionati.  
  
|||  
|-|-|  
|**Variabili**|Un attributo nel modello di data mining.|  
|**Valori**|Un valore dell'attributo selezionato in **Variabili**.|  
|**Predilige \<1 del cluster >**|Il grafico a barre a sinistra rappresenta la probabilità che la coppia attributo-valore selezionata sia rappresentativa del cluster selezionato in **Cluster 1**. È possibile posizionare il mouse sulla barra per vedere il valore rappresentato in percentuale. Si noti che anche se il valore è zero, questo non significa che il valore dell'attributo è necessariamente mancano dal cluster, solo che la distribuzione prediletto fortemente un cluster rispetto a un altro.|  
|**Predilige \<2 del cluster >**|Il grafico a barre a destra rappresenta la probabilità che la coppia attributo-valore selezionata sia rappresentativa del cluster selezionato in **Cluster 2**.|  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizzatori modello di data mining &#40;Progettazione modelli di data mining&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizzatori modello di data mining](data-mining/data-mining-model-viewers.md)  
  
  
