---
title: O (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 45063e9f2aca6a924289d4d52434535d16c9a08e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68055715"
---
# <a name="or-mdx"></a>OR (MDX)


  Esegue la disgiunzione logica di due espressioni numeriche.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Expression1 OR Expression2   
```  
  
#### <a name="parameters"></a>Parametri  
 Expression1  
 Espressione MDX (Multidimensional Expression) valida che restituisce un valore numerico.  
  
 Expression2  
 Espressione MDX valida che restituisce un valore numerico.  
  
## <a name="return-value"></a>Valore restituito  
 Valore booleano che restituisce **true** se uno o entrambi gli argomenti restituiscono **true**; in caso contrario, **false**.  
  
## <a name="remarks"></a>Osservazioni  
 L'operatore **or** considera entrambi gli argomenti come valori booleani (zero, 0, come **false**; in caso contrario, **true**) prima che l'operatore esegua la disgiunzione logica. Nella tabella seguente viene illustrato il modo in cui l'operatore **or** esegue la disgiunzione logica.  
  
|*Expression1*|*Expression2*|Valore restituito|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="example"></a>Esempio  
 La query seguente contiene una misura calcolata che restituisce la stringa "MARRIED OR MALE" Se il membro corrente nella gerarchia Gender della dimensione Customer è un maschio oppure il membro corrente della gerarchia di stato civile della dimensione Customer è sposato; in caso contrario, restituisce la stringa "Unmarried o FEMALe".  
  
```  
WITH  
MEMBER MEASURES.ORDEMO AS  
IIF(  
([Customer].[Gender].CURRENTMEMBER IS [Customer].[Gender].&[M])  
OR  
([Customer].[Marital Status].CURRENTMEMBER IS [Customer].[Marital Status].&[M]),  
"MARRIED OR MALE",  
"UNMARRIED OR FEMALE")  
SELECT [Customer].[Gender].[Gender].MEMBERS ON 0,  
[Customer].[Marital Status].[Marital Status].MEMBERS ON 1  
FROM [Adventure Works]  
WHERE(MEASURES.ORDEMO)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento agli operatori MDX &#40;&#41;MDX](../mdx/mdx-operator-reference-mdx.md)  
  
  
