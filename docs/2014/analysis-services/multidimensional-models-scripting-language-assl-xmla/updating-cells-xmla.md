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
manager: craigg
ms.openlocfilehash: 56c4313ea77fc342c2d7ac4fb142d922038948ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62702022"
---
# <a name="updating-cells-xmla"></a>Aggiornamento di celle (XMLA)
  È possibile usare la [UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla) comandi per modificare il valore di uno o più celle in un cubo abilitato per il writeback del cubo. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Archivia le informazioni aggiornate in una tabella writeback separata per ogni partizione che contiene le celle da aggiornare.  
  
> [!NOTE]  
>  Il comando `UpdateCells` non supporta le allocazioni durante il writeback del cubo. Per utilizzare l'allocazione del writeback, è consigliabile usare la [istruzione](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) comando per inviare un'istruzione UPDATE di MDX (Multidimensional Expressions). Per altre informazioni, vedere [istruzione UPDATE CUBE &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-update-cube).  
  
## <a name="specifying-cells"></a>Specifica di celle  
 Il [cella](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) proprietà del `UpdateCells` comando contiene le celle da aggiornare. Per identificare ogni cella nella proprietà `Cell`, utilizzare i numero ordinale della cella specifica. Concettualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] numeri di celle in un cubo come se quest'ultimo fosse una *p*-matrice dimensionale, dove *p* è il numero di assi. Le celle sono indirizzate in ordine di riga. Nell'illustrazione seguente viene illustrata la formula per calcolare il numero ordinale di una cella.  
  
 ![Formula per calcolare la posizione ordinale della cella](../../../2014/analysis-services/dev-guide/media/cellordinalformula.gif "Formula per calcolare la posizione ordinale della cella")  
  
 Dopo aver individuato un numero ordinale della cella, è possibile indicare il valore desiderato della cella i [valore](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/value-element-xmla) proprietà del [cella](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) proprietà.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornare l'elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [Sviluppo con XMLA in Analysis Services](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
