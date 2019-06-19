---
title: LTRIM (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- leading blanks
- LTRIM function
ms.assetid: d082f42a-d7e7-49f5-a503-ac44ba630832
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 51785a66b005ec3c7f9b6af498803064c93635a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65725189"
---
# <a name="ltrim-ssis-expression"></a>LTRIM (espressione SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Restituisce un'espressione di caratteri dopo aver rimosso gli spazi iniziali.  
  
> [!NOTE]  
>  LTRIM non rimuove altri caratteri spazio, quali i caratteri di tabulazione o avanzamento riga. Unicode offre elementi di codice per molti tipi diversi di spazi, ma questa funzione riconosce solo l'elemento di codice Unicode 0x0020. Quando stringhe DBCS (Double-Byte Character Set) vengono convertite in Unicode, possono includere caratteri spazio diversi da 0x0020 e la funzione non può rimuovere tali spazi. Per rimuovere qualsiasi tipo di spazi, è possibile utilizzare il metodo Microsoft Visual Basic .NET LTrim in uno script eseguito dal componente Script.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
LTRIM(character expression)  
```  
  
## <a name="arguments"></a>Argomenti  
 *character_expression*  
 Espressione di caratteri da cui rimuovere gli spazi.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 È possibile utilizzare LTRIM solo con il tipo di dati DT_WSTR. Se l'argomento *character_expression* è un valore letterale stringa o una colonna di dati con tipo di dati DT_STR, prima di eseguire l'operazione prevista da LTRIM verrà eseguito il cast implicito al tipo di dati DT_WSTR. Per gli altri tipi di dati è necessario il cast esplicito al tipo di dati DT_WSTR. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md) e [Cast &#40;espressione SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 Se l'argomento è Null, LTRIM restituirà Null.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio vengono rimossi gli spazi iniziali da un valore letterale stringa. Il risultato restituito è "Hello".  
  
```  
LTRIM("    Hello")  
```  
  
 In questo esempio vengono rimossi gli spazi iniziali dalla colonna **FirstName** .  
  
```  
LTRIM(FirstName)  
```  
  
 In questo esempio vengono rimossi gli spazi iniziali dalla variabile **FirstName** .  
  
```  
LTRIM(@FirstName)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [RTRIM &#40;espressione SSIS&#41;](../../integration-services/expressions/rtrim-ssis-expression.md)   
 [TRIM &#40;espressione SSIS&#41;](../../integration-services/expressions/trim-ssis-expression.md)   
 [Funzioni &#40;espressione SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
