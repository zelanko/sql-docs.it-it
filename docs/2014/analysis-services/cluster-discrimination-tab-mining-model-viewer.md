---
title: Scheda Analisi discriminante tra cluster (Visualizzatore modello di data mining) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087903"
---
# <a name="cluster-discrimination-tab-mining-model-viewer"></a>Scheda Analisi discriminante tra cluster (Visualizzatore modello di data mining)
  Usare la scheda **Analisi discriminante tra cluster** per confrontare due cluster esistenti in un modello di clustering. È possibile vedere la modalità di rappresentazione di combinazioni diverse di attributi e valori all'interno dei cluster.  
  
 **Per ulteriori informazioni:** [algoritmo Microsoft Clustering](data-mining/microsoft-clustering-algorithm.md), [visualizzare un modello utilizzando il Visualizzatore Microsoft Clustering](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
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
  
 **Punteggi di analisi \<discriminante per cluster \<1> e cluster 2>**  
 Nelle colonne del grafico vengono fornite informazioni sulle modalità di correlazione tra ogni coppia attributo-valore e i due cluster selezionati.  
  
|||  
|-|-|  
|**Variabili**|Un attributo nel modello di data mining.|  
|**Valori**|Un valore dell'attributo selezionato in **Variabili**.|  
|**Predilige \<il cluster 1>**|Il grafico a barre a sinistra rappresenta la probabilità che la coppia attributo-valore selezionata sia rappresentativa del cluster selezionato in **Cluster 1**. È possibile posizionare il mouse sulla barra per vedere il valore rappresentato in percentuale. Si noti che, anche se il valore è zero, non significa che il valore dell'attributo è necessariamente mancante dal cluster, solo che la distribuzione predilige fortemente un cluster rispetto all'altro.|  
|**Predilige \<il cluster 2>**|Il grafico a barre a destra rappresenta la probabilità che la coppia attributo-valore selezionata sia rappresentativa del cluster selezionato in **Cluster 2**.|  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmi di data mining &#40;Analysis Services-&#41;di data mining](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizzatori modello di data mining &#40;Progettazione modelli di data mining&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizzatori modello di data mining](data-mining/data-mining-model-viewers.md)  
  
  
