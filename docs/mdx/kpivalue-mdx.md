---
description: KPIValue (MDX)
title: KPIValue (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 24189ffb3e9a550fd4819b15cfbd8ae41a48a64f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471813"
---
# <a name="kpivalue-mdx"></a>KPIValue (MDX)


  Restituisce il membro da cui viene calcolato il valore dell'indicatore di prestazioni chiave (KPI) specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
KPIValue(KPI_Name)  
```  
  
## <a name="arguments"></a>Argomenti  
 *KPI_Name*  
 Espressione stringa valida che specifica il nome dell'indicatore di prestazioni chiave (KPI).  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono restituiti valore, obiettivo, stato e tendenza dell'indicatore di prestazioni chiave (KPI) relativo alla misura del ricavo del canale per i discendenti di tre membri della gerarchia dell'attributo Fiscal Year.  
  
```  
SELECT  
   { KPIValue("Channel Revenue"),   
     KPIGoal("Channel Revenue"),  
     KPIStatus("Channel Revenue"),   
     KPITrend("Channel Revenue")  
   } ON Columns,  
Descendants  
   ( { [Date].[Fiscal].[Fiscal Year].&[2002],  
       [Date].[Fiscal].[Fiscal Year].&[2003],  
       [Date].[Fiscal].[Fiscal Year].&[2004]   
     }, [Date].[Fiscal].[Fiscal Quarter]  
   ) ON Rows  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
