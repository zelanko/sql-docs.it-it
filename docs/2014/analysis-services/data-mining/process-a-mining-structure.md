---
title: Elaborare una struttura di Data Mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], processing
ms.assetid: 4162f33e-c23f-4293-8905-271781e45fa4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 92793adcf2fd04b1dac0c26933c1d5969a31f1a5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083105"
---
# <a name="process-a-mining-structure"></a>Elaborare una struttura di data mining
  Per poter esplorare o utilizzare i modelli di data mining associati a una struttura di data mining, è necessario distribuire il progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ed elaborare la struttura e i modelli di data mining. Inoltre, se si apporta una modifica alla struttura o ai modelli di data mining, verrà richiesto di eseguire di nuovo la distribuzione e l'elaborazione. L'elaborazione della struttura nella scheda **Struttura di data mining** di Progettazione modelli di data mining in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] comporta l'elaborazione di tutti i modelli associati.  
  
 È possibile elaborare una struttura di data mining utilizzando gli strumenti seguenti:  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   XMLA: Comando Process  
  
 Per informazioni sull'elaborazione di singoli modelli, vedere [Elaborare un modello di data mining](process-a-mining-model.md).  
  
### <a name="to-process-a-mining-structure-and-all-associated-mining-models-using-sql-server-data-tools"></a>Per elaborare una struttura di data mining e tutti i modelli di data mining associati utilizzando gli strumenti dati di SQL Server  
  
1.  Scegliere la voce di menu **Modello di data mining** , quindi **Elabora struttura di data mining e tutti i modelli** in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
     Se sono state apportate modifiche alla struttura, prima di elaborare i modelli verrà richiesto di ridistribuire la struttura. Scegliere **Sì**.  
  
2.  Fare clic su **eseguiti** nel **Processing Mining Structure - \<struttura >** nella finestra di dialogo.  
  
     Verrà aperta la finestra di dialogo **Stato elaborazione** in cui vengono visualizzate informazioni sull'elaborazione dei modelli.  
  
3.  Fare clic su **Chiudi** nella finestra di dialogo **Stato elaborazione** dopo che l'elaborazione dei modelli è stata completata.  
  
4.  Fare clic su **Close** nel **Processing Mining Structure - \<struttura >** nella finestra di dialogo.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e procedure relative alla struttura di data mining](mining-structure-tasks-and-how-tos.md)  
  
  
