---
title: Modificare le proprietà di una struttura di Data Mining | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8064fcc088c7ae9e7dd96c5c132b1246fe0ae2db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62670173"
---
# <a name="change-the-properties-of-a-mining-structure"></a>Modificare le proprietà di una struttura di data mining
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Sono disponibili due tipi di proprietà su una struttura di data mining, entrambi modificabili:  
  
-   Proprietà della struttura di data mining che influiscono sull'intera struttura  
  
-   Proprietà su singole colonne della struttura  
  
 Si noti che alcune proprietà dipendono da altre impostazioni di proprietà. Non è ad esempio possibile impostare le proprietà che controllano la creazione di contenitori, ad esempio <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> o <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A>finché non viene impostato il tipo di dati della colonna su **Discretized**.  
  
 Per altre informazioni sulle proprietà di data mining, vedere [Colonne della struttura di data mining](../../analysis-services/data-mining/mining-structure-columns.md).  
  
### <a name="to-change-the-properties-of-a-mining-structure"></a>Per modificare le proprietà di una struttura di data mining  
  
1.  Nella scheda **Struttura di data mining** di Progettazione modelli di data mining fare clic con il pulsante destro del mouse sulla struttura di data mining o su una colonna della struttura e quindi scegliere **Proprietà**.  
  
     A destra dello schermo verrà visualizzata la finestra **Proprietà** , se non è già visualizzata.  
  
2.  Nella finestra **Proprietà** selezionare il valore corrispondente alla proprietà che si vuole modificare e quindi immettere il nuovo valore.  
  
     Il nuovo valore diventerà effettivo quando si seleziona un elemento diverso nella finestra di progettazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e procedure relative alla struttura di data mining](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
