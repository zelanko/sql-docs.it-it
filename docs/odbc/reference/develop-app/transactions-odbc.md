---
title: Transazioni ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f6ce5decd2744c0ce9d753e355321a40d00fd620
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305807"
---
# <a name="transactions-odbc"></a>Transazioni ODBC
Oggetto *transazione* è un'unità di lavoro che viene eseguita come una singola operazione atomica, vale a dire, l'operazione ha esito positivo o non riesce nel suo complesso. Si consideri, ad esempio, il trasferimento di denaro da una banca a un'altra. Ciò comporta due passaggi: prelievo del denaro dal primo account e che lo inserisce nella seconda. È importante che entrambi questi passaggi avranno esito positivo; non è accettabile per un unico passaggio abbia esito positivo e l'altro errore. Un database che supporta le transazioni è in grado di garantire questo.  
  
 Le transazioni possono essere completate da entrambi in corso *commit* o in corso *rollback*. Quando una transazione viene eseguito il commit, le modifiche apportate in quanto transazione vengono rese permanenti. Quando una transazione viene eseguito il rollback, le righe interessate vengono restituite lo stato che si trovavano prima dell'inizio della transazione. Per estendere l'esempio di trasferimento di account, un'applicazione esegue un'istruzione SQL venga addebitato il primo account e un'istruzione SQL diversa per il secondo account di credito. Se entrambe le istruzioni hanno esito positivo, quindi esegue il commit della transazione. Ma se l'istruzione non riesce per qualsiasi motivo, l'applicazione esegue il rollback della transazione. In entrambi i casi, l'applicazione garantisce uno stato coerente alla fine della transazione.  
  
 Una singola transazione può includere più operazioni di database che si verificano in momenti diversi. Se altre transazioni ha accesso completo ai risultati intermedi, le transazioni potrebbero interferire con loro. Ad esempio, si supponga che una transazione inserisce una riga, una seconda transazione legge tale riga e della prima transazione viene eseguito il rollback. La seconda transazione ora dispone di dati per una riga che non esiste.  
  
 Per risolvere questo problema, esistono vari schemi per isolare le transazioni uno da altro. *Isolamento delle transazioni* viene in genere implementata dal blocco di righe, che preclude più di una transazione dall'uso della stessa riga nello stesso momento. In alcuni database, il blocco di una riga può anche bloccare le altre righe.  
  
 Isolamento delle transazioni deriva ridotto *concorrenza,* o la possibilità di due transazioni utilizzano gli stessi dati nello stesso momento. Per altre informazioni, vedere [impostazione del livello di isolamento delle transazioni](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Transazioni in ODBC](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [Isolamento della transazione](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [Controllo della concorrenza](../../../odbc/reference/develop-app/concurrency-control.md)
