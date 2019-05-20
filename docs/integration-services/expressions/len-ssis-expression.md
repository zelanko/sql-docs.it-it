---
title: LEN (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- LEN function
- number of characters
ms.assetid: d961398b-e4d0-4936-be17-8f4c5882a640
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 83256bfc8b610869b8bbc1938f7846ce41971b1b
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725281"
---
# <a name="len-ssis-expression"></a>LEN (espressione SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Viene restituito il numero di caratteri in un'espressione di caratteri. Se la stringa contiene spazi vuoti iniziali e finali, la funzione li includerà nel conteggio. Per una stessa stringa rappresentata con caratteri a uno e due byte, LEN restituisce valori identici.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
LEN(character_expression)  
```  
  
## <a name="arguments"></a>Argomenti  
 *character_expression*  
 Espressione da valutare.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 L'argomento *character_expression* può essere un tipo di dati DT_WSTR, DT_TEXT, DT_NTEXT o DT_IMAGE. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Se *character_expression* è un valore letterale stringa o una colonna di dati con tipo di dati DT_STR, prima di eseguire l'operazione prevista da LEN verrà eseguito il cast implicito al tipo di dati DT_WSTR. Per gli altri tipi di dati è necessario il cast esplicito al tipo di dati DT_WSTR. Per altre informazioni, vedere [Cast &#40;espressione SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 Se l'argomento passato alla funzione LEN ha un tipo di dati BLOB (Binary Large Object), ad esempio DT_TEXT, DT_NTEXT o DT_IMAGE, la funzione restituirà il numero dei byte.  
  
 Se l'argomento è Null, LEN restituirà Null.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene restituita la lunghezza di un valore letterale stringa. Il risultato restituito è 12.  
  
```  
LEN("Ball Bearing")  
```  
  
 In questo esempio viene restituita la differenza tra le lunghezze dei valori nelle colonne **FirstName** e **LastName** .  
  
```  
LEN(FirstName) - LEN(LastName)  
```  
  
 In questo esempio viene restituita la lunghezza di un nome di computer usando la variabile di sistema **MachineName**.  
  
```  
LEN(@MachineName)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni &#40;espressione SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
