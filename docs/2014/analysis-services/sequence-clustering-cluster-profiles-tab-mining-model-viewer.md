---
title: Scheda Profili cluster Sequence Clustering (Visualizzatore modello di data mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.profiles.f1
ms.assetid: 44230895-0a42-4032-8d6c-0cdb8a2dbb8c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4f277abea585715f6a3656fffe7672f347233507
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66069100"
---
# <a name="sequence-clustering-cluster-profiles-tab-mining-model-viewer"></a>Scheda Profili cluster Sequence Clustering (Visualizzatore modello di data mining)
  Nella scheda **Profili cluster** in **Visualizzatore Microsoft Sequence Clustering** è disponibile una vista contraddistinta dal colore delle sequenze incluse in ogni cluster.  
  
 Utilizzare questa vista di un modello Sequence Clustering per visualizzare rapidamente la modalità di raggruppamento delle sequenze individuate dal modello. È possibile vedere immediatamente il numero di sequenze lunghe e corte. Inoltre, è possibile fare clic su un cluster e visualizzare **Legenda data mining** per vedere esattamente gli stati rappresentati dai colori in ogni sequenza.  
  
 **Per altre informazioni:**  [Algoritmo Microsoft Sequence Clustering](data-mining/microsoft-sequence-clustering-algorithm.md), [Visualizzare un modello utilizzando il Visualizzatore Microsoft Sequence Clustering](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>Opzioni  
 **Aggiorna contenuto visualizzatore**  
 Consente di ricaricare il modello di data mining nel visualizzatore.  
  
 **Modello di data mining**  
 Fare clic su un modello di data mining da visualizzare contenuto nella struttura di data mining corrente. Il modello di data mining verrà aperto nel visualizzatore associato.  
  
 **Visualizzatore**  
 Consente di scegliere un visualizzatore da utilizzare per l'esplorazione del modello di data mining selezionato. È possibile utilizzare il visualizzatore personalizzato o **Microsoft Generic Content Tree Viewer**. Se disponibili, è anche possibile utilizzare i visualizzatori plug-in.  
  
 **Mostra legenda**  
 Selezionare questa opzione per visualizzare una legenda in cui viene mostrata la correlazione tra i colori visualizzati nei profili di cluster e i valori di testo degli stati.  
  
 **Barre istogramma**  
 Utilizzare questa opzione per modificare il numero di barre colorate incluse nell'istogramma. In caso esistano più barre rispetto a quelle scelte per la visualizzazione, le barre più significative verranno mantenute e le rimanenti verranno raggruppate all'interno di **Altro**.  
  
 **Attributi** e **Profili cluster**  
 In questa sezione del grafico sono elencati i cluster delle sequenze individuate nel modello.  
  
 Ogni cluster di sequenza viene visualizzato utilizzando il numero di stati selezionati nell'opzione **Barre istogramma**.  
  
 Due set di istogrammi vengono visualizzati per ogni cluster nel modello, ognuno in una riga diversa del grafico:  
  
-   **nome attributo>. Samples: gli istogrammi di questa riga mostrano le sequenze di elementi rappresentativi di ogni cluster. \<** In termini DMX, si tratta dei case di esempio per ogni cluster.  
  
-   nome attributo>: gli istogrammi in questa riga descrivono tutti gli elementi contenuti nel cluster e la relativa distribuzione complessiva. ** \< ** Fare clic su un istogramma quando **Legenda data mining** è visibile ed è possibile visualizzare i valori numerici per ognuno  
  
 **Stati**  
 Questa colonna del grafico è facoltativa e può essere visualizzata o rimossa selezionando l'opzione **Mostra legenda** . Tramite la colonna **Stati** è possibile comprendere la correlazione tra stati e colori nell'istogramma dei cluster corrispondente.  
  
## <a name="see-also"></a>Vedi anche  
 [Algoritmi di data mining &#40;Analysis Services-&#41;di data mining](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Algoritmo Microsoft Sequence Clustering](data-mining/microsoft-sequence-clustering-algorithm.md)   
 [Visualizzatori modello di data mining &#40;Progettazione modelli di data mining&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizzatori modello di data mining](data-mining/data-mining-model-viewers.md)   
 [Visualizzare un modello usando il Visualizzatore Microsoft Sequence Clustering](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
  
