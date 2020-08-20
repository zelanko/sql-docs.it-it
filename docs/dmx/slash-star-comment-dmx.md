---
description: Barra stella (commento) (DMX)
title: Barra stella (commento) (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 011d72bfcb0b72d1b73579e81dc6f82e4d50da69
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500863"
---
# <a name="slash-star-comment-dmx"></a>Barra stella (commento) (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Indica una stringa di testo che non deve essere eseguita da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Il server non valuta il testo tra i caratteri di commento/* e \* /. I commenti possono essere nidificati in un'espressione DMX (Data Mining Extensions), inclusi alla fine di una riga di codice o inseriti su una riga distinta.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
/* Comment_Text */  
```  
  
#### <a name="parameters"></a>Parametri  
 *Comment_Text*  
 Stringa contenente il testo del commento.  
  
## <a name="remarks"></a>Osservazioni  
 I commenti su più righe devono essere contrassegnati da /* e \*/.  
  
 I commenti possono essere di qualsiasi lunghezza.  
  
 Per ulteriori informazioni sull'utilizzo di diversi tipi di commenti in DMX, vedere la pagina relativa ai [commenti &#40;&#41;DMX ](../dmx/comments-dmx.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Barra doppia &#40;commento&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)   
 [--&#40;commento&#41; &#40;Riepilogo&#41; DMX](../dmx/comment-dmx-summary.md)   
 [Guida di riferimento agli operatori DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operatori &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
