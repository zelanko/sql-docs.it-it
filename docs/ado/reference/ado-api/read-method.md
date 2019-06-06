---
title: Metodo Read | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Stream::raw_Read
- _Stream::Read
helpviewer_keywords:
- Read method [ADO]
ms.assetid: 838502de-80f1-4eeb-8838-dd3d9403e567
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f4594e4b85ad66b1ab11a2966bc7a0d79815db09
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702976"
---
# <a name="read-method"></a>Metodo Read
Legge un numero specificato di byte da un file binario [Stream](../../../ado/reference/ado-api/stream-object-ado.md) oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Variant = Stream.Read ( NumBytes)  
```  
  
#### <a name="parameters"></a>Parametri  
 *NumBytes*  
 Facoltativo. Oggetto **lungo** valore che specifica il numero di byte da leggere dal file o la [StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md) valore **adReadAll**, ovvero l'impostazione predefinita.  
  
## <a name="return-value"></a>Valore restituito  
 Il **Read** metodo legge un numero specificato di byte o dell'intero flusso da un **Stream** dell'oggetto e restituisce i dati risultanti come una **Variant**.  
  
## <a name="remarks"></a>Note  
 Se *NumBytes* è maggiore del numero di byte a sinistra nel **Stream**, vengono restituiti solo i byte rimanenti. I dati letti non possono essere riempiti per corrispondere alla lunghezza specificata da *NumBytes*. Se sono presenti byte rimanenti da leggere, viene restituita una variante con un valore null. **Lettura** non può essere usato per leggere le versioni precedenti.  
  
> [!NOTE]
>  *NumBytes* misura sempre i byte. Per il testo **Stream** oggetti ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) viene **adTypeText**), usare [ReadText](../../../ado/reference/ado-api/readtext-method.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo ReadText](../../../ado/reference/ado-api/readtext-method.md)
