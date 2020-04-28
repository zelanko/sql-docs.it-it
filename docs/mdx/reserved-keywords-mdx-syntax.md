---
title: Parole chiave riservate (sintassi MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d88e78e49a52919ff710cd123ab2b25022aa5d1b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68037065"
---
# <a name="reserved-keywords-mdx-syntax"></a>Parole chiave riservate (sintassi MDX)


  Analysis Services riserva determinate parole chiave per l'uso esclusivo. Per un elenco delle parole chiave riservate, vedere [parole riservate MDX](../mdx/mdx-reserved-words.md).  
  
 Di seguito sono riportate le linee guida per l'utilizzo delle parole chiave riservate:  
  
-   Non è possibile includere parole chiave riservate in un'istruzione MDX (Multidimensional Expressions) in posizioni diverse da quella definita da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
-   Non è possibile assegnare agli oggetti di database nomi uguali a parole chiave riservate. Se esistono oggetti con nomi di questo tipo, per farvi riferimento sarà sempre necessario utilizzare identificatori delimitati. Anche se in questo modo è possibile assegnare agli oggetti nomi costituiti da parole riservate, è comunque preferibile evitare di utilizzare parole chiave come nomi per gli oggetti.  
  
-   Adottare una convenzione di denominazione che evita l'utilizzo di parole chiave riservate. Se è necessario attribuire a un oggetto un nome simile a una parola chiave riservata, eliminare le consonanti o le vocali da tale parola.  
  
## <a name="see-also"></a>Vedere anche  
 [Elementi della sintassi MDX &#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
