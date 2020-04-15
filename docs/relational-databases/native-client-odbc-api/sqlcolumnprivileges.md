---
title: Proprietà SQLColumnPrivileges . Documenti Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLColumnPrivileges function
ms.assetid: c78acd4e-8668-4abc-9bc9-6ad381965863
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9e8197e0a9b105ea6236666a82624ecd97a80568
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302612"
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLColumnPrivileges** restituisce SQL_SUCCESS se esistono o meno valori per i parametri*CatalogName*, *SchemaName*, *TableName*o *ColumnName* . **SQLFetch** restituisce SQL_NO_DATA quando vengono utilizzati valori non validi in questi parametri.  
  
 **SQLColumnPrivileges** può essere eseguito su un cursore server statico. Un tentativo di eseguire **SQLColumnPrivileges** su un cursore aggiornabile (dinamico o keyset) restituirà SQL_SUCCESS_WITH_INFO che indica che il tipo di cursore è stato modificato.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client supporta le informazioni di report per le tabelle nei server collegati accettando un nome in due parti per il parametro *CatalogName:* *Linked_Server_Name.Catalog_Name*.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLColumnPrivilegesSQLColumnPrivileges Function](https://go.microsoft.com/fwlink/?LinkId=59335)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
