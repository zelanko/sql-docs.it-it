---
title: Funzioni dell'API ODBC supportate . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC, API functions
- ODBC SQL grammar, API functions mapped to driver (table) [ODBC]
ms.assetid: b28a8ed6-09b1-4acf-bf3e-f90bb32422de
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec6ceaf57d8fe3c5325f85a9644cf4c8016663e4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304102"
---
# <a name="supported-odbc-api-functions"></a>Funzioni API ODBC supportate
Lo scopo del livellamento è quello di informare l'applicazione quali funzionalità sono disponibili per esso dal driver. I driver di database desktop Microsoft ODBC supportano tutte le funzioni Core e Livello 1.  
  
 Per ulteriori informazioni sui livelli di conformità per le funzioni e la grammatica, vedere Livelli di [conformità](../../odbc/reference/develop-app/conformance-levels.md) in *ODBC Programmer's Reference*.  
  
 Il supporto delle funzioni dell'API ODBC può dipendere dal driver utilizzato. Nella tabella seguente viene riepilogato il supporto per le funzioni. La colonna più a sinistra fornisce un collegamento alla pagina di riferimento generale per ogni funzione. Queste pagine di riferimento sono elencate in ordine alfabetico nella sezione [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md) , in ODBC [Programmer's Reference](../../odbc/reference/odbc-programmer-s-reference.md). Le colonne a destra forniscono collegamenti a note specifiche del driver su ogni funzione supportata. Questi argomenti specifici del driver sono elencati nella sezione "Altri dettagli di programmazione" per ogni driver. In alternativa, se le stesse osservazioni su una funzione si applicano a tutti i driver di database desktop ODBC, la colonna all'estrema destra fornisce un collegamento a un argomento che riepiloga il supporto dei driver di Database desktop per tale funzione. Questi argomenti sono elencati alla fine della sezione corrente ("Funzioni API ODBC supportate").  
  
