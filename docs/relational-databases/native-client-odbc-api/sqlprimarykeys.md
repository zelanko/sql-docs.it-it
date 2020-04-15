---
title: Proprietà SQLPrimaryKeys . Documenti Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLPrimaryKeys function
ms.assetid: bc61cd5b-d2f4-4f87-abc7-743cf9ea772d
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2695d253030f13f71785046a25997ec6ee768622
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288983"
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Una tabella può avere una o più colonne che possono essere utilizzate come identificatori di riga univoci e le tabelle create senza un vincolo PRIMARY KEY restituiscono un set di risultati vuoto a SQLPrimaryKeys. La funzione ODBC [SQLSpecialColumns](../../relational-databases/native-client-odbc-api/sqlspecialcolumns.md) segnala i candidati identificatore di riga per le tabelle senza chiavi primarie.  
  
 SQLPrimaryKeys restituisce SQL_SUCCESS se esistono valori per i parametri *CatalogName*, *SchemaName*o *TableName* . SQLFetch restituisce SQL_NO_DATA quando in questi parametri vengono utilizzati valori non validi.  
  
 SQLPrimaryKeys può essere eseguito su un cursore statico del server. Un tentativo di eseguire SQLPrimaryKeys su un cursore aggiornabile (dinamico o keyset) restituirà SQL_SUCCESS_WITH_INFO che indica che il tipo di cursore è stato modificato.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client supporta le informazioni di report per le tabelle nei server collegati accettando un nome in due parti per il parametro *CatalogName:* *Linked_Server_Name.Catalog_Name*.  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys e parametri con valori di tabella  
 Se l'attributo SQL_SOPT_SS_NAME_SCOPE dell'istruzione ha il valore SQL_SS_NAME_SCOPE_TABLE_TYPE, anziché il valore predefinito di SQL_SS_NAME_SCOPE_TABLE, SQLPrimaryKeys restituirà informazioni sulle colonne di chiave primaria dei tipi di tabella. Per ulteriori informazioni sulle SQL_SOPT_SS_NAME_SCOPE, vedere [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Per ulteriori informazioni sui parametri con valori di tabella, vedere Parametri con valori di [tabella &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLPrimaryKeysSQLPrimaryKeys Function](https://go.microsoft.com/fwlink/?LinkId=59361)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
