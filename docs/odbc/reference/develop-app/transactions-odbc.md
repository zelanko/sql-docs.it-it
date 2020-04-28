---
title: ODBC transazioni | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81297956"
---
# <a name="transactions-odbc"></a>Transazioni ODBC
Una *transazione* è un'unità di lavoro eseguita come singola operazione atomica; ovvero l'operazione ha esito positivo o negativo nel suo complesso. Si consideri, ad esempio, il trasferimento di denaro da un conto bancario a un altro. Questo implica due passaggi: il ritiro del denaro dal primo account e il relativo deposito nel secondo. È importante che entrambi i passaggi abbiano esito positivo. non è accettabile che un passaggio abbia esito positivo e l'altro abbia esito negativo. Un database che supporta le transazioni può garantire questo problema.  
  
 Per completare le transazioni è necessario eseguire il *commit* o il *rollback*. Quando viene eseguito il commit di una transazione, le modifiche apportate in tale transazione vengono rese permanenti. Quando viene eseguito il rollback di una transazione, le righe interessate vengono restituite allo stato in cui si trovavano prima dell'avvio della transazione. Per estendere l'esempio di trasferimento dell'account, un'applicazione esegue un'istruzione SQL per addebitare il primo account e un'altra istruzione SQL per accreditare il secondo account. Se entrambe le istruzioni hanno esito positivo, l'applicazione eseguirà il commit della transazione. Tuttavia, se una delle due istruzioni ha esito negativo per qualsiasi motivo, l'applicazione esegue il rollback della transazione. In entrambi i casi, l'applicazione garantisce uno stato coerente alla fine della transazione.  
  
 Una singola transazione può includere più operazioni di database che si verificano in momenti diversi. Se altre transazioni hanno accesso completo ai risultati intermedi, le transazioni potrebbero interferire tra loro. Si supponga, ad esempio, che una transazione inserisca una riga, una seconda transazione legga la riga e venga eseguito il rollback della prima transazione. La seconda transazione dispone ora di dati per una riga inesistente.  
  
 Per risolvere questo problema, esistono diversi schemi per isolare le transazioni l'una dall'altra. L' *isolamento delle transazioni* viene in genere implementato tramite il blocco di righe, che impedisce a più di una transazione di utilizzare la stessa riga nello stesso momento. In alcuni database il blocco di una riga può anche bloccare altre righe.  
  
 Con l'isolamento delle transazioni maggiore viene rilevata una *concorrenza* ridotta o la possibilità di due transazioni di utilizzare contemporaneamente gli stessi dati. Per ulteriori informazioni, vedere [impostazione del livello di isolamento delle transazioni](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Transazioni in ODBC](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [Isolamento della transazione](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [Controllo della concorrenza](../../../odbc/reference/develop-app/concurrency-control.md)
