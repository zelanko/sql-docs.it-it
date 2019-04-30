---
title: Proprietà EOS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EOS
- Stream::EOS
helpviewer_keywords:
- EOS property
ms.assetid: 57e08c5f-f3ed-4ecd-8c66-50b83b1031d1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47b3e48e612e0ee5595ada33127f016ee6b986f1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63180992"
---
# <a name="eos-property"></a>Proprietà EOS
Indica se la posizione corrente è alla fine del [flusso](../../../ado/reference/ado-api/stream-object-ado.md).  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un **booleana** valore che indica se la posizione corrente è alla fine del flusso. **EOS** restituisce **True** se esistono più byte nel flusso; restituisce **False** se sono presenti più byte seguendo la posizione corrente.  
  
 Per impostare la fine della posizione del flusso, usare il [SetEOS](../../../ado/reference/ado-api/seteos-method.md) (metodo). Per determinare la posizione corrente, usare il [posizione](../../../ado/reference/ado-api/position-property-ado.md) proprietà.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [EOS e LineSeparator proprietà e metodo SkipLine esempio (VB)](../../../ado/reference/ado-api/eos-and-lineseparator-properties-and-skipline-method-example-vb.md)   
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
