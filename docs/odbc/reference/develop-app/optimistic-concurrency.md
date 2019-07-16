---
title: La concorrenza ottimistica | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023387"
---
# <a name="optimistic-concurrency"></a>Concorrenza ottimistica
*La concorrenza ottimistica* il relativo nome deriva dal presupposto ottimistico che raramente si verificheranno conflitti tra le transazioni, viene definito un conflitto si sono verificati quando un'altra transazione aggiorna o elimina una riga di dati tra il momento in cui viene letto la transazione corrente e l'ora aggiornata o eliminata. È l'opposto del *concorrenza pessimistica,* o si blocca, in cui lo sviluppatore dell'applicazione ritiene che tali conflitti siano comuni.  
  
 Nella concorrenza ottimistica, una riga viene lasciata sbloccato fino a quando non al momento di aggiornarla o eliminarla. A questo punto, la riga viene riletto e controllata per verificare se è stato modificato dopo l'ultima lettura. Se la riga è stata modificata, l'aggiornamento o eliminazione di ha esito negativo e deve essere ritentata.  
  
 Per determinare se una riga è stata modificata, la nuova versione viene confrontata con una versione memorizzata nella cache della riga. Questo controllo può basarsi sulla versione di riga, ad esempio la colonna timestamp in SQL Server o i valori di ogni colonna nella riga. Maggior parte dei DBMS non supportano le versioni di riga.  
  
 La concorrenza ottimistica può essere implementata da origine dati o l'applicazione. In entrambi i casi, l'applicazione deve utilizzare un livello di isolamento basso, ad esempio Read Committed; con un livello superiore Nega la concorrenza maggiore ottenuta tramite la concorrenza ottimistica.  
  
 Se la concorrenza ottimistica viene implementata dall'origine dati, l'applicazione imposta l'attributo di istruzione SQL_ATTR_CONCURRENCY su SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES. Per aggiornare o eliminare una riga, viene eseguito un aggiornamento posizionato o istruzione delete o chiamate **SQLSetPos** esattamente come farebbe con la concorrenza pessimistica; l'origine dati o driver restituisce SQLSTATE 01001 (conflitto dell'operazione del cursore) se la Update o delete ha esito negativo a causa di un conflitto.  
  
 Se l'applicazione stessa implementa la concorrenza ottimistica, imposta l'attributo di istruzione SQL_ATTR_CONCURRENCY su SQL_CONCUR_READ_ONLY per leggere una riga. Se confronterà le versioni di riga e non dispone di una colonna della versione di riga, chiama il metodo **SQLSpecialColumns** con l'opzione SQL_ROWVER per determinare il nome della colonna.  
  
 L'applicazione aggiorna o elimina la riga, aumentando la concorrenza SQL_CONCUR_LOCK (per ottenere l'accesso in scrittura alla riga) e l'esecuzione di un' **UPDATE** oppure **eliminare** istruzione con un **in cui**  clausola che specifica la versione o della riga di valori rilevati in fase di applicazione leggerlo. Se la riga è cambiato da allora, l'istruzione avrà esito negativo. Se il **in cui** clausola non identifica in modo univoco la riga, l'istruzione potrebbe essere anche aggiornare o eliminare le altre righe; le versioni delle righe identificano sempre in modo univoco le righe, ma i valori di riga identificano righe solo se includono la chiave primaria.
