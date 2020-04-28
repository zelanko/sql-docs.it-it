---
title: Serializzabilità | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304162"
---
# <a name="serializability"></a>Serializzabilità
Idealmente, le transazioni devono essere *serializzabili*. Le transazioni sono denominate serializzabili se i risultati dell'esecuzione simultanea delle transazioni corrispondono ai risultati dell'esecuzione seriale, ovvero uno dopo l'altro. Non è importante che la transazione venga eseguita per prima, ma solo che il risultato non rifletta alcuna combinazione di transazioni.  
  
 Si supponga, ad esempio, che la transazione A moltiplichi i valori dei dati per 2 e che la transazione B aggiunga 1 ai valori dei dati. Si supponga ora che siano presenti due valori di dati: 0 e 10. Se queste transazioni vengono eseguite una dopo l'altra, i nuovi valori saranno 1 e 21 se la transazione A viene eseguita per prima oppure 2 e 22 se la transazione B viene eseguita per prima. Ma cosa accade se l'ordine in cui vengono eseguite le due transazioni è diverso per ogni valore? Se la transazione A viene eseguita per prima sul primo valore e la transazione B viene eseguita per prima sul secondo valore, i nuovi valori sono 1 e 22. Se l'ordine è invertito, i nuovi valori sono 2 e 21. Le transazioni sono serializzabili se 1, 21 e 2, 22 sono gli unici risultati possibili. Le transazioni non sono serializzabili se 1, 22 o 2, 21 è un possibile risultato.  
  
 Perché la serializzabilità è auspicabile? In altre parole, perché è importante che venga completata una transazione prima dell'avvio della successiva transazione? Si consideri il seguente problema. Un venditore sta inserendo gli ordini nello stesso momento in cui un addetto invia fatture. Si supponga che il venditore immetta un ordine dall'azienda X, ma non ne esegue il commit; il venditore sta ancora parlando al rappresentante dell'azienda X. Il clerk richiede un elenco di tutti gli ordini aperti e individua l'ordine per la società X e invia una fattura. A questo punto, il rappresentante della società X decide di modificare l'ordine, in modo che il venditore lo modifichi prima di eseguire il commit della transazione. La società X riceve una fattura non corretta.  
  
 Se le transazioni del venditore e del clerk sono serializzabili, questo problema non si verifica mai. La transazione del commesso è stata completata prima dell'avvio della transazione del clerk, nel qual caso il clerk avrebbe inviato la fattura corretta o la transazione del clerk avrebbe terminato prima dell'avvio della transazione del venditore, nel qual caso il clerk non avrebbe inviato una fattura all'azienda X.
