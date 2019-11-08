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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 21565a3eb897c66175ce91a375bdb0b04b767d74
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73787470"
---
# <a name="sqlclosecursor"></a>SQLCloseCursor
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLCloseCursor** sostituisce [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) con il valore dell' *opzione* SQL_CLOSE. Alla ricezione di **SQLCloseCursor**, il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client elimina le righe del set di risultati in sospeso. Notare che le associazioni di parametro e colonna dell'istruzione, se presenti, non vengono modificate da **SQLCloseCursor**.  
  
## <a name="see-also"></a>Vedere anche  
   [SQLCloseCursor](https://go.microsoft.com/fwlink/?LinkId=59331)  
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
