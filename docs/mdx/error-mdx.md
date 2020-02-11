---
title: Errore (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 91d07c6bbb4eb4731c9a802e47cd8f4c71aa5aeb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68031233"
---
# <a name="error-mdx"></a>Error (MDX)


  Genera un errore, visualizzando facoltativamente il messaggio di errore specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Error( [ Error_Text ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Error_Text*  
 Espressione stringa valida contenente il messaggio di errore da restituire.  
  
## <a name="examples"></a>Esempi  
 Nella query seguente viene illustrato come utilizzare la funzione **Error** all'interno di una misura calcolata:  
  
 `WITH MEMBER MEASURES.ERRORDEMO AS ERROR("THIS IS AN ERROR")`  
  
 `SELECT`  
  
 `MEASURES.ERRORDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
