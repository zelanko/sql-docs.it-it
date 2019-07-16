---
title: Elaborare un modello di Data Mining | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2bfc8d22ff87f467fa89d178d46b422918aa4dd6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209737"
---
# <a name="process-a-mining-model"></a>Elaborare un modello di data mining
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La scheda Modelli di data mining di Progettazione modelli di data mining in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]consente di elaborare un modello di data mining specifico associato a una struttura di data mining oppure tutti i modelli associati alla struttura.  
  
 È possibile elaborare un modello di data mining utilizzando gli strumenti seguenti:  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
 Inoltre, è possibile utilizzare un comando di elaborazione XMLA. Per altre informazioni, vedere [Strumenti e approcci per l’elaborazione &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/tools-and-approaches-for-processing-analysis-services.md).  
  
### <a name="process-a-single-mining-model-using-sql-server-data-tools"></a>Elaborare un singolo modello di data mining utilizzando SQL Server Data Tools  
  
1.  Nella scheda **Modelli di data mining** di Progettazione modelli di data mining selezionare un modello di data mining in una o più colonne di modelli nella griglia.  
  
2.  Scegliere **Elabora modello** dal menu **Modello di data mining**.  
  
     Se sono state apportate modifiche alla struttura di data mining, prima di elaborare il modello verrà richiesto di ridistribuire la struttura. Scegliere **Sì**.  
  
3.  Nel **Elaboramodello di Data Mining - \<modello >** della finestra di dialogo fare clic su **eseguire**.  
  
     Verrà visualizzata la finestra di dialogo **Stato elaborazione** contenente informazioni sull'elaborazione dei modelli.  
  
4.  Al termine dell'elaborazione del modello, fare clic su **Chiudi** nella finestra di dialogo **Stato elaborazione** .  
  
5.  Fare clic su **Close** nel **Elaboramodello di Data Mining - \<modello >** nella finestra di dialogo.  
  
 Tramite questa procedura sono stati elaborati solo la struttura di data mining e il modello di data mining associato.  
  
### <a name="process-all-mining-models-that-are-associated-with-a-mining-structure"></a>Elaborare tutti i modelli di data mining associati a una struttura di data mining  
  
1.  Nella scheda **Modelli di data mining** di Progettazione modelli di data mining scegliere **Elabora struttura di data mining e tutti i modelli** dal menu **Modello di data mining** .  
  
2.  Se sono state apportate modifiche alla struttura di data mining, prima di elaborare i modelli verrà richiesto di ridistribuire la struttura. Scegliere **Sì**.  
  
3.  Nel **Processing Mining Structure - \<struttura >** della finestra di dialogo fare clic su **eseguire**.  
  
4.  Verrà visualizzata la finestra di dialogo **Stato elaborazione** contenente informazioni sull'elaborazione dei modelli.  
  
5.  Al termine dell'elaborazione dei modelli, fare clic su **Chiudi** nella finestra di dialogo **Stato elaborazione** .  
  
6.  Fare clic su **Close** nel **elaborazione \<modello >** nella finestra di dialogo.  
  
 Tramite questa procedura sono stati elaborati la struttura di data mining e tutti i modelli di data mining associati.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e procedure relative al modello di data mining](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
