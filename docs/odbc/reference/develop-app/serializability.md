---
title: Serializabilità Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transaction isolation [ODBC]
- transactions [ODBC], serialization
- serialization [ODBC]
- transactions [ODBC], isolation
ms.assetid: 142e4ac0-2977-4a2b-96ae-c9e5bd2c448a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0557e011578d313765614c05a2a9cf1b975bbc08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304162"
---
# <a name="serializability"></a>Serializzabilità
Idealmente, le transazioni dovrebbero essere *serializzabili.* Le transazioni sono dette serializzabili se i risultati dell'esecuzione simultanea delle transazioni sono gli stessi dei risultati dell'esecuzione seriale, ovvero una dopo l'altra. Non è importante quale transazione viene eseguita per prima, ma solo che il risultato non riflette alcuna combinazione delle transazioni.  
  
 Si supponga, ad esempio, che la transazione A moltiplichi i valori dei dati per 2 e che la transazione B aggiunga 1 ai valori dei dati. Si supponga ora che siano presenti due valori di dati: 0 e 10. Se queste transazioni vengono eseguite una dopo l'altra, i nuovi valori saranno 1 e 21 se la transazione A viene eseguita per prima oppure 2 e 22 se la transazione B viene eseguita per prima. Ma cosa succede se l'ordine in cui vengono eseguite le due transazioni è diverso per ogni valore? Se la transazione A viene eseguita per prima sul primo valore e la transazione B viene eseguita per prima sul secondo valore, i nuovi valori sono 1 e 22. Se questo ordine è invertito, i nuovi valori sono 2 e 21. Le transazioni sono serializzabili se 1, 21 e 2, 22 sono gli unici risultati possibili. Le transazioni non sono serializzabili se 1, 22 o 2, 21 è un risultato possibile.  
  
 Allora perché è desiderabile la serializzabilità? In altre parole, perché è importante che sembri che una transazione termini prima dell'inizio della transazione successiva? Si consideri il problema seguente. Un venditore sta immettendo ordini nello stesso momento in cui un impiegato sta inviando le fatture. Si supponga che il venditore immetta un ordine dalla società X ma non ne esetrae il commit; il venditore sta ancora parlando con il rappresentante della società X. L'impiegato richiede un elenco di tutti gli ordini aperti e scopre l'ordine per la società X e invia loro una fattura. Ora il rappresentante della società X decide di voler modificare l'ordine, in modo che il venditore lo modifichi prima di eseguire il commit della transazione. La società X riceve una fattura errata.  
  
 Se le transazioni del venditore e dell'impiegato fossero serializzabili, questo problema non si sarebbe mai verificato. O la transazione del venditore sarebbe terminata prima dell'inizio della transazione dell'impiegato, nel qual caso l'impiegato avrebbe inviato la fattura corretta, oppure la transazione dell'impiegato sarebbe terminata prima dell'inizio della transazione del venditore, nel qual caso l'impiegato non avrebbe inviato una fattura alla società X.
