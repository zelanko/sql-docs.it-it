---
title: Barra asterisco (commento) (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5d0b929ba60915f116d9ff6843b4f20b3105a7ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942840"
---
# <a name="slash-star-comment-dmx"></a>Barra asterisco (commento) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Indica una stringa di testo che non deve essere eseguita da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Il server non valuta il testo tra i caratteri di commento / * e \*/. I commenti possono essere nidificati in un'espressione DMX (Data Mining Extensions), inclusi alla fine di una riga di codice o inseriti su una riga distinta.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
/* Comment_Text */  
```  
  
#### <a name="parameters"></a>Parametri  
 *Comment_Text*  
 Stringa contenente il testo del commento.  
  
## <a name="remarks"></a>Note  
 I commenti su più righe devono essere contrassegnati da /* e \*/.  
  
 I commenti possono essere di qualsiasi lunghezza.  
  
 Per altre informazioni su come usare diversi tipi di commenti in DMX, vedere [commenti &#40;DMX&#41;](../dmx/comments-dmx.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Doppia barra &#40;commento&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)   
 [- &#40;Commento&#41; &#40;DMX&#41; riepilogo](../dmx/comment-dmx-summary.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; di riferimento agli operatori](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operators &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
