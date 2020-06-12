---
title: Operatori aritmetici (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 149cd67594cac64fc8ad315b2fca9bb1cda373d5
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669311"
---
# <a name="operators---arithmetic"></a>Operatori aritmetici
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  È possibile utilizzare gli operatori aritmetici in DMX (Data Mining Extensions) per calcoli aritmetici in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , tra cui addizioni, sottrazioni, moltiplicazioni e divisioni.  
  
 Gli operatori aritmetici supportati da DMX sono indicati nella tabella seguente.  
  
|Operatore|Descrizione|  
|--------------|-----------------|  
|[+ &#40;aggiungere&#41; &#40;DMX&#41;](../dmx/add-dmx.md)|Somma due numeri.|  
|[-&#40;sottrarre&#41; &#40;DMX&#41;](../dmx/subtract-dmx.md)|Sottrae un numero da un altro.|  
|[&#42; &#40;moltiplica&#41; &#40;DMX&#41;](../dmx/multiply-dmx.md)|Esegue una moltiplicazione tra due numeri.|  
|[&#40;divide&#41; &#40;DMX&#41;](../dmx/divide-dmx.md)|Esegue una divisione di un numero per un altro.|  
  
 L'ordine di precedenza per gli operatori aritmetici in un'espressione DMX è determinato dalle regole seguenti:  
  
-   Se un'espressione include più operatori aritmetici, verranno eseguite per prime le operazioni di moltiplicazione e divisione, seguite da sottrazione e addizione.  
  
-   Se tutti gli operatori aritmetici di un'espressione hanno la stessa precedenza, le operazioni verranno eseguite da sinistra a destra.  
  
-   Le espressioni tra parentesi hanno la precedenza su tutte le altre operazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle estensioni di data mining &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Guida di riferimento agli operatori DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Guida di riferimento alle istruzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40;le convenzioni della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Data Mining Extensions &#40;elementi della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Espressioni &#40;DMX&#41;](../dmx/expressions-dmx.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Operatori &#40;DMX&#41;](../dmx/operators-dmx.md)   
 [Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
