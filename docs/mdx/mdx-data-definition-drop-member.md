---
description: Definizione dei dati MDX - DROP MEMBER
title: Istruzione DROP MEMBER (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f71232997c24a1bdca9a1294a804e8b30660d704
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483854"
---
# <a name="mdx-data-definition---drop-member"></a>Definizione dei dati MDX - DROP MEMBER


  Rimuove un membro calcolato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DROP MEMBER   
   CURRENTCUBE | Cube_Name  
      .Member_Name   
               [,CURRENTCUBE | Cube_Name.Member_Name ...n]  
```  
  
## <a name="arguments"></a>Argomenti  
 *Cube_Name*  
 Espressione stringa valida che specifica il nome di un cubo.  
  
 *Member_Identifier*  
 Espressione stringa valida che specifica il nome o la chiave di un membro.  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione CREATE MEMBER &#40;MDX&#41;](../mdx/mdx-data-definition-create-member.md)   
 [Istruzioni MDX per la definizione dei dati &#40;&#41;MDX ](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
