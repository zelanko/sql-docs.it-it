---
title: 'Tipi di dati C : Documenti Microsoft'
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
- C buffers [ODBC]
ms.assetid: b681d260-3dbb-47df-a616-4910d727add7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 979bfe85e1e78b55718e1f12fdcfcc7583097bb4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292301"
---
# <a name="c-data-types"></a>Tipi di dati C
I tipi di dati C ODBC indicano il tipo di dati dei buffer C utilizzati per archiviare i dati nell'applicazione.  
  
 Tutti i driver devono supportare tutti i tipi di dati C.All drivers must support all C data types. Questa operazione è necessaria perché tutti i driver devono supportare tutti i tipi C in cui è possibile convertire i tipi SQL che supportano e tutti i driver supportano almeno un tipo SQL carattere. Poiché il tipo SQL carattere può essere convertito in e da tutti i tipi C, tutti i driver devono supportare tutti i tipi C.  
  
 Il tipo di dati C viene specificato nelle funzioni **SQLBindCol** e **SQLGetData** con l'argomento *TargetType* e nella funzione **SQLBindParameter** con l'argomento *ValueType.* Può anche essere specificato chiamando **SQLSetDescField** per impostare il campo SQL_DESC_CONCISE_TYPE di un ARD o APD o chiamando **SQLSetDescRec** con il *Type* argomento (e il *SubType* argomento se necessario) e *il DescriptorHandle* argomento impostato per l'handle di un ARD o APD.  
  
 Nelle tabelle seguenti sono elencati gli identificatori di tipo validi per i tipi di dati C. Nella tabella sono inoltre elencati il tipo di dati C ODBC che corrisponde a ogni identificatore e la definizione di questo tipo di dati.  
  
|Identificatore del tipo C|ODBC C typedef|Tipo C|  
|-----------------------|--------------------|------------|  
|SQL_C_CHAR|Proprietà SQLCHAR .|unsigned char *|  
|SQL_C_WCHAR|Proprietà SQLWCHAR .|wchar_t *|  
|SQL_C_SSHORT[j]|SQLSMALLINT|short int|  
|SQL_C_USHORT[j]|SQLUSMALLINT (informazioni in lingua inglese)|unsigned short int|  
|SQL_C_SLONG[j]|SQLINTEGER|long int|  
|SQL_C_ULONG[j]|SQLUINTEGER|unsigned long int|  
|SQL_C_FLOAT|SQLREAL (Informazioni IN LINGUA inglese)|float|  
|SQL_C_DOUBLE|SQLDOUBLE, SQLFLOAT|double|  
|SQL_C_BIT|SQLCHAR|unsigned char|  
|SQL_C_STINYINT[j]|ISTRUZIONE SQLSCHAR (Istruzione SQL)|signed char|  
|SQL_C_UTINYINT[j]|SQLCHAR|unsigned char|  
|SQL_C_SBIGINT|SQLBIGINT|_int64[h]|  
|SQL_C_UBIGINT|SQLUBIGINT (informazioni in lingua inglese)|_int64 non firmati[h]|  
|SQL_C_BINARY|Proprietà SQLCHAR .|unsigned char *|  
|SQL_C_BOOKMARK[i]|Segnalibro|unsigned long int[d]|  
|SQL_C_VARBOOKMARK|Proprietà SQLCHAR .|unsigned char *|  
|Tutti i tipi di dati intervallo C|SQL_INTERVAL_STRUCT|Vedere la sezione [Struttura intervallo C](../../../odbc/reference/appendixes/c-interval-structure.md) più avanti in questa appendice.|  
  
 **Identificatore del tipo C** SQL_C_TYPE_DATE[c]  
  
 **ODBC C typedef** SQL_DATE_STRUCT  
  
 **Tipo C**  
  
```  
struct tagDATE_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;    
} DATE_STRUCT;[a]  
```  
  
 **Identificatore del tipo C** SQL_C_TYPE_TIME[c]  
  
 **ODBC C typedef** SQL_TIME_STRUCT  
  
 **Tipo C**  
  
```  
struct tagTIME_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
} TIME_STRUCT;[a]  
```  
  
 **Identificatore del tipo C** SQL_C_TYPE_TIMESTAMP[c]  
  
 **ODBC C typedef** SQL_TIMESTAMP_STRUCT  
  
 **Tipo C**  
  
```  
struct tagTIMESTAMP_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
   SQLUINTEGER fraction;[b]   
} TIMESTAMP_STRUCT;[a]  
```  
  
 **Identificatore del tipo C** SQL_C_NUMERIC  
  
 **ODBC C typedef** SQL_NUMERIC_STRUCT  
  
 **Tipo C**  
  
