---
title: Aggiornamento di celle (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- modifying cells
- XMLA, cells
- updating cells
- cells [Analysis Services]
- XML for Analysis, cells
ms.assetid: a1c61496-36ee-4bce-98d9-d13440d349aa
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2c3d9a7c27533666c75102d9eac3b8311bfe4af6
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544913"
---
# <a name="updating-cells-xmla"></a>Aggiornamento di celle (XMLA)
  È possibile utilizzare il comando [UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla) per modificare il valore di una o più celle in un cubo abilitato per il writeback del cubo. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] archivia le informazioni aggiornate in una tabella writeback separata per ogni partizione che contiene le celle da aggiornare.  
  
> [!NOTE]  
>  Il comando `UpdateCells` non supporta le allocazioni durante il writeback del cubo. Per utilizzare il writeback allocato, è necessario utilizzare il comando [Statement](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) per inviare un'istruzione di aggiornamento MDX (Multidimensional Expressions). Per ulteriori informazioni, vedere [istruzione UPDATE CUBE &#40;&#41;MDX ](/sql/mdx/mdx-data-manipulation-update-cube).  
  
## <a name="specifying-cells"></a>Specifica di celle  
 La proprietà [Cell](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) del `UpdateCells` comando contiene le celle da aggiornare. Per identificare ogni cella nella proprietà `Cell`, utilizzare i numero ordinale della cella specifica. Concettualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] numera le celle di un cubo come se il cubo fosse una matrice *p*-dimensionale, dove *p* è il numero di assi. Le celle sono indirizzate in ordine di riga. Nell'illustrazione seguente viene illustrata la formula per calcolare il numero ordinale di una cella.  
  
 ![Formula per calcolare la posizione ordinale della cella](../../analysis-services/dev-guide/media/cellordinalformula.gif "Formula per calcolare la posizione ordinale della cella")  
  
 Quando si conosce il numero ordinale di una cella, è possibile indicare il valore desiderato della cella nella proprietà [value](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/value-element-xmla) della proprietà della [cella](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) .  
  
## <a name="see-also"></a>Vedere anche  
 [Elemento Update &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [Sviluppo con XMLA in Analysis Services](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
