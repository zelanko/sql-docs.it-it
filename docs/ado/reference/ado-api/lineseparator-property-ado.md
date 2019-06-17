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
manager: jroth
ms.openlocfilehash: e3035e8614dbe57d131ee77dc77fb85605499c15
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66694728"
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
