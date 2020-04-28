---
title: SQLCloseCursor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLCloseCursor function
ms.assetid: e7134d65-5c1c-4ae2-b119-d9b4b9a42483
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fb20bfa7ca76b8156ef2400e6db3235c590680ba
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302629"
---
# <a name="sqlclosecursor"></a>SQLCloseCursor
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLCloseCursor** sostituisce [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) con il valore dell' *opzione* SQL_CLOSE. Alla ricezione di **SQLCloseCursor**, il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client elimina le righe del set di risultati in sospeso. Notare che le associazioni di parametro e colonna dell'istruzione, se presenti, non vengono modificate da **SQLCloseCursor**.  
  
## <a name="see-also"></a>Vedere anche  
 [SQLCloseCursor](https://go.microsoft.com/fwlink/?LinkId=59331)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
