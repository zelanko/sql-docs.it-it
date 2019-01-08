---
title: Tipi di dati SQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 623ac38791eebc6db84380dfadd499651af938af
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52507498"
---
# <a name="sql-data-types"></a>Tipi di dati SQL
Ogni sistema DBMS definisce i proprio tipi SQL. Ogni driver ODBC espone solo questi tipi di dati SQL che definisce il sistema DBMS associato. Informazioni sulle modalità di mapping di un driver SQL DBMS tipi per gli identificatori di tipo definite da ODBC SQL e come un driver esegue il mapping di tipi SQL DBMS per i proprio identificatori dei tipi specifici del driver SQL viene restituito tramite una chiamata a **SQLGetTypeInfo**. Un driver restituisce anche i tipi di dati SQL quando si descrivono i tipi di dati delle colonne e i parametri tramite le chiamate a **SQLColAttribute**, **SQLColumns**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLProcedureColumns**, e **SQLSpecialColumns**.  
  
> [!NOTE]  
>  I tipi di dati SQL sono contenuti nei campi SQL_DESC_ CONCISE_TYPE SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE di descrittori di implementazione. Caratteristiche dei tipi di dati SQL sono contenute nei campi SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH e SQL_DESC_OCTET_LENGTH di descrittori di implementazione. Per altre informazioni, vedere [identificatori di tipo di dati e i descrittori](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) più avanti in questa appendice.  
  
 Un driver e i dati di origine specificato non supportano necessariamente tutti i tipi di dati SQL che sono definiti in questa appendice. Supporto del driver per i tipi di dati SQL dipende dal livello di SQL-92 il driver conforme. Per determinare il livello di grammatica SQL-92 supportata dal driver, un'applicazione chiama **SQLGetInfo** con il tipo di informazioni SQL_SQL_CONFORMANCE. Inoltre, un driver e i dati di origine specificato può supportare tipi di dati SQL aggiuntivi, specifiche del driver. Per determinare i tipi di dati che un driver supportati, un'applicazione chiama **SQLGetTypeInfo**. Per informazioni sui tipi di dati specifici del driver SQL, vedere la documentazione del driver. Per informazioni sui tipi di dati in un'origine dati specifica, vedere la documentazione per l'origine dati.  
  
> [!IMPORTANT]  
>  Le tabelle in questa appendice sono solo le linee guida e Mostra in genere utilizzato nomi, intervalli e i limiti dei tipi di dati SQL. Una determinata origine dati potrebbe supportare solo alcuni dei tipi di dati elencati e le caratteristiche dei tipi di dati supportati possono differire da quelli elencati.  
  
 Nella tabella seguente sono elencati gli identificatori di tipo SQL validi per tutti i tipi di dati SQL. La tabella elenca anche il nome e la descrizione del tipo di dati corrispondente da SQL-92 (se presente).  
  
