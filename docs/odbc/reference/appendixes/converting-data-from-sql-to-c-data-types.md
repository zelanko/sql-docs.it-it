---
title: Conversione di dati da SQL a Tipi di dati C Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1a10730cb3910c55679c264583801cd57c83bfc3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284751"
---
# <a name="converting-data-from-sql-to-c-data-types"></a>Conversione di dati da SQL ai tipi di dati C
Quando un'applicazione chiama **SQLFetch**, **SQLFetchScroll**o **SQLGetData**, il driver recupera i dati dall'origine dati. Se necessario, converte i dati dal tipo di dati in cui il driver ha recuperato nel tipo di dati specificato dal *TargetType* argomento **SQLBindCol** o **SQLGetData.** Infine, archivia i dati nella posizione a cui fa riferimento il *TargetValuePtr* argomento in **SQLBindCol** o **SQLGetData** (e il SQL_DESC_DATA_PTR campo del ARD).  
  
 Nella tabella seguente vengono illustrate le conversioni supportate dai tipi di dati SQL ODBC ai tipi di dati ODBC C. Un cerchio pieno indica la conversione predefinita per un tipo di dati SQL (il tipo di dati C in cui verranno convertiti i dati quando il valore di *TargetType* è SQL_C_DEFAULT). Un cerchio vuoto indica una conversione supportata.  
  
 Per un'applicazione ODBC *3.x* che utilizza un driver ODBC *2.x,* la conversione da tipi di dati specifici del driver potrebbe non essere supportata.  
  
 Il formato dei dati convertiti non è influenzato dall'impostazione del paese di Windows®.  
  
 Le tabelle nelle sezioni seguenti descrivono come il driver o l'origine dati converte i dati recuperati dall'origine dati. i driver sono necessari per supportare le conversioni a tutti i tipi di dati ODBC C dai tipi di dati SQL ODBC che supportano. Per un determinato tipo di dati SQL ODBC, nella prima colonna della tabella sono elencati i valori di input valida dell'argomento *TargetType* in **SQLBindCol** e **SQLGetData**. Nella seconda colonna sono elencati i risultati di un test, spesso utilizzando l'argomento *BufferLength* specificato in **SQLBindCol** o **SQLGetData**, che il driver esegue per determinare se è possibile convertire i dati. Per ogni risultato, la terza e la quarta colonna elencano i valori inseriti nei buffer specificati dal *TargetValuePtr* e *StrLen_or_IndPtr* argomenti specificati in **SQLBindCol** o **SQLGetData** dopo che il driver ha tentato di convertire i dati. (L'argomento *StrLen_or_IndPtr* corrisponde al campo SQL_DESC_OCTET_LENGTH_PTR dell'ARD.) Nell'ultima colonna sono elencati i valori SQLSTATE restituiti per ogni risultato da **SQLFetch**, **SQLFetchScroll**o **SQLGetData**.  
  
 Se l'argomento *TargetType* in **SQLBindCol** o **SQLGetData** contiene un identificatore per un tipo di dati ODBC C non illustrato nella tabella per un determinato tipo di dati ODBC SQL, **SQLFetch**, **SQLFetchScroll**o **SQLGetData** restituisce SQLSTATE 07006 (violazione dell'attributo del tipo di dati con restrizioni). Se l'argomento *TargetType* contiene un identificatore che specifica una conversione da un tipo di dati SQL specifico del driver a un tipo di dati ODBC C e questa conversione non è supportata dal driver **SQLFetch**, **SQLFetchScroll**o **SQLGetData** restituisce SQLSTATE HYC00 (funzionalità facoltativa non implementata).  
  
 Anche se non è illustrato nelle tabelle, il driver restituisce SQL_NULL_DATA nel buffer specificato dal *StrLen_or_IndPtr* argomento quando il valore dei dati SQL è NULL. Per una spiegazione dell'uso di *StrLen_or_IndPtr* quando vengono effettuate più chiamate per recuperare i dati, vedere la descrizione della funzione [SQLGetData.](../../../odbc/reference/syntax/sqlgetdata-function.md) Quando i dati SQL vengono convertiti in dati \*di tipo carattere C, il numero di caratteri restituito in *StrLen_or_IndPtr* non include il byte di terminazione null. Se *TargetValuePtr* è un puntatore null, **SQLGetData** restituisce SQLSTATE HY009 (utilizzo non valido del puntatore null); in **SQLBindCol**, questa operazione disassocia la colonna.  
  
 Nelle tabelle vengono utilizzati i termini e le convenzioni seguenti:  
  
-   **Lunghezza in byte dei dati** è il numero di byte di dati C disponibili per la restituzione in*TargetValuePtr*, indipendentemente dal fatto che i dati vengano troncati o meno prima di essere restituiti all'applicazione. Per i dati stringa, non include lo spazio per il carattere di terminazione null.  
  
-   **Lunghezza byte carattere** indica il numero totale di byte necessari per visualizzare i dati in formato carattere. Questa operazione è definita per ogni tipo di dati C nella sezione [Dimensione di visualizzazione](../../../odbc/reference/appendixes/display-size.md), ad eccezione del fatto che la lunghezza dei byte dei caratteri è in byte mentre la dimensione di visualizzazione è in caratteri.  
  
-   Le parole in *corsivo* rappresentano gli argomenti della funzione o gli elementi della grammatica SQL. Per la sintassi degli elementi grammaticali, vedere [Appendice C: Grammatica SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Da SQL a C: carattere](../../../odbc/reference/appendixes/sql-to-c-character.md)  
  
-   [Da SQL a C: dati numerici](../../../odbc/reference/appendixes/sql-to-c-numeric.md)  
  
-   [Da SQL a C: bit](../../../odbc/reference/appendixes/sql-to-c-bit.md)  
  
-   [Da SQL a C: dati binari](../../../odbc/reference/appendixes/sql-to-c-binary.md)  
  
-   [Da SQL a C: data](../../../odbc/reference/appendixes/sql-to-c-date.md)  
  
-   [Da SQL a C: GUID](../../../odbc/reference/appendixes/sql-to-c-guid.md)  
  
-   [Da SQL a C: ora](../../../odbc/reference/appendixes/sql-to-c-time.md)  
  
-   [Da SQL a C: timestamp](../../../odbc/reference/appendixes/sql-to-c-timestamp.md)  
  
-   [Da SQL a C: intervalli anno-mese](../../../odbc/reference/appendixes/sql-to-c-year-month-intervals.md)  
  
-   [Da SQL a C: intervalli di tempo](../../../odbc/reference/appendixes/sql-to-c-day-time-intervals.md)  
  
-   [Esempi di conversione di dati da SQL a C](../../../odbc/reference/appendixes/sql-to-c-data-conversion-examples.md)
