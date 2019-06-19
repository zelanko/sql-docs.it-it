---
title: DATEPART (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], DATEPART
- DATEPART function
ms.assetid: 3e590094-fc49-4144-805f-fdc1bf2fe509
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cf646a6cc26b757b65e0c7c1e561aa7aff26d020
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65725505"
---
# <a name="datepart-ssis-expression"></a>DATEPART (espressione SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Restituisce un valore integer che rappresenta una parte di una data.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DATEPART(datepart, date)  
```  
  
## <a name="arguments"></a>Argomenti  
 *parte di una data*  
 Parametro che consente di specificare per quale parte della data si desidera restituire un nuovo valore.  
  
 *data*  
 Espressione che restituisce una data valida o una stringa con formato di data.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 Se l'argomento è Null, DATEPART restituirà Null.  
  
 Per i valori letterali di data è necessario eseguire il cast esplicito a uno dei tipi di dati date. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Nella tabella seguente sono elencate le parti della data e le abbreviazioni riconosciute dall'analizzatore di espressioni. Per i nomi delle parti della data non viene fatta distinzione tra maiuscole e minuscole.  
  
|parte di una data|Abbreviazioni|  
|--------------|-------------------|  
|Year|yy, yyyy|  
|Quarter|qq, q|  
|Month|mm, m|  
|Dayofyear|dy, y|  
|Day|dd, d|  
|Week|wk, ww|  
|Giorno feriale|dw|  
|Ora|Hh|  
|Minuto|mi, n|  
|Secondo|ss, s|  
|Millisecond|Ms|  
  
## <a name="ssis-expression-examples"></a>Esempi di espressione SSIS  
 In questo esempio viene restituito un valore integer che rappresenta il mese in un valore letterale data. Se la data è in formato "mm/gg/aaaa", l'esempio restituirà 11.  
  
```  
DATEPART("month", (DT_DBTIMESTAMP)"11/04/2002")  
```  
  
 In questo esempio viene restituito un valore integer che rappresenta il giorno nella colonna **ModifiedDate** .  
  
```  
DATEPART("dd", ModifiedDate)  
```  
  
 In questo esempio viene restituito un valore integer che rappresenta l'anno nella data corrente.  
  
```  
DATEPART("yy",GETDATE())  
```  
  
## <a name="see-also"></a>Vedere anche  
 [DATEADD &#40;espressione SSIS&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40;espressione SSIS&#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DAY &#40;espressione SSIS&#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [MONTH &#40;espressione SSIS&#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [YEAR &#40;espressione SSIS&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [Funzioni &#40;espressione SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
