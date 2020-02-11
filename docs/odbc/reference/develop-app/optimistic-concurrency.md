---
title: Concorrenza ottimistica | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f5f4b7101718ea8372c9635a064dc81e1d8f6c1a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68023387"
---
# <a name="optimistic-concurrency"></a>Concorrenza ottimistica
La *concorrenza ottimistica* deriva dal presupposto ottimistico che le collisioni tra le transazioni si verificano raramente; si è affermato che si è verificato un conflitto quando un'altra transazione aggiorna o Elimina una riga di dati tra il momento in cui viene letta dalla transazione corrente e il momento in cui viene aggiornata o eliminata. Si tratta del contrario della *concorrenza pessimistica,* o del blocco, in cui lo sviluppatore di applicazioni ritiene che tali collisioni siano comuni.  
  
 Nella concorrenza ottimistica, una riga viene lasciata sbloccata fino a quando non è necessario aggiornarla o eliminarla. A questo punto, la riga viene riletta e controllata per verificare se è stata modificata dall'ultima lettura. Se la riga è cambiata, l'aggiornamento o l'eliminazione ha esito negativo e deve essere riprovata.  
  
 Per determinare se una riga è stata modificata, la nuova versione viene verificata rispetto a una versione memorizzata nella cache della riga. Questa verifica può essere basata sulla versione di riga, ad esempio la colonna timestamp in SQL Server o i valori di ogni colonna della riga. Molti DBMS non supportano le versioni di riga.  
  
 La concorrenza ottimistica può essere implementata dall'origine dati o dall'applicazione. In entrambi i casi, l'applicazione deve utilizzare un livello di isolamento delle transazioni basso, ad esempio Read Committed; l'utilizzo di un livello superiore nega la maggiore concorrenza ottenuta utilizzando la concorrenza ottimistica.  
  
 Se la concorrenza ottimistica viene implementata dall'origine dati, l'applicazione imposta l'attributo dell'istruzione SQL_ATTR_CONCURRENCY su SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES. Per aggiornare o eliminare una riga, viene eseguita un'istruzione Update o DELETE posizionata o viene chiamato **SQLSetPos** esattamente come con la concorrenza pessimistica; il driver o l'origine dati restituisce SQLSTATE 01001 (conflitto dell'operazione del cursore) se l'aggiornamento o l'eliminazione ha esito negativo a causa di un conflitto.  
  
 Se l'applicazione stessa implementa la concorrenza ottimistica, imposta l'attributo dell'istruzione SQL_ATTR_CONCURRENCY su SQL_CONCUR_READ_ONLY per leggere una riga. Se le versioni di riga vengono confrontate e non si conosce la colonna della versione della riga, viene chiamato **SQLSpecialColumns** con l'opzione SQL_ROWVER per determinare il nome della colonna.  
  
 L'applicazione aggiorna o Elimina la riga aumentando la concorrenza a SQL_CONCUR_LOCK (per ottenere l'accesso in scrittura alla riga) ed eseguendo un'istruzione **Update** o **Delete** con una clausola **where** che specifica la versione o i valori della riga durante la lettura dell'applicazione. Se la riga è cambiata da allora, l'istruzione avrà esito negativo. Se la clausola **where** non identifica in modo univoco la riga, l'istruzione potrebbe anche aggiornare o eliminare altre righe. le versioni di riga identificano sempre in modo univoco le righe, ma i valori di riga identificano in modo univoco le righe solo se includono la chiave primaria.
