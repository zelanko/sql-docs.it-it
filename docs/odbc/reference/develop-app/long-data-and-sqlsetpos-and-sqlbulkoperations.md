---
title: Long Data e SQLSetPos e SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- SQLSetPos function [ODBC], long data and SQLBulkOperations
- data updates [ODBC], long data
- updating data [ODBC], long data
- SQLBulkOperations function [ODBC], long data
ms.assetid: e2fdf842-5e4c-46ca-bb21-4625c3324f28
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 578c85331a65c15cb25b5d9b75b7156ab509e910
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036415"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>Dati di tipo Long e SQLSetPos e SQLBulkOperations
Come nel caso dei parametri nelle istruzioni SQL, è possibile inviare dati lunghi quando si aggiornano le righe con **SQLBulkOperations** o **SQLSetPos** o quando si inseriscono righe con **SQLBulkOperations**. I dati vengono inviati in parti, con più chiamate a **SQLPutData**. Le colonne per le quali vengono inviati i dati in fase di esecuzione sono note come *colonne data-at-execution*.  
  
> [!NOTE]  
>  Un'applicazione può effettivamente inviare qualsiasi tipo di dati in fase di esecuzione con **SQLPutData**, anche se in parti possono essere inviati solo dati di tipo carattere e binario. Tuttavia, se i dati sono sufficientemente piccoli da adattarsi a un singolo buffer, in genere non esiste alcun motivo per usare **SQLPutData**. È molto più semplice associare il buffer e consentire al driver di recuperare i dati dal buffer.  
  
 Poiché le colonne di dati Long non sono in genere associate, l'applicazione deve associare la colonna prima di chiamare **SQLBulkOperations** o **SQLSetPos** e disassociarla dopo la chiamata di **SQLBulkOperations** o **SQLSetPos**. La colonna deve essere associata perché **SQLBulkOperations** o **SQLSetPos** funziona solo su colonne associate e deve essere non associato, in modo che sia possibile utilizzare **SQLGetData** per recuperare i dati dalla colonna.  
  
 Per inviare dati in fase di esecuzione, l'applicazione esegue le operazioni seguenti:  
  
1.  Inserisce un valore a 32 bit nel buffer del set di righe anziché un valore di dati. Questo valore verrà restituito all'applicazione in un secondo momento, quindi l'applicazione deve impostarla su un valore significativo, ad esempio il numero della colonna o l'handle di un file contenente i dati.  
  
2.  Imposta il valore nel buffer di lunghezza/indicatore sul risultato della macro SQL_LEN_DATA_AT_EXEC (*length*). Questo valore indica al driver che i dati per il parametro verranno inviati con **SQLPutData**. Il valore *length* viene utilizzato quando si inviano dati Long a un'origine dati che deve essere in grado di stabilire il numero di byte di dati lunghi da inviare, in modo da poter preallocare lo spazio. Per determinare se un'origine dati richiede questo valore, l'applicazione chiama **SQLGetInfo** con l'opzione SQL_NEED_LONG_DATA_LEN. Tutti i driver devono supportare questa macro. Se per l'origine dati non è necessaria la lunghezza in byte, il driver può ignorarlo.  
  
3.  Chiama **SQLBulkOperations** o **SQLSetPos**. Il driver rileva che un buffer di lunghezza/indicatore contiene il risultato della macro SQL_LEN_DATA_AT_EXEC (*length*) e restituisce SQL_NEED_DATA come valore restituito della funzione.  
  
4.  Chiama **SQLParamData** in risposta al valore restituito SQL_NEED_DATA. Se è necessario inviare dati lunghi, **SQLParamData** restituisce SQL_NEED_DATA. Nel buffer a cui punta l'argomento *ValuePtrPtr* , il driver restituisce il valore univoco che l'applicazione ha inserito nel buffer del set di righe. Se è presente più di una colonna data-at-execution, l'applicazione utilizza questo valore per determinare la colonna per cui inviare i dati; il driver non deve richiedere i dati per le colonne data-at-execution in un ordine particolare.  
  
5.  Chiama **SQLPutData** per inviare i dati della colonna al driver. Se i dati della colonna non rientrano in un singolo buffer, come spesso accade con i dati lunghi, l'applicazione chiama ripetutamente **SQLPutData** per inviare i dati in parti; è possibile riassemblare i dati al driver e all'origine dati. Se l'applicazione passa dati stringa con terminazione null, il driver o l'origine dati deve rimuovere il carattere di terminazione null come parte del processo di riassemblaggio.  
  
6.  Chiama di nuovo **SQLParamData** per indicare che sono stati inviati tutti i dati per la colonna. Se sono presenti colonne data-at-execution per cui non sono stati inviati dati, il driver restituisce SQL_NEED_DATA e il valore univoco per la colonna data-at-execution successiva; l'applicazione torna al passaggio 5. Se i dati sono stati inviati per tutte le colonne data-at-execution, i dati per la riga vengono inviati all'origine dati. **SQLParamData** restituisce quindi SQL_SUCCESS o SQL_SUCCESS_WITH_INFO e può restituire qualsiasi SQLSTATE che **SQLBulkOperations** o **SQLSetPos** può restituire.  
  
 Dopo che **SQLBulkOperations** o **SQLSetPos** restituisce SQL_NEED_DATA e prima che i dati siano stati inviati completamente per l'ultima colonna data-at-execution, l'istruzione è in uno stato dei dati necessario. In questo stato, l'applicazione può chiamare solo **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**o **SQLGetDiagRec**; tutte le altre funzioni restituiscono SQLSTATE HY010 (errore della sequenza di funzioni). Se si chiama **SQLCancel** , l'esecuzione dell'istruzione viene annullata e restituita allo stato precedente. Per ulteriori informazioni, vedere [Appendice B: tabelle di transizione dello stato ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
