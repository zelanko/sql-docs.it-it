---
title: Proprietà Size (flusso ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e17bb879c63e01d8f912bb7147061099bd3e2c10
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759867"
---
# <a name="size-property-ado-stream"></a>Proprietà Size (Stream - ADO)
Indica le dimensioni del flusso in numero di byte.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un valore **Long** che specifica le dimensioni del flusso in numero di byte. Il valore predefinito corrisponde alla dimensione del flusso oppure-1 se la dimensione del flusso non è nota.  
  
## <a name="remarks"></a>Osservazioni  
 Le **dimensioni** possono essere utilizzate solo con gli oggetti [flusso](../../../ado/reference/ado-api/stream-object-ado.md) aperti.  
  
> [!NOTE]
>  Un numero qualsiasi di bit può essere archiviato in un oggetto **flusso** , limitato solo dalle risorse di sistema. Se il **flusso** contiene più bit di quelli che possono essere rappresentati da un valore **Long** , le **dimensioni** vengono troncate e pertanto non rappresentano accuratamente la lunghezza del **flusso**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà Size (Parameter - ADO)](../../../ado/reference/ado-api/size-property-ado-parameter.md)
