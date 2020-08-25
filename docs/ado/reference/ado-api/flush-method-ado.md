---
description: Metodo Flush (ADO)
title: Metodo Flush (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Flush
- _Stream::raw_Flush
helpviewer_keywords:
- Flush method [ADO]
ms.assetid: 938522b4-f836-4c80-8d27-a598a000f0ee
author: rothja
ms.author: jroth
ms.openlocfilehash: 532a6bf973960e5c6a0a7d6f44ff8e0a2c2d1d09
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775140"
---
# <a name="flush-method-ado"></a>Metodo Flush (ADO)
Impone il contenuto del [flusso](./stream-object-ado.md) rimanente nel buffer ADO all'oggetto sottostante a cui è associato il **flusso** .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Stream.Flush  
```  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo può essere utilizzato per inviare il contenuto del buffer del flusso all'oggetto sottostante, ad esempio il nodo o il file rappresentato dall'URL che rappresenta l'origine dell'oggetto **flusso** . Questo metodo deve essere chiamato quando si desidera assicurarsi che tutte le modifiche apportate al contenuto di un **flusso** siano state scritte. Tuttavia, con ADO, in genere non è necessario chiamare **Flush**, in quanto ADO Scarica continuamente il buffer nel modo più possibile in background. Le modifiche al contenuto di un **flusso** vengono eseguite automaticamente e non vengono memorizzate nella cache finché non viene chiamato lo **svuotamento** .  
  
 La chiusura di un **flusso** con il metodo [Close](./close-method-ado.md) Scarica automaticamente il contenuto di un **flusso** ; non è necessario chiamare in modo esplicito lo **svuotamento** immediatamente prima della **chiusura**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](./stream-object-ado.md)