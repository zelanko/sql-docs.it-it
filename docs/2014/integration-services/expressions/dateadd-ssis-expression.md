---
title: DATEADD (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], DATEADD
- dates [Integration Services]
- DATEADD function
ms.assetid: fa5c37b1-2ddc-4857-8f8e-f6d5643b654f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3c744d3f28bc27373f3dc9798ba591848d4b720e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62769348"
---
# <a name="dateadd-ssis-expression"></a>DATEADD (espressione SSIS)
  Viene restituito un nuovo valore DT_DBTIMESTAMP dopo aver aggiunto alla parte specificata di una data un numero che rappresenta un intervallo di date o di ore. Il parametro number deve restituire un valore integer e il parametro date deve restituire una data valida.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DATEADD(datepart, number, date)  
```  
  
## <a name="arguments"></a>Argomenti  
 *datepart*  
 Parametro che specifica la parte della data a cui aggiungere il numero.  
  
 *number*  
 Valore usato per incrementare il valore *datepart*. Deve essere un valore integer noto al momento dell'analisi dell'espressione.  
  
 *date*  
 Espressione che restituisce una data valida o una stringa con formato di data.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_DBTIMESTAMP  
  
## <a name="remarks"></a>Osservazioni  
 Nella tabella seguente sono elencate le parti della data e le abbreviazioni riconosciute dall'analizzatore di espressioni. Per i nomi delle parti della data non viene fatta distinzione tra maiuscole e minuscole.  
  
|parte di una data|Abbreviazioni|  
|--------------|-------------------|  
|Year|yy, yyyy|  
|Quarter|qq, q|  
|Month|mm, m|  
|Dayofyear|dy, y|  
|Giorno|dd, d|  
|Week|wk, ww|  
|Giorno della settimana|dw, w|  
|Ora|Hh|  
|Minuto|mi, n|  
|Second|ss, s|  
|Millisecond|Ms|  
  
 L'argomento *number* deve essere disponibile al momento dell'analisi dell'espressione. Può essere una costante o una variabile. Non è possibile utilizzare valori di colonna, perché tali valori non sono noti al momento dell'analisi dell'espressione.  
  
 L'argomento *datepart* deve essere racchiuso tra virgolette.  
  
 Per i valori letterali di data è necessario eseguire il cast esplicito a uno dei tipi di dati date. Per altre informazioni, vedere [Tipi di dati di Integration Services](../data-flow/integration-services-data-types.md).  
  
 Se l'argomento è Null, DATEADD restituirà Null.  
  
 Se la data non è valida, l'unità di data o tempo non è una stringa oppure l'incremento non è un valore integer statico, verrà generato un errore.  
  
## <a name="ssis-expression-examples"></a>Esempi di espressione SSIS  
 In questo esempio viene aggiunto un mese alla data corrente.  
  
```  
DATEADD("Month", 1,GETDATE())  
```  
  
 In questo esempio vengono aggiunti 21 giorni alle date nella colonna **ModifiedDate** .  
  
```  
DATEADD("day", 21, ModifiedDate)  
```  
  
 In questo esempio vengono aggiunti 2 anni a un valore letterale data.  
  
```  
DATEADD("yyyy", 2, (DT_DBTIMESTAMP)"8/6/2003")  
```  
  
## <a name="see-also"></a>Vedere anche  
 [DATEDIFF &#40;espressione SSIS&#41;](datediff-ssis-expression.md)   
 [DATEPART &#40;espressione SSIS&#41;](datepart-ssis-expression.md)   
 [DAY &#40;espressione SSIS&#41;](day-ssis-expression.md)   
 [MONTH &#40;espressione SSIS&#41;](month-ssis-expression.md)   
 [YEAR &#40;espressione SSIS&#41;](year-ssis-expression.md)   
 [Funzioni &#40;espressione SSIS&#41;](functions-ssis-expression.md)  
  
  
