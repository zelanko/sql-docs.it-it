---
title: Istruzione CALL (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: de74590ac4c43a9141c0ab2092babf41ffd23ba5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68106305"
---
# <a name="mdx-data-manipulation---call"></a>Manipolazione dei dati MDX - CALL


  Esegue una stored procedure che restituisce un valore void nell'ambito corrente o facoltativamente in un cubo specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CALL SP_Name   
   [ (SP_Argument   
      [, SP_Argument ,...n]  
      ) ]   
[ONCube_Expression]  
```  
  
## <a name="arguments"></a>Argomenti  
 *SP_Name*  
 Espressione stringa valida che specifica il nome di una stored procedure.  
  
 *SP_Argument*  
 Espressione stringa valida che specifica un argomento per la stored procedure chiamata.  
  
 *Cube_Expression*  
 Stringa espressione di cubo valida che specifica il nome del cubo.  
  
## <a name="remarks"></a>Osservazioni  
 L'istruzione **Call** esegue una stored procedure registrata specificata, includendo facoltativamente uno o più argomenti per la stored procedure specificata. L'istruzione **Call** viene utilizzata solo con le stored procedure che restituiscono void. Questa istruzione non può essere combinata con altre funzioni o altri operatori in un'espressione MDX. Le stored procedure registrate che restituiscono valori possono essere chiamate direttamente all'interno delle espressioni MDX e combinate con altre funzioni e altri operatori MDX.  
  
 Se non viene specificato un cubo, l'istruzione esegue la stored procedure sul cubo corrente.  
  
> [!NOTE]  
>  Se il stored procedure non è registrato sul client, l'istruzione **Call** tenta di chiamare il stored procedure da un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzioni di manipolazione dei dati MDX &#40;&#41;MDX](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [Utilizzo di stored procedure &#40;&#41;MDX](../mdx/using-stored-procedures-mdx.md)  
  
  
