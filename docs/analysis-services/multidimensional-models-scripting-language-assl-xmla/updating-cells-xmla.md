---
title: Aggiornamento di celle (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0cfee2adf9d730b458fd482317d16d963f15ebc1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63262170"
---
# <a name="updating-cells-xmla"></a>Aggiornamento di celle (XMLA)
  È possibile usare la [UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla) comandi per modificare il valore di uno o più celle in un cubo abilitato per il writeback del cubo. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Archivia le informazioni aggiornate in una tabella writeback separata per ogni partizione che contiene le celle da aggiornare.  
  
> [!NOTE]  
>  Il **UpdateCells** comando non supporta le allocazioni durante il writeback del cubo. Per utilizzare l'allocazione del writeback, è consigliabile usare la [istruzione](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) comando per inviare un'istruzione UPDATE di MDX (Multidimensional Expressions). Per altre informazioni, vedere [istruzione UPDATE CUBE &#40;MDX&#41;](../../mdx/mdx-data-manipulation-update-cube.md).  
  
## <a name="specifying-cells"></a>Specifica di celle  
 Il [cella](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) proprietà delle **UpdateCells** comando contiene le celle da aggiornare. Identificare ogni cella nella **cella** proprietà utilizzando un numero ordinale della cella. Concettualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] numeri di celle in un cubo come se quest'ultimo fosse una *p*-matrice dimensionale, dove *p* è il numero di assi. Le celle sono indirizzate in ordine di riga. Nell'illustrazione seguente viene illustrata la formula per calcolare il numero ordinale di una cella.  
  
 ![Formula per calcolare la posizione ordinale della cella](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/media/cellordinalformula.gif "Formula per calcolare la posizione ordinale della cella")  
  
 Dopo aver individuato un numero ordinale della cella, è possibile indicare il valore desiderato della cella i [valore](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/value-element-xmla) proprietà del [cella](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) proprietà.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornare l'elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [Sviluppo con XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
