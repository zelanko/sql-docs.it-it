---
title: I cursori dinamici | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], dynamic
- dynamic cursors [ADO]
ms.assetid: 00460f30-8cf7-494e-82df-41012f40ae51
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0d7a19476a00fb88e0b2195c761993f91b7a5d4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161787"
---
# <a name="dynamic-cursors"></a>Cursori dinamici
I cursori dinamici rilevano tutte le modifiche apportate alle righe nel set di risultati, indipendentemente dal fatto che si verificano le modifiche dall'interno del cursore o da altri utenti all'esterno del cursore. Tutti i insert, update e istruzioni delete eseguite da tutti gli utenti sono visibili nel cursore. Il cursore dinamico può rilevare eventuali modifiche apportate alle righe, ordine e i valori nel set di risultati dopo l'apertura del cursore. Gli aggiornamenti apportati all'esterno del cursore non sono visibili fino a quando non sono state assegnate (a meno che il livello di isolamento delle transazioni di cursore è impostato su "commit").  
  
 Si supponga, ad esempio, un cursore dinamico recupera due righe e un'altra applicazione, quindi aggiorna una di queste righe e consente di eliminare l'altra. Se a questo punto il cursore dinamico recupera tali righe, non troverà la riga eliminata, ma visualizzerà i nuovi valori per la riga aggiornata.  
  
 Il cursore dinamico è un'ottima scelta se l'applicazione deve rilevare tutti gli aggiornamenti simultanei apportati da altri utenti. Usare la **Impostare CursorTypeEnum** per indicare che si desidera utilizzare un cursore dinamico in ADO.  
  
## <a name="see-also"></a>Vedere anche  
 [Cursori forward-Only](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursori statici](../../../ado/guide/data/static-cursors.md)   
 [Cursori keyset](../../../ado/guide/data/keyset-cursors.md)
