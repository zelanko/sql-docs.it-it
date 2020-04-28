---
title: Cursori statici | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], static
- static cursors [ADO]
ms.assetid: cce93ace-c4ed-4c6c-940c-28a50ff2fd12
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 520c484bdaaa6eb59488900208993a607c5b0f7b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924112"
---
# <a name="static-cursors"></a>Cursori statici
Il cursore statico Visualizza sempre il set di risultati così come era quando il cursore è stato aperto per la prima volta. A seconda dell'implementazione, i cursori statici sono di sola lettura o di lettura/scrittura e forniscono lo scorrimento avanti e indietro. Il cursore statico non rileva in genere le modifiche apportate all'appartenenza, all'ordine o ai valori del set di risultati dopo l'apertura del cursore. I cursori statici possono rilevare le proprie operazioni di aggiornamento, eliminazione e inserimento, anche se tale rilevamento non è obbligatorio per cursori di questo tipo.  
  
 I cursori statici non rilevano mai altri aggiornamenti, eliminazioni e inserimenti. Si supponga, ad esempio, che un cursore statico recuperi una riga e che un'altra applicazione aggiorni in seguito tale riga. Se l'applicazione recupera nuovamente la riga dal cursore statico, i valori che rileva sono invariati, nonostante le modifiche apportate dall'altra applicazione. Sono supportati tutti i tipi di scorrimento, ma è possibile che i provider non supportino i segnalibri.  
  
 Se non è necessario che l'applicazione rilevi le modifiche ai dati ed è necessario lo scorrimento, il cursore statico è la scelta migliore. Usare **AdOpenStatic CursorTypeEnum** per indicare che si vuole usare un cursore statico in ADO.  
  
## <a name="see-also"></a>Vedere anche  
 [Cursori di sola trasmissione](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursori keyset](../../../ado/guide/data/keyset-cursors.md)   
 [Cursori dinamici](../../../ado/guide/data/dynamic-cursors.md)
