---
title: SQLTables | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLTables function
ms.assetid: 77b6c15c-9cf7-4019-b3f0-3d27d23ef656
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3a7ccecb3923dc46ebf8442e3c006ee88564749b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130976"
---
# <a name="sqltables"></a>SQLTables
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  SQLTables può essere eseguito su un cursore server statico. Un tentativo di eseguire SQLTables su un cursore aggiornabile (dinamico o keyset) restituirà SQL_SUCCESS_WITH_INFO che indica che il tipo di cursore è stato modificato.  
  
 SQLTables report delle tabelle da tutti i database quando le *CatalogName* parametro è SQL_ALL_CATALOGS e tutti gli altri parametri contengono valori predefiniti (puntatori NULL).  
  
 Per segnalare i cataloghi disponibili, schemi e tipi di tabella, SQLTables fa uso speciale delle stringhe vuote (puntatori byte di lunghezza zero). Le stringhe vuote non sono valori predefiniti (puntatori NULL).  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client supporta la segnalazione di informazioni relative alle tabelle sui server collegati mediante l'accettazione di un nome in due parti per il *CatalogName* parametro: *Linked_server_name*.  
  
 SQLTables restituisce informazioni riguardo a qualsiasi tabella il cui nome corrisponde a *TableName* e sono di proprietà dell'utente corrente.  
  
## <a name="sqltables-and-table-valued-parameters"></a>SQLTables e parametri con valori di tabella  
 Quando l'attributo dell'istruzione SQL_SOPT_SS_NAME_SCOPE è impostato sul valore SQL_SS_NAME_SCOPE_TABLE_TYPE, anziché il valore predefinito di SQL_SS_NAME_SCOPE_TABLE, SQLTables restituisce informazioni sui tipi di tabella. Il valore TABLE_TYPE restituito per un tipo di tabella nella colonna 4 del set di risultati restituito da SQLTables è tipo di tabella. Per altre informazioni su SQL_SOPT_SS_NAME_SCOPE, vedere [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Tabelle, viste e sinonimi condividono uno spazio dei nomi comune che è distinto dallo spazio dei nomi utilizzato dai tipi di tabella. Anche se non è possibile avere una tabella e una vista con lo stesso nome, è possibile avere una tabella e un tipo di tabella con lo stesso nome nello stesso catalogo e schema.  
  
 Per altre informazioni sui parametri con valori di tabella, vedere [parametri con valori di tabella &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="example"></a>Esempio  
  
```  
// Get a list of all tables in the current database.  
SQLTables(hstmt, NULL, 0, NULL, 0, NULL, 0, NULL,0);  
  
// Get a list of all tables in all databases.  
SQLTables(hstmt, (SQLCHAR*) "%", SQL_NTS, NULL, 0, NULL, 0, NULL,0);  
  
// Get a list of databases on the current connection's server.  
SQLTables(hstmt, (SQLCHAR*) "%", SQL_NTS, (SQLCHAR*)"", 0, (SQLCHAR*)"",  
    0, NULL, 0);  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLTables](https://go.microsoft.com/fwlink/?LinkId=59374)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
