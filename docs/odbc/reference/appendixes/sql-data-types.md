---
title: Tipi di dati SQL - Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC]
- SQL data types [ODBC], about SQL data types
- data types [ODBC], SQL data types
ms.assetid: 1b22f985-f5e4-4779-87eb-e43329a442b1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3cc91213533aa39f30be1bc838cc014c20e70884
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305005"
---
# <a name="sql-data-types"></a>Tipi di dati SQL
Ogni DBMS definisce i propri tipi SQL. Ogni driver ODBC espone solo i tipi di dati SQL definiti dal sistema DBMS associato. Le informazioni sul modo in cui un driver esegue il mapping dei tipi SQL DBMS agli identificatori di tipo SQL definiti da ODBC e su come un driver esegue il mapping dei tipi SQL DBMS ai propri identificatori di tipo SQL specifici del driver tramite una chiamata a **SQLGetTypeInfo**. Un driver restituisce inoltre i tipi di dati SQL durante la descrizione dei tipi di dati di colonne e parametri tramite chiamate a **SQLColAttribute**, **SQLColumns**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLProcedureColumns**e **SQLSpecialColumns**.  
  
> [!NOTE]  
>  I tipi di dati SQL sono contenuti nei campi SQL_DESC_ CONCISE_TYPE, SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE dei descrittori di implementazione. Le caratteristiche dei tipi di dati SQL sono contenute nei campi SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH e SQL_DESC_OCTET_LENGTH dei descrittori di implementazione. Per altre informazioni, vedere Identificatori di tipi di [dati e descrittori](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) più avanti in questa appendice.  
  
 Un driver e un'origine dati specificati non supportano necessariamente tutti i tipi di dati SQL definiti in questa appendice. Il supporto di un driver per i tipi di dati SQL dipende dal livello di SQL-92 che il driver è conforme. Per determinare il livello di grammatica SQL-92 supportato dal driver, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_SQL_CONFORMANCE. Inoltre, un driver e un'origine dati specifici del driver possono supportare tipi di dati SQL aggiuntivi specifici del driver. Per determinare i tipi di dati supportati da un driver, un'applicazione chiama **SQLGetTypeInfo**. Per informazioni sui tipi di dati SQL specifici del driver, vedere la documentazione del driver. Per informazioni sui tipi di dati in un'origine dati specifica, vedere la documentazione relativa a tale origine dati.  
  
> [!IMPORTANT]  
>  Le tabelle in questa appendice sono solo linee guida e mostrano nomi, intervalli e limiti utilizzati in genere dei tipi di dati SQL. Una determinata origine dati può supportare solo alcuni dei tipi di dati elencati e le caratteristiche dei tipi di dati supportati possono essere diverse da quelle elencate.  
  
 Nella tabella seguente sono elencati gli identificatori di tipo SQL validi per tutti i tipi di dati SQL. La tabella elenca anche il nome e la descrizione del tipo di dati corrispondente da SQL-92 (se presente).  
  
