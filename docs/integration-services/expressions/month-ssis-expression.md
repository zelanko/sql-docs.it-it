---
title: MONTH (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], MONTH
- MONTH function
ms.assetid: b5a47a11-c2ef-49bd-bd70-235632ff7bf6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cb4bd503220a08736053674c30b0e6c1c3d9b1de
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725146"
---
# <a name="month-ssis-expression"></a>MONTH (espressione SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Viene restituito un valore integer che rappresenta la parte corrispondente al mese di una data.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
MONTH(date)  
```  
  
## <a name="arguments"></a>Argomenti  
 *data*  
 Data in qualsiasi formato di data.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 Se l'argomento è Null, MONTH restituirà Null.  
  
 Per i valori letterali di data è necessario eseguire il cast esplicito a uno dei tipi di dati date. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
> [!NOTE]  
>  La convalida dell'espressione non riesce quando viene eseguito il cast esplicito di un valore letterale di data a uno di questi tipi di dati relativi alle date: DT_DBTIMESTAMPOFFSET e DT_DBTIMESTAMP2.  
  
 La funzione MONTH costituisce una forma più breve, ma equivalente, della funzione DATEPART("Month", date).  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene restituito il numero del mese in un valore letterale di data. Se la data è in formato "mm/gg/aaaa", l'esempio restituirà 11.  
  
```  
MONTH((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 In questo esempio viene restituito un Integer che rappresenta il mese nella colonna **ModifiedDate** .  
  
```  
MONTH(ModifiedDate)  
```  
  
 In questo esempio viene restituito un valore integer che rappresenta il mese nella data corrente.  
  
```  
MONTH(GETDATE())  
```  
  
## <a name="see-also"></a>Vedere anche  
 [DATEADD &#40;espressione SSIS&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40;espressione SSIS&#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART &#40;espressione SSIS&#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [DAY &#40;espressione SSIS&#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [YEAR &#40;espressione SSIS&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [Funzioni &#40;espressione SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
