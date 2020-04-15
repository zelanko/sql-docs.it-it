---
title: Proprietà SQLSTATEs . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be4bca929b8d48c301c6e71917503387004a6ec5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299728"
---
# <a name="sqlstates"></a>SQLSTATE
SqlSTATEs forniscono informazioni dettagliate sulla causa di un avviso o di un errore. Le sqlSTATE in questo manuale sono basate su quelle presenti nella specifica ISO/IEF CLI, anche se quelle SQLSTATE che iniziano con IM sono specifiche di ODBC.  
  
 A differenza dei codici restituiti, i SQLSTATE in questo manuale sono linee guida e i driver non sono necessari per restituirli. Pertanto, mentre i driver devono restituire il codice SQLSTATE appropriato per qualsiasi errore o avviso che sono in grado di rilevare, le applicazioni non devono contare su questo sempre che si verificano. Le ragioni di questa situazione sono duplici:  
  
-   **Incompletezza** Anche se questo manuale elenca un gran numero di errori e avvisi e possibili cause di tali errori e avvisi, non è completo e probabilmente non lo sarà mai; le implementazioni del driver variano semplicemente troppo. Qualsiasi driver specificato probabilmente non restituirà tutti i SQLSTATE elencati in questo manuale e potrebbe restituire SQLSTATEs non elencati in questo manuale.  
  
-   **Complessità** Alcuni motori di database, in particolare i motori di database relazionali, restituiscono letteralmente migliaia di errori e avvisi. I driver per tali motori è improbabile eseguire il mapping di tutti questi errori e avvisi a SQLSTATE a causa dello sforzo richiesto, l'inesattezza dei mapping, le dimensioni grandi del codice risultante e il valore basso del codice risultante, che spesso restituisce errori di programmazione che non dovrebbero mai essere rilevati in fase di esecuzione. Pertanto, i driver devono eseguire il mapping di tutti gli errori e gli avvisi come sembra ragionevole ed essere sicuri di eseguire il mapping di tali errori e avvisi su cui la logica dell'applicazione potrebbe essere basata, ad esempio SQLSTATE 01004 (dati troncati).  
  
 Poiché sqlSTATE non vengono restituite in modo affidabile, la maggior parte delle applicazioni le visualizza all'utente insieme al messaggio di diagnostica associato, che è spesso adattato all'errore o all'avviso specifico che si è verificato e al codice di errore nativo. Raramente si è perdita di funzionalità in questo modo, perché le applicazioni non possono basare la logica di programmazione sulla maggior parte SQLSTATEs comunque. Si supponga, ad esempio, **che SQLExecDirect** restituisca SQLSTATE 42000 (errore di sintassi o violazione di accesso). Se l'istruzione SQL che ha causato questo errore è hardcoded o compilata dall'applicazione, si tratta di un errore di programmazione e il codice deve essere corretto. Se l'istruzione SQL viene immessa dall'utente, si tratta di un errore dell'utente e l'applicazione ha fatto tutto il possibile informando l'utente del problema.  
  
 Quando le applicazioni basano la logica di programmazione su SQLSTATEs, devono essere preparate per il SQLSTATE non deve essere restituito o per un diverso SQLSTATE da restituire. Esattamente quali SQLSTATEs vengono restituiti in modo affidabile può essere basato solo sull'esperienza con numerosi driver. Tuttavia, una linea guida generale è che SQLSTATEs per gli errori che si verificano nel driver o Gestione Driver, al contrario dell'origine dati, sono più probabilità di essere restituiti in modo affidabile. Ad esempio, la maggior parte dei driver probabilmente restituisce SQLSTATE HYC00 (funzionalità facoltativa non implementata), mentre un numero inferiore di driver probabilmente restituisce SQLSTATE 42021 (colonna già esistente).  
  
 I seguenti SQLSTATE indicano errori o avvisi in fase di esecuzione e sono buoni candidati su cui basare la logica di programmazione. Tuttavia, non vi è alcuna garanzia che tutti i conducenti li restituiscano.  
  
-   01004 (Dati troncati)  
  
-   01S02 (valore dell'opzione modificato)  
  
-   HY008 (Operazione annullata)  
  
-   HYC00 (funzionalità facoltativa non implementata)  
  
-   HYT00 (Timeout scaduto)  
  
 SQLSTATE HYC00 (funzionalità facoltativa non implementata) è particolarmente significativo perché è l'unico modo in cui un'applicazione può determinare se un driver supporta una particolare istruzione o attributo di connessione.  
  
 Per un elenco completo delle funzioni SQLSTATEes e delle funzioni che le restituiscono, vedere [Appendice A: Codici](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)di errore ODBC . Per una spiegazione dettagliata delle condizioni in cui ogni funzione potrebbe restituire un particolare SQLSTATE, vedere tale funzione.
