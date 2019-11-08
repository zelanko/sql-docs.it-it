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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a5356d408a5116f6ab2cd6ae6e0e16d2dc7c26df
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73787480"
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLColumnPrivileges** restituisce SQL_SUCCESS se sono presenti o meno valori per i parametri*CatalogName*, *SchemaName*, *TableName*o *ColumnName* . **SQLFetch** restituisce SQL_NO_DATA quando in questi parametri vengono utilizzati valori non validi.  
  
 **SQLColumnPrivileges** può essere eseguito su un cursore del server statico. Il tentativo di eseguire **SQLColumnPrivileges** su un cursore aggiornabile (dinamico o keyset) restituirà SQL_SUCCESS_WITH_INFO indicante che il tipo di cursore è stato modificato.  
  
 Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client supporta la segnalazione di informazioni per le tabelle nei server collegati accettando un nome in due parti per il parametro *CatalogName* : *linked_server_name. catalog_name*.  
  
## <a name="see-also"></a>Vedere anche  
   [funzione SQLColumnPrivileges](https://go.microsoft.com/fwlink/?LinkId=59335)  
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
