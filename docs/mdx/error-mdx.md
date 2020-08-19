---
description: Error (MDX)
title: Errore (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f95ee71586f5571d91221fe8889198a44a1252b3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494924"
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
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
