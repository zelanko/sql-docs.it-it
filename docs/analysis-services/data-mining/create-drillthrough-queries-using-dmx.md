---
title: Creare query drill-through tramite DMX | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6616f90f475da91f3f5c38c0f5922d16d72a5408
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210144"
---
# <a name="create-drillthrough-queries-using-dmx"></a>Creare query drill-through tramite DMX
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Per tutti i modelli che supportano il drill-through, è possibile recuperare i dati del case e della struttura creando una query DMX in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o in qualsiasi altro client che supporta DMX.  
  
> [!WARNING]  
>  Per visualizzare i dati, è necessario aver abilitato il drill-through e disporre delle autorizzazioni necessarie.  
  
## <a name="specifying-drillthrough-options"></a>Impostazione delle opzioni di drill-through  
 La sintassi generale per il recupero di case del modello e di case della struttura è la seguente:  
  
```  
SELECT <model column list>, StructureColumn('<structure column name') FROM <modelname>.CASES  
```  
  
 Per altre informazioni sull'utilizzo di query DMX per restituire dati del case, vedere [SELECT FROM &#60;model&#62;.CASES &#40;DMX&#41;](../../dmx/select-from-model-cases-dmx.md) e [SELECT FROM &#60;structure&#62;.CASES](../../dmx/select-from-structure-cases.md).  
  
## <a name="examples"></a>Esempi  
 La query DMX seguente restituisce i dati del case relativi a una serie di prodotti specifica da un modello Time Series. La query restituisce anche la colonna **Amount**che non viene utilizzata nel modello, ma risulta disponibile nella struttura di data mining.  
  
```  
SELECT [DateSeries], [Model Region], Quantity, StructureColumn('Amount') AS [M200 Pacific Amount]  
FROM Forecasting.CASES  
WHERE [Model Region] = 'M200 Pacific'  
```  
  
 In questo esempio viene utilizzato un alias per rinominare la colonna della struttura. Se non si assegna un alias alla colonna della struttura, la colonna viene restituita con il nome 'Expression'. Si tratta del comportamento predefinito per tutte le colonne senza nome.  
  
## <a name="see-also"></a>Vedere anche  
 [Query drill-through &#40;Data mining&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)   
 [Drill-through sulle strutture di data mining](../../analysis-services/data-mining/drillthrough-on-mining-structures.md)  
  
  
