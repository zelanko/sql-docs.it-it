---
title: Tipi di dati C | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f948b50fae0995e16024ac41d8dd891630d1dbe
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53208462"
---
# <a name="c-data-types"></a>Tipi di dati C
Tipi di dati C ODBC indicano il tipo di dati di C buffer usato per archiviare i dati nell'applicazione.  
  
 Tutti i driver devono supportare tutti i tipi di dati C. Questa operazione è necessaria perché tutti i driver devono supportare tutti i tipi C a cui possono essere convertiti tipi SQL supportano a loro, e tutti i driver supportano almeno un carattere di tipo SQL. Perché il tipo di carattere SQL può essere convertito in e da tutti i tipi di C, tutti i driver devono supportare tutti i tipi C.  
  
 Viene specificato il tipo di dati C nel **SQLBindCol** e **SQLGetData** funzioni con il *TargetType* argomento e nella **SQLBindParameter**delle funzioni con il *ValueType* argomento. Può anche essere specificato tramite la chiamata **SQLSetDescField** per impostare il campo SQL_DESC_CONCISE_TYPE di un ARD o APD, oppure chiamando **SQLSetDescRec** con il *tipo* argomento (e il *sottotipo* argomento se necessario) e il *DescriptorHandle* argomento impostato per l'handle di un ARD o APD.  
  
 Nelle tabelle seguenti sono elencati gli identificatori di tipo valido per i tipi di dati C. Nella tabella sono inoltre elencati il tipo di dati C ODBC che corrisponde a ogni identificatore e la definizione di questo tipo di dati.  
  
