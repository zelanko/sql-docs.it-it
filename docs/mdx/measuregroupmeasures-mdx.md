---
description: MeasureGroupMeasures (MDX)
title: MeasureGroupMeasures (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3adb11cd39e5a85e498f9b04ac714385d944c48a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483834"
---
# <a name="measuregroupmeasures-mdx"></a>MeasureGroupMeasures (MDX)


  Restituisce un set di misure appartenente al gruppo di misure specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
MEASUREGROUPMEASURES(MeasureGroupName)  
```  
  
## <a name="arguments"></a>Argomenti  
 *MeasureGroupName*  
 Espressione stringa valida contenente il nome del gruppo di misure da cui recuperare il set di misure.  
  
## <a name="remarks"></a>Osservazioni  
 La stringa specificata deve corrispondere esattamente al nome del gruppo di misure. Non è necessario racchiudere tra parentesi quadre i nomi di gruppi di misure contenenti spazi.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono restituite tutte le misure nel gruppo di misure Internet Sales nel cubo Adventure Works.  
  
```  
SELECT MeasureGroupMeasures('Internet Sales') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
