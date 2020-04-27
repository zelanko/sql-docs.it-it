---
title: Scheda Profili cluster (Visualizzatore modello di data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.clustering.profiles.f1
ms.assetid: 1ebafa1f-74e9-4c05-b278-a690fa8543bd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ebed4b2b7cc5c6496ab0c681450897a477e4707a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66087865"
---
# <a name="cluster-profiles-tab-mining-model-viewer"></a>Scheda Profili cluster (Visualizzatore modello di data mining)
  Usare la scheda **Profili cluster** per una vista complessiva dei cluster individuati dall'algoritmo all'interno di un modello di clustering. In questa scheda viene visualizzato ogni attributo, insieme alla relativa distribuzione in ciascun cluster.  
  
 **Per altre informazioni:** [Algoritmo Microsoft Clustering](data-mining/microsoft-clustering-algorithm.md), [Visualizzare un modello usando il Visualizzatore Microsoft Clustering](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
## <a name="options"></a>Opzioni  
 **Aggiorna contenuto visualizzatore**  
 Consente di ricaricare il modello di data mining nel visualizzatore.  
  
 **Modello di data mining**  
 Consente di scegliere un modello di data mining tra quelli presenti nella struttura di data mining corrente. Il modello di data mining verrà aperto nel visualizzatore associato.  
  
 **Visualizzatore**  
 Consente di scegliere un visualizzatore da utilizzare per la visualizzazione del modello di data mining selezionato. È possibile utilizzare il visualizzatore personalizzato per il modello di data mining o il Visualizzatore contenuto di data mining [!INCLUDE[msCoName](../includes/msconame-md.md)] . Se disponibili, è anche possibile utilizzare i visualizzatori plug-in.  
  
 **Mostra legenda**  
 Selezionare questa opzione per visualizzare una chiave in cui viene mostrato il mapping dei colori nel visualizzatore ai valori nella colonna **Stati** .  
  
 **Barre istogramma**  
 Modificare questo valore per controllare il numero di stati inclusi in ogni istogramma. Se esistono più stati di quelli scelti per la visualizzazione, gli stati con la probabilità più elevata vengono mostrati nell'istogramma, mentre quelli rimanenti vengono raggruppati in **Altro**.  
  
 **Attributi**  
 Vengono elencate le colonne presenti nel modello di clustering. Negli istogrammi per ogni attributo viene mostrata la modalità di distribuzione dell'attributo tra i cluster identificati dall'algoritmo.  
  
 **Stati**  
 Viene fornita una chiave che indica il colore che rappresenta ogni stato nella riga corrispondente di cluster o un dispositivo di scorrimento con diamante che indica la distribuzione di valori numerici continui. È possibile mostrare o nascondere questa colonna tramite la casella di controllo **Mostra legenda** .  
  
 **Profili cluster**  
 In questa sezione è contenuta una colonna per ogni cluster nel modello. Per ogni attributo, nell'istogramma viene mostrata la distribuzione dei valori nell'attributo solo per tale cluster. Nel grafico è inoltre disponibile una colonna per **Popolazione**in cui vengono usati gli istogrammi per visualizzare la distribuzione dei valori per ogni attributo, ma per tutti i case nel modello.  
  
## <a name="see-also"></a>Vedi anche  
 [Algoritmi di data mining &#40;Analysis Services-&#41;di data mining](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizzatori modello di data mining &#40;Progettazione modelli di data mining&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizzatori modello di data mining](data-mining/data-mining-model-viewers.md)  
  
  