|Identificatore di tipo C|Typedef di ODBC C|Tipo C|  
|-----------------------|--------------------|------------|  
|SQL_C_CHAR|SQLCHAR *|unsigned char *|  
|SQL_C_WCHAR|SQLWCHAR *|wchar_t *|  
|SQL_C_SSHORT [j#]|SQLSMALLINT|short int|  
|SQL_C_USHORT [j#]|SQLUSMALLINT|Unsigned Integer a breve|  
|SQL_C_SLONG [j#]|SQLINTEGER|long int|  
|SQL_C_ULONG [j#]|SQLUINTEGER|long int senza segno|  
|SQL_C_FLOAT|SQLREAL|FLOAT|  
|SQL_C_DOUBLE|SQLDOUBLE, SQLFLOAT|double|  
|SQL_C_BIT|SQLCHAR|unsigned char|  
|SQL_C_STINYINT [j#]|SQLSCHAR|char con segno|  
|SQL_C_UTINYINT [j#]|SQLCHAR|unsigned char|  
|SQL_C_SBIGINT|SQLBIGINT|_int64 [h]|  
|SQL_C_UBIGINT|SQLUBIGINT|_int64 non firmati [h]|  
|SQL_C_BINARY|SQLCHAR *|unsigned char *|  
|SQL_C_BOOKMARK [i]|SEGNALIBRO|long int senza segno [d]|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|  
|Tutti i tipi di dati di intervallo C|SQL_INTERVAL_STRUCT|Vedere le [struttura C Interval](../../../odbc/reference/appendixes/c-interval-structure.md) più avanti in questa appendice.|  
  
 **Identificatore di tipo C** SQL_C_TYPE_DATE [c]  
  
 **Typedef di ODBC C** valore SQL_DATE_STRUCT  
  
 **Tipo C**  
  
```  
struct tagDATE_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;    
} DATE_STRUCT;[a]  
```  
  
 **Identificatore di tipo C** SQL_C_TYPE_TIME [c]  
  
 **Typedef di ODBC C** SQL_TIME_STRUCT  
  
 **Tipo C**  
  
```  
struct tagTIME_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
} TIME_STRUCT;[a]  
```  
  
 **Identificatore di tipo C** SQL_C_TYPE_TIMESTAMP [c]  
  
 **Typedef di ODBC C** SQL_TIMESTAMP_STRUCT  
  
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
  
 **Identificatore di tipo C** SQL_C_NUMERIC  
  
 **Typedef di ODBC C** SQL_NUMERIC_STRUCT  
  
 **Tipo C**  
  
```  
struct tagSQL_NUMERIC_STRUCT {  
   SQLCHAR precision;  
   SQLSCHAR scale;  
   SQLCHAR sign[g];  
   SQLCHAR val[SQL_MAX_NUMERIC_LEN];[e], [f]   
} SQL_NUMERIC_STRUCT;  
```  
  
 **Identificatore di tipo C** SQL_C_GUID  
  
 **Typedef di ODBC C** SQLGUID  
  
 **Tipo C**  
  
```  
struct tagSQLGUID {  
   DWORD Data1;  
   WORD Data2;  
   WORD Data3;  
   BYTE Data4[8];  
} SQLGUID;[k]  
```  
  
 [a] i valori di anno, mese, giorno, ora, minuto e secondo campi nei tipi di dati datetime C devono essere conforme ai vincoli del calendario gregoriano. (Vedere [vincoli del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md) più avanti in questa appendice.)  
  
 [b] il valore del campo frazione è il numero di miliardesimi di secondo e compreso tra 0 e 999.999.999 (1 meno di 1 miliardo). Ad esempio, il valore del campo della frazione per mezzo secondo viene 500,000,000, per un millesimo di secondo (un millisecondo) è pari a 1.000.000, per un milionesimo di secondo (un microsecondo) è 1.000 e per un miliardesimo di secondo (un nanosecondo) è 1.  
  
 [c] in ODBC 2. *x*, i tipi di dati date, time e timestamp C sono SQL_C_DATE SQL_C_TIME e SQL_C_TIMESTAMP.  
  
 [d] ODBC 3*x* le applicazioni devono utilizzare SQL_C_VARBOOKMARK, non SQL_C_BOOKMARK. Quando un'applicazione ODBC 3 *. x* applicazione funziona con un'API ODBC 2. *x* driver ODBC 3*x* gestione Driver assocerà SQL_C_VARBOOKMARK SQL_C_BOOKMARK.  
  
 numero [e] A viene archiviato nel *val* campo della struttura SQL_NUMERIC_STRUCT come un integer ridotto, in modalità little-endian piccolo (il byte più a sinistra in corso il byte meno significativo). È ad esempio, aumentare il numero 10,001 in base 10, con una scala pari a 4, per un numero intero di 100010. Poiché si tratta 186AA in formato esadecimale, il valore in SQL_NUMERIC_STRUCT sarebbe "AA 86 01 00 00... 00", con il numero di byte definito dal SQL_MAX_NUMERIC_LEN **#define**.  
  
 Per altre informazioni sulle **SQL_NUMERIC_STRUCT**, vedere [HOWTO: Recupero di dati numerici con SQL_NUMERIC_STRUCT](retrieve-numeric-data-sql-numeric-struct-kb222831.md).  
  
 [f] i campi di precisione e scala di quelli SQL_C_NUMERIC digitare areused per l'input da un'applicazione e per l'output dal driver per l'applicazione. Quando il driver scrive un valore numerico nel SQL_NUMERIC_STRUCT, userà il proprio predefinito specifico del driver come valore per il *precisione* campo che userà il valore nel campo del descrittore applicazione (SQL_DESC_SCALE quale valore predefinito è 0) per il *scalabilità* campo. Un'applicazione può fornire i propri valori per la precisione e scala definendo i campi SQL_DESC_PRECISION e SQL_DESC_SCALE del descrittore dell'applicazione.  
  
 [g] il campo di accesso è 1 se è positivo, 0 se è negativo.  
  
 [h] _int64 potrebbe non essere fornito da alcuni compilatori.  
  
 [i] _SQL_C_BOOKMARK è stata deprecata in ODBC 3*x*.  
  
 [j#] _SQL_C_SHORT SQL_C_LONG e SQL_C_TINYINT sono stati sostituiti in ODBC da tipi signed che unsigned: SQL_C_SSHORT e SQL_C_USHORT, SQL_C_SLONG e SQL_C_ULONG e SQL_C_STINYINT e SQL_C_UTINYINT. Un'applicazione ODBC 3 *. x* driver che dovrebbero lavorare con l'API ODBC 2. *x* le applicazioni devono supportare SQL_C_SHORT SQL_C_LONG e SQL_C_TINYINT, perché quando vengono chiamati, gestione Driver li passa attraverso al driver.  
  
 [k] SQL_C_GUID può essere convertito solo in SQL_CHAR o SQL_WCHAR.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Strutture di interi a 64 bit](../../../odbc/reference/appendixes/64-bit-integer-structures.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati C in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)
