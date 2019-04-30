---
title: La serializzabilità è infatti | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e7972fb72607edca8c1599c2d028b073c184642
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63251481"
---
# <a name="serializability"></a>Serializzabilità
In teoria, le transazioni devono essere *serializzabile*. Le transazioni vengono detti essere serializzabile se i risultati dell'esecuzione simultanea di transazioni sono uguali come i risultati di eseguirli in modo seriale, vale a dire, uno dopo l'altro. Non è importante la transazione viene eseguita in primo luogo, solo che il risultato non riflette qualsiasi combinazione delle transazioni.  
  
 Si supponga, ad esempio, la transazione A Moltiplica i valori dei dati per 2 e la transazione B aggiunge 1 a valori dei dati. Si supponga ora che sono presenti due valori di dati: 0 e 10. Se queste operazioni vengono eseguite una dopo l'altro, i nuovi valori sarà 1 e 21 se la transazione viene eseguita prima di tutto o 2 e 22 se la transazione B è eseguita per prima. Ma cosa accade se l'ordine in cui vengono eseguite le due transazioni è diverso per ogni valore? Se un viene eseguito primo del primo valore di transazione e la transazione B viene eseguiti prima del secondo valore, i nuovi valori sono 1 e 22. Se questo ordine è invertito, i nuovi valori sono 2 e 21. Le transazioni sono serializzabili se 1, 21 e 2, 22 sono riportati i risultati solo possibili. Le transazioni non sono serializzabile se 1, 22 o 2, 21 è un risultato possibile.  
  
 Quindi, perché è la serializzabilità è infatti auspicabile? In altre parole, perché è importante che venga visualizzato che una transazione termina prima dell'avvio della transazione successiva? Si consideri il seguente problema. Un agente sta entrando ordini allo stesso tempo che un clerk è l'invio di fatture. Si supponga che l'agente accede un ordine dalla società X ma non esegue il commit. l'agente è continuano a comunicare con il rappresentante dall'azienda X. La classe clerk richiede un elenco di tutti gli ordini aperti e individua l'ordine per la società X e li invia una fattura. A questo punto il rappresentante la società X decide che desiderano modificare l'ordine, in modo che l'agente viene modificato prima del commit della transazione. La società X Ottiene una fattura corretta.  
  
 Se le transazioni dell'agente e del clerk serializzabile, il problema non sarebbe state eseguite. Transazione del venditore potrebbe aver completato prima dell'avvio transazione del clerk, nel qual caso il clerk verrà hanno inviata la fattura corretta oppure potrebbero avere delle transazioni del clerk prima dell'avvio transazione del venditore, nel qual caso il Clerk sarebbe non hai inviato una fattura per la società X affatto.
