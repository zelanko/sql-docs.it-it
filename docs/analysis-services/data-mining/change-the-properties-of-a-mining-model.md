---
title: Modificare le proprietà di un modello di Data Mining | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a3650b284e8817c2b7f8aee6a0beca71c275d6a1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62670381"
---
# <a name="change-the-properties-of-a-mining-model"></a>Modificare le proprietà di un modello di data mining
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Alcune proprietà dei modelli di data mining si applicano all'intero modello, altre solo a singole colonne. Esempi di proprietà che si applicano all'intero modello sono la proprietà **Drillthrough** , che specifica se i dati del case devono essere disponibili per le query, e la proprietà **Description** . Le proprietà che si applicano alle singole colonne sono **Usage** e **ModelingFlags**, che controllano il modo in cui i dati della colonna vengono usati all'interno del modello.  
  
 Le proprietà del modello seguenti sono associate a editor avanzati che è possibile utilizzare per creare espressioni o configurare proprietà più complesse. Di seguito sono elencate queste proprietà.  
  
-   **Filtro** proprietà: Apre la [filtro dei Set di dati o finestra di dialogo Filtro modello](http://msdn.microsoft.com/library/a9602174-b7e2-4e16-8ded-dfd8eb9264d7).  
  
-   **AlgorithmParameters** proprietà: Apre la [finestra di dialogo parametri algoritmo &#40;visualizzazione di modelli di Data Mining&#41;](http://msdn.microsoft.com/library/57f9f6f8-8ca4-4a6e-8f18-85f0571b7060).  
  
 Per informazioni su come impostare le proprietà in un modello di data mining, vedere [Colonne del modello di data mining](../../analysis-services/data-mining/mining-model-columns.md).  
  
### <a name="to-change-the-properties-of-a-mining-model"></a>Per modificare le proprietà di un modello di data mining  
  
1.  Nella scheda **Modelli di data mining** di Progettazione modelli di data mining fare clic con il pulsante destro del mouse sull'intestazione di colonna che contiene il nome del modello di data mining o sulla riga della griglia che contiene il nome dell'algoritmo di data mining e quindi scegliere **Proprietà**.  
  
2.  Nella finestra **Proprietà** a destra dello schermo evidenziare il valore corrispondente alla proprietà da modificare e quindi immettere il nuovo valore.  
  
     Il nuovo valore diventerà effettivo quando si seleziona un elemento diverso nella finestra di progettazione.  
  
### <a name="to-change-the-properties-of-a-mining-model-column"></a>Per modificare le proprietà di un modello di data mining  
  
1.  Nella scheda **Modelli di data mining** di Progettazione modelli di data mining fare clic con il pulsante destro del mouse sulla cella della griglia in corrispondenza dell'intersezione tra la colonna della struttura di data mining e il modello di data mining e quindi scegliere **Proprietà**.  
  
2.  Nella finestra **Proprietà** a destra dello schermo evidenziare il valore corrispondente alla proprietà da modificare e quindi immettere il nuovo valore.  
  
    > [!NOTE]  
    >  Se l'uso della colonna è impostato su **Ignore**, la finestra **Proprietà** per la colonna è vuota.  
  
     Il nuovo valore diventerà effettivo quando si seleziona un elemento diverso nella finestra di progettazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e procedure relative al modello di data mining](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
