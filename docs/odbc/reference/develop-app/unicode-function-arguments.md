---
title: 'Argomenti della funzione Unicode : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: eafe8c7e-f6d2-44d7-99ee-cf2148a30f4f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a25dd6fe0a77aad5c5ec9ba15eaf12bd2ec3fc18
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284291"
---
# <a name="unicode-function-arguments"></a>Argomenti funzione Unicode
Gestione Driver ODBC 3.5 (o versione successiva) supporta entrambe le versioni ANSI e Unicode di tutte le funzioni che accettano puntatori a stringhe di caratteri o SQLPOINTER nei relativi argomenti. Le funzioni Unicode vengono implementate come funzioni (con un suffisso *W*), non come macro. Le funzioni ANSI (che possono essere chiamate con o senza un suffisso *A*) sono identiche alle funzioni API ODBC correnti.  
  
## <a name="remarks"></a>Osservazioni  
 Le funzioni Unicode che restituiscono o accettano sempre stringhe o argomenti di lunghezza vengono passate come count-of-characters. Per le funzioni che restituiscono informazioni sulla lunghezza dei dati del server, le dimensioni e la precisione di visualizzazione sono descritte in numero di caratteri. Quando una lunghezza (dimensione di trasferimento dei dati) può fare riferimento a dati stringa o non stringa, la lunghezza è descritta in lunghezze di ottetti. Ad esempio, **SQLGetInfoW** assumerà comunque la lunghezza come conteggio dei byte, ma **SQLExecDirectW** utilizzerà il conteggio dei caratteri.  
  
 Il numero di caratteri si riferisce al numero di byte (ottetti) per le funzioni ANSI e al numero di wCHAR (parole a 16 bit) per le funzioni UNICODE. In particolare, una sequenza di caratteri a byte doppio (DBCS) o una sequenza di caratteri multibyte (MBCS) può essere composta da più byte. Una sequenza di caratteri Unicode UTF-16 può essere composta da più CCHAR.  
  
 Di seguito è riportato un elenco delle funzioni dell'API ODBC che supportano entrambe le versioni Unicode (W) e ANSI (A):  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagRec**|  
|**SQLColAttribute**|**SQLGetInfo**|  
|**ATTRIBUTI SQLCol**|**SQLGetStmtAttr**|  
|**SQLColumnPrivileges**|**SQLGetTypeInfo**|  
|**SQLColumns**|**SQLNativeSQL (SQLNativeSQL)**|  
|**SQLConnect**|**SQLPrepare**|  
|**SqlDataSourcesSQLDataSources**|**SQLPrimaryKeys**|  
|**SQLDescribeCol**|**SQLProcedureColumns**|  
|**SQLDriverConnect**|**SQLProcedures**|  
|**SQLDrivers**|**SQLSetConnectAttr**|  
|**Sqlerror**|**Sqlsetconnectoption**|  
|**SQLExecDirect**|**SQLSetCursorName (Nome cursore)**|  
|**SQLForeignKeys**|**SQLSetDescField**|  
|**SQLGetConnectAttr**|**SQLSetStmtAttr**|  
|**SQLGetConnectOption (Opzione SQLGetConnectOption)**|**SQLSpecialColumns**|  
|**SQLGetCursorName**|**SQLStatistics**|  
|**SQLGetDescField**|**SQLTablePrivileges**|  
|**SQLGetDescRec**|**SQLTables**|  
|**SQLGetDiagField**||  
  
 Di seguito è riportato un elenco delle funzioni del programma di installazione ODBC e del traduttore ODBC che supportano entrambe le versioni Unicode (W) e ANSI (A) :  
  
|||  
|-|-|  
|**SQLConfigDataSource**|**SQLInstallDriverManager (informazioni in lingua inglese)**|  
|**SQLCreateDataSource (origine SQLCreateDataSource)**|**Errore SQLInstallerError**|  
|**SQLDataSourceToDriver (informazioni in lingua inglese)**|**SQLInstallODBC (INFORMAZIONI in lingua inglese)**|  
|**SQLDriverToDataSourceSQLDriverToDataSource**|**SQLReadFileDSN (Informazioni in lingua inglese)**|  
|**SQLGetAvailableDrivers (Driver di SQLGetAvailableDrivers)**|**SQLRemoveDSNFromINI**|  
|**SQLGetInstalledDrivers (Driver SQLGetInstalledDrivers)**|**SQLValidDSN (Istruzione SQLValidDSN)**|  
|**SQLGetTranslator (Traduttore)**|**SQLWriteDSNToINI**|  
|**SQLInstallDriver (driver)**||  
  
> [!NOTE]
>  Le funzioni deprecate supportano il mapping Da Unicode a ANSI perché Gestione driver ODBC *3.x* supporta la ricompilazione di applicazioni ODBC *2.x* con unicode **#DEFINE**.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Applicazioni Unicode](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Driver di Unicode](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [Mapping di funzioni in Gestione driver](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
