---
title: Cursori statici ODBC Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b99566c473e88684e8b092a5ac9fc899e7dce177
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282446"
---
# <a name="odbc-static-cursors"></a>Cursori statici ODBC
Un cursore statico è un cursore in cui il set di risultati sembra essere statico. In genere non rileva le modifiche apportate all'appartenenza, all'ordine o ai valori del set di risultati dopo l'apertura del cursore. Si supponga, ad esempio, che un cursore statico recuperi una riga e che un'altra applicazione aggiorni tale riga. Se il cursore statico recupera nuovamente la riga, i valori visualizzati non vengono modificati, nonostante le modifiche apportate dall'altra applicazione.  
  
 I cursori statici possono rilevare i propri aggiornamenti, eliminazioni e inserimenti, anche se non sono necessari per eseguire questa operazione. Se un particolare cursore statico rileva queste modifiche viene segnalato tramite l'opzione SQL_STATIC_SENSITIVITY in **SQLGetInfo**. I cursori statici non rilevano mai altri aggiornamenti, eliminazioni e inserimenti.  
  
 La matrice di stato della riga specificata dall'attributo di istruzione SQL_ATTR_ROW_STATUS_PTR può contenere SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO o SQL_ROW_ERROR per qualsiasi riga. Restituisce SQL_ROW_UPDATED, SQL_ROW_DELETED o SQL_ROW_ADDED per le righe aggiornate, eliminate o inserite dal cursore, presupponendo che il cursore sia in grado di rilevare tali modifiche.  
  
 I cursori statici vengono in genere implementati bloccando le righe nel set di risultati o eseguendo una copia, o snapshot, del set di risultati. Sebbene il blocco delle righe sia relativamente semplice da eseguire, presenta lo svantaggio di ridurre in modo significativo la concorrenza. La creazione di una copia consente una maggiore concorrenza e consente al cursore di tenere traccia dei propri aggiornamenti, eliminazioni e inserimenti modificando la copia. Tuttavia, una copia è più costosa da eseguire e può divergere dai dati sottostanti man mano che i dati vengono modificati da altri utenti.
