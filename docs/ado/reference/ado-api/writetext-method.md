---
title: Metodo WriteText | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_WriteText
- _Stream::WriteText
helpviewer_keywords:
- WriteText method [ADO]
ms.assetid: 7a669048-13f4-4574-a2b1-985e089729d5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3b50db388151de1f5b99d8d9a3f48904e6d7c2c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642957"
---
# <a name="writetext-method"></a>Metodo WriteText
Scrive una stringa di testo specificato in un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Stream.WriteText Data, Options  
```  
  
#### <a name="parameters"></a>Parametri  
 *Dati*  
 Oggetto **stringa** valore contenente il testo in caratteri da scrivere.  
  
 *Opzioni*  
 Facoltativo. Oggetto [StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md) valore che indica se deve essere scritto un carattere separatore di riga alla fine della stringa specificata.  
  
## <a name="remarks"></a>Note  
 Stringhe specificate sono scritti per il **Stream** oggetto senza spazi o caratteri tra ogni stringa.  
  
 L'oggetto corrente [posizione](../../../ado/reference/ado-api/position-property-ado.md) è impostato sul carattere che segue i dati scritti. Il **WriteText** metodo non tronca il resto dei dati in un flusso. Se si desidera troncare questi caratteri, chiamare [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 Se si scrivono corrente [EOS](../../../ado/reference/ado-api/eos-property.md) posizione, la [Size](../../../ado/reference/ado-api/size-property-ado-stream.md) del **Stream** aumenterà per includere eventuali nuovi caratteri, e **EOS** verrà pertanto spostato di nuovo ultimo byte i **Stream**.  
  
> [!NOTE]
>  Il **WriteText** metodo viene utilizzato con i flussi di testo ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) viene **adTypeText**). Per i flussi binari (**tipo** viene **adTypeBinary**), utilizzare [scrivere](../../../ado/reference/ado-api/write-method.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Write](../../../ado/reference/ado-api/write-method.md)
