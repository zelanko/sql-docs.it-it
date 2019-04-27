---
title: Parole chiave (DMX) riservate | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7af060203d044435e364803ace67d35711eb63ea
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62658805"
---
# <a name="reserved-keywords-dmx"></a>Parole chiave riservate (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)] riserva determinate parole chiave per un uso esclusivo. Tali parole chiave non possono essere utilizzate liberamente nelle istruzioni DMX (Data Mining Extensions), ma solo nelle posizioni definite da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] nelle informazioni di riferimento al linguaggio DMX. Queste parole chiave DMX con restrizioni includono i membri seguenti:  
  
-   Tutte le istruzioni di definizione dei dati elencate nell'argomento [istruzioni di definizione dati DMX](../dmx/dmx-statements-data-definition.md).  
  
-   Tutti i dati elencate nell'argomento, le funzioni di query di data mining [riferimento alle funzioni DMX](../dmx/data-mining-extensions-dmx-function-reference.md).  
  
-   Tutti gli operatori elencati nell'argomento [riferimento agli operatori DMX](../dmx/data-mining-extensions-dmx-operator-reference.md).  
  
-   Le parole chiave definite nel linguaggio di query MDX (Multidimensional Expressions) sono incluse come parte di un'istruzione DMX.  
  
-   Le parole chiave definite nella specifica OLE DB for Data Mining sono incluse come parte di un'istruzione DMX.  
  
 Quando si assegnano nomi agli oggetti di un database, è consigliabile utilizzare una convenzione di denominazione che eviti l'utilizzo delle parole chiave riservate.  
  
 Se il database contiene nomi che corrispondono a parole chiave riservate, sarà necessario utilizzare identificatori delimitati per fare riferimento a tali oggetti. Per altre informazioni, vedere [identificatori &#40;DMX&#41;](../dmx/identifiers-dmx.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle istruzioni](../dmx/data-mining-extensions-dmx-statements.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; convenzioni della sintassi](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; gli elementi della sintassi](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
