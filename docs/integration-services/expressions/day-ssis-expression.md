---
title: DAY (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- DAY function
- dates [Integration Services], DAY
ms.assetid: d8447187-49df-45b7-a98e-142ad44fd3e2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4f85a19231a7d3e3adaf514ef304f459357c5ec0
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58271947"
---
# <a name="day-ssis-expression"></a>DAY (espressione SSIS)
  Viene restituito un valore integer che rappresenta la parte del giorno in una data.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DAY(date)  
```  
  
## <a name="arguments"></a>Argomenti  
 *data*  
 Espressione che restituisce una data valida o una stringa con formato di data.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 Se l'argomento è Null, DAY restituirà Null.  
  
 Per i valori letterali di data è necessario eseguire il cast esplicito a uno dei tipi di dati date. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
> [!NOTE]  
>  La convalida dell'espressione non riesce quando viene eseguito il cast esplicito di un valore letterale di data a uno di questi tipi di dati relativi alle date: DT_DBTIMESTAMPOFFSET e DT_DBTIMESTAMP2.  
  
 La funzione DAY costituisce una forma più breve, ma equivalente, della funzione DATEPART("Day", date).  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene restituito il numero del giorno in un valore letterale di data. Se la data è in formato "mm/gg/aaaa", l'esempio restituirà 23.  
  
```  
DAY((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 In questo esempio viene restituito un Integer che rappresenta il giorno nella colonna **ModifiedDate** .  
  
```  
DAY(ModifiedDate)  
```  
  
 In questo esempio viene restituito un valore integer che rappresenta il giorno nella data corrente.  
  
```  
DAY(GETDATE())  
```  
  
## <a name="see-also"></a>Vedere anche  
 [DATEADD &#40;espressione SSIS&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40;espressione SSIS&#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART &#40;espressione SSIS&#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [MONTH &#40;espressione SSIS&#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [YEAR &#40;espressione SSIS&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [Funzioni &#40;espressione SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
