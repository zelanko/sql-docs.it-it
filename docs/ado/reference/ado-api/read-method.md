---
description: Metodo Read
title: Metodo Read | Microsoft Docs
ms.prod: sql
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6600c02af5c24fc1ce27a04422678f8a3f40a179
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442553"
---
# <a name="read-method"></a>Metodo Read
Legge un numero specificato di byte da un oggetto [flusso](../../../ado/reference/ado-api/stream-object-ado.md) binario.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Variant = Stream.Read ( NumBytes)  
```  
  
#### <a name="parameters"></a>Parametri  
 *NumBytes*  
 Facoltativo. Valore **Long** che specifica il numero di byte da leggere dal file o il valore [StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md) **adReadAll**, che corrisponde all'impostazione predefinita.  
  
## <a name="return-value"></a>Valore restituito  
 Il metodo **Read** legge un numero specificato di byte o l'intero flusso da un oggetto **Stream** e restituisce i dati risultanti come **Variant**.  
  
## <a name="remarks"></a>Osservazioni  
 Se *numBytes* è maggiore del numero di byte rimanenti nel **flusso**, vengono restituiti solo i byte rimanenti. I dati letti non vengono riempiti in modo da corrispondere alla lunghezza specificata da *numBytes*. Se non ci sono byte rimanenti da leggere, viene restituita una variante con un valore null. Impossibile utilizzare **Read** per leggere le versioni precedenti.  
  
> [!NOTE]
>  *NumBytes* misura sempre i byte. Per gli oggetti del **flusso** di testo ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) è **adTypeText**), usare [READTEXT](../../../ado/reference/ado-api/readtext-method.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo ReadText](../../../ado/reference/ado-api/readtext-method.md)
