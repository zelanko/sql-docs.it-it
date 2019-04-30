---
title: Effetto delle operazioni su cursori e le istruzioni preparate | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- cursors [ODBC], transaction commits or roll backs
- prepared statements [ODBC]
- transactions [ODBC], cursors
ms.assetid: 523e22a2-7b53-4c25-97c1-ef0284aec76e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 41c2c6b06744965144ca9d5feb27e9ea16d9903c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305721"
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>Effetto delle transazioni sui cursori e sulle istruzioni preparate
Il commit o il rollback di una transazione ha l'effetto seguente sulle cursori e piani di accesso:  
  
-   Tutti i cursori vengono chiusi e vengono eliminati i piani di accesso per le istruzioni preparate in tale connessione.  
  
-   Tutti i cursori vengono chiusi e i piani di accesso per le istruzioni preparate per quella connessione rimangono invariati.  
  
-   Tutti i cursori rimangono aperti e i piani di accesso per le istruzioni preparate per quella connessione rimangono invariati.  
  
 Si supponga, ad esempio, che un'origine dati mostra il comportamento prima in questo elenco, le più restrittive di questi comportamenti. Ora si supponga che un'applicazione esegue le operazioni seguenti:  
  
1.  Imposta la modalità di commit di commit manuale.  
  
2.  Crea un set di risultati di ordini di vendita nell'istruzione 1.  
  
3.  Crea un set di risultati delle righe in un ordine di vendita nell'istruzione 2, quando l'utente viene evidenziata quell'ordine.  
  
4.  Le chiamate **SQLExecute** per eseguire un'istruzione di aggiornamento posizionato che è stata preparata in istruzione 3, quando l'utente non aggiorna una riga.  
  
5.  Le chiamate **SQLEndTran** per eseguire il commit dell'istruzione per gli aggiornamenti posizionati.  
  
 A causa di un comportamento dell'origine dati, la chiamata a **SQLEndTran** nel passaggio 5 comporta per chiudere i cursori nelle istruzioni 1 e 2 e per eliminare il piano di accesso su tutte le istruzioni. L'applicazione deve eseguito nuovamente il set di istruzioni 1 e 2 per ricreare il risultato e reprepare statement on istruzione 3.  
  
 In modalità autocommit, funzioni diverse da **SQLEndTran** commit delle transazioni:  
  
-   **SQLExecute** oppure **SQLExecDirect** nell'esempio precedente, la chiamata al **SQLExecute** nel passaggio 4 esegue il commit di una transazione. In questo modo l'origine dati chiudere i cursori nelle istruzioni 1 e 2 ed eliminare il piano di accesso su tutte le istruzioni in tale connessione.  
  
-   **SQLBulkOperations** oppure **SQLSetPos** nell'esempio precedente, si supponga che nel passaggio 4 l'applicazione chiama **SQLSetPos** con l'opzione SQL_UPDATE nell'istruzione 2, anziché l'esecuzione di un istruzione di aggiornamento posizionato nell'istruzione 3. Questo commit di una transazione e fa sì che l'origine dati chiudere i cursori nelle istruzioni 1 e 2 e rimuove tutti i piani di accesso su tale connessione.  
  
-   **SQLCloseCursor** nell'esempio precedente, si supponga che quando l'utente viene evidenziato un ordine di vendita diverso, l'applicazione chiama **SQLCloseCursor** nell'istruzione 2 prima di creare un risultato delle righe per le nuove vendite ordine. La chiamata a **SQLCloseCursor** esegue il commit di **seleziona** istruzione create set di risultati di righe e fa sì che l'origine dati chiudere il cursore sull'istruzione 1 Elimina quindi tutti i piani di accesso su esso connessione.  
  
 Le applicazioni, in particolare su schermo in cui l'utente scorre il set di risultati e gli aggiornamenti o Elimina le righe, è necessario prestare attenzione al codice intorno a questo comportamento.  
  
 Per stabilire il comportamento di un'origine dati quando una transazione viene eseguito il commit o rollback, un'applicazione chiama **SQLGetInfo** con le opzioni SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR.
