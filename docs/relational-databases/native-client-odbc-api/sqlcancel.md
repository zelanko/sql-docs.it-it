---
title: SQLCancel | Documenti di Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5eb5f86d73166976e18b10f5bcf8e319ebfe18ea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132005"
---
# <a name="sqlcancel"></a>SQLCancel
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Il [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516) argomento afferma che in ODBC 2.x, se un'applicazione chiama **SQLCancel** quando non si è fatta alcuna elaborazione nell'istruzione **SQLCancel** ha lo stesso effetto  **SQLFreeStmt** con il **SQL_CLOSE** opzione; questo comportamento viene definito solo per motivi di completezza e le applicazioni devono chiamare **SQLFreeStmt** o  **SQLCloseCursor** per chiudere i cursori. Ma anche se il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] applicazioni Native Client imposta la versione dell'API ODBC da 3.5 o versione successiva, il **SQLCancel** funzione utilizzerà il comportamento ODBC 2. x.  
  
## <a name="see-also"></a>Vedere anche  
 [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
