---
title: SQLTablePrivileges | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLTablePrivileges function
ms.assetid: 8cce22d5-28b1-4b50-a5bc-1de03e0ffd6b
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a295df72be56343cdca65591a147adf173b36059
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73785585"
---
# <a name="sqltableprivileges"></a>SQLTablePrivileges
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLTablePrivileges** può essere eseguito su un cursore statico. Un tentativo di eseguire **SQLTablePrivileges** su un oggetto aggiornabile (gestito da keyset o dinamico) restituisce SQL_SUCCESS_WITH_INFO indicante che il tipo di cursore è stato modificato.  
  
 Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client supporta la segnalazione di informazioni per le tabelle nei server collegati accettando un nome in due parti per il parametro *CatalogName* : *linked_server_name. catalog_name*.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLTablePrivileges] (https://go.microsoft.com/fwlink/?LinkId=59373\)   
 [Dettagli di implementazione dell'API ODBC](~/relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
