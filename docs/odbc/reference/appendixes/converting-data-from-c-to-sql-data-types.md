---
title: Conversione di dati da C ai tipi di dati SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], about converting
- converting data from c to SQL types [ODBC]
- data conversions from C to SQL types [ODBC], about converting
- data types [ODBC], C data types
- data types [ODBC], converting data
- SQL data types [ODBC], converting from C types
- data types [ODBC], SQL data types
- data conversions from C to SQL types [ODBC]
- C data types [ODBC], converting to SQL types
ms.assetid: ee0afe78-b58f-4d34-ad9b-616bb23653bd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 168fa55d89488277cd17f4bdca3105f7d879c8f8
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52509405"
---
# <a name="converting-data-from-c-to-sql-data-types"></a>Conversione di dati da C ai tipi di dati SQL
Quando un'applicazione chiama **SQLExecute** oppure **SQLExecDirect**, il driver può recuperare i dati per i parametri associati con **SQLBindParameter** nei percorsi di archiviazione in l'applicazione. Quando un'applicazione chiama **SQLSetPos**, il driver recupera i dati per un aggiornamento o l'aggiunta di operazione da colonne associate **SQLBindCol**. Per i parametri data-at-execution, l'applicazione invia i dati del parametro con **SQLPutData**. Se necessario, il driver converte i dati dal tipo di dati specificato dal *ValueType* argomento nella **SQLBindParameter** al tipo di dati specificato da di *ParameterType*nell'argomento **SQLBindParameter**e quindi invia i dati all'origine dati.  
  
 Nella tabella seguente sono illustrate le conversioni supportate da ODBC C i tipi di dati per i tipi di dati SQL ODBC. Un cerchio pieno indica che la conversione predefinita per un tipo di dati SQL (il tipo di dati C da cui verranno convertiti i dati quando il valore di *ValueType* o il campo di descrizione SQL_DESC_CONCISE_TYPE è SQL_C_DEFAULT). Un cerchio vuoto indica una conversione supportata.  
  
 Il formato dei dati convertiti non dipende dall'impostazione Windows® paese.  
  
 ![Conversioni supportate: ODBC C in tipi di dati SQL](../../../odbc/reference/appendixes/media/apd1b.gif "apd1b")  
  
 Le tabelle nelle sezioni seguenti descrivono come il driver o l'origine dati converte i dati inviati all'origine dati; i driver devono supportare le conversioni da tutti i tipi di dati ODBC C ai tipi di dati SQL ODBC supportata. Per un determinato tipo di dati C ODBC, la prima colonna della tabella sono elencati i valori di input validi del *ParameterType* nell'argomento **SQLBindParameter**. La seconda colonna elenca i risultati di un test che il driver esegue per determinare se è possibile convertire i dati. La terza colonna indica il valore SQLSTATE restituito per ogni risultato dal **SQLExecDirect**, **SQLExecute**, **SQLBulkOperations**, **SQLSetPos**, oppure **SQLPutData**. I dati viene inviati all'origine dati solo se viene restituito SQL_SUCCESS.  
  
 Se il *ParameterType* nell'argomento **SQLBindParameter** contiene l'identificatore di un tipo di dati ODBC SQL che non viene visualizzato nella tabella per un determinato tipo di dati C, **SQLBindParameter**restituisce SQLSTATE 07006 (violazione dell'attributo del tipo di dati). Se il *ParameterType* l'argomento contiene un identificatore specifico del driver e il driver non supporta la conversione dal tipo di dati ODBC C specifico di tale tipo di dati specifici del driver SQL **SQLBindParameter** restituisce SQLSTATE HYC00 (funzionalità facoltativa non implementata).  
  
 Se il *ParameterValuePtr* e *StrLen_or_IndPtr* specificato nell'argomento **SQLBindParameter** sono entrambi puntatori null, che funzione restituisce SQLSTATE HY009 (non è valido utilizzo del puntatore null). Anche se non è visualizzata nelle tabelle, un'applicazione imposta il valore del buffer di lunghezza/indicatore a cui fa riferimento il *StrLen_or_IndPtr* argomento di **SQLBindParameter** oppure il valore della  *StrLen_or_IndPtr* dell'argomento **SQLPutData** su SQL_NULL_DATA per specificare un valore di dati SQL NULL. (Il *StrLen_or_IndPtr* argomento corrisponde al campo SQL_DESC_OCTET_LENGTH_PTR di APD.) L'applicazione imposta questi valori per SQL_NTS per specificare che il valore in \* *ParameterValuePtr* nelle **SQLBindParameter** oppure \* *DataPtr*nelle **SQLPutData** (a cui fa riferimento il campo SQL_DESC_DATA_PTR di APD) è una stringa con terminazione null.  
  
 Nelle tabelle vengono utilizzati i termini seguenti:  
  
-   **Lunghezza in byte dei dati** : numero di byte di dati SQL disponibili per l'invio all'origine dati, o meno i dati verranno troncati prima che venga inviata all'origine dati. Per i dati stringa, questo non include lo spazio per il carattere di terminazione null.  
  
-   **Lunghezza in byte colonna** -numero di byte necessari per archiviare i dati nell'origine dati.  
  
-   **Lunghezza in byte di caratteri** - massimo numero di byte necessari per visualizzare i dati in formato carattere. Si tratta come definito per ogni tipo di dati SQL in [visualizzare le dimensioni](../../../odbc/reference/appendixes/display-size.md), ad eccezione del fatto lunghezza in byte di caratteri è espresso in byte, mentre le dimensioni di visualizzazione sono in caratteri.  
  
-   **Numero di cifre** : numero di caratteri utilizzati per rappresentare un numero, incluso il segno di sottrazione, un separatore decimale e un esponente (se necessario).  
  
-   **Parole in**   
     ***corsivo*** -elementi di grammatica SQL. Per la sintassi di elementi di grammatica, vedere [appendice c: Grammatica SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [C a SQL: Carattere](../../../odbc/reference/appendixes/c-to-sql-character.md)  
  
-   [C a SQL: Numerico](../../../odbc/reference/appendixes/c-to-sql-numeric.md)  
  
-   [C a SQL: Bit](../../../odbc/reference/appendixes/c-to-sql-bit.md)  
  
-   [C a SQL: file binario](../../../odbc/reference/appendixes/c-to-sql-binary.md)  
  
-   [C a SQL: Data](../../../odbc/reference/appendixes/c-to-sql-date.md)  
  
-   [C a SQL: GUID](../../../odbc/reference/appendixes/c-to-sql-guid.md)  
  
-   [C a SQL: Ora](../../../odbc/reference/appendixes/c-to-sql-time.md)  
  
-   [C a SQL: timestamp](../../../odbc/reference/appendixes/c-to-sql-timestamp.md)  
  
-   [C a SQL: Intervalli anno-mese](../../../odbc/reference/appendixes/c-to-sql-year-month-intervals.md)  
  
-   [C a SQL: Intervalli di tempo](../../../odbc/reference/appendixes/c-to-sql-day-time-intervals.md)  
  
-   [Esempi di conversione di dati da C a SQL](../../../odbc/reference/appendixes/c-to-sql-data-conversion-examples.md)
