---
title: Argomenti della funzione Unicode | Microsoft Docs
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
ms.openlocfilehash: 40ef9f63345572b5613942c1174ceeecadd146ee
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529740"
---
# <a name="unicode-function-arguments"></a>Argomenti funzione Unicode
Gestione driver ODBC 3,5 (o versione successiva) supporta le versioni ANSI e Unicode di tutte le funzioni che accettano puntatori a stringhe di caratteri o SQLPOINTER nei rispettivi argomenti. Le funzioni Unicode sono implementate come funzioni (con suffisso *W*), non come macro. Le funzioni ANSI, che possono essere chiamate con o senza un suffisso di *un*, sono identiche alle funzioni API ODBC correnti.  
  
## <a name="remarks"></a>Commenti  
 Per le funzioni Unicode che restituiscono sempre o accettano stringhe o argomenti di lunghezza, gli argomenti vengono passati come conteggio dei caratteri. Per le funzioni che restituiscono informazioni sulla lunghezza per i dati del server, le dimensioni e la precisione di visualizzazione sono descritte in numero di caratteri. Quando una lunghezza (dimensione di trasferimento dei dati) può fare riferimento a dati di stringa o non stringa, la lunghezza viene descritta in ottetti lunghezze. Ad esempio, la lunghezza di **SQLGetInfoW** sarà comunque pari a Count-of-bytes, ma **SQLExecDirectW** utilizzerà il numero di caratteri.  
  
 Il conteggio dei caratteri si riferisce al numero di byte (ottetti) per le funzioni ANSI e al numero di WCHAR (parole a 16 bit) per le funzioni UNICODE. In particolare, una sequenza di caratteri a doppio byte (DBCS) o una sequenza di caratteri multibyte (MBCS) può essere composta da più byte. Una sequenza di caratteri Unicode UTF-16 può essere composta da più WCHAR.  
  
 Di seguito è riportato un elenco delle funzioni API ODBC che supportano le versioni Unicode (W) e ANSI (A):  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagRec**|  
|**SQLColAttribute**|**SQLGetInfo**|  
|**SQLColAttributes**|**SQLGetStmtAttr**|  
|**SQLColumnPrivileges**|**SQLGetTypeInfo**|  
|**SQLColumns**|**SQLNativeSQL**|  
|**SQLConnect**|**SQLPrepare**|  
|**SQLDataSources**|**SQLPrimaryKeys**|  
|**SQLDescribeCol**|**SQLProcedureColumns**|  
|**SQLDriverConnect**|**SQLProcedures**|  
|**SQLDrivers**|**SQLSetConnectAttr**|  
|**SQLError**|**SQLSetConnectOption**|  
|**SQLExecDirect**|**SQLSetCursorName**|  
|**SQLForeignKeys**|**SQLSetDescField**|  
|**SQLGetConnectAttr**|**SQLSetStmtAttr**|  
|**SQLGetConnectOption**|**SQLSpecialColumns**|  
|**SQLGetCursorName**|**SQLStatistics**|  
|**SQLGetDescField**|**SQLTablePrivileges**|  
|**SQLGetDescRec**|**SQLTables**|  
|**SQLGetDiagField**||  
  
 Di seguito è riportato un elenco delle funzioni ODBC Installer e ODBC Translator che supportano le versioni Unicode (W) e ANSI (A):  
  
|||  
|-|-|  
|**SQLConfigDataSource**|**SQLInstallDriverManager**|  
|**SQLCreateDataSource**|**SQLInstallerError**|  
|**SQLDataSourceToDriver**|**SQLInstallODBC**|  
|**SQLDriverToDataSource**|**SQLReadFileDSN**|  
|**SQLGetAvailableDrivers**|**SQLRemoveDSNFromINI**|  
|**SQLGetInstalledDrivers**|**SQLValidDSN**|  
|**SQLGetTranslator**|**SQLWriteDSNToINI**|  
|**SQLInstallDriver**||  
  
> [!NOTE]
>  Le funzioni deprecate hanno supporto per il mapping da Unicode a ANSI perché il gestore di driver ODBC *3. x* supporta la ricompilazione di applicazioni ODBC *2. x* con il **#define**Unicode.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Applicazioni Unicode](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Driver di Unicode](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [Mapping di funzioni in Gestione driver](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
