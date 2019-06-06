---
title: Proprietà (ADO Stream) di tipo | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c8cad8d669452fb5d3bdff154cd7c07239f25044
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710885"
---
# <a name="type-property-ado-stream"></a>Proprietà Type (Stream - ADO)
Indica il tipo di dati contenuti nella [Stream](../../../ado/reference/ado-api/stream-object-ado.md) (binario o testo).  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un [StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md) valore che specifica il tipo di dati contenuti nella **Stream** oggetto. Il valore predefinito è **adTypeText**. Tuttavia, se i dati binari viene scritto inizialmente in un nuovo, vuoto **Stream**, il **tipo** verrà modificato **adTypeBinary**.  
  
## <a name="remarks"></a>Note  
 Il **tipo** proprietà è di lettura/scrittura solo quando la posizione corrente è all'inizio del **Stream** ([posizione](../../../ado/reference/ado-api/position-property-ado.md) è 0), sola lettura e in qualsiasi altra posizione.  
  
 Il**tipo** proprietà determina quali metodi usare per leggere e scrivere le **Stream**. Per il testo **flussi**, usare [ReadText](../../../ado/reference/ado-api/readtext-method.md) e [WriteText](../../../ado/reference/ado-api/writetext-method.md). Per i dati binari **flussi**, usare [lettura](../../../ado/reference/ado-api/read-method.md) e [scrivere](../../../ado/reference/ado-api/write-method.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà RecordType (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Proprietà Type (ADO)](../../../ado/reference/ado-api/type-property-ado.md)
