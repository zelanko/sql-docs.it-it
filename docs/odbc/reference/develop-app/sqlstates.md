---
title: Sqlstates | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299728"
---
# <a name="sqlstates"></a>SQLSTATE
Sqlstates fornisce informazioni dettagliate sulla motivo di un avviso o di un errore. Gli Stati Uniti in questo manuale sono basati su quelli presenti nella specifica dell'interfaccia della riga di comando ISO/Framework dell'esperienza, anche se tali SQLSTATE che iniziano con IM sono specifici di ODBC.  
  
 A differenza dei codici restituiti, i SQLSTATE in questo manuale sono linee guida e non è necessario che i driver li restituiscano. Pertanto, sebbene i driver debbano restituire il numero SQLSTATE corretto per qualsiasi errore o avviso, è possibile che vengano rilevati, le applicazioni non devono essere conteggiate in questa situazione. Il motivo di questa situazione è duplice:  
  
-   **Incompletezza** Anche se questo manuale elenca un numero elevato di errori e avvisi e le possibili cause di questi errori e avvisi, non è completo e probabilmente non sarà mai; le implementazioni di driver variano semplicemente. Tutti i driver specificati, probabilmente, non restituiranno tutti gli Stati SQLSTATE elencati in questo manuale e potrebbero restituire sqlstates non elencati in questo manuale.  
  
-   **Complessità** Alcuni motori di database, in particolare i motori di database relazionali, restituiscono letteralmente migliaia di errori e avvisi. È improbabile che i driver di tali motori eseguano il mapping di tutti questi errori e avvisi a SQLSTATE a causa del lavoro richiesto, dell'inesattezza dei mapping, della grande dimensione del codice risultante e del valore basso del codice risultante, che spesso restituisce errori di programmazione che non devono mai essere rilevati in fase di esecuzione. I driver dovrebbero pertanto mappare tutti gli errori e gli avvisi come sembra ragionevole e assicurarsi di eseguire il mapping degli errori e degli avvisi su cui potrebbe basarsi la logica dell'applicazione, ad esempio SQLSTATE 01004 (dati troncati).  
  
 Poiché SQLSTATE non vengono restituite in modo affidabile, la maggior parte delle applicazioni le visualizzano all'utente insieme al messaggio di diagnostica associato, che è spesso adattato a un errore o a un avviso specifico che si è verificato e codice di errore nativo. In questo modo si verifica raramente una perdita di funzionalità, perché le applicazioni non possono basare la logica di programmazione sulla maggior parte di SQLSTATE. Si supponga, ad esempio, che **SQLExecDirect** restituisca SQLSTATE 42000 (errore di sintassi o violazione di accesso). Se l'istruzione SQL che ha causato questo errore è hardcoded o è compilata dall'applicazione, si tratta di un errore di programmazione e il codice deve essere corretto. Se l'istruzione SQL viene immessa dall'utente, si tratta di un errore dell'utente e l'applicazione ha eseguito tutte le operazioni possibili segnalando all'utente il problema.  
  
 Quando le applicazioni eseguono la logica di programmazione di base in sqlstates, devono essere preparate per la mancata restituzione di SQLSTATE o per la restituzione di un valore SQLSTATE diverso. Esattamente quali SQLSTATE vengono restituiti in modo affidabile possono essere basati solo sull'esperienza con numerosi driver. Tuttavia, una linea guida generale è che sqlstates per gli errori che si verificano nel driver o nella gestione driver, anziché nell'origine dati, è più probabile che vengano restituiti in modo affidabile. Ad esempio, la maggior parte dei driver restituisce probabilmente SQLSTATE HYC00 (funzionalità facoltativa non implementata), mentre un minor numero di driver restituirà probabilmente SQLSTATE 42021 (la colonna esiste già).  
  
 I seguenti SQLSTATE indicano errori di run-time o avvisi e sono ottimi candidati su cui basare la logica di programmazione. Tuttavia, non vi è alcuna garanzia che tutti i driver li restituiscano.  
  
-   01004 (dati troncati)  
  
-   01S02 (valore opzione modificato)  
  
-   HY008 (operazione annullata)  
  
-   HYC00 (funzionalità facoltativa non implementata)  
  
-   HYT00 (timeout scaduto)  
  
 SQLSTATE HYC00 (funzionalità facoltativa non implementata) è particolarmente importante perché è l'unico modo in cui un'applicazione può determinare se un driver supporta un'istruzione o un attributo di connessione specifico.  
  
 Per un elenco completo di SQLSTATE e delle funzioni che li restituiscono, vedere [appendice a: codici di errore ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md). Per una spiegazione dettagliata delle condizioni in base alle quali ogni funzione può restituire un particolare SQLSTATE, vedere la funzione.
