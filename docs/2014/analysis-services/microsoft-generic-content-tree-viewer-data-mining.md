---
title: Microsoft Generic Content Tree Viewer (data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.contentviewer.f1
ms.assetid: 751b4393-f6fd-48c1-bcef-bdca589ce34c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ba3b64847e2f63a96533a0f57cee41208176a7b7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66077804"
---
# <a name="microsoft-generic-content-tree-viewer-data-mining"></a>Microsoft Generic Content Tree Viewer (Data mining)
  In **Microsoft Generic Content Tree Viewer** vengono visualizzate informazioni dettagliate sul contenuto di un modello di data mining in un formato di tabella HTML standardizzato. Questa vista è utile poiché vengono esposti la struttura sottostante del modello, nonché i dettagli sui coefficienti, sulla distribuzione dei valori e così via.  
  
 Il contenuto effettivo visualizzato nella tabella varia a seconda dell'algoritmo utilizzato e possono essere inclusi colonne, regole, proprietà, attributi, nodi e formule. Per altre informazioni sul contenuto del modello e su come interpretare le informazioni per ogni tipo di modello, vedere [Contenuto del modello di data mining &#40;Analysis Services - Data Mining&#41;](data-mining/mining-model-content-analysis-services-data-mining.md).  
  
 Per le informazioni fornite nel visualizzatore viene utilizzata una struttura comune basata sul set di righe dello schema relativo al contenuto per i modelli di data mining. Tale set di righe è un framework generico per l'archiviazione degli schemi, delle statistiche e di altro contenuto di un modello di data mining. Per un elenco delle colonne del set di righe dello schema di data mining per i modelli di data mining, vedere [Set di righe DMSCHEMA_MINING_MODEL_CONTENT](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset).  
  
## <a name="options"></a>Opzioni  
 **Didascalia del nodo (ID univoco)**  
 In questo riquadro viene visualizzato un elenco di tutti i nodi nel modello di data mining selezionato. La modalità di disposizione dei nodi nell'albero è diversa a seconda del tipo di modello visualizzato.  
  
 È possibile fare clic su ogni nodo per visualizzare le relative informazioni dettagliate nel riquadro **Dettagli nodo** .  
  
 **Dettagli nodo**  
 Vengono visualizzate informazioni dettagliate sul contenuto del nodo selezionato. In ogni nodo vengono archiviate le relative informazioni in un formato standardizzato, tuttavia il contenuto e il significato di ogni riga della tabella dipendono dal tipo di modello o di nodo visualizzato. Ad esempio, le informazioni archiviate per un nodo che rappresenta una regola in un modello di associazione sono diverse rispetto a quelle di un nodo che rappresenta un albero in un modello di albero delle decisioni.  
  
 Per informazioni su come interpretare le informazioni per un tipo di modello specifico, vedere [Contenuto del modello di data mining &#40;Analysis Services - Data Mining&#41;](data-mining/mining-model-content-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmi di data mining &#40;Analysis Services-&#41;di data mining](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizzatori modello di data mining &#40;Progettazione modelli di data mining&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Query di data mining](data-mining/data-mining-queries.md)  
  
  
