---
description: Metodo CopyTo (ADO)
title: Metodo CopyTo (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7bbb394810ebbfe8d8c0e1d598641a1e77e7d204
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974552"
---
# <a name="copyto-method-ado"></a>Metodo CopyTo (ADO)
Copia il numero specificato di caratteri o byte (a seconda del [tipo](./type-property-ado-stream.md)) nel [flusso](./stream-object-ado.md) in un altro oggetto **flusso** .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Stream.CopyTo DestStream, NumChars  
```  
  
#### <a name="parameters"></a>Parametri  
 *DestStream*  
 Valore della variabile oggetto che contiene un riferimento a un oggetto **flusso** aperto. Il **flusso** corrente viene copiato nel **flusso** di destinazione specificato da *DestStream*. Il **flusso** di destinazione deve essere già aperto. In caso contrario, si verifica un errore di run-time.  
  
> [!NOTE]
>  Il parametro *DestStream* non può essere un proxy di un oggetto **Stream** perché è necessario l'accesso a un'interfaccia privata nell'oggetto **flusso** che non può essere eseguito in modalità remota per il client.  
  
 *NumChars*  
 Facoltativa. Valore **intero** che specifica il numero di byte o caratteri da copiare dalla posizione corrente nel **flusso** di origine al **flusso**di destinazione. Il valore predefinito è-1, che specifica che tutti i caratteri o i byte vengono copiati dalla posizione corrente a [EOS](./eos-property.md).  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo copia il numero specificato di caratteri o byte, a partire dalla posizione corrente specificata dalla proprietà [position](./position-property-ado.md) . Se il numero specificato è maggiore del numero di byte disponibili fino a **EOS**, vengono copiati solo i caratteri o i byte dalla posizione corrente a **EOS** . Se il valore di *NumChars* è-1 o omesso, vengono copiati tutti i caratteri o i byte a partire dalla posizione corrente.  
  
 Se nel flusso di destinazione sono presenti caratteri o byte esistenti, tutto il contenuto oltre il punto in cui termina la copia rimane invariato e non viene troncato. **Position** diventa il byte immediatamente successivo all'ultimo byte copiato. Se si desidera troncare questi byte, chiamare [SetEOS](./seteos-method.md).  
  
 **CopyTo** deve essere usato per copiare i dati in un **flusso** di destinazione dello stesso tipo del **flusso** di origine (le impostazioni delle proprietà del **tipo** sono sia **adTypeText** sia **adTypeBinary**). Per gli oggetti del **flusso** di testo, è possibile modificare l'impostazione della proprietà [CharSet](./charset-property-ado.md) del **flusso** di destinazione per tradurre da un set di caratteri a un altro. Inoltre, gli oggetti del **flusso** di testo possono essere copiati correttamente in oggetti **flusso** binario, ma gli oggetti **flusso** binario non possono essere copiati in oggetti del **flusso** di testo.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](./stream-object-ado.md)