|Identificatore di tipo SQL [1]|Dati SQL tipica<br /><br /> tipo [2]|Descrizione del tipo tipico|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR (*n*)|Stringa di lunghezza fissa di caratteri *n*.|  
|SQL_VARCHAR|VARCHAR (*n*)|Stringa di caratteri a lunghezza variabile con lunghezza massima delle stringhe *n*.|  
|SQL_LONGVARCHAR|LONG VARCHAR|Dati di caratteri di lunghezza variabile. Lunghezza massima è dipendente dall'origine dati. [9]|  
|SQL_WCHAR|WCHAR (*n*)|Stringa di caratteri Unicode di lunghezza stringa fissa *n*|  
|SQL_WVARCHAR|VARWCHAR (*n*)|Stringa di caratteri di lunghezza variabile Unicode con lunghezza massima delle stringhe *n*|  
|SQL_WLONGVARCHAR|LONGWVARCHAR|Dati di tipo carattere a lunghezza variabile Unicode. Lunghezza massima: dipende dall'origine dati|  
|SQL_DECIMAL|DECIMAL (*p*,*s*)|Firmato, a valore numerico esatto con precisione pari ad almeno *p* e la scala *s.* (La precisione massima è definito dal driver). (1 < = *p* < = 15; *s* <= *p*). [ 4]|  
|SQL_NUMERIC|NUMERICO (*p*,*s*)|Firmato, a valore numerico esatto con precisione *p* e la scalabilità *s* (1 < = *p* < = 15; *s* <= *p*). [ 4]|  
|SQL_SMALLINT|SMALLINT|Valore numerico esatto con precisione 5 e scala 0 (firmato:-32.768 e < = *n* < = 32.767, senza segno:  0 < = *n* < = 65.535) [3].|  
|SQL_INTEGER|INTEGER|Valore numerico esatto con precisione 10 e scala 0 (firmato: -2 [31] < = *n* < = 2 [31] - 1, senza segno:  0 < = *n* < = 2 [32] - 1) [3].|  
|SQL_REAL|real|Valore con segno, numerico approssimativo con una precisione binaria di 24 (zero o valore assoluto da 10 [-38] a 10[38]).|  
|SQL_FLOAT|FLOAT (*p*)|Valore con segno, numerico approssimativo con una precisione binaria di almeno *p*. (La precisione massima è definito dal driver). [5]|  
|SQL_DOUBLE|DOUBLE PRECISION|Valore con segno, numerico approssimativo con una precisione binaria di 53 (zero o valore assoluto da 10 [-308] a 10[308]).|  
|SQL_BIT|BIT|Dati binari a singolo bit. [8]|  
|SQL_TINYINT|TINYINT|Valore numerico esatto con precisione 3 e scala 0 (firmato: da -128 < = *n* < = 127, senza segno:  0 < = *n* < = 255) [3].|  
|SQL_BIGINT|bigint|Esatto valore numerico con precisione 19 (con segno) o 20 (se senza segno) e scala 0 (firmato: -2 [63] < = *n* < = 2 [63] - 1, senza segno: 0 < = *n* < = 2 [64] - 1) [3], [9].|  
|SQL_BINARY|BINARIO (*n*)|Dati binari a lunghezza fissa *n*. [ 9]|  
|SQL_VARBINARY|VARBINARY (*n*)|Dati binari a lunghezza variabile di lunghezza massima *n*. Il valore massimo è impostato dall'utente. [9]|  
|SQL_LONGVARBINARY|LONG VARBINARY|Dati binari a lunghezza variabile. Lunghezza massima è dipendente dall'origine dati. [9]|  
|SQL_TYPE_DATE [6]|DATE|Anno, mese e giorno campi, conforme alle regole del calendario gregoriano. (Vedere [vincoli del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md), più avanti in questa appendice.)|  
|SQL_TYPE_TIME [6]|TEMPO (*p*)|Ora, minuto e secondo campi, con i valori validi per ore di valori validi da 00 a 23, da 00 a 59 minuti e i valori validi per i secondi da 00 a 61. Precisione *p* indica la precisione dei secondi.|  
|SQL_TYPE_TIMESTAMP [6]|TIMESTAMP (*p*)|Anno, mese, giorno, ora, minuto e secondo campi, con i valori validi come definito per i tipi di dati data e ora.|  
|SQL_TYPE_UTCDATETIME|UTCDATETIME|Anno, mese, giorno, ora, minuto, secondo, utchour e utcminute campi. I campi utchour e utcminute ha una precisione di microsecondo 1/10.|  
|SQL_TYPE_UTCTIME|UTCTIME|Ora, minuto, secondo, utchour e utcminute campi. I campi utchour e utcminute ha una precisione di 1/10 microsecondo...|  
|SQL_INTERVAL_MONTH [7]|INTERVALLO mese (*p*)|Numero di mesi tra due date; *p* è l'intervallo di precisione iniziale.|  
|SQL_INTERVAL_YEAR [7]|INTERVAL YEAR (*p*)|Numero di anni tra due date; *p* è l'intervallo di precisione iniziale.|  
|SQL_INTERVAL_YEAR_TO_MONTH [7]|INTERVAL YEAR (*p*) al mese|Numero di anni e mesi che intercorrono tra due date; *p* è l'intervallo di precisione iniziale.|  
|SQL_INTERVAL_DAY [7]|INTERVAL DAY (*p*)|Numero di giorni tra due date; *p* è l'intervallo di precisione iniziale.|  
|SQL_INTERVAL_HOUR [7]|INTERVALLO ora (*p*)|Numero di ore tra due date/ore; *p* è l'intervallo di precisione iniziale.|  
|SQL_INTERVAL_MINUTE [7]|MINUTI di intervallo (*p*)|Numero di minuti tra due date/ore; *p* è l'intervallo di precisione iniziale.|  
|SQL_INTERVAL_SECOND [7]|INTERVALLO di secondo (*p*,*q*)|Numero di secondi tra due date/ore; *p* è l'intervallo di precisione iniziale e *q* è la precisione dei secondi di intervallo.|  
|SQL_INTERVAL_DAY_TO_HOUR [7]|INTERVAL DAY (*p*) all'ora|Numero di giorni/ore tra due date/ore; *p* è l'intervallo di precisione iniziale.|  
|SQL_INTERVAL_DAY_TO_MINUTE [7]|INTERVAL DAY (*p*) al minuto|Numero di giorni/ore/minuti tra due date/ore; *p* è l'intervallo di precisione iniziale.|  
|SQL_INTERVAL_DAY_TO_SECOND [7]|INTERVAL DAY (*p*) al secondo (*q*)|Numero di giorni/ore/minuti/secondi tra due date/ore; *p* è l'intervallo di precisione iniziale e *q* è la precisione dei secondi di intervallo.|  
|SQL_INTERVAL_HOUR_TO_MINUTE [7]|INTERVALLO ora (*p*) al minuto|Numero di ore o minuti tra due date/ore; *p* è l'intervallo di precisione iniziale.|  
|SQL_INTERVAL_HOUR_TO_SECOND [7]|INTERVALLO ora (*p*) al secondo (*q*)|Numero di ore/minuti/secondi tra due date/ore; *p* è l'intervallo di precisione iniziale e *q* è la precisione dei secondi di intervallo.|  
|SQL_INTERVAL_MINUTE_TO_SECOND [7]|MINUTI di intervallo (*p*) al secondo (*q*)|Numero di minuti/secondi tra due date/ore; *p* è l'intervallo di precisione iniziale e *q* è la precisione dei secondi di intervallo.|  
|SQL_GUID|GUID|GUID di lunghezza fissa.|  
  
 [1]. questo è il valore restituito nella colonna DATA_TYPE da una chiamata a **SQLGetTypeInfo**.  
  
 [2] si tratta del valore restituito nella colonna nome e la creazione di parametri da una chiamata a **SQLGetTypeInfo**. La colonna nome restituisce la designazione-CHAR, ad esempio,-mentre la colonna creare PARAMS restituisce un elenco delimitato da virgole dei parametri di creazione, ad esempio precisione, scala e lunghezza.  
  
 [3] un'applicazione utilizza **SQLGetTypeInfo** oppure **SQLColAttribute** per determinare se un particolare tipo di dati o una colonna specifica in un set di risultati è senza segno.  
  
 [4] tipi di dati SQL_DECIMAL e SQL_NUMERIC differiscono solo per loro precisione. La precisione di un numero decimale (*p*,*s*) è una precisione decimale definito dall'implementazione che è non inferiore a *p*, mentre la precisione di un valore numerico (*p* ,*s*) è esattamente uguale alla *p*.  
  
 [5] a seconda dell'implementazione, può essere la precisione del SQL_FLOAT 24 o 53: se è 24, il tipo di dati SQL_FLOAT è identico SQL_REAL; Se è 53, il tipo di dati SQL_FLOAT è identico SQL_DOUBLE.  
  
 [6] in ODBC 3 *. x*, i tipi di dati SQL date, time e timestamp sono SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP, rispettivamente; in ODBC 2. *x*, i tipi di dati sono SQL_DATE, SQL_TIME e SQL_TIMESTAMP.  
  
 [7] per altre informazioni sui tipi di dati intervallo SQL, vedere la [tipi di dati intervallo](../../../odbc/reference/appendixes/interval-data-types.md) più avanti in questa appendice.  
  
 [8] il tipo di dati SQL_BIT ha caratteristiche diverse rispetto al tipo BIT SQL-92.  
  
 [9] questo tipo di dati non dispone di alcun tipo di dati corrispondente in SQL-92.  
  
 Questa sezione vengono fornite nell'esempio seguente.  
  
-   [Esempio di set di risultati SQLGetTypeInfo](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
