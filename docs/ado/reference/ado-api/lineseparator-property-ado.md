---
description: Proprietà LineSeparator (ADO)
title: Proprietà LineSeparator (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 7bd1e14d5c7ebc84ea4736da08296eca0e02ea38
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990722"
---
# <a name="lineseparator-property-ado"></a>Proprietà LineSeparator (ADO)
Indica il carattere binario da utilizzare come separatore di riga negli oggetti del [flusso](./stream-object-ado.md) di testo.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore [LineSeparatorsEnum](./lineseparatorsenum.md) che indica il carattere separatore di riga usato nel **flusso**. Il valore predefinito è **adCRLF**.  
  
## <a name="remarks"></a>Osservazioni  
 **LineSeparator** viene utilizzato per interpretare le linee durante la lettura del contenuto di un **flusso**di testo. Le righe possono essere ignorate con il metodo [SkipLine](./skipline-method.md) .  
  
 **LineSeparator** viene utilizzato solo con gli oggetti del **flusso** di testo (il[tipo](./type-property-ado-stream.md) è **adTypeText**). Questa proprietà viene ignorata se il **tipo** è **adTypeBinary**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Stream (ADO)](./stream-object-ado.md)