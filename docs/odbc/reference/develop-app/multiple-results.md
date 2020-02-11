---
title: Più risultati | Microsoft Docs
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
ms.openlocfilehash: f8679bea49b63ffd5dc7164942b42ac9eed7e9ab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086357"
---
# <a name="multiple-results"></a>Risultati multipli
Un *risultato* è un elemento restituito dall'origine dati dopo l'esecuzione di un'istruzione. In ODBC sono presenti due tipi di risultati: set di risultati e conteggi di righe. I *conteggi* delle righe sono il numero di righe interessate da un'istruzione Update, DELETE o INSERT. I batch, descritti in [batch di istruzioni SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md), possono generare più risultati.  
  
 Nella tabella seguente sono elencate le opzioni di **SQLGetInfo** utilizzate da un'applicazione per determinare se un'origine dati restituisce più risultati per ogni tipo di batch diverso. In particolare, un'origine dati può restituire un numero di righe singolo per l'intero batch di istruzioni o singoli conteggi di righe per ogni istruzione nel batch. Nel caso di un'istruzione di generazione dei set di risultati eseguita con una matrice di parametri, l'origine dati può restituire un singolo set di risultati per tutti i set di parametri o singoli set di risultati per ogni set di parametri.  
  
|Tipo batch|Conteggi di righe|Set di risultati|  
|----------------|----------------|-----------------|  
|Batch esplicito|SQL_BATCH_ROW_COUNT [a]|--[b]|  
|Procedura|SQL_BATCH_ROW_COUNT [a]|--[b]|  
|Matrici di parametri|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 [a] è possibile che siano supportate le istruzioni per la generazione di conteggi di righe in un batch, ma il ritorno dei conteggi delle righe non è supportato. L'opzione SQL_BATCH_SUPPORT in **SQLGetInfo** indica se le istruzioni di generazione dei conteggi delle righe sono consentite in batch; l'opzione SQL_BATCH_ROW_COUNTS indica se i conteggi delle righe vengono restituiti all'applicazione.  
  
 [b] i batch e le routine espliciti restituiscono sempre più set di risultati quando includono più istruzioni che generano più set di risultati.  
  
> [!NOTE]  
>  L'opzione SQL_MULT_RESULT_SETS introdotta in ODBC 1,0 fornisce solo informazioni generali sulla possibilità di restituire più set di risultati. In particolare, è impostato su "Y" Se vengono restituiti i bit SQL_BS_SELECT_EXPLICIT o SQL_BS_SELECT_PROC per SQL_BATCH_SUPPORT o se viene restituito SQL_PAS_BATCH per SQL_PARAM_ARRAYS_SELECT.  
  
 Per elaborare più risultati, un'applicazione chiama **SQLMoreResults**. Questa funzione Elimina il risultato corrente e rende disponibile il risultato successivo. Restituisce SQL_NO_DATA se non sono disponibili altri risultati. Si supponga, ad esempio, che le istruzioni seguenti vengano eseguite come batch:  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 Dopo l'esecuzione di queste istruzioni, l'applicazione recupera le righe dal set di risultati creato dall'istruzione **Select** . Al termine del recupero delle righe, chiama **SQLMoreResults** per rendere disponibile il numero di parti che sono state ricalcolate. Se necessario, **SQLMoreResults** rimuove le righe non recuperate e chiude il cursore. Tramite l'applicazione viene quindi chiamato **SQLRowCount** per determinare il numero di parti che sono state rivalutate dall'istruzione **Update** .  
  
 È specifico del driver se l'intera istruzione batch viene eseguita prima che siano disponibili risultati. In alcune implementazioni, questo è il caso. in altri casi, la chiamata di **SQLMoreResults** attiva l'esecuzione dell'istruzione successiva nel batch.  
  
 Se una delle istruzioni in un batch ha esito negativo, **SQLMoreResults** restituirà SQL_ERROR o SQL_SUCCESS_WITH_INFO. Se il batch è stato interrotto quando l'istruzione ha avuto esito negativo o l'istruzione non riuscita era l'ultima istruzione nel batch, **SQLMoreResults** restituirà SQL_ERROR. Se il batch non è stato interrotto quando l'istruzione ha avuto esito negativo e l'istruzione non riuscita non era l'ultima istruzione nel batch, **SQLMoreResults** restituirà SQL_SUCCESS_WITH_INFO. SQL_SUCCESS_WITH_INFO indica che è stato generato almeno un set di risultati o un conteggio e che il batch non è stato interrotto.
