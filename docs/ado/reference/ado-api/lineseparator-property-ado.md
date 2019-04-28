---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b55f82e92ff74ba359074613205bc8086af81b5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62864455"
---
# <a name="lineseparator-property-ado"></a>Proprietà LineSeparator (ADO)
Indica il carattere da usare come separatore di riga nel testo binario [Stream](../../../ado/reference/ado-api/stream-object-ado.md) oggetti.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un [LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md) valore che indica il carattere separatore di riga utilizzato nel **Stream**. Il valore predefinito è **adCRLF**.  
  
## <a name="remarks"></a>Note  
 **Proprietà LineSeparator** viene utilizzato per interpretare le righe durante la lettura del contenuto di testo **Stream**. È possibile ignorare le righe con la [SkipLine](../../../ado/reference/ado-api/skipline-method.md) (metodo).  
  
 **Proprietà LineSeparator** viene usato solo con il testo **Stream** oggetti ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) viene **adTypeText**). Questa proprietà viene ignorata se **tipo** viene **adTypeBinary**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