|Identificatore del tipo SQL[1]|Dati SQL tipici<br /><br /> di tipo[2]|Descrizione del tipo tipico|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR(*n*)|Stringa di caratteri di lunghezza stringa fissa *n*.|  
|SQL_VARCHAR|VARCHAR(*n*)|Stringa di caratteri a lunghezza variabile con lunghezza massima della stringa *n*.|  
|SQL_LONGVARCHAR|LONG VARCHAR|Dati di caratteri a lunghezza variabile. La lunghezza massima dipende dall'origine dati. [9]|  
|SQL_WCHAR|WCHAR(*n*)|Stringa di caratteri Unicode di lunghezza fissa della stringa *n*|  
|SQL_WVARCHAR|VARWCHAR(*n*)|Stringa di caratteri a lunghezza variabile Unicode con lunghezza massima della stringa *n*|  
|SQL_WLONGVARCHAR|LONGWVARCHAR|Dati di caratteri a lunghezza variabile Unicode. La lunghezza massima dipende dall'origine dati|  
|SQL_DECIMAL|DECIMAL(*p*,*s*)|Valore con segno, esatto, numerico con una precisione di almeno *p* e scala *s.* (La precisione massima è definita dal driver.) (1 <- *p* <15; *s* <= *p*). [4]|  
|SQL_NUMERIC|NUMERIC(*p*,*s*)|Valore con segno, esatto, numerico con precisione *p* e scala *s* (1 <: *p* <- 15; *s* <= *p*). [4]|  
|SQL_SMALLINT|SMALLINT|Valore numerico esatto con precisione 5 e scala 0 (con segno: -32.768 <: *n* <: 32.767, senza segno: 0 <- *n* <- 65.535)[3].|  
|SQL_INTEGER|INTEGER|Valore numerico esatto con precisione 10 e scala 0 (con segno: -2[31] <*n* <- 2[31] - 1, senza segno: 0 <- *n* <- 2[32] - 1)[3].|  
|SQL_REAL|real|Valore numerico con segno, approssimativo e con precisione binaria 24 (zero o valore assoluto 10[-38] a 10[38]).|  
|SQL_FLOAT|FLOAT(*p*)|Valore numerico con segno, approssimativo e con una precisione binaria di almeno *p*. (La precisione massima è definita dal driver.) [5]|  
|SQL_DOUBLE|DOUBLE PRECISION|Valore numerico con segno, approssimativo e con una precisione binaria 53 (valore zero o assoluto 10[-308] a 10[308]).|  
|SQL_BIT|BIT|Dati binari a bit singolo. [8]|  
|SQL_TINYINT|TINYINT|Valore numerico esatto con precisione 3 e scala 0 (con segno: -128 <- *n* <: 127, unsigned: 0 <- *n* <s 255)[3].|  
|SQL_BIGINT|bigint|Valore numerico esatto con precisione 19 (se con segno) o 20 (se senza segno) e scala 0 (con segno: -2[63] <- *n* <- 2[63] - 1, senza segno: 0 <- *n* <- 2[64] - 1)[3],[9].|  
|SQL_BINARY|BINARIO(*n*)|Dati binari di lunghezza fissa *n*. [9]|  
|SQL_VARBINARY|VARBINARY(*n*)|Dati binari a lunghezza variabile di lunghezza massima *n*. Il valore massimo viene impostato dall'utente. [9]|  
|SQL_LONGVARBINARY|VARBINARY LUNGO|Dati binari a lunghezza variabile. La lunghezza massima dipende dall'origine dati. [9]|  
|SQL_TYPE_DATE[6]|DATE|Campi Anno, mese e giorno, conformi alle regole del calendario gregoriano. (Vedere [vincoli del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md), più avanti in questa appendice.)|  
|SQL_TYPE_TIME[6]|ORARIO(*p*)|Campi ora, minuto e secondo, con valori validi per ore da 00 a 23, valori validi per i minuti da 00 a 59 e valori validi per secondi da 00 a 61. Precisione *p* indica la precisione dei secondi.|  
|SQL_TYPE_TIMESTAMP[6]|TIMESTAMP(*p*)|Campi Anno, mese, giorno, ora, minuto e secondo, con valori validi definiti per i tipi di dati DATE e TIME.|  
|SQL_TYPE_UTCDATETIME|UTCDATETIME|Campi Anno, mese, giorno, ora, minuto, secondo, utchour e utcminute. I campi utchour e utcminute hanno una precisione di 1/10 microsecondi.|  
|SQL_TYPE_UTCTIME|UTCORA|Campi Hour, minute, second, utchour e utcminute. I campi utchour e utcminute hanno una precisione di 1/10 microsecondi.|  
|SQL_INTERVAL_MONTH[7]|MESE DI INTERVALLO(*p*)|Numero di mesi tra due date; *p* è la precisione di interlinea dell'intervallo.|  
|SQL_INTERVAL_YEAR[7]|INTERVAL ANNO(*p*)|Numero di anni tra due date; *p* è la precisione di interlinea dell'intervallo.|  
|SQL_INTERVAL_YEAR_TO_MONTH[7]|INTERVALLO ANNO(*p*) A MESE|Numero di anni e mesi tra due date; *p* è la precisione di interlinea dell'intervallo.|  
|SQL_INTERVAL_DAY[7]|GIORNO INTERVALLO(*p*)|Numero di giorni tra due date; *p* è la precisione di interlinea dell'intervallo.|  
|SQL_INTERVAL_HOUR[7]|INTERVAL HOUR(*p*)|Numero di ore tra due date/ore; *p* è la precisione di interlinea dell'intervallo.|  
|SQL_INTERVAL_MINUTE[7]|INTERVALLO MINUTE(*p*)|Numero di minuti tra due date/ore; *p* è la precisione di interlinea dell'intervallo.|  
|SQL_INTERVAL_SECOND[7]|INTERVALLO SECONDI(*p*,*q*)|Numero di secondi tra due date/ore; *p* è la precisione interlinea dell'intervallo e *q* è la precisione dei secondi dell'intervallo.|  
|SQL_INTERVAL_DAY_TO_HOUR[7]|INTERVALLO GIORNO(*p*) A ORA|Numero di giorni/ore tra due date/ore; *p* è la precisione di interlinea dell'intervallo.|  
|SQL_INTERVAL_DAY_TO_MINUTE[7]|INTERVALLO GIORNO(*p*) A MINUTO|Numero di giorni/ore/minuti tra due date/ore; *p* è la precisione di interlinea dell'intervallo.|  
|SQL_INTERVAL_DAY_TO_SECOND|GIORNO INTERVALLO(*p*) A SECONDI(*q*)|Numero di giorni/ore/minuti/secondi tra due date/ore; *p* è la precisione interlinea dell'intervallo e *q* è la precisione dei secondi dell'intervallo.|  
|SQL_INTERVAL_HOUR_TO_MINUTE[7]|INTERVALLO ORA(*p*) A MINUTO|Numero di ore/minuti tra due date/ore; *p* è la precisione di interlinea dell'intervallo.|  
|SQL_INTERVAL_HOUR_TO_SECOND[7]|INTERVALLO ORA(*p*) A SECONDI(*q*)|Numero di ore/minuti/secondi tra due date/ore; *p* è la precisione interlinea dell'intervallo e *q* è la precisione dei secondi dell'intervallo.|  
|SQL_INTERVAL_MINUTE_TO_SECOND[7]|INTERVALLO MINUTO(*p*) A SECONDI(*q*)|Numero di minuti/secondi tra due date/ore; *p* è la precisione interlinea dell'intervallo e *q* è la precisione dei secondi dell'intervallo.|  
|SQL_GUID|GUID|GUID a lunghezza fissa.|  
  
 [1] Questo è il valore restituito nella colonna DATA_TYPE da una chiamata a **SQLGetTypeInfo**.  
  
 [2] Questo è il valore restituito nella colonna NAME e CREATE PARAMS da una chiamata a **SQLGetTypeInfo**. La colonna NAME restituisce la tabella di designazione, ad esempio CHAR, mentre la colonna CREATE PARAMS restituisce un elenco separato da virgole di parametri di creazione quali precisione, scala e lunghezza.  
  
 [3] Un'applicazione utilizza **SQLGetTypeInfo** o **SQLColAttribute** per determinare se un particolare tipo di dati o una particolare colonna in un set di risultati è senza segno.  
  
 [4] i tipi di dati SQL_DECIMAL e SQL_NUMERIC differiscono solo per la loro precisione. La precisione di un DECIMAL(*p*,*s*) è una precisione decimale definita dall'implementazione che non è inferiore a *p*, mentre la precisione di un VALORE NUMERIC(*p*,*s*) è esattamente uguale a *p*.  
  
 [5] A seconda dell'implementazione, la precisione di SQL_FLOAT può essere 24 o 53: se è 24, il tipo di dati SQL_FLOAT è lo stesso di SQL_REAL; se è 53, il tipo di dati SQL_FLOAT è lo stesso di SQL_DOUBLE.  
  
 In ODBC *3.x*, i tipi di dati sql data, ora e timestamp sono rispettivamente SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP; in ODBC *2.x*i tipi di dati sono SQL_DATE, SQL_TIME e SQL_TIMESTAMP.  
  
 [7] Per ulteriori informazioni sui tipi di dati SQL di intervallo, vedere la sezione Tipi di [dati intervallo](../../../odbc/reference/appendixes/interval-data-types.md) più avanti in questa appendice.  
  
 Il tipo di dati SQL_BIT ha caratteristiche diverse rispetto al tipo BIT in SQL-92.  
  
 [9] Questo tipo di dati non ha un tipo di dati corrispondente in SQL-92.  
  
 In questa sezione viene fornito l'esempio seguente.  
  
-   [Esempio di set di risultati SQLGetTypeInfo](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
