---
title: Dati di tipo Long e SQLSetPos e SQLBulkOperations | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036415"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>Dati di tipo Long e SQLSetPos e SQLBulkOperations
Come avviene con i parametri nelle istruzioni SQL, dati di tipo long possono essere inviati quando l'aggiornamento di righe con **SQLBulkOperations** oppure **SQLSetPos** o durante l'inserimento di righe con **SQLBulkOperations**. I dati vengono inviati in parti, con più chiamate a **SQLPutData**. Le colonne per cui i dati vengono inviati in fase di esecuzione sono noti come *colonne data-at-execution*.  
  
> [!NOTE]  
>  Un'applicazione può inviare effettivamente qualsiasi tipo di dati in fase di esecuzione con **SQLPutData**, anche se solo i caratteri e dati binari possono essere inviati in parti. Tuttavia, se i dati sono sufficientemente piccoli da rientrare in un singolo buffer, non è in genere necessario usare **SQLPutData**. È molto più semplice associare il buffer e lasciare che il driver di recuperare i dati dal buffer.  
  
 Poiché le colonne di dati long non sono in genere associate, l'applicazione deve essere associata la colonna prima di chiamare **SQLBulkOperations** oppure **SQLSetPos** e annullamento del binding, dopo la chiamata **SQLBulkOperations**  oppure **SQLSetPos**. La colonna deve essere associata poiché **SQLBulkOperations** oppure **SQLSetPos** opera solo sulle colonne associate e deve essere associato in modo che **SQLGetData** può essere utilizzato per recuperare i dati dalla colonna.  
  
 Per inviare dati in fase di esecuzione, l'applicazione effettua quanto segue:  
  
1.  Inserisce un valore a 32 bit nel buffer di set di righe anziché un valore di dati. Questo valore verrà restituito all'applicazione in un secondo momento, in modo che l'applicazione deve impostarla su un valore significativo, ad esempio il numero della colonna o l'handle di un file contenente i dati.  
  
2.  Imposta il valore nel buffer di lunghezza/indicatore al risultato della finestra di SQL_LEN_DATA_AT_EXEC (*lunghezza*) (macro). Questo valore indica al driver che verranno inviati con i dati per il parametro **SQLPutData**. Il *lunghezza* valore viene usato quando si inviano dati di tipo long a un'origine dati che deve conoscere il numero di byte di dati long verrà inviato in modo che può preallocare lo spazio. Per determinare se un'origine dati richiede questo valore, l'applicazione chiama **SQLGetInfo** con l'opzione SQL_NEED_LONG_DATA_LEN. Tutti i driver devono supportare questa macro. Se l'origine dati non richiede la lunghezza in byte, il driver può ignorarlo.  
  
3.  Le chiamate **SQLBulkOperations** oppure **SQLSetPos**. Il driver rileva che un buffer di lunghezza/indicatore contiene il risultato della finestra di SQL_LEN_DATA_AT_EXEC (*lunghezza*) restituisce SQL_NEED_DATA come valore restituito della funzione e macro.  
  
4.  Le chiamate **SQLParamData** in risposta a SQL_NEED_DATA il valore restituito. Se devono essere inviato, dati di tipo long **SQLParamData** restituisce SQL_NEED_DATA. Nel buffer a cui fa riferimento il *ValuePtrPtr* argomento, il driver restituisce il valore univoco che l'applicazione è collocata nel buffer di set di righe. Se è presente più di una colonna data-at-execution, l'applicazione utilizza questo valore per determinare quale colonna per inviare i dati; il driver non è necessario per richiedere i dati per le colonne data-at-execution in un ordine particolare.  
  
5.  Le chiamate **SQLPutData** per inviare i dati della colonna per il driver. Se i dati della colonna non rientrano in un singolo buffer, come accade spesso con dati di tipo long, l'applicazione chiama **SQLPutData** ripetutamente per inviare i dati in parti; in questo caso, il driver e l'origine dati per riassemblare i dati. Se l'applicazione passa i dati di stringa a terminazione null, l'origine dati o driver necessario rimuovere il carattere di terminazione null come parte del processo di riassemblaggio.  
  
6.  Le chiamate **SQLParamData** nuovamente per indicare che è stato inviato a tutti i dati per la colonna. Se sono presenti colonne data-at-execution per i quali non sono stati inviati i dati, il driver restituisce SQL_NEED_DATA e il valore univoco per la colonna data-at-execution successivo. l'applicazione torna al passaggio 5. Se i dati sono stati inviati per tutte le colonne data-at-execution, i dati per la riga viene inviati all'origine dati. **SQLParamData** restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO e può restituire qualsiasi valore SQLSTATE **SQLBulkOperations** oppure **SQLSetPos** può restituire.  
  
 Dopo aver **SQLBulkOperations** oppure **SQLSetPos** restituisce SQL_NEED_DATA e prima che i dati sono stati inviati completamente per l'ultima colonna data-at-execution, l'istruzione si trova in uno stato necessario dei dati. In questo stato, l'applicazione può chiamare solo **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**, o **SQLGetDiagRec**; tutte le altre funzioni restituiscono SQLSTATE HY010 (funzione di errore nella sequenza). La chiamata **SQLCancel** Annulla l'esecuzione dell'istruzione e lo restituisce lo stato precedente. Per altre informazioni, vedere [appendice b: Tabelle della transizione di stato ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
