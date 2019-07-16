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
ms.openlocfilehash: 86e51b7880004117e8efc96bd310c6de705d43a6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925500"
---
# <a name="dynamic-cursors"></a>Cursori dinamici
I cursori dinamici rilevano tutte le modifiche apportate alle righe nel set di risultati, indipendentemente dal fatto che si verificano le modifiche dall'interno del cursore o da altri utenti all'esterno del cursore. Tutti i insert, update e istruzioni delete eseguite da tutti gli utenti sono visibili nel cursore. Il cursore dinamico può rilevare eventuali modifiche apportate alle righe, ordine e i valori nel set di risultati dopo l'apertura del cursore. Gli aggiornamenti apportati all'esterno del cursore non sono visibili fino a quando non sono state assegnate (a meno che il livello di isolamento delle transazioni di cursore è impostato su "commit").  
  
 Si supponga, ad esempio, un cursore dinamico recupera due righe e un'altra applicazione, quindi aggiorna una di queste righe e consente di eliminare l'altra. Se a questo punto il cursore dinamico recupera tali righe, non troverà la riga eliminata, ma visualizzerà i nuovi valori per la riga aggiornata.  
  
 Il cursore dinamico è un'ottima scelta se l'applicazione deve rilevare tutti gli aggiornamenti simultanei apportati da altri utenti. Usare la **Impostare CursorTypeEnum** per indicare che si desidera utilizzare un cursore dinamico in ADO.  
  
## <a name="see-also"></a>Vedere anche  
 [Cursori forward-Only](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursori statici](../../../ado/guide/data/static-cursors.md)   
 [Cursori keyset](../../../ado/guide/data/keyset-cursors.md)
