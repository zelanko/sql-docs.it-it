---
title: SQLSTATEs | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], sqlstates
- SQLSTATE [ODBC]
ms.assetid: f29fff2e-3d09-4a8c-a2f9-2059062cbebf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ad31d9fd07e0b9f7bdf633f8ed546331880787c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149044"
---
# <a name="sqlstates"></a>SQLSTATE
SQLSTATE forniscono informazioni dettagliate sulla causa di un avviso o errore. SQLSTATE in questo manuale sono basate su quelle disponibili nella specifica ISO/IEF dell'interfaccia della riga, anche se tali SQLSTATEs che iniziano con messaggio immediato sono specifici per ODBC.  
  
 A differenza dei codici restituiti, SQLSTATEs in questo manuale sono linee guida e i driver non sono necessari per restituirle. Pertanto, anche se i driver devono restituire il valore SQLSTATE appropriato per qualsiasi errore o avviso che sono in grado di rilevare, le applicazioni non devono influire sulla tale inconveniente, sempre. Il motivo per questa situazione è duplice:  
  
-   **Incompletezza** anche se questo manuale elenca un numero elevato di errori e avvisi e le possibili cause per tali errori e avvisi, non è completa e non sarà probabilmente mai; le implementazioni di driver semplicemente variare troppe operazioni. Qualsiasi driver specificato potrebbe non restituire tutti i SQLSTATEs elencati in questo manuale e possono restituire SQLSTATEs non elencato in questo manuale.  
  
-   **Complessità** alcuni motori di database - motori di database relazionale particolarmente - restituiscono letteralmente migliaia di avvisi ed errori. I driver per tali motori sono probabilmente non eseguire il mapping di tutti questi errori e avvisi da SQLSTATEs a causa di impegno implicati, inexactness dei mapping, le dimensioni del codice risulta e il valore minimo del codice risulta, che spesso restituisce programmazione errori che non devono essere mai rilevati in fase di esecuzione. Pertanto, i driver devono eseguire il mapping di tutti gli errori e gli avvisi come sembra ragionevole e assicurarsi di eseguire il mapping di tali errori e avvisi in cui la logica dell'applicazione potrebbero essere basa, ad esempio SQLSTATE 01004 (dati troncati).  
  
 Poiché non vengono restituiti in modo affidabile SQLSTATEs, la maggior parte delle applicazioni semplicemente visualizzano all'utente con il messaggio di diagnostica associato, spesso personalizzata in base a un messaggio di errore o avviso che si sono verificati e codice di errore nativo. Si verifica raramente nessuna perdita delle funzionalità in questo modo, poiché le applicazioni non è possibile basare la logica di programmazione SQLSTATEs la maggior parte delle comunque. Ad esempio supponga **SQLExecDirect** restituisce SQLSTATE 42000 (sintassi o violazione di accesso). Se l'istruzione SQL che ha causato l'errore è a livello di codice o compilata dall'applicazione, si tratta di un errore di programmazione e il codice deve essere corretto. Se l'istruzione SQL viene immesso dall'utente, si tratta di un errore dell'utente e l'applicazione ha eseguito tutto ciò che è possibile informare gli utenti del problema.  
  
 Quando le applicazioni di basare la logica di programmazione SQLSTATEs, devono essere preparati per il valore SQLSTATE non devono essere restituiti o per un valore SQLSTATE di diversi da restituire. Esattamente quali SQLSTATE vengono restituiti in modo affidabile può basarsi solo sull'esperienza con numerosi driver. Tuttavia, in generale è che SQLSTATE errori che si verificano nel driver o gestione Driver, a differenza dell'origine dati, hanno maggiori probabilità di essere restituito in modo affidabile. Ad esempio, la maggior parte dei driver potrebbe restituire SQLSTATE HYC00 (funzionalità facoltativa non implementata), mentre i driver meno probabile che restituiscono SQLSTATE 42021 (colonna esiste già).  
  
 I seguente SQLSTATE indicano avvisi o errori di run-time, sono candidati ideali su cui basare la logica di programmazione. Tuttavia, non c'è garanzia che li restituiscono tutti i driver.  
  
-   01004 (dati troncati)  
  
-   01S02 (valore dell'opzione modificato)  
  
-   HY008 (operazione annullata)  
  
-   HYC00 (funzionalità facoltativa non implementata)  
  
-   HYT00 (Timeout scaduto)  
  
 SQLSTATE HYC00 (funzionalità facoltativa non implementata) è particolarmente significativo perché è l'unico modo in cui un'applicazione può determinare se un driver supporta un particolare attributo di istruzione o la connessione.  
  
 Per un elenco completo di SQLState e restituiranno quali funzioni, vedere [appendice a: Codici di errore ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md). Per una spiegazione dettagliata delle condizioni in cui ciascuna funzione potrebbe restituire un valore SQLSTATE specifico, vedere tale funzione.
