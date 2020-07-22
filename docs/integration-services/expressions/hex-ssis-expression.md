---
title: HEX (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- hexadecimal data
- HEX function
ms.assetid: f5d471ee-aeef-421c-b6e1-55b9676c3842
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e9189790bb29d5595459f0fcabecdf735fc0bdf1
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86910820"
---
# <a name="hex-ssis-expression"></a>HEX (espressione SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Viene restituita una stringa che rappresenta il valore esadecimale di un valore integer.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
HEX(integer_expression)  
```  
  
## <a name="arguments"></a>Argomenti  
 *integer_expression*  
 Valore integer con o senza segno.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_WSTR  
  
## <a name="remarks"></a>Osservazioni  
 HEX restituisce Null se *integer_expression* è Null.  
  
 L'argomento *integer_expression* argomento deve valutare un numero intero. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Il risultato restituito non include qualificatori, ad esempio il prefisso 0x. Per includere un prefisso, utilizzare l'operatore di concatenazione (+). Per altre informazioni, vedere [+ &#40;concatenazione&#41; &#40;espressione SSIS&#41;](../../integration-services/expressions/concatenate-ssis-expression.md).  
  
 Le lettere da A a F, usate nella notazione esadecimale, vengono visualizzate in maiuscolo.  
  
 La lunghezza della stringa risultante per i tipi di dati integer è la seguente:  
  
-   Per i tipi di dati DT_I1 e DT_UI1 viene restituita una stringa con lunghezza massima pari a 2.  
  
-   Per i tipi di dati DT_I2 e DT_UI2 viene restituita una stringa con lunghezza massima pari a 4.  
  
-   Per i tipi di dati DT_I4 e DT_UI4 viene restituita una stringa con lunghezza massima pari a 8.  
  
-   Per i tipi di dati DT_I8 e DT_UI8 viene restituita una stringa con lunghezza massima pari a 16.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene utilizzato un valore letterale numerico. La funzione restituisce il valore 190.  
  
```  
HEX(400)   
```  
  
 In questo esempio viene usata la colonna **ReorderPoint** . Il tipo di dati della colonna è **smallint**. Se **ReorderPoint** ha valore 750, la funzione restituirà 2EE.  
  
```  
HEX(ReorderPoint)   
```  
  
 In questo esempio viene usata la variabile di sistema **LocaleID**. Se **LocaleID** ha valore 1033, la funzione restituirà 409.  
  
```  
HEX(@LocaleID)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni &#40;espressione SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
