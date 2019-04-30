---
title: Argomenti funzione Unicode | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3caa5feb387a7acdfa682f048bf77f2d999b560
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305789"
---
# <a name="unicode-function-arguments"></a>Argomenti funzione Unicode
La gestione Driver ODBC 3.5 (o versioni successive) supporta ANSI sia Unicode versioni di tutte le funzioni che accettano puntatori alle stringhe di caratteri o SQLPOINTER nei relativi argomenti. Le funzioni Unicode vengono implementate come funzioni (con suffisso *W*), non come macro. Le funzioni ANSI (che può essere chiamato con o senza un suffisso *oggetto*) sono identiche alle funzioni API ODBC corrente.  
  
## <a name="remarks"></a>Note  
 Le funzioni Unicode che restituiscono sempre o accettano stringhe o gli argomenti di lunghezza vengono passate come conteggio di caratteri. Per le funzioni che restituiscono informazioni sulla lunghezza per i dati del server, le dimensioni di visualizzazione e la precisione sono descritte nel numero di caratteri. Quando una lunghezza (dimensione di trasferimento dei dati) potrebbe fare riferimento ai dati stringa o non di tipo stringa, la lunghezza è descritta in lunghezze ottetto. Ad esempio, **SQLGetInfoW** richiederà comunque la lunghezza come conteggio di byte, ma **SQLExecDirectW** userà conteggio di caratteri.  
  
 Numero di caratteri si intende il numero di byte (in ottetti) per le funzioni ANSI e il numero di WCHAR (parole a 16 bit) per le funzioni UNICODE. In particolare, una sequenza di caratteri a byte doppio (DBCS) o una sequenza di caratteri multibyte (MBCS) può essere composte di più byte. Una sequenza di caratteri UTF-16 Unicode può essere costituita da più WCHAR.  
  
 Di seguito è riportato un elenco delle funzioni API ODBC che supportano le versioni sia Unicode (W) e ANSI (A):  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagField**|  
|**SQLColAttribute**|**SQLGetDiagRec**|  
|**SQLColAttributes**|**SQLGetInfo**|  
|**SQLColumnPrivileges**|**SQLGetStmtAttr**|  
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
  
 Di seguito è riportato un elenco delle funzioni di programma di installazione ODBC e funzione di conversione ODBC che supportano le versioni sia Unicode (W) e ANSI (A):  
  
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
>  Funzioni deprecate dispongono di supporto di mapping Unicode-to-ANSI poiché ODBC 3 *. x* Driver Manager supporta la ricompilazione di ODBC 2. *x* le applicazioni con la versione UNICODE **#define**.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Applicazioni Unicode](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Driver di Unicode](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [Mapping di funzioni in Gestione driver](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
