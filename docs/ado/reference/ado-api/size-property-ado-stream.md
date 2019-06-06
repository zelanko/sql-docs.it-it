---
title: Proprietà (ADO Stream) Size | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Size
helpviewer_keywords:
- Size property [ADO Stream]
ms.assetid: a487c241-d953-4c31-ae7e-6358d5cf6733
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 42a4725efde507112d51b4f9c41af4ba83f63da4
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719090"
---
# <a name="size-property-ado-stream"></a>Proprietà Size (Stream - ADO)
Indica le dimensioni del flusso in numero di byte.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un **lungo** valore che specifica le dimensioni del flusso in numero di byte. Il valore predefinito è la dimensione di flusso, oppure -1 se la dimensione del flusso non è noto.  
  
## <a name="remarks"></a>Note  
 **Le dimensioni** può essere utilizzata solo con open [Stream](../../../ado/reference/ado-api/stream-object-ado.md) oggetti.  
  
> [!NOTE]
>  Qualsiasi numero di bit può essere archiviato un **Stream** oggetto, limitato solo dalle risorse di sistema. Se il **Stream** contiene più bit che può essere rappresentato da un **lungo** valore **dimensioni** viene troncato e pertanto non rappresentare accuratamente la lunghezza del **Stream**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà Size (parametro ADO)](../../../ado/reference/ado-api/size-property-ado-parameter.md)
