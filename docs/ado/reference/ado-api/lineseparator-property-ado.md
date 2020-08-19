---
description: Proprietà LineSeparator (ADO)
title: Proprietà LineSeparator (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::LineSeparator
helpviewer_keywords:
- LineSeparator property [ADO]
ms.assetid: 0b20fbb8-6b83-48ec-b442-f96c8a4bafbb
author: rothja
ms.author: jroth
ms.openlocfilehash: e3571f6a01fc60377380c0dcc40c870dfc71276a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443373"
---
# <a name="lineseparator-property-ado"></a>Proprietà LineSeparator (ADO)
Indica il carattere binario da utilizzare come separatore di riga negli oggetti del [flusso](../../../ado/reference/ado-api/stream-object-ado.md) di testo.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore [LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md) che indica il carattere separatore di riga usato nel **flusso**. Il valore predefinito è **adCRLF**.  
  
## <a name="remarks"></a>Osservazioni  
 **LineSeparator** viene utilizzato per interpretare le linee durante la lettura del contenuto di un **flusso**di testo. Le righe possono essere ignorate con il metodo [SkipLine](../../../ado/reference/ado-api/skipline-method.md) .  
  
 **LineSeparator** viene utilizzato solo con gli oggetti del **flusso** di testo (il[tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) è **adTypeText**). Questa proprietà viene ignorata se il **tipo** è **adTypeBinary**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
