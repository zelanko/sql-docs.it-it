---
title: Abilitare il drill-through per un modello di data mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], how-to topics
- drillthrough [Analysis Services]
ms.assetid: 4fa44f60-ef9a-4b59-98c0-c0baf1195c8e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 06ce3967bf9258e9b8f6cd4a28cb28a29a1e0588
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084535"
---
# <a name="enable-drillthrough-for-a-mining-model"></a>Abilitare il drill-through per un modello di data mining
  Se è stato abilitato il drill-through per un modello di data mining, quando si esplora il modello è possibile recuperare informazioni dettagliate sui case utilizzati per creare il modello. Per visualizzare queste informazioni sono necessarie le autorizzazioni adeguate e la struttura deve essere stata già elaborata.  
  
 **Autorizzazioni** Per eseguire il drill-through dei dati del modello o della struttura, l'utente deve essere membro di un ruolo che disponga di autorizzazioni [AllowDrillThrough](https://docs.microsoft.com/bi-reference/assl/properties/allowdrillthrough-element-assl) per il modello o la struttura di data mining. Le autorizzazioni di drill-through vengono impostate separatamente per la struttura e per il modello.  
  
-   Le autorizzazioni drill-through sul modello consentono di eseguire il drill-through dal modello, anche se non si dispone di autorizzazioni sulla struttura.  
  
-   Le autorizzazioni di drill-through per la struttura consentono di includere colonne della struttura nelle query di drill-through dal modello usando la funzione [StructureColumn &#40;DMX&#41;](/sql/dmx/structurecolumn-dmx). È anche possibile eseguire una query sui test case e di training nella struttura usando l'istruzione SELECT... DALLA \<struttura>. Sintassi CASEs.  
  
 **Memorizzazione nella cache dei case di training** Il drill-through consente di recuperare informazioni sui case di training nella struttura di data mining. Queste informazioni vengono memorizzate nella cache quando la struttura viene elaborata. Pertanto, se si sceglie di cancellare tutti i dati memorizzati nella cache impostando la proprietà <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> su `ClearAfterProcessing`, il drill-through non funzionerà.  
  
> [!NOTE]  
>  Se i case di training non sono stati memorizzati nella cache, è necessario impostare la proprietà <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> su **KeepTrainingCases** e rielaborare quindi il modello prima che sia possibile visualizzare i dati dei case.  
  
 Per altre informazioni, vedere [Query drill-through &#40;Data mining&#41;](drillthrough-queries-data-mining.md).  
  
### <a name="to-enable-drillthrough-on-a-mining-model"></a>Per abilitare il drill-through su un modello di data mining  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], nella scheda **Modelli di data mining** di Progettazione modelli di data mining fare clic con il pulsante destro del mouse sul nome del modello di data mining in cui si vuole abilitare il drill-through e quindi scegliere **Proprietà**.  
  
2.  Nelle finestre **Proprietà** fare clic su **AllowDrillThrough**e selezionare **true**.  
  
3.  Nella scheda **Modelli di data mining** fare clic con il pulsante destro del mouse sul modello e scegliere **Elabora modello**.  
  
### <a name="to-enable-caching-for-a-mining-structure"></a>Per attivare la memorizzazione nella cache per una struttura di data mining  
  
1.  Nella scheda [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]Struttura di data mining **di Progettazione modelli di data mining in** , fare clic con il pulsante destro del mouse sul nome della struttura di data mining.  
  
2.  Aprire la finestra **Proprietà** .  
  
3.  Nella finestra **Proprietà** individuare la proprietà **CacheMode** e selezionare **KeepTrainingCases** nell'elenco.  
  
4.  Selezionare **Elabora** dal menu **Database**.  
  
## <a name="see-also"></a>Vedere anche  
 [Query drill-through &#40;&#41;di data mining](drillthrough-queries-data-mining.md)  
  
  
