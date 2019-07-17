---
title: Gli argomenti in funzioni di catalogo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arguments in catalog functions [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], about arguments
- functions [ODBC], catalog functions
ms.assetid: f5e0abec-8f24-42e0-b94f-16dd1f2004fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 649c00f1db486dab4a996138be4e26b0e270fbae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106290"
---
# <a name="arguments-in-catalog-functions"></a>Argomenti nelle funzioni di catalogo
Tutte le funzioni di catalogo di accettare argomenti con cui un'applicazione può limitare l'ambito dei dati restituiti. Ad esempio, le chiamate per primo e il seconda **SQLTables** nel codice seguente restituisce un set di risultati contenente informazioni su tutte le tabelle, mentre la terza chiamata restituisce informazioni relative alla tabella Orders:  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 Gli argomenti stringa della funzione catalogo rientrano in quattro tipi diversi: argomento ordinario (OA), argomento di valore pattern (PV), argomento dell'identificatore (ID) e argomento di valore di elenco (VL). La maggior parte degli argomenti di tipo stringa possono essere di uno dei due tipi diversi, a seconda del valore dell'attributo di istruzione SQL_ATTR_METADATA_ID. Nella tabella seguente sono elencati gli argomenti per ogni funzione di catalogo e descrive il tipo dell'argomento per valore SQL_TRUE o SQL_FALSE pari SQL_ATTR_METADATA_ID.  
  
|Funzione|Argomento|Al tipo quando SQL _<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_FALSE|Al tipo quando SQL _<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*CatalogName* *SchemaName* *NomeTabella* *ColumnName*|OA OA OA PV|ID ID ID ID|  
|**SQLColumns**|*CatalogName* *SchemaName* *NomeTabella* *ColumnName*|OA PV PV PV|ID ID ID ID|  
|**SQLForeignKeys**|*PKCatalogName* *PKSchemaName* *PKTableName* *FKCatalogName* *FKSchemaName* *FKTableName*|OA OA OA OA OA OA|ID ID ID ID ID ID|  
|**SQLPrimaryKeys**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID ID ID|  
|**SQLProcedureColumns**|*CatalogName* *SchemaName* *ProcName* *ColumnName*|OA PV PV PV|ID ID ID ID|  
|**SQLProcedures**|*CatalogName* *SchemaName* *ProcName*|PV PV OA|ID ID ID|  
|**SQLSpecialColumns**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID ID ID|  
|**SQLStatistics**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID ID ID|  
|**SQLTablePrivileges**|*CatalogName* *SchemaName* *TableName*|PV PV OA|ID ID ID|  
|**SQLTables**|*CatalogName* *SchemaName* *NomeTabella* *TableType*|PV PV PV VL|ID ID ID VL|  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Argomenti ordinari](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [Argomenti del valore criterio](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [Argomenti di tipo identificatore](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [Argomenti dell'elenco di valori](../../../odbc/reference/develop-app/value-list-arguments.md)
