---
title: Conversione di dati da SQL ai tipi di dati C | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC]
- data conversions from SQL to C types [ODBC], about converting
- data types [ODBC], C data types
- data types [ODBC], converting data
- data types [ODBC], SQL data types
- SQL data types [ODBC], converting to C types
- converting data from SQL to c types [ODBC]
- converting data from SQL to c types [ODBC], about converting
- C data types [ODBC], converting from SQL types
ms.assetid: 029727f6-d3f0-499a-911c-bcaf9714e43b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6819b28ba57f1e6314535a6a90ad13de39b4842c
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793200"
---
# <a name="converting-data-from-sql-to-c-data-types"></a>Conversione di dati da SQL ai tipi di dati C
Quando un'applicazione chiama **SQLFetch**, **SQLFetchScroll**, o **SQLGetData**, i dati vengono recuperati dall'origine dati. Se necessario, ne converte i dati dal tipo di dati in cui il driver è stato recuperato al tipo di dati specificato per il *TargetType* argomento nella **SQLBindCol** o **SQLGetData.** Infine, archivia i dati nella posizione a cui fa riferimento il *TargetValuePtr* argomento nella **SQLBindCol** oppure **SQLGetData** (e il campo SQL_DESC_DATA_PTR del ARD).  
  
 Nella tabella seguente sono illustrate le conversioni supportate da ODBC SQL i tipi di dati per i tipi di dati C ODBC. Un cerchio pieno indica che la conversione predefinita per un tipo di dati SQL (il tipo di dati C nel quale saranno convertiti i dati quando il valore di *TargetType* è SQL_C_DEFAULT). Un cerchio vuoto indica una conversione supportata.  
  
 Per un database ODBC *3.x* funziona con un database ODBC *2.x* driver, la conversione da dati specifici del driver tipi potrebbero non essere supportati.  
  
 Il formato dei dati convertiti non dipende dall'impostazione Windows® paese.  
  
 Le tabelle nelle sezioni seguenti descrivono come il driver o l'origine di dati converte i dati recuperati dall'origine dati. i driver devono supportare le conversioni in tutti i tipi di dati C ODBC dai tipi di dati SQL ODBC supportata. Per un determinato tipo di dati SQL ODBC, la prima colonna della tabella sono elencati i valori di input validi del *TargetType* nell'argomento **SQLBindCol** e **SQLGetData**. La seconda colonna elenca i risultati di un test, spesso usando il *BufferLength* specificato nell'argomento **SQLBindCol** o **SQLGetData**, quali il driver esegue a determinare se è possibile convertire i dati. Per ogni risultato, la terza e la quarta colonna elenca i valori inseriti nel buffer specificato dal *TargetValuePtr* e *StrLen_or_IndPtr* gli argomenti specificati **SQLBindCol** oppure **SQLGetData** dopo che il driver ha tentato di convertire i dati. (Il *StrLen_or_IndPtr* argomento corrisponde al campo SQL_DESC_OCTET_LENGTH_PTR del ARD.) L'ultima colonna elenca il valore SQLSTATE restituito per ogni risultato dal **SQLFetch**, **SQLFetchScroll**, o **SQLGetData**.  
  
 Se il *TargetType* argomento nella **SQLBindCol** oppure **SQLGetData** contiene un identificatore per un tipo di dati C ODBC non indicato nella tabella per un determinato tipo di dati SQL ODBC  **SQLFetch**, **SQLFetchScroll**, o **SQLGetData** restituisce SQLSTATE 07006 (violazione dell'attributo del tipo di dati). Se il *TargetType* l'argomento contiene un identificatore che specifica una conversione da un tipo di dati specifici del driver SQL per un tipo di dati C ODBC e questa conversione non è supportata dal driver, **SQLFetch**, **SQLFetchScroll**, o **SQLGetData** restituisce SQLSTATE HYC00 (funzionalità facoltativa non implementata).  
  
 Anche se non è visualizzata nelle tabelle, il driver restituisce SQL_NULL_DATA nel buffer specificato per il *StrLen_or_IndPtr* argomento quando il valore di dati SQL è NULL. Per una spiegazione dell'uso del *StrLen_or_IndPtr* quando vengono effettuate più chiamate per recuperare i dati, vedere la [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)descrizione della funzione. Quando i dati di SQL viene convertiti in dati di tipo carattere C, il numero di caratteri restituiti nella \* *StrLen_or_IndPtr* non include i byte di terminazione null. Se *TargetValuePtr* è un puntatore null **SQLGetData** restituisce SQLSTATE HY009 (utilizzo non valido del puntatore null), in **SQLBindCol**, rimuove il binding della colonna.  
  
 Nelle tabelle vengono usate i termini e le convenzioni seguenti:  
  
-   **Lunghezza in byte dei dati** è il numero di byte di dati C disponibili da restituire in **TargetValuePtr*, se i dati verranno troncati prima che venga restituito all'applicazione. Per i dati stringa, questo non include lo spazio per il carattere di terminazione null.  
  
-   **Lunghezza in byte di caratteri** è il numero totale di byte necessari per visualizzare i dati in formato carattere. Si tratta come definito per ogni tipo di dati C nella sezione [visualizzare le dimensioni](../../../odbc/reference/appendixes/display-size.md), ad eccezione del fatto che lunghezza in byte di caratteri è espresso in byte, mentre le dimensioni di visualizzazione sono in caratteri.  
  
-   Parole *corsivo* rappresentano gli argomenti della funzione o gli elementi di grammatica SQL. Per la sintassi di elementi di grammatica, vedere [appendice c: Grammatica SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [SQL a c: Carattere](../../../odbc/reference/appendixes/sql-to-c-character.md)  
  
-   [SQL a c: Numeric](../../../odbc/reference/appendixes/sql-to-c-numeric.md)  
  
-   [SQL a c: Bit](../../../odbc/reference/appendixes/sql-to-c-bit.md)  
  
-   [SQL a c: file binario](../../../odbc/reference/appendixes/sql-to-c-binary.md)  
  
-   [SQL a c: Data](../../../odbc/reference/appendixes/sql-to-c-date.md)  
  
-   [SQL a c: GUID](../../../odbc/reference/appendixes/sql-to-c-guid.md)  
  
-   [SQL a c: Ora](../../../odbc/reference/appendixes/sql-to-c-time.md)  
  
-   [SQL a c: Timestamp](../../../odbc/reference/appendixes/sql-to-c-timestamp.md)  
  
-   [SQL a c: Intervalli anno-mese](../../../odbc/reference/appendixes/sql-to-c-year-month-intervals.md)  
  
-   [SQL a c: Intervalli di tempo](../../../odbc/reference/appendixes/sql-to-c-day-time-intervals.md)  
  
-   [Esempi di conversione di dati da SQL a C](../../../odbc/reference/appendixes/sql-to-c-data-conversion-examples.md)
