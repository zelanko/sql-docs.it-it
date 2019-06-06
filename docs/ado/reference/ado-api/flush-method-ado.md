---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6cfc8cf9a618851e3e53b35d54fa1a989ce9c785
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697949"
---
# <a name="flush-method-ado"></a>Metodo Flush (ADO)
Forza il contenuto del [Stream](../../../ado/reference/ado-api/stream-object-ado.md) rimanenti nel buffer di ADO per l'oggetto sottostante a cui il **Stream** è associato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Stream.Flush  
```  
  
## <a name="remarks"></a>Note  
 Questo metodo può essere utilizzato per inviare il contenuto del buffer del flusso all'oggetto sottostante: ad esempio, il nodo o il file rappresentato dall'URL che rappresenta l'origine del **Stream** oggetto. Questo metodo deve essere chiamato quando si desidera garantire che tutte le modifiche che sono state apportate al contenuto di un **Stream** sono state scritte. Tuttavia, con ADO non è in genere necessario chiamare **Flush**, come ADO continuamente Svuota il buffer di quanto più possibile in background. Modifiche al contenuto di un **Stream** vengono eseguite automaticamente e non memorizzato nella cache finché **Flush** viene chiamato.  
  
 Chiusura una **Stream** con il [Chiudi](../../../ado/reference/ado-api/close-method-ado.md) metodo svuota il contenuto di un **Stream** automaticamente; non esiste, è necessario chiamare in modo esplicito **Flush**immediatamente prima **Chiudi**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
