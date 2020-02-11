---
title: Argomenti nelle funzioni di catalogo | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68106290"
---
# <a name="arguments-in-catalog-functions"></a>Argomenti nelle funzioni di catalogo
Tutte le funzioni di catalogo accettano argomenti con cui un'applicazione può limitare l'ambito dei dati restituiti. La prima e la seconda chiamata a **SQLTables** nel codice seguente, ad esempio, restituiscono un set di risultati contenente informazioni su tutte le tabelle, mentre la terza chiamata restituisce informazioni sulla tabella Orders:  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 Gli argomenti di stringa della funzione di catalogo rientrano in quattro tipi diversi: argomento ordinario (OA), argomento valore pattern (PV), argomento identificatore (ID) e argomento elenco valore (VL). La maggior parte degli argomenti stringa può essere di uno dei due tipi diversi, a seconda del valore dell'attributo dell'istruzione SQL_ATTR_METADATA_ID. Nella tabella seguente sono elencati gli argomenti per ogni funzione di catalogo e viene descritto il tipo di argomento per un SQL_TRUE o SQL_FALSE valore di SQL_ATTR_METADATA_ID.  
  
|Funzione|Argomento|Digitare quando SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_FALSE|Digitare quando SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*CatalogName* *SchemaName* *TableName TableName* **|OA OA PV|ID ID ID|  
|**SQLColumns**|*CatalogName* *SchemaName* *TableName TableName* **|PV PV PV PV|ID ID ID|  
|**SQLForeignKeys**|*PKCatalogName* *PKSchemaName* *PKTableName* *FKCatalogName* *FKSchemaName* *FKTableName*|OA OA OA OA OA OA|ID ID ID ID ID|  
|**SQLPrimaryKeys**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID ID ID|  
|**SQLProcedureColumns**|*CatalogName* *SchemaName* *ProcName* *ColumnName*|PV PV PV PV|ID ID ID|  
|**SQLProcedures**|*CatalogName* *SchemaName* *ProcName*|PV PV PV|ID ID ID|  
|**SQLSpecialColumns**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID ID ID|  
|**SQLStatistics**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID ID ID|  
|**SQLTablePrivileges**|*CatalogName* *SchemaName* *TableName*|PV PV PV|ID ID ID|  
|**SQLTables**|*CatalogName* *SchemaName* *TableName* *TableType*|PV PV PV VL|ID ID VL|  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Argomenti ordinari](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [Argomenti del valore dei criteri](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [Argomenti di tipo identificatore](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [Argomenti dell'elenco di valori](../../../odbc/reference/develop-app/value-list-arguments.md)
