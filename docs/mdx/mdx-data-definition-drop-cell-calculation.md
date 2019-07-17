---
title: Istruzione DROP CELL CALCULATION (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bccdd6efcf17af9d485e155b6653bab52bbcbd3b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038221"
---
# <a name="mdx-data-definition---drop-cell-calculation"></a>Definizione dei dati MDX - DROP CELL CALCULATION


  Rimuove la formula per il calcolo di celle specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DROP [ SESSION ] CELL CALCULATION CURRENTCUBE | Cube_Name.CellCalc_Name  
```  
  
## <a name="arguments"></a>Argomenti  
 *Cube_Name*  
 Espressione stringa valida che specifica il nome di una espressione di cubo.  
  
 *CellCalc_Name*  
 Espressione stringa valida che specifica il nome della formula per il calcolo di celle da eliminare.  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione CREATE CELL CALCULATION &#40;MDX&#41;](../mdx/mdx-data-definition-create-cell-calculation.md)   
 [Istruzioni di definizione dei dati MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
