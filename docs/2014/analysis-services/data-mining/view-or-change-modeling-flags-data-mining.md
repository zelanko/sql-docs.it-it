---
title: Visualizzare o modificare i flag di modellazione (data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d1169735-fb18-417b-b8d6-9a161e444020
author: minewiskan
ms.author: owend
ms.openlocfilehash: 3ad72ec94c8125b2f3bd9067a3a2ce413eeaba21
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84520197"
---
# <a name="view-or-change-modeling-flags-data-mining"></a>Visualizzare o modificare flag di modellazione (Data mining)
  I flag di modellazione sono proprietà impostate in una colonna della struttura di data mining o in colonne del modello di data mining per controllare la modalità di elaborazione dei dati durante l'analisi da parte dell'algoritmo.  
  
 In Progettazione modelli di data mining è possibile visualizzare e modificare i flag di modellazione associati a una struttura di data mining o a una colonna di data mining visualizzando le proprietà della struttura o del modello. Inoltre, è possibile impostare i flag di modellazione tramite DMX, AMO o XMLA.  
  
 In questa procedura viene descritto come modificare i flag di modellazione nella finestra di progettazione.  
  
### <a name="view-or-change-the-modeling-flag-for-a-structure-column-or-model-column"></a>Visualizzare o modificare il flag di modellazione per una colonna della struttura o una colonna del modello  
  
1.  In SQL Server Design Studio aprire Esplora soluzioni, quindi fare doppio clic sulla struttura di data mining.  
  
2.  Per impostare il flag di modellazione NOT NULL, fare clic sulla scheda **struttura di data mining** . Per impostare il REGRESSOre o i flag di MODEL_EXISTENCE_ONLY, fare clic sulla scheda **modello di data mining** .  
  
3.  Fare clic con il pulsante destro del mouse sulla colonna da visualizzare o modificare, quindi scegliere **Proprietà**.  
  
4.  Per aggiungere un nuovo flag di modellazione, fare clic sulla casella di testo accanto alla proprietà **ModelingFlags** e selezionare le casella o le caselle di controllo relative ai flag di modellazione che si desidera utilizzare.  
  
     I flag di modellazione vengono visualizzati solo se sono appropriati per il tipo di dati della colonna.  
  
    > [!NOTE]  
    >  Dopo avere modificato un flag di modellazione, è necessario rielaborare il modello.  
  
### <a name="get-the-modeling-flags-used-in-the-model"></a>Recuperare i flag di modellazione utilizzati nel modello  
  
-   In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aprire una finestra Query DMX e digitare una query simile alla seguente:  
  
    ```  
    SELECT COLUMN_NAME, CONTENT_TYPE, MODELING_FLAG  
    FROM $system.DMSCHEMA_MINING_COLUMNS  
    WHERE MODEL_NAME = 'Forecasting'  
  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e procedure relative al modello di data mining](mining-model-tasks-and-how-tos.md)   
 [Flag di modellazione &#40;data mining&#41;](modeling-flags-data-mining.md)  
  
  
