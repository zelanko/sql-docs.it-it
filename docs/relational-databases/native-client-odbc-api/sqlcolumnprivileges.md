---
title: SQLColumnPrivileges | Microsoft Docs
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
ms.openlocfilehash: 1d6d66d01c33d6fefdb9637a8c535462ea00a641
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86006654"
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  **SQLColumnPrivileges** restituisce SQL_SUCCESS se sono presenti o meno valori per i parametri*CatalogName*, *SchemaName*, *TableName*o *ColumnName* . **SQLFetch** restituisce SQL_NO_DATA quando in questi parametri vengono utilizzati valori non validi.  
  
 **SQLColumnPrivileges** può essere eseguito su un cursore del server statico. Il tentativo di eseguire **SQLColumnPrivileges** su un cursore aggiornabile (dinamico o keyset) restituirà SQL_SUCCESS_WITH_INFO indicante che il tipo di cursore è stato modificato.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client supporta la segnalazione di informazioni per le tabelle nei server collegati accettando un nome in due parti per il parametro *CatalogName* : *linked_server_name. catalog_name*.  
  
## <a name="see-also"></a>Vedere anche  
 [SQLColumnPrivileges (funzione)](https://go.microsoft.com/fwlink/?LinkId=59335)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
