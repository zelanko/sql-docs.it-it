---
title: I cursori statici ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], static
- static cursors [ODBC]
ms.assetid: 28cb324c-e1c3-4b5c-bc3e-54df87037317
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bcb7c39d39492b91c0b62c5eff2229eb5f61df6b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987833"
---
# <a name="odbc-static-cursors"></a>Cursori statici ODBC
Un cursore statico è uno in cui il set di risultati viene visualizzata come statico. Non è in genere rilevare le modifiche apportate per l'appartenenza, ordine o i valori del set di risultati dopo l'apertura del cursore. Si supponga, ad esempio, un cursore statico recupera una riga e un'altra applicazione, quindi aggiorna tale riga. Se un cursore statico recupera nuovamente la riga, i valori rilevati sono identiche, nonostante le modifiche apportate da altre applicazioni.  
  
 I cursori statici possono rilevare i propri aggiornamenti, eliminazioni e inserimenti, anche se essi non sono necessari per eseguire questa operazione. Indica se un cursore statico particolare rileva queste modifiche viene segnalato tramite l'opzione SQL_STATIC_SENSITIVITY **SQLGetInfo**. I cursori statici rilevano mai altri aggiornamenti, eliminazione e inserimento.  
  
 La matrice di stato di riga specificata dall'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR può contenere SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO o SQL_ROW_ERROR ogni riga. Restituisce SQL_ROW_UPDATED, SQL_ROW_DELETED o SQL_ROW_ADDED per le righe aggiornate, eliminate o inserite dal cursore, presupponendo che il cursore è possibile rilevare tali modifiche.  
  
 I cursori statici vengono in genere implementati dal blocco di righe nel set di risultati o eseguendo una copia dello snapshot, del risultato impostare. Anche se il blocco di righe è relativamente facile, ha lo svantaggio di ridurre significativamente la concorrenza. Creazione di una copia consente maggiore concorrenza e consente il cursore tenere traccia dei propri aggiornamenti, eliminazioni e inserisce modificando la copia. Tuttavia, una copia è più costosa da apportare e può far divergere dai dati sottostanti come tali dati viene modificati da altri utenti.
