---
title: Effetto delle transazioni sui cursori e sulle istruzioni preparate . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ef3cb4095410b8ccb03b0a138f65b8df2cfb1a4b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300471"
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>Effetto delle transazioni sui cursori e sulle istruzioni preparate
Il commit o il rollback di una transazione ha il seguente effetto sui cursori e sui piani di accesso:  
  
-   Tutti i cursori vengono chiusi e i piani di accesso per le istruzioni preparate su tale connessione vengono eliminati.  
  
-   Tutti i cursori vengono chiusi e i piani di accesso per le istruzioni preparate su tale connessione rimangono intatti.  
  
-   Tutti i cursori rimangono aperti e i piani di accesso per le istruzioni preparate su tale connessione rimangono intatti.  
  
 Si supponga, ad esempio, che un'origine dati presenti il primo comportamento in questo elenco, il più restrittivo di questi comportamenti. Si supponga ora che un'applicazione esegua le operazioni seguenti:Now suppose an application does the following:  
  
1.  Imposta la modalità di commit su manual-commit.  
  
2.  Crea un set di risultati di ordini cliente nel rendiconto 1.  
  
3.  Crea un set di risultati delle righe in un ordine cliente nel rendiconto 2, quando l'utente evidenzia tale ordine.  
  
4.  Chiama **SQLExecute** per eseguire un'istruzione di aggiornamento posizionato che è stata preparata sull'istruzione 3, quando l'utente aggiorna una riga.  
  
5.  Chiama **SQLEndTran** per eseguire il commit dell'istruzione di aggiornamento posizionato.  
  
 A causa del comportamento dell'origine dati, la chiamata a **SQLEndTran** nel passaggio 5 fa sì che chiude i cursori sulle istruzioni 1 e 2 e per eliminare il piano di accesso su tutte le istruzioni. L'applicazione deve rieseguire le istruzioni 1 e 2 per ricreare i set di risultati e ripreparare l'istruzione sull'istruzione 3.  
  
 In modalità di commit automatico, funzioni diverse da SQLEndTran eseguono il commit delle transazioni:In auto-commit mode, functions other than **SQLEndTran** commit transactions:  
  
-   **SQLExecute** o **SQLExecDirect** Nell'esempio precedente, la chiamata a **SQLExecute** nel passaggio 4 esegue il commit di una transazione. In questo modo l'origine dati chiudere i cursori sulle istruzioni 1 e 2 ed eliminare il piano di accesso su tutte le istruzioni su tale connessione.  
  
-   **SQLBulkOperations** o **SQLSetPos** Nell'esempio precedente, si supponga che nel passaggio 4 l'applicazione chiama **SQLSetPos** con l'opzione SQL_UPDATE sull'istruzione 2, anziché eseguire un'istruzione di aggiornamento posizionato sull'istruzione 3. In questo modo viene eseguito il commit di una transazione e l'origine dati chiude i cursori nelle istruzioni 1 e 2 ed elimina tutti i piani di accesso per tale connessione.  
  
-   **Cursore SQL** Nell'esempio precedente, si supponga che quando l'utente evidenzia un ordine cliente diverso, l'applicazione chiama **SQLCloseCursor** sull'istruzione 2 prima di creare un risultato delle righe per il nuovo ordine cliente. La chiamata a **SQLCloseCursor** esegue il commit dell'istruzione **SELECT** che ha creato il set di risultati delle righe e fa sì che l'origine dati chiuda il cursore sull'istruzione 1, quindi elimina tutti i piani di accesso su tale connessione.  
  
 Le applicazioni, in particolare le applicazioni basate su schermo in cui l'utente scorre il set di risultati e aggiorna o elimina le righe, devono prestare attenzione al codice intorno a questo comportamento.  
  
 Per determinare il modo in cui un'origine dati si comporta quando viene eseguito il commit o il rollback di una transazione, un'applicazione chiama **SQLGetInfo** con le opzioni SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR.
