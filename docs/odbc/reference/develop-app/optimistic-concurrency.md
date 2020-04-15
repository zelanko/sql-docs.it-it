---
title: Concorrenza ottimistica . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- optimistic concurrency [ODBC]
ms.assetid: 9d71e09e-bc68-4c1f-9229-ed2a7be7d324
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 30eba3ea03b4c798a74a8cb928014b582846607b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282486"
---
# <a name="optimistic-concurrency"></a>Concorrenza ottimistica
*La concorrenza ottimistica* deriva il proprio nome dal presupposto ottimistico che i conflitti tra le transazioni si verificheranno raramente; si dice che si sia verificato un conflitto quando un'altra transazione aggiorna o elimina una riga di dati tra il momento in cui viene letta dalla transazione corrente e l'ora in cui viene aggiornata o eliminata. È l'opposto della *concorrenza pessimistica,* o blocco, in cui lo sviluppatore dell'applicazione ritiene che tali conflitti siano all'ordine del giorno.  
  
 Nella concorrenza ottimistica, una riga viene lasciata sbloccata fino al momento di aggiornarla o eliminarla. A questo punto, la riga viene riletta e controllata per verificare se è stata modificata dopo l'ultima lettura. Se la riga è stata modificata, l'aggiornamento o l'eliminazione ha esito negativo e deve essere riprovato.  
  
 Per determinare se una riga è stata modificata, la nuova versione viene confrontata con una versione memorizzata nella cache della riga. Questo controllo può essere basato sulla versione della riga, ad esempio la colonna timestamp in SQL ServerSQL Server o sui valori di ogni colonna della riga. Molti DBS non supportano le versioni di riga.  
  
 La concorrenza ottimistica può essere implementata dall'origine dati o dall'applicazione. In entrambi i casi, l'applicazione deve utilizzare un livello di isolamento delle transazioni basso, ad esempio Read Committed. l'utilizzo di un livello superiore nega l'aumento della concorrenza ottenuto utilizzando la concorrenza ottimistica.  
  
 Se la concorrenza ottimistica viene implementata dall'origine dati, l'applicazione imposta l'attributo dell'istruzione SQL_ATTR_CONCURRENCY su SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES. Per aggiornare o eliminare una riga, esegue un'istruzione di aggiornamento o eliminazione posizionata o chiama **SQLSetPos** come farebbe con la concorrenza pessimistica; il driver o l'origine dati restituisce SQLSTATE 01001 (conflitto di operazione cursore) se l'aggiornamento o l'eliminazione non riesce a causa di un conflitto.  
  
 Se l'applicazione stessa implementa la concorrenza ottimistica, imposta l'attributo dell'istruzione SQL_ATTR_CONCURRENCY su SQL_CONCUR_READ_ONLY per leggere una riga. Se si confrontano le versioni di riga e non conosce la colonna della versione di riga, chiama **SQLSpecialColumns** con l'opzione SQL_ROWVER per determinare il nome di questa colonna.  
  
 L'applicazione aggiorna o elimina la riga aumentando la concorrenza a SQL_CONCUR_LOCK (per ottenere l'accesso in scrittura alla riga) ed eseguendo un'istruzione **UPDATE** o **DELETE** con una clausola **WHERE** che specifica la versione o i valori della riga quando l'applicazione l'ha letta. Se la riga è stata modificata da allora, l'istruzione avrà esito negativo. Se la clausola **WHERE** non identifica in modo univoco la riga, l'istruzione potrebbe anche aggiornare o eliminare altre righe; Le versioni di riga identificano sempre in modo univoco le righe, ma i valori di riga identificano in modo univoco le righe solo se includono la chiave primaria.
