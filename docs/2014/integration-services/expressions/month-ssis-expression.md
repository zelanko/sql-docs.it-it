---
title: MONTH (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], MONTH
- MONTH function
ms.assetid: b5a47a11-c2ef-49bd-bd70-235632ff7bf6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d587a860ad402c8a7458bb148741b753f3aeb2ae
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437228"
---
# <a name="month-ssis-expression"></a>MONTH (espressione SSIS)
  Viene restituito un valore integer che rappresenta la parte corrispondente al mese di una data.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
MONTH(date)  
```  
  
## <a name="arguments"></a>Argomenti  
 *date*  
 Data in qualsiasi formato di data.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_I4  
  
## <a name="remarks"></a>Osservazioni  
 Se l'argomento è Null, MONTH restituirà Null.  
  
 Per i valori letterali di data è necessario eseguire il cast esplicito a uno dei tipi di dati date. Per altre informazioni, vedere [Tipi di dati di Integration Services](../data-flow/integration-services-data-types.md).  
  
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
 [DATEADD &#40;espressione SSIS&#41;](dateadd-ssis-expression.md)   
 [DATEDIFF &#40;espressione SSIS&#41;](datediff-ssis-expression.md)   
 [DATEPART &#40;espressione SSIS&#41;](datepart-ssis-expression.md)   
 [DAY &#40;espressione SSIS&#41;](day-ssis-expression.md)   
 [YEAR &#40;espressione SSIS&#41;](year-ssis-expression.md)   
 [Funzioni &#40;espressione SSIS&#41;](functions-ssis-expression.md)  
  
  
