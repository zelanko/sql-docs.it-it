---
title: Metodo CopyTo (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_CopyTo
- _Stream::CopyTo
helpviewer_keywords:
- CopyTo method [ADO]
ms.assetid: b4aa5714-916b-48b8-8b09-cc2708379602
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cbfdff7c22152acfd0deb97a6e278bd5fd3f553f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698435"
---
# <a name="copyto-method-ado"></a>Metodo CopyTo (ADO)
Copia il numero specificato di caratteri o byte (a seconda [tipo](../../../ado/reference/ado-api/type-property-ado-stream.md)) nella [Stream](../../../ado/reference/ado-api/stream-object-ado.md) a un altro **Stream** oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Stream.CopyTo DestStream, NumChars  
```  
  
#### <a name="parameters"></a>Parametri  
 *DestStream*  
 Un valore della variabile oggetto che contiene un riferimento a un oggetto aperto **Stream** oggetto. L'oggetto corrente **Stream** viene copiato nella destinazione **Stream** specificati da *DestStream*. La destinazione **Stream** deve già essere aperta. In caso contrario, si verifica un errore di run-time.  
  
> [!NOTE]
>  Il *DestStream* parametro non può essere un proxy di **Stream** dell'oggetto perché questo richiede l'accesso a un'interfaccia privata nel **Stream** oggetto che non può essere eseguita in modalità remota per il client.  
  
 *NumChars*  
 Facoltativo. Un' **Integer** valore che specifica il numero di byte o caratteri da copiare dalla posizione corrente nell'origine **Stream** alla destinazione **Stream**. Il valore predefinito è -1, che specifica che tutti i caratteri o byte vengono copiati dalla posizione corrente per [EOS](../../../ado/reference/ado-api/eos-property.md).  
  
## <a name="remarks"></a>Note  
 Questo metodo copia il numero specificato di caratteri o byte, a partire dalla posizione corrente specificata dal [posizione](../../../ado/reference/ado-api/position-property-ado.md) proprietà. Se il numero specificato è maggiore del numero disponibile di byte fino **EOS**, quindi solo caratteri o byte dalla posizione corrente alla **EOS** vengono copiati. Se il valore di *NumChars* è -1 o viene omesso, vengono copiati tutti i caratteri o byte a partire dalla posizione corrente.  
  
 Se sono presenti caratteri o byte nel flusso di destinazione, tutto il contenuto oltre il punto in cui termina la copia rimanga e non viene troncato. **Posizione** diventa il byte immediatamente dopo l'ultimo byte copiato. Se si desidera troncare i byte, chiamare [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 **CopyTo** deve essere utilizzato per copiare i dati a una destinazione **Stream** dello stesso tipo dell'origine **Stream** (loro **tipo** le impostazioni delle proprietà sono entrambe **adTypeText** o entrambi **adTypeBinary**). Per il testo **Stream** oggetti, è possibile modificare le [Charset](../../../ado/reference/ado-api/charset-property-ado.md) impostazione della proprietà dell'oggetto di destinazione **Stream** per la conversione da un set di caratteri da un altro. Inoltre, il testo **Stream** gli oggetti possono essere copiati in formato binario **Stream** oggetti, ma binario **Stream** oggetti non possono essere copiati in testo **Stream**  oggetti.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
