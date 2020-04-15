---
title: Argomenti nelle funzioni di catalogo Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 819c10d0b137d5e0999c1e10bf22810392509f76
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288167"
---
# <a name="arguments-in-catalog-functions"></a>Argomenti nelle funzioni di catalogo
Tutte le funzioni di catalogo accettano argomenti con cui un'applicazione può limitare l'ambito dei dati restituiti. Ad esempio, la prima e la seconda chiamata a **SQLTables** nel codice seguente restituiscono un set di risultati contenente informazioni su tutte le tabelle, mentre la terza chiamata restituisce informazioni sulla tabella Orders:  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 Gli argomenti della stringa della funzione catalogo rientrano in quattro tipi diversi: argomento ordinario (OA), argomento di valore modello (PV), argomento identificatore (ID) e argomento elenco valori (VL). La maggior parte degli argomenti stringa può essere di uno dei due tipi diversi, a seconda del valore dell'attributo di istruzione SQL_ATTR_METADATA_ID. Nella tabella seguente sono elencati gli argomenti per ogni funzione di catalogo e vengono descritti il tipo dell'argomento per un SQL_TRUE o SQL_FALSE valore di SQL_ATTR_METADATA_ID.  
  
|Funzione|Argomento|Digitare quando SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_FALSE|Digitare quando SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID (ID) SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*NomeCatalogName* *NomeSchemaNomeTabella* *NomeColonna* *ColumnName*|OA OA OA PV|ID ID ID ID|  
|**SQLColumns**|*NomeCatalogName* *NomeSchemaNomeTabella* *NomeColonna* *ColumnName*|OA PV PV PV|ID ID ID ID|  
|**SQLForeignKeys**|*PKCatalogName* *PKSchemaName* *PKTableName FKCatalogName* *FKCatalogName* *FKSchemaName* *NomeFKTableName*|OA OA OA OA OA OA|ID ID ID ID ID ID|  
|**SQLPrimaryKeys**|*NomeCatalogo* *NomeSchema* *NomeTabellaNomeTabella*|OA OA OA|ID ID ID|  
|**SQLProcedureColumns**|*NomeCatalogo* *NomeSchema ProcName* *ProcName* *NomeColonna*|OA PV PV PV|ID ID ID ID|  
|**SQLProcedures**|*NomeCatalogo* *NomeSchema* *NomeProc*|OA PV PV|ID ID ID|  
|**SQLSpecialColumns**|*NomeCatalogo* *NomeSchema* *NomeTabellaNomeTabella*|OA OA OA|ID ID ID|  
|**SQLStatistics**|*NomeCatalogo* *NomeSchema* *NomeTabellaNomeTabella*|OA OA OA|ID ID ID|  
|**SQLTablePrivileges**|*NomeCatalogo* *NomeSchema* *NomeTabellaNomeTabella*|OA PV PV|ID ID ID|  
|**SQLTables**|*NomeCatalogName* *NomeSchemaNomeTabella* *NomeTabellaTipo* *TableType*|PV PV PV VL|ID ID ID VL|  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Argomenti ordinari](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [Argomenti del valore dei criteri](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [Argomenti di tipo identificatore](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [Argomenti dell'elenco di valori](../../../odbc/reference/develop-app/value-list-arguments.md)
