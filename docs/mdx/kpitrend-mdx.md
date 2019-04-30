---
title: Kpitrend=1=«String (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d5d1a211e473cf2eed96603d91b581a52e9062d7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63272734"
---
# <a name="kpitrend-mdx"></a>KPITrend (MDX)


  Restituisce il valore normalizzato che rappresenta la parte relativa alla tendenza dell'indicatore di prestazioni chiave (KPI) specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
KPITrend(KPI_Name)  
```  
  
## <a name="arguments"></a>Argomenti  
 *KPI_Name*  
 Espressione stringa valida che specifica il nome dell'indicatore di prestazioni chiave (KPI).  
  
## <a name="remarks"></a>Note  
 Il valore della tendenza è in genere un valore normalizzato compreso tra -1 e 1.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono restituiti valore, obiettivo, stato e tendenza dell'indicatore di prestazioni chiave (KPI) relativo alla misura del ricavo del canale per i discendenti di tre membri della gerarchia dell'attributo Fiscal Year:  
  
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
  
  
