---
title: SQLCancel | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2db2c4b66940a81dd65064ee730cd683e2206a58
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302643"
---
# <a name="sqlcancel"></a>SQLCancel
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Nell' [argomento SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516) si afferma che in ODBC 2. x, se un'applicazione **chiama SQLCancel** quando non viene eseguita alcuna elaborazione sull'istruzione, **SQLCancel** ha lo stesso effetto di **SQLFreeStmt** con l'opzione **SQL_CLOSE** ; Questo comportamento viene definito solo per completezza e le applicazioni devono chiamare **SQLFreeStmt** o **SQLCloseCursor** per chiudere i cursori. Tuttavia, anche se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'applicazione client nativa imposta la versione dell'API ODBC su 3.5. x o versioni successive, la funzione **SQLCancel** utilizzerà il comportamento ODBC 2. x.  
  
## <a name="see-also"></a>Vedere anche  
 [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
