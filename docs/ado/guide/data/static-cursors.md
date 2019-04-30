---
title: I cursori statici | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: e8815522ee4f9a4221887696a23a201910d7cfad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63062837"
---
# <a name="static-cursors"></a>Cursori statici
Un cursore statico Visualizza sempre il risultato impostato com'era quando il cursore è stato aperto. A seconda di implementazione, cursori statici sono di sola lettura o lettura/scrittura e fornire lo scorrimento in avanti e indietro. In genere un cursore statico non vengono rilevate le modifiche apportate per l'appartenenza, ordine o i valori del set di risultati dopo l'apertura del cursore. I cursori statici possono rilevare le proprie operazioni di aggiornamento, eliminazione e inserimento, anche se tale rilevamento non è obbligatorio per cursori di questo tipo.  
  
 I cursori statici rilevano mai altri aggiornamenti, eliminazione e inserimento. Si supponga, ad esempio, che un cursore statico recuperi una riga e che un'altra applicazione aggiorni in seguito tale riga. Se l'applicazione recupera nuovamente la riga dal cursore statico, i valori che rileva sono invariati, nonostante le modifiche apportate dall'altra applicazione. Sono supportati tutti i tipi di scorrimento, ma i provider possono o potrebbero non supportare i segnalibri.  
  
 Se l'applicazione non è necessario rilevare i dati cambiano e richiede lo scorrimento, il cursore statico è la scelta migliore. Usare la **adOpenStatic CursorTypeEnum** per indicare che si desidera utilizzare un cursore statico in ADO.  
  
## <a name="see-also"></a>Vedere anche  
 [Cursori forward-Only](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursori keyset](../../../ado/guide/data/keyset-cursors.md)   
 [Cursori dinamici](../../../ado/guide/data/dynamic-cursors.md)
