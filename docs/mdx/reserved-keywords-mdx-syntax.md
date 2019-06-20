---
title: Parole chiave (sintassi MDX) riservate | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2f50b0292b9139dcbb2b3a5652ad41136b31702a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149861"
---
# <a name="reserved-keywords-mdx-syntax"></a>Parole chiave riservate (sintassi MDX)


  Analysis Services vengano riservate determinate parole chiave per un uso esclusivo. Per un elenco di parole chiave riservate, vedere [parole riservate MDX](../mdx/mdx-reserved-words.md).  
  
 Di seguito sono riportate le linee guida per l'utilizzo delle parole chiave riservate:  
  
-   Non è possibile includere parole chiave riservate in un'istruzione MDX (Multidimensional Expressions) in posizioni diverse da quella definita da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
-   Non è possibile assegnare agli oggetti di database nomi uguali a parole chiave riservate. Se esistono oggetti con nomi di questo tipo, per farvi riferimento sarà sempre necessario utilizzare identificatori delimitati. Anche se in questo modo è possibile assegnare agli oggetti nomi costituiti da parole riservate, è comunque preferibile evitare di utilizzare parole chiave come nomi per gli oggetti.  
  
-   Adottare una convenzione di denominazione che evita l'utilizzo di parole chiave riservate. Se è necessario attribuire a un oggetto un nome simile a una parola chiave riservata, eliminare le consonanti o le vocali da tale parola.  
  
## <a name="see-also"></a>Vedere anche  
 [Elementi della sintassi MDX &#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
