---
description: Rilascio di un handle di istruzione
title: Liberazione di un handle di istruzione | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- reusing statement handles
- freeing statement handles
- statements [ODBC], statement handles
- SQLFreeStmt function
- ODBC applications, statements
- statement handles [ODBC]
ms.assetid: 96fdff84-0ca7-460a-a240-94ee826ea41c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0588ee69620ece2de4bea80f1adb7de3288267d3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478092"
---
# <a name="freeing-a-statement-handle"></a>Rilascio di un handle di istruzione
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  È più efficiente riutilizzare handle di istruzione anziché eliminarli e allocarne di nuovi. Prima di eseguire una nuova istruzione SQL su un handle di istruzione, le applicazioni devono verificare che le impostazioni delle istruzioni correnti siano corrette. Tra le impostazioni sono inclusi gli attributi di istruzione, le associazioni di parametri e le associazioni dei set di risultati. In genere, i parametri e i set di risultati per l'istruzione SQL precedente devono essere non associati chiamando [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) con le opzioni SQL_RESET_PARAMS e SQL_UNBIND e quindi riassociati per la nuova istruzione SQL.  
  
 Al termine dell'utilizzo dell'istruzione, l'applicazione chiama [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) per liberare l'istruzione. Si noti che **Disconnect** libera automaticamente tutte le istruzioni in una connessione.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di query &#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
