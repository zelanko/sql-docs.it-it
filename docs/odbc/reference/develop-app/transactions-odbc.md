---
title: 'Transazioni ODBC : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], about transactions
- transactions [ODBC]
ms.assetid: b4ca861a-c164-4e87-8672-d5de15e3823c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a40c34b2abeb346c7a718994ba2484bfc728e2b1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297956"
---
# <a name="transactions-odbc"></a>Transazioni ODBC
Una *transazione* è un'unità di lavoro che viene eseguita come una singola operazione atomica; vale a dire, l'operazione ha esito positivo o negativo nel suo complesso. Ad esempio, prendi in considerazione il trasferimento di denaro da un conto bancario a un altro. Ciò comporta due fasi: ritirare il denaro dal primo conto e depositarlo nel secondo. È importante che entrambi i passaggi abbiano successo; non è accettabile che un passo abbia successo e l'altro fallisca. Un database che supporta le transazioni è in grado di garantire questo.  
  
 Le transazioni possono essere completate eseguendo il *commit* o eseguendo il *rollback*. Quando viene eseguito il commit di una transazione, le modifiche apportate in tale transazione vengono rese permanenti. Quando viene eseguito il rollback di una transazione, le righe interessate vengono restituite allo stato in cui si trovavano prima dell'avvio della transazione. Per estendere l'esempio di trasferimento dei conti, un'applicazione esegue un'istruzione SQL per addebitare il primo conto e un'istruzione SQL diversa per accreditare il secondo conto. Se entrambe le istruzioni hanno esito positivo, l'applicazione esegue quindi il commit della transazione. Ma se una delle istruzioni ha esito negativo per qualsiasi motivo, l'applicazione esegue il rollback della transazione. In entrambi i casi, l'applicazione garantisce uno stato coerente alla fine della transazione.  
  
 Una singola transazione può comprendere più operazioni di database che si verificano in momenti diversi. Se altre transazioni avessero accesso completo ai risultati intermedi, le transazioni potrebbero interferire tra loro. Si supponga, ad esempio, che una transazione inserisca una riga, che una seconda transazione legga tale riga e che venga eseguito il rollback della prima transazione. La seconda transazione contiene ora i dati per una riga che non esiste.  
  
 Per risolvere questo problema, esistono vari schemi per isolare le transazioni l'una dall'altra. *L'isolamento* delle transazioni viene in genere implementato bloccando le righe, impedendo a più transazioni di utilizzare contemporaneamente la stessa riga. In alcuni database, il blocco di una riga può anche bloccare altre righe.  
  
 Con l'aumento dell'isolamento delle transazioni viene ridotta *la concorrenza,* o la capacità di due transazioni di utilizzare gli stessi dati allo stesso tempo. Per ulteriori informazioni, vedere Impostazione del livello di [isolamento delle transazioni](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Transazioni in ODBC](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [Isolamento della transazione](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [Controllo della concorrenzaConcurrency Control](../../../odbc/reference/develop-app/concurrency-control.md)
