---
title: 'Risultati multipli : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLMoreResults function [ODBC], multiple results
- row counts [ODBC]
- multiple results [ODBC]
- result sets [ODBC], multiple results
- SQLGetInfo function [ODBC], multiple results
ms.assetid: a3c32e4b-8fe7-4a33-ae39-ae664001f315
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d90414b631a7e81a7868ab7974b64ea84a0ea452
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302412"
---
# <a name="multiple-results"></a>Risultati multipli
Un *risultato* è un valore restituito dall'origine dati dopo l'esecuzione di un'istruzione. ODBC dispone di due tipi di risultati: set di risultati e conteggi di righe. *I conteggi delle righe* sono il numero di righe interessate da un'istruzione update, delete o insert. I batch, descritti in [Batch di istruzioni SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md), possono generare più risultati.  
  
 Nella tabella seguente sono elencate le opzioni **di SQLGetInfo** utilizzate da un'applicazione per determinare se un'origine dati restituisce più risultati per ogni tipo diverso di batch. In particolare, un'origine dati può restituire un conteggio di singole righe per l'intero batch di istruzioni o i conteggi di singole righe per ogni istruzione nel batch. Nel caso di un'istruzione che genera set di risultati eseguita con una matrice di parametri, l'origine dati può restituire un singolo set di risultati per tutti i set di parametri o singoli set di risultati per ogni set di parametri.  
  
|Tipo di batch|Conteggio righe|Set di risultati|  
|----------------|----------------|-----------------|  
|Batch esplicito|SQL_BATCH_ROW_COUNT[a]|--[b]|  
|Procedura|SQL_BATCH_ROW_COUNT[a]|--[b]|  
|Matrici di parametri|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 [a] Le istruzioni che generano conteggio righe in un batch possono essere supportate, ma la restituzione dei conteggi delle righe non è supportata. L'opzione SQL_BATCH_SUPPORT in **SQLGetInfo** indica se le istruzioni di generazione del conteggio delle righe sono consentite in batch. l'opzione SQL_BATCH_ROW_COUNTS indica se questi conteggi di righe vengono restituiti all'applicazione.  
  
 [b] I batch e le routine esplicite restituiscono sempre più set di risultati quando includono più istruzioni che generano set di risultati.  
  
> [!NOTE]  
>  L'opzione SQL_MULT_RESULT_SETS introdotta in ODBC 1.0 fornisce solo informazioni generali sulla restituzione di più set di risultati. In particolare, è impostata su "Y" se i bit SQL_BS_SELECT_EXPLICIT o SQL_BS_SELECT_PROC vengono restituiti per SQL_BATCH_SUPPORT o se SQL_PAS_BATCH viene restituito per SQL_PARAM_ARRAYS_SELECT.  
  
 Per elaborare più risultati, un'applicazione chiama **SQLMoreResults**. Questa funzione elimina il risultato corrente e rende disponibile il risultato successivo. Restituisce SQL_NO_DATA quando non sono disponibili altri risultati. Si supponga, ad esempio, che le istruzioni seguenti vengano eseguite come batch:  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 Dopo l'esecuzione di queste istruzioni, l'applicazione recupera le righe dal set di risultati creato dall'istruzione **SELECT.** Al termine del recupero delle righe, chiama **SQLMoreResults** per rendere disponibile il numero di parti che sono state rivalutate. Se necessario, **SQLMoreResults** elimina le righe inrecuperate e chiude il cursore. L'applicazione chiama quindi **SQLRowCount** per determinare quante parti sono state rivalutate dall'istruzione **UPDATE.**  
  
 È specifico del driver se l'intera istruzione batch viene eseguita prima che siano disponibili i risultati. In alcune implementazioni, questo è il caso; in altri, la chiamata **SQLMoreResults** attiva l'esecuzione dell'istruzione successiva nel batch.  
  
 Se una delle istruzioni in un batch ha esito negativo, **SQLMoreResults** restituirà SQL_ERROR o SQL_SUCCESS_WITH_INFO. Se il batch è stato interrotto quando l'istruzione non è riuscita o l'istruzione non riuscita è l'ultima istruzione del batch, **SQLMoreResults** restituirà SQL_ERROR. Se il batch non è stato interrotto quando l'istruzione non è riuscita e l'istruzione non riuscita non è l'ultima istruzione del batch, **SQLMoreResults** restituirà SQL_SUCCESS_WITH_INFO. SQL_SUCCESS_WITH_INFO indica che è stato generato almeno un set di risultati o un conteggio e che il batch non è stato interrotto.
