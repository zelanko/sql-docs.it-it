---
description: SQLFreeHandle
title: SQLFreeHandle | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFreeHandle function
ms.assetid: d374e5c8-ed35-43bf-8dd6-c37e38d9b5f1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7453cd40119f161e31c24394663a00206ed29aa2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465202"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  In modalità di commit manuale, la chiamata di **SQLFreeHandle** su un handle di istruzione con una transazione aperta causa un rollback delle modifiche in sospeso al database. La chiamata di **SQLFreeHandle** su un handle di istruzione chiude sempre tutti i cursori aperti e ignora i risultati in sospeso, liberando tutte le risorse associate all'handle di istruzione.  
  
## <a name="see-also"></a>Vedere anche  
 [SQLFreeHandle (funzione)](../../odbc/reference/syntax/sqlfreehandle-function.md)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
