---
title: Scheda albero delle decisioni (Visualizzatore modello di data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.decisiontree.f1
ms.assetid: dc88606f-ba7c-4f8d-af65-bfa17ec16e2b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cee721aca66f5266a29d3bf61babf9060e9aef32
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66082294"
---
# <a name="decision-tree-tab-mining-model-viewer"></a>Scheda Albero delle decisioni (Visualizzatore modello di data mining)
  Nel riquadro **Albero delle decisioni** è disponibile una rappresentazione visiva delle regole delle decisioni create in un modello di albero delle decisioni. Nelle regole delle decisioni viene descritto il percorso verso un determinato risultato.  
  
 **Per altre informazioni:** [Algoritmo Microsoft Decision Trees](data-mining/microsoft-decision-trees-algorithm.md), [Visualizzare un modello utilizzando il Visualizzatore Microsoft Decision Trees](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
## <a name="options"></a>Opzioni  
 **Aggiorna contenuto visualizzatore**  
 Consente di ricaricare il modello di data mining nel visualizzatore.  
  
 **Modello di data mining**  
 Consente di scegliere un modello di data mining tra quelli presenti nella struttura di data mining corrente. Il modello di data mining verrà aperto nel visualizzatore associato.  
  
 **Visualizzatore**  
 Consente di scegliere un visualizzatore da utilizzare per l'esplorazione del modello di data mining selezionato. È possibile usare il visualizzatore personalizzato o il Visualizzatore contenuto di data mining [!INCLUDE[msCoName](../includes/msconame-md.md)] . Se disponibili, è anche possibile utilizzare i visualizzatori plug-in.  
  
 **Zoom avanti**  
 Consente di eseguire lo zoom avanti per ottenere una vista più dettagliata dei nodi e dei rami dell'albero delle decisioni. In un modello complesso, gli alberi delle decisioni possono disporre di molti livelli di diramazione.  
  
 **Zoom indietro**  
 Consente di eseguire lo zoom indietro per ottenere una vista complessiva dell'albero.  
  
 **Copia parte visibile del grafico**  
 Consente di copiare la sezione visibile del diagramma negli Appunti.  
  
 **Copia grafico intero**  
 Consente di copiare tutto il diagramma negli Appunti.  
  
 **Ridimensiona e adatta il diagramma alla finestra**  
 Consente di eseguire lo zoom indietro del diagramma finché l'intero albero non si adatta alla schermata.  
  
 **Istogrammi**  
 Consente di selezionare il numero di stati che possono essere visualizzati nell'istogramma per ogni nodo. Se il numero di stati nel modello è inferiore al valore selezionato, non vengono visualizzate barre aggiuntive.  
  
 **Albero**  
 Consente di scegliere un albero da visualizzare nel visualizzatore. Se si crea un modello che dispone di più attributi stimabili, l'algoritmo consente di creare un albero separato per ogni attributo stimabile.  
  
 **Background**  
 Consente di scegliere un valore dell'attributo stimabile da utilizzare per rappresentare il colore di sfondo di ogni nodo. Ad esempio, nei modelli di esempio AdventureWorks se si imposta **Sfondo** su 1 ([Bike Buyer] = Sì), ai nodi viene applicata un'ombreggiatura più scura se dispongono di una proporzione maggiore di acquirenti di biciclette. Questa opzione offre un segnale visivo aggiuntivo sul significato dei rami e dei nodi nell'albero.  
  
 **Espansione predefinita**  
 Consente di scegliere un valore dall'elenco per selezionare l'impostazione predefinita per il numero di livelli visualizzati nel grafico dell'albero.  
  
 **Mostra livello**  
 Consente di spostare a destra o a sinistra la barra del dispositivo di scorrimento per modificare il numero di livelli visualizzati nel grafico dell'albero. Per vedere tutti i nodi nel modello, far scorrere la barra completamente a destra.  
  
## <a name="see-also"></a>Vedi anche  
 [Algoritmi di data mining &#40;Analysis Services-&#41;di data mining](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizzatori modello di data mining &#40;Progettazione modelli di data mining&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizzatori modello di data mining](data-mining/data-mining-model-viewers.md)  
  
  
