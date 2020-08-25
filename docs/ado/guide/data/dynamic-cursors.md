---
description: Cursori dinamici
title: Cursori dinamici | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: f646a608c8cbc25e16c5200f8271c133a62d3457
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806155"
---
# <a name="dynamic-cursors"></a>Cursori dinamici
I cursori dinamici rilevano tutte le modifiche apportate alle righe nel set di risultati, indipendentemente dal fatto che vengano apportate all'interno del cursore o da altri utenti all'esterno del cursore. Tutte le istruzioni INSERT, Update e DELETE eseguite da tutti gli utenti sono visibili tramite il cursore. Il cursore dinamico può rilevare le modifiche apportate alle righe, all'ordine e ai valori nel set di risultati dopo l'apertura del cursore. Gli aggiornamenti eseguiti all'esterno del cursore non sono visibili finché non ne viene eseguito il commit, a meno che il livello di isolamento della transazione del cursore non sia impostato su "non sottoposto a commit".  
  
 Si supponga, ad esempio, che un cursore dinamico recuperi due righe e un'altra applicazione, quindi aggiorna una di queste righe ed Elimina l'altra. Se a questo punto il cursore dinamico recupera tali righe, non troverà la riga eliminata, ma visualizzerà i nuovi valori per la riga aggiornata.  
  
 Il cursore dinamico è una scelta ottimale se l'applicazione deve rilevare tutti gli aggiornamenti simultanei eseguiti da altri utenti. Utilizzare il **CursorTypeEnum adOpenDynamic** per indicare che si desidera utilizzare un cursore dinamico in ADO.  
  
## <a name="see-also"></a>Vedere anche  
 [Cursori di sola trasmissione](./forward-only-cursors.md)   
 [Cursori statici](./static-cursors.md)   
 [Cursori keyset](./keyset-cursors.md)