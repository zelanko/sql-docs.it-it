---
title: Effetto delle transazioni sui cursori e sulle istruzioni preparate | Microsoft Docs
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
ms.openlocfilehash: 83b693922d08f7298d0c5282fe2c7d1c20149d5b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046886"
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>Effetto delle transazioni sui cursori e sulle istruzioni preparate
Il commit o il rollback di una transazione ha effetto sui cursori e sui piani di accesso seguenti:  
  
-   Tutti i cursori vengono chiusi e i piani di accesso per le istruzioni preparate su tale connessione vengono eliminati.  
  
-   Tutti i cursori vengono chiusi e i piani di accesso per le istruzioni preparate su tale connessione rimangono intatti.  
  
-   Tutti i cursori rimangono aperti e i piani di accesso per le istruzioni preparate su tale connessione rimangono intatti.  
  
 Si supponga, ad esempio, che un'origine dati esponga il primo comportamento in questo elenco, più restrittivo di questi comportamenti. Si supponga ora che un'applicazione esegue le operazioni seguenti:  
  
1.  Imposta la modalità di commit su Manual-commit.  
  
2.  Crea un set di risultati di ordini di vendita nell'istruzione 1.  
  
3.  Crea un set di risultati delle righe in un ordine di vendita sull'istruzione 2, quando l'utente evidenzia tale ordine.  
  
4.  Chiama **SQLExecute** per eseguire un'istruzione UPDATE posizionata preparata sull'istruzione 3, quando l'utente aggiorna una riga.  
  
5.  Chiama **SQLEndTran** per eseguire il commit dell'istruzione di aggiornamento posizionata.  
  
 A causa del comportamento dell'origine dati, la chiamata a **SQLEndTran** nel passaggio 5 causa la chiusura dei cursori nelle istruzioni 1 e 2 e l'eliminazione del piano di accesso per tutte le istruzioni. L'applicazione deve eseguire nuovamente le istruzioni 1 e 2 per ricreare i set di risultati e ripreparare l'istruzione nell'istruzione 3.  
  
 In modalità autocommit, funzioni diverse da **SQLEndTran** commit Transactions:  
  
-   **SQLExecute** o **SQLExecDirect** nell'esempio precedente, la chiamata a **SQLExecute** nel passaggio 4 esegue il commit di una transazione. In questo modo, l'origine dati chiuderà i cursori nelle istruzioni 1 e 2 ed eliminerà il piano di accesso per tutte le istruzioni della connessione.  
  
-   **SQLBulkOperations** o **SQLSetPos** nell'esempio precedente, si supponga che nel passaggio 4 l'applicazione chiami **SQLSetPos** con l'opzione SQL_UPDATE nell'istruzione 2, anziché eseguire un'istruzione UPDATE posizionata nell'istruzione 3. Viene eseguito il commit di una transazione e l'origine dati chiuderà i cursori sulle istruzioni 1 e 2 e eliminerà tutti i piani di accesso per tale connessione.  
  
-   **SQLCloseCursor** Nell'esempio precedente, si supponga che quando l'utente evidenzia un ordine di vendita diverso, l'applicazione chiama **SQLCloseCursor** sull'istruzione 2 prima di creare un risultato delle righe per il nuovo ordine di vendita. La chiamata a **SQLCloseCursor** esegue il commit dell'istruzione **SELECT** che ha creato il set di risultati delle righe e fa in modo che l'origine dati chiuda il cursore sull'istruzione 1 e quindi elimini tutti i piani di accesso per tale connessione.  
  
 Le applicazioni, in particolare quelle basate sullo schermo in cui l'utente scorre il set di risultati e aggiorna o Elimina le righe, devono prestare attenzione a scrivere codice intorno a questo comportamento.  
  
 Per determinare il comportamento di un'origine dati quando si esegue il commit o il rollback di una transazione, un'applicazione chiama **SQLGetInfo** con le opzioni SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR.
