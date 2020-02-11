---
title: Parole chiave riservate (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fa17a4fb673ad6508fbfc70d5bab39e398d6c3aa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67928451"
---
# <a name="reserved-keywords-dmx"></a>Parole chiave riservate (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)] riserva determinate parole chiave per l'uso esclusivo. Tali parole chiave non possono essere utilizzate liberamente nelle istruzioni DMX (Data Mining Extensions), ma solo nelle posizioni definite da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] nelle informazioni di riferimento al linguaggio DMX. Queste parole chiave DMX con restrizioni includono i membri seguenti:  
  
-   Tutte le istruzioni di definizione dei dati elencate nell'argomento [istruzioni DMX per la definizione dei dati](../dmx/dmx-statements-data-definition.md).  
  
-   Tutte data mining funzioni di query elencate nell'argomento Guida di riferimento alle funzioni [DMX](../dmx/data-mining-extensions-dmx-function-reference.md).  
  
-   Tutti gli operatori elencati nell'argomento [riferimento all'operatore DMX](../dmx/data-mining-extensions-dmx-operator-reference.md).  
  
-   Le parole chiave definite nel linguaggio di query MDX (Multidimensional Expressions) sono incluse come parte di un'istruzione DMX.  
  
-   Le parole chiave definite nella specifica OLE DB for Data Mining sono incluse come parte di un'istruzione DMX.  
  
 Quando si assegnano nomi agli oggetti di un database, è consigliabile utilizzare una convenzione di denominazione che eviti l'utilizzo delle parole chiave riservate.  
  
 Se il database contiene nomi che corrispondono a parole chiave riservate, sarà necessario utilizzare identificatori delimitati per fare riferimento a tali oggetti. Per ulteriori informazioni, vedere [identificatori &#40;&#41;DMX ](../dmx/identifiers-dmx.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle estensioni di data mining &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Guida di riferimento alle istruzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40;le convenzioni della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Data Mining Extensions &#40;elementi della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
