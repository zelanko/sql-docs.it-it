---
title: Metodo Write | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_Write
- _Stream::Write
helpviewer_keywords:
- Write method [ADO]
ms.assetid: 02982e6a-ac5f-4af2-b82e-ce12534b84b2
author: rothja
ms.author: jroth
ms.openlocfilehash: 911a9dfb21c054dc95c54d9fb429d628d8e01fa4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764432"
---
# <a name="write-method"></a>Metodo Write
Scrive dati binari in un oggetto [flusso](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Stream.Write Buffer  
```  
  
#### <a name="parameters"></a>Parametri  
 *Buffer*  
 **Variant** che contiene una matrice di byte da scrivere.  
  
## <a name="remarks"></a>Commenti  
 I byte specificati vengono scritti nell'oggetto **flusso** senza spazi intermedi tra i byte.  
  
 La [posizione](../../../ado/reference/ado-api/position-property-ado.md) corrente è impostata sul byte che segue i dati scritti. Il metodo **Write** non tronca il resto dei dati in un flusso. Se si desidera troncare questi byte, chiamare [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 Se si scrive oltre la posizione [EOS](../../../ado/reference/ado-api/eos-property.md) corrente, le [dimensioni](../../../ado/reference/ado-api/size-property-ado-stream.md) del **flusso** verranno aumentate in modo da contenere nuovi byte e **EOS** passerà al nuovo ultimo byte nel **flusso**.  
  
> [!NOTE]
>  Il metodo **Write** viene usato con i flussi binari (il[tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) è **adTypeBinary**). Per i flussi di testo (**tipo** è **adTypeText**), usare [WRITETEXT](../../../ado/reference/ado-api/writetext-method.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo WriteText](../../../ado/reference/ado-api/writetext-method.md)
