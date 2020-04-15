---
title: Dati lunghi e SQLSetPos e SQLBulkOperations Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4bc6c5d2da2f796a7c312971635fc36bc2fae8af
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287865"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>Dati di tipo Long e SQLSetPos e SQLBulkOperations
Come nel caso dei parametri nelle istruzioni SQL, i dati long possono essere inviati quando si aggiornano righe con **SQLBulkOperations** o **SQLSetPos** o quando si inseriscono righe con **SQLBulkOperations**. I dati vengono inviati in parti, con più chiamate a **SQLPutData**. Le colonne per le quali i dati vengono inviati in fase di esecuzione sono note come *colonne data-at-execution*.  
  
> [!NOTE]  
>  Un'applicazione può effettivamente inviare qualsiasi tipo di dati in fase di esecuzione con **SQLPutData**, anche se solo i dati di tipo carattere e binario possono essere inviati in parti. Tuttavia, se i dati sono sufficientemente piccoli da essere contenuti in un singolo buffer, non vi è in genere alcun motivo per utilizzare **SQLPutData**. È molto più semplice associare il buffer e consentire al driver di recuperare i dati dal buffer.  
  
 Poiché le colonne di dati lunghe in genere non sono associate, l'applicazione deve associare la colonna prima di chiamare **SQLBulkOperations** o **SQLSetPos** e annullarne l'associazione dopo aver chiamato **SQLBulkOperations** o **SQLSetPos**. La colonna deve essere associata perché **SQLBulkOperations** o **SQLSetPos** opera solo su colonne associate e deve essere non associata in modo che **SQLGetData** possa essere utilizzato per recuperare i dati dalla colonna.  
  
 Per inviare dati in fase di esecuzione, l'applicazione esegue le operazioni seguenti:To send data at execution time, the application does the following:  
  
1.  Inserisce un valore a 32 bit nel buffer del set di righe anziché un valore di dati. Questo valore verrà restituito all'applicazione in un secondo momento, pertanto l'applicazione deve impostarlo su un valore significativo, ad esempio il numero della colonna o l'handle di un file contenente dati.  
  
2.  Imposta il valore nel buffer di lunghezza/indicatore sul risultato della macro SQL_LEN_DATA_AT_EXEC(*length).* Questo valore indica al driver che i dati per il parametro verranno inviati con **SQLPutData**. Il valore di *lunghezza* viene utilizzato quando si inviano dati lunghi a un'origine dati che deve sapere quanti byte di dati long verranno inviati in modo da poter preallocare spazio. Per determinare se un'origine dati richiede questo valore, l'applicazione chiama **SQLGetInfo** con l'opzione SQL_NEED_LONG_DATA_LEN. Tutti i driver devono supportare questa macro; Se l'origine dati non richiede la lunghezza in byte, il driver può ignorarla.  
  
3.  Chiama **SQLBulkOperations** o **SQLSetPos**. Il driver rileva che un buffer di lunghezza/indicatore contiene il risultato della macro SQL_LEN_DATA_AT_EXEC(*length*) e restituisce SQL_NEED_DATA come valore restituito della funzione.  
  
4.  Chiama **SQLParamData** in risposta al valore restituito SQL_NEED_DATA. Se è necessario inviare dati lunghi, **SQLParamData** restituisce SQL_NEED_DATA. Nel buffer a cui punta l'argomento *ValuePtrPtr,* il driver restituisce il valore univoco inserito dall'applicazione nel buffer del set di righe. Se è presente più di una colonna data-at-execution, l'applicazione utilizza questo valore per determinare per quale colonna inviare i dati; il driver non è necessario richiedere dati per le colonne data-at-execution in un ordine particolare.  
  
5.  Chiama **SQLPutData** per inviare i dati della colonna al driver. Se i dati della colonna non rientrano in un singolo buffer, come spesso accade con i dati lunghi, l'applicazione chiama **SQLPutData** ripetutamente per inviare i dati in parti; spetta al driver e all'origine dati riassemblare i dati. Se l'applicazione passa dati stringa con terminazione null, il driver o l'origine dati deve rimuovere il carattere di terminazione null come parte del processo di riassemblaggio.  
  
6.  Chiama nuovamente **SQLParamData** per indicare che ha inviato tutti i dati per la colonna. Se sono presenti colonne data-at-execution per le quali i dati non sono stati inviati, il driver restituisce SQL_NEED_DATA e il valore univoco per la colonna data-at-execution successiva; l'applicazione torna al passaggio 5. Se sono stati inviati dati per tutte le colonne data-at-execution, i dati per la riga vengono inviati all'origine dati. **SQLParamData** restituisce quindi SQL_SUCCESS o SQL_SUCCESS_WITH_INFO e può restituire qualsiasi SQLSTATE che **SQLBulkOperations** o **SQLSetPos** può restituire.  
  
 Dopo **SQLBulkOperations** o **SQLSetPos** restituisce SQL_NEED_DATA e prima che i dati siano stati completamente inviati per l'ultima colonna data-at-execution, l'istruzione è in uno stato di dati necessari. In questo stato, l'applicazione può chiamare solo **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**o **SQLGetDiagRec**; tutte le altre funzioni restituiscono SQLSTATE HY010 (errore di sequenza di funzione). La chiamata a **SQLCancel** annulla l'esecuzione dell'istruzione e la riporta allo stato precedente. Per ulteriori informazioni, vedere [Appendice B: tabelle](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)di transizione dello stato ODBC .