```  
struct tagSQL_NUMERIC_STRUCT {  
   SQLCHAR precision;  
   SQLSCHAR scale;  
   SQLCHAR sign[g];  
   SQLCHAR val[SQL_MAX_NUMERIC_LEN];[e], [f]   
} SQL_NUMERIC_STRUCT;  
```  
  
 **Identificatore del tipo C** SQL_C_GUID  
  
 **ODBC C typedef** Sqlguid  
  
 **Tipo C**  
  
```  
struct tagSQLGUID {  
   DWORD Data1;  
   WORD Data2;  
   WORD Data3;  
   BYTE Data4[8];  
} SQLGUID;[k]  
```  
  
 [a] I valori dei campi year, month, day, hour, minute e second nei tipi di dati datetime C devono essere conformi ai vincoli del calendario gregoriano. (Vedere [vincoli del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md) più avanti in questa appendice.)  
  
 [b] Il valore del campo frazione è il numero di miliardesimi di secondo e varia da 0 a 999.999.999 (1 meno di 1 miliardo). Ad esempio, il valore del campo frazionario per mezzo secondo è 500.000.000, per un millesimo di secondo (un millisecondo) è 1.000.000, per un milionesimo di secondo (un microsecondo) è 1.000 e per un miliardesimo di secondo (un nanosecondo) è 1.  
  
 [c] In ODBC 2. *x*, i tipi di dati Data, ora e timestamp C sono SQL_C_DATE, SQL_C_TIME e SQL_C_TIMESTAMP.  
  
 [d] Le applicazioni ODBC 3 *.x* devono utilizzare SQL_C_VARBOOKMARK, non SQL_C_BOOKMARK. Quando un'applicazione *.x* ODBC 3 funziona con un ODBC 2. *x* driver, ODBC 3 *.x* Gestione Driver verrà mappato SQL_C_VARBOOKMARK a SQL_C_BOOKMARK.  
  
 [e] Un numero è memorizzato nel campo *val* della struttura SQL_NUMERIC_STRUCT come un numero intero scalato, in modalità little endian (il byte più a sinistra è il byte meno significativo). Ad esempio, il numero 10.001 in base 10, con una scala di 4, viene ridimensionato a un numero intero di 100010. Poiché si tratta di 186AA in formato esadecimale, il valore in SQL_NUMERIC_STRUCT sarebbe "AA 86 01 00 00 ... 00", con il numero di byte definito dal SQL_MAX_NUMERIC_LEN **#define**.  
  
 Per ulteriori informazioni **sullSQL_NUMERIC_STRUCT**, vedere [HOWTO: Recupero di dati numerici con SQL_NUMERIC_STRUCT](retrieve-numeric-data-sql-numeric-struct-kb222831.md).  
  
 [f] I campi di precisione e scala del tipo di dati SQL_C_NUMERIC vengono utilizzati per l'input da un'applicazione e per l'output dal driver all'applicazione. Quando il driver scrive un valore numerico nel SQL_NUMERIC_STRUCT, utilizzerà il proprio valore predefinito specifico del driver come valore per il campo di *precisione* e utilizzerà il valore nel campo SQL_DESC_SCALE del descrittore dell'applicazione (che il valore predefinito è 0) per il campo *di scala.* Un'applicazione può fornire i propri valori per precisione e scala impostando i SQL_DESC_PRECISION e SQL_DESC_SCALE campi del descrittore dell'applicazione.  
  
 [g] Il campo del segno è 1 se positivo, 0 se negativo.  
  
 [h] _int64 potrebbero non essere forniti da alcuni compilatori.  
  
 [i] _SQL_C_BOOKMARK è stata deprecata in ODBC 3 *.x*.  
  
 [j] _SQL_C_SHORT, SQL_C_LONG e SQL_C_TINYINT sono stati sostituiti in ODBC da tipi firmati e senza segno: SQL_C_SSHORT e SQL_C_USHORT, SQL_C_SLONG e SQL_C_ULONG e SQL_C_STINYINT e SQL_C_UTINYINT. Un driver *.x* ODBC 3 che deve funzionare con ODBC 2. *x* applicazioni devono supportare SQL_C_SHORT, SQL_C_LONG e SQL_C_TINYINT, perché quando vengono chiamati, Gestione Driver li passa attraverso al driver.  
  
 [k] SQL_C_GUID possono essere convertiti solo in SQL_CHAR o SQL_WCHAR.  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Strutture di interi a 64 bit](../../../odbc/reference/appendixes/64-bit-integer-structures.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati C in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)
