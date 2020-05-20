---
title: Proprietà Type (flusso ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Type
- _Stream::get_Type
- _Stream::put_Type
helpviewer_keywords:
- Type property [ADO Stream]
ms.assetid: f6a17e8c-7a28-48d0-bded-76b9e0cf7639
author: rothja
ms.author: jroth
ms.openlocfilehash: de61f4877dc6adcdfaa9644f5f266cd827a1d096
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765342"
---
# <a name="type-property-ado-stream"></a>Proprietà Type (Stream - ADO)
Indica il tipo di dati contenuti nel [flusso](../../../ado/reference/ado-api/stream-object-ado.md) (binario o testo).  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore [StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md) che specifica il tipo di dati contenuti nell'oggetto **flusso** . Il valore predefinito è **adTypeText**. Tuttavia, se inizialmente i dati binari vengono scritti in un nuovo **flusso**vuoto, il **tipo** verrà modificato in **adTypeBinary**.  
  
## <a name="remarks"></a>Commenti  
 La proprietà **Type** è di lettura/scrittura solo quando la posizione corrente si trova all'inizio del **flusso** ([position](../../../ado/reference/ado-api/position-property-ado.md) è 0) e di sola lettura in qualsiasi altra posizione.  
  
 La proprietà**Type** determina i metodi da utilizzare per la lettura e la scrittura del **flusso**. Per i **flussi**di testo, usare [READTEXT](../../../ado/reference/ado-api/readtext-method.md) e [WRITETEXT](../../../ado/reference/ado-api/writetext-method.md). Per i **flussi**binari, usare [lettura](../../../ado/reference/ado-api/read-method.md) e [scrittura](../../../ado/reference/ado-api/write-method.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà RecordType (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Proprietà Type (ADO)](../../../ado/reference/ado-api/type-property-ado.md)
