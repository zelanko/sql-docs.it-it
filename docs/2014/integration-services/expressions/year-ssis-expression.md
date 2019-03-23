---
title: YEAR (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], YEAR
- YEAR function
ms.assetid: 9d88dead-ace8-44b9-b8e2-916c1842e155
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4e677a4a0c36f52ae62dfc06cd597ad5401fc8e3
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58379749"
---
# <a name="year-ssis-expression"></a>YEAR (espressione SSIS)
  Viene restituito un valore integer che rappresenta la parte corrispondente all'anno di una data.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
YEAR(date)  
```  
  
## <a name="arguments"></a>Argomenti  
 *data*  
 Data in qualsiasi formato di data.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_I4  
  
## <a name="remarks"></a>Note  
 Se l'argomento è Null, YEAR restituirà Null.  
  
 Per i valori letterali di data è necessario eseguire il cast esplicito a uno dei tipi di dati date. Per altre informazioni, vedere [Tipi di dati di Integration Services](../data-flow/integration-services-data-types.md).  
  
> [!NOTE]  
>  L'espressione di convalida non riesce quando un valore letterale data in modo esplicito viene eseguito il cast a uno di questi tipi di dati di data: DT_DBTIMESTAMPOFFSET e DT_DBTIMESTAMP2.  
  
 La funzione YEAR costituisce una forma più breve, ma equivalente, della funzione DATEPART("Year", date).  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene restituito il numero dell'anno in un valore letterale di data. Se la data è in formato mm/gg/aaaa, l'esempio restituirà "2002".  
  
```  
YEAR((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 In questo esempio viene restituito un Integer che rappresenta l'anno nella colonna **ModifiedDate** .  
  
```  
YEAR(ModifiedDate)  
```  
  
 In questo esempio viene restituito un valore integer che rappresenta l'anno nella data corrente.  
  
```  
YEAR(GETDATE())  
```  
  
## <a name="see-also"></a>Vedere anche  
 [DATEADD &#40;espressione SSIS&#41;](dateadd-ssis-expression.md)   
 [DATEDIFF &#40;espressione SSIS&#41;](datediff-ssis-expression.md)   
 [DATEPART &#40;espressione SSIS&#41;](datepart-ssis-expression.md)   
 [DAY &#40;espressione SSIS&#41;](day-ssis-expression.md)   
 [MONTH &#40;espressione SSIS&#41;](month-ssis-expression.md)   
 [Funzioni &#40;espressione SSIS&#41;](functions-ssis-expression.md)  
  
  
