---
title: Risultati multipli | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47e1250a92b78aefdc1611fd88e0ee9b0f772ad0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63254169"
---
# <a name="multiple-results"></a>Risultati multipli
Oggetto *risultato* è un elemento restituito dall'origine dati dopo che viene eseguita un'istruzione. ODBC include due tipi di risultati: set di risultati e conteggio delle righe. *Conteggio delle righe* sono il numero di righe interessate da un aggiornamento, eliminazione o istruzione insert. Batch, descritto nella [batch di istruzioni SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md), è possibile generare più risultati.  
  
 La tabella seguente elenca i **SQLGetInfo** opzioni un'applicazione utilizza per determinare se un'origine dati restituisce più risultati per ogni tipo di batch. In particolare, un'origine dati può restituire un conteggio delle righe solo per l'intero batch di istruzioni o i conteggi delle righe singole per ogni istruzione nel batch. Nel caso di un'istruzione di generazione di set di risultati eseguita con una matrice di parametri, l'origine dati può restituire un singolo set di risultati per tutti i set di parametri o singoli set di risultati per ogni set di parametri.  
  
|Tipo batch|Conteggio delle righe|Set di risultati|  
|----------------|----------------|-----------------|  
|Batch esplicita|SQL_BATCH_ROW_COUNT[a]|--[b]|  
|Routine|SQL_BATCH_ROW_COUNT[a]|--[b]|  
|Matrici di parametri|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 [a] riga numero di generazione di istruzioni in un batch potrebbero essere più supportate, ma la restituzione dei conteggi delle righe non è supportato. L'opzione SQL_BATCH_SUPPORT **SQLGetInfo** indica se sono consentite istruzioni di generazione di conteggio delle righe in batch, l'opzione SQL_BATCH_ROW_COUNTS indica se i conteggi delle righe vengono restituite all'applicazione.  
  
 [b] batch esplicite e alle procedure sempre restituiscono più set di risultati quando si includono più istruzioni che generano set di risultati.  
  
> [!NOTE]  
>  L'opzione SQL_MULT_RESULT_SETS introdotta in ODBC 1.0 fornisce informazioni generali solo sul fatto che possono essere restituiti più set di risultati. In particolare, è impostato su "Y" se vengono restituiti i bit SQL_BS_SELECT_EXPLICIT o SQL_BS_SELECT_PROC per SQL_BATCH_SUPPORT o se viene restituito SQL_PAS_BATCH per SQL_PARAM_ARRAYS_SELECT.  
  
 Per elaborare più risultati, un'applicazione chiama **SQLMoreResults**. Questa funzione Elimina il risultato corrente e rende disponibile il risultato successivo. Viene restituito SQL_NO_DATA quando non sono più disponibili. Si supponga, ad esempio, che le istruzioni seguenti vengono eseguite come batch:  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 Dopo queste istruzioni vengono eseguite, l'applicazione recupera righe dal set di risultati creati per il **seleziona** istruzione. Dopo che è stata eseguita durante il recupero di righe, viene chiamato **SQLMoreResults** per rendere disponibile il numero di parti che sono stati repriced. Se necessario, **SQLMoreResults** Elimina le righe non recuperate e chiude il cursore. L'applicazione chiama quindi **SQLRowCount** per determinare quante parti erano repriced dalle **UPDATE** istruzione.  
  
 È specifico del driver indica se l'istruzione dell'intero batch viene eseguita prima che i risultati siano disponibili. In alcune implementazioni, questo è il caso; in altri casi, la chiamata **SQLMoreResults** attiva l'esecuzione dell'istruzione successiva nel batch.  
  
 Se una delle istruzioni in un batch ha esito negativo, **SQLMoreResults** restituirà SQL_ERROR o SQL_SUCCESS_WITH_INFO. Se il batch è stato interrotto quando l'istruzione non è riuscita o l'istruzione non riuscita era l'ultima istruzione nel batch **SQLMoreResults** restituirà SQL_ERROR. Se il batch non è stato interrotto quando l'istruzione non è riuscita e l'istruzione non riuscita non era l'ultima istruzione nel batch, **SQLMoreResults** restituirà SQL_SUCCESS_WITH_INFO. SQL_SUCCESS_WITH_INFO indica che è stato generato almeno un set di risultati o conteggio e che il batch non è stata interrotta.
