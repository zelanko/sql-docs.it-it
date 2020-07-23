---
title: Istruzione CREATE MEASURE (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3bac5d7d067186e2b84277a5c0dc02cd31cba011
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "86967382"
---
# <a name="mdx-data-definition---create-measure"></a>Definizione dei dati MDX - CREATE MEASURE


  Consente di creare una misura in un modello tabulare.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CREATE MEASURE Table_Name[Measure_Name] = DAX_Expression  
[; CREATE MEASURE ...n]  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *Table_Name*  
 Valore letterale stringa valido che fornisce il nome della tabella in cui verrà creata la misura.  
  
 *Measure_Name*  
 Valore letterale stringa valido che fornisce il nome di una misura.  
  
 *DAX_Expression*  
 Espressione DAX valida tramite cui viene restituito un singolo valore scalare.  
  
## <a name="remarks"></a>Osservazioni  
 Il *Measure_Name* deve essere racchiuso tra parentesi quadre.  
  
 L'istruzione CREATE MEASURE può essere utilizzata solo all'interno di una definizione di script MDX. vedere [elemento MdxScript &#40;&#41;ASSL ](https://docs.microsoft.com/analysis-services/assl/objects/mdxscript-element-assl?view=asallproducts-allversions).  
  
 È inoltre possibile definire un membro calcolato da usare in un'unica query. Per definire un membro calcolato limitato a una singola query, è possibile usare la clausola WITH nell'istruzione SELECT. Per ulteriori informazioni, vedere [compilazione di misure in MDX](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-building-measures).  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzioni MDX per la definizione dei dati &#40;&#41;MDX](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
