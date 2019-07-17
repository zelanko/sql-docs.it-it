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
ms.openlocfilehash: e9eb05d633dcbe660c34793fa39c10d788574700
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098378"
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
  
## <a name="remarks"></a>Note  
 Il *Measure_Name* deve essere racchiuso tra parentesi quadre.  
  
 L'istruzione CREATE MEASURE può essere usato solo all'interno di una definizione di script MDX. visualizzare [elemento MdxScript &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/objects/mdxscript-element-assl).  
  
 È inoltre possibile definire un membro calcolato da usare in un'unica query. Per definire un membro calcolato limitato a una singola query, è possibile usare la clausola WITH nell'istruzione SELECT. Per altre informazioni, vedere [compilazione di misure in MDX](../analysis-services/multidimensional-models/mdx/mdx-building-measures.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzioni di definizione dei dati MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