|Funzione ODBC|Accedere alle note specifiche del driver|note specifiche del driver dBASE|Note specifiche del driver Paradox|Note specifiche del driver di file di testo|Note specifiche del driver di Excel|Note rilevanti per tutti i conducenti|  
|-------------------|-----------------------------------|----------------------------------|------------------------------------|--------------------------------------|----------------------------------|-----------------------------------|  
|[SQLBindParameter](../../odbc/reference/syntax/sqlbindparameter-function.md)|||||[Excel](../../odbc/microsoft/sqlbindparameter-excel-driver.md)||  
|[ATTRIBUTI SQLCol](../../odbc/reference/syntax/sqlcolattributes-function.md)|[Accesso](../../odbc/microsoft/sqlcolattributes-access-driver.md)|[Dbase](../../odbc/microsoft/sqlcolattributes-dbase-driver.md)|[Paradosso](../../odbc/microsoft/sqlcolattributes-paradox-driver.md)|[File di testo](../../odbc/microsoft/sqlcolattributes-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlcolattributes-excel-driver.md)||  
|[SQLColumns](../../odbc/reference/syntax/sqlcolattributes-function.md)|[Accesso](../../odbc/microsoft/sqlcolattributes-access-driver.md)|[Dbase](../../odbc/microsoft/sqlcolattributes-dbase-driver.md)|[Paradosso](../../odbc/microsoft/sqlcolattributes-paradox-driver.md)|[File di testo](../../odbc/microsoft/sqlcolattributes-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlcolattributes-excel-driver.md)||  
|[SQLConfigDataSource](../../odbc/reference/syntax/sqlconfigdatasource-function.md)|[Accesso](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)|[Dbase](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)|[Paradosso](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)|[File di testo](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)|[Excel](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)||  
|[SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)|[Accesso](../../odbc/microsoft/sqldriverconnect-access-driver.md)|[Dbase](../../odbc/microsoft/sqldriverconnect-dbase-driver.md)|[Paradosso](../../odbc/microsoft/sqldriverconnect-paradox-driver.md)|[File di testo](../../odbc/microsoft/sqldriverconnect-text-file-driver.md)|[Excel](../../odbc/microsoft/sqldriverconnect-excel-driver.md)||  
|[SQLGetCursorName](../../odbc/reference/syntax/sqlgetcursorname-function.md)||||||[Tutti i driver](../../odbc/microsoft/sqlgetcursorname-desktop-database-drivers.md)|  
|[SQLGetData](../../odbc/reference/syntax/sqlgetdata-function.md)||||||[Tutti i driver](../../odbc/microsoft/sqlgetdata-desktop-database-drivers.md)|  
|[SQLGetInfo](../../odbc/reference/syntax/sqlgetinfo-function.md)|[Accesso](../../odbc/microsoft/sqlgetinfo-access-driver.md)|[Dbase](../../odbc/microsoft/sqlgetinfo-dbase-driver.md)|[Paradosso](../../odbc/microsoft/sqlgetinfo-paradox-driver.md)|[File di testo](../../odbc/microsoft/sqlgetinfo-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlgetinfo-excel-driver.md)|
|[Opzione SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md)||||||[Tutti i driver](../../odbc/microsoft/sqlgetstmtoption-desktop-database-drivers.md)|  
|[SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md)|[Accesso](../../odbc/microsoft/sqlgettypeinfo-access-driver.md)|[Dbase](../../odbc/microsoft/sqlgettypeinfo-dbase-driver.md)|[Paradosso](../../odbc/microsoft/sqlgettypeinfo-paradox-driver.md)|[File di testo](../../odbc/microsoft/sqlgettypeinfo-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlgettypeinfo-excel-driver.md)||  
|[SQLMoreResults](../../odbc/reference/syntax/sqlmoreresults-function.md)||||||[Tutti i driver](../../odbc/microsoft/sqlmoreresults-desktop-database-drivers.md)|  
|[SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md)||||||[Tutti i driver](../../odbc/microsoft/sqlprepare-desktop-database-drivers.md)|  
|[SQLProcedureColumns](../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|[Accesso](../../odbc/microsoft/sqlprocedurecolumns-access-driver.md)||||||  
|[SQLProcedures](../../odbc/reference/syntax/sqlprocedures-function.md)||||||[Tutti i driver](../../odbc/microsoft/sqlprocedures-desktop-database-drivers.md)|  
|[Sqlsetconnectoption](../../odbc/reference/syntax/sqlsetconnectoption-function.md)|[Accesso](../../odbc/microsoft/sqlsetconnectoption-access-driver.md)|[Dbase](../../odbc/microsoft/sqlsetconnectoption-dbase-driver.md)|[Paradosso](../../odbc/microsoft/sqlsetconnectoption-paradox-driver.md)|[File di testo](../../odbc/microsoft/sqlsetconnectoption-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlsetconnectoption-excel-driver.md)||  
|[SQLSetCursorName (Nome cursore)](../../odbc/reference/syntax/sqlsetcursorname-function.md)||||||[Tutti i driver](../../odbc/microsoft/sqlsetcursorname-desktop-database-drivers.md)|  
|[SQLSetPos](../../odbc/reference/syntax/sqlsetpos-function.md)||||||[Tutti i driver](../../odbc/microsoft/sqlsetpos-desktop-database-drivers.md)|  
|[Opzioni SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md)||||||[Tutti i driver](../../odbc/microsoft/sqlsetscrolloptions-desktop-database-drivers.md)|  
|[Opzione SQLSetStmmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md)||||||[Tutti i driver](../../odbc/microsoft/sqlsetstmtoption-desktop-database-drivers.md)|  
|[SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md)||||||[Tutti i driver](../../odbc/microsoft/sqlspecialcolumns-desktop-database-drivers.md)|  
|[SQLStatistics](../../odbc/reference/syntax/sqlstatistics-function.md)|[Accesso](../../odbc/microsoft/sqlstatistics-access-driver.md)|[Dbase](../../odbc/microsoft/sqlstatistics-dbase-driver.md)|[Paradosso](../../odbc/microsoft/sqlstatistics-paradox-driver.md)|[File di testo](../../odbc/microsoft/sqlstatistics-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlstatistics-excel-driver.md)||  
|[SQLTables](../../odbc/reference/syntax/sqltables-function.md)|[Accesso](../../odbc/microsoft/sqltables-access-driver.md)|[Dbase](../../odbc/microsoft/sqltables-dbase-driver.md)|[Paradosso](../../odbc/microsoft/sqltables-paradox-driver.md)|[File di testo](../../odbc/microsoft/sqltables-text-file-driver.md)|[Excel](../../odbc/microsoft/sqltables-excel-driver.md)|  
|[SQLTransact (transazione SQLTransact)](../../odbc/reference/syntax/sqltransact-function.md)|[Accesso](../../odbc/microsoft/sqltransact-access-driver.md)|[Dbase](../../odbc/microsoft/sqltransact-dbase-driver.md)|[Paradosso](../../odbc/microsoft/sqltransact-paradox-driver.md)|[File di testo](../../odbc/microsoft/sqltransact-text-file-driver.md)|[Excel](../../odbc/microsoft/sqltransact-excel-driver.md)||  
  
 Negli argomenti riportati di seguito vengono fornite commenti sulle funzioni ODBC. Queste osservazioni si applicano a tutti i driver di database desktop ODBC.  
  
-   [SQLGetData (driver di database desktop)](../../odbc/microsoft/sqlgetdata-desktop-database-drivers.md)  
  
-   [SQLGetStmtOption(Driver di database desktop)](../../odbc/microsoft/sqlgetstmtoption-desktop-database-drivers.md)  
  
-   [SQLMoreResults (driver di database desktop)](../../odbc/microsoft/sqlmoreresults-desktop-database-drivers.md)  
  
-   [SQLPrepare (driver di database desktop)](../../odbc/microsoft/sqlprepare-desktop-database-drivers.md)  
  
-   [SQLProcedures (driver di database desktop)](../../odbc/microsoft/sqlprocedures-desktop-database-drivers.md)  
  
-   [SQLSetCursorName (driver di database desktop)](../../odbc/microsoft/sqlsetcursorname-desktop-database-drivers.md)  
  
-   [SQLSetPos (driver di database desktop)](../../odbc/microsoft/sqlsetpos-desktop-database-drivers.md)  
  
-   [SQLSetScrollOptions (driver di database desktop)](../../odbc/microsoft/sqlsetscrolloptions-desktop-database-drivers.md)  
  
-   [SQLSetStmtOption (driver di database desktop)](../../odbc/microsoft/sqlsetstmtoption-desktop-database-drivers.md)  
  
-   [SQLSpecialColumns (driver di database desktop)](../../odbc/microsoft/sqlspecialcolumns-desktop-database-drivers.md)
