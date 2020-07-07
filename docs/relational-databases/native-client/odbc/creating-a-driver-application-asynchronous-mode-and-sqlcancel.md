---
title: Modalità asincrona e SQLCancel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- asynchronous operations [SQL Server Native Client]
- SQLCancel function
- SQLSetConnectAttr function
- SQL Server Native Client, asynchronous operations
- ODBC functions
- ODBC applications, asynchronous operations
- SQL Server Native Client ODBC driver, asynchronous mode
ms.assetid: f31702a2-df76-4589-ac3b-da5412c03dc2
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a76901e1b3c5e4074e9c8257029f19ed156a3fd1
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009796"
---
# <a name="creating-a-driver-application---asynchronous-mode-and-sqlcancel"></a>Creazione di un'applicazione driver - Modalità asincrona e SQLCancel
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Alcune funzioni ODBC possono essere utilizzate in modo sincrono o in modo asincrono. Le operazioni asincrone possono essere abilitate per un handle di istruzione o per un handle di connessione. Se l'opzione viene impostata per un handle di connessione, sarà valida per tutti gli handle di istruzione nell'handle di connessione. Per abilitare o disabilitare le operazioni asincrone vengono utilizzate le istruzioni seguenti:  
  
```  
SQLSetConnectAttr(hdbc, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
SQLSetConnectAttr(hdbc, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_OFF, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_OFF, SQL_IS_INTEGER);  
```  
  
 Quando una funzione ODBC viene chiamata in modalità sincrona, il driver restituisce il controllo all'applicazione solo dopo la notifica del completamento del comando da parte del server.  
  
 In modalità asincrona, il driver restituisce immediatamente il controllo all'applicazione, anche prima dell'invio del comando al server. Il driver imposta il codice restituito su SQL_STILL_EXECUTING. È quindi possibile eseguire altre operazioni.  
  
 Durante il controllo del completamento del comando, viene effettuata la stessa chiamata di funzione con gli stessi parametri al driver. Se il driver non riceve una risposta dal server, restituirà nuovamente SQL_STILL_EXECUTING. È necessario controllare periodicamente il comando finché il codice restituito non sia diverso da SQL_STILL_EXECUTING. Quando si ottiene un codice restituito diverso, anche SQL_ERROR, è possibile determinare che il comando è stato completato.  
  
 A volte un comando rimane in attesa per molto tempo. Se l'applicazione deve annullare il comando senza attendere una risposta, è possibile eseguire questa operazione chiamando **SQLCancel** con lo stesso handle di istruzione del comando in attesa. Questa è l'unica volta in cui deve essere utilizzato **SQLCancel** . Alcuni programmatori utilizzano **SQLCancel** quando elaborano in modo parziale un set di risultati e desiderano annullare il resto del set di risultati. È necessario utilizzare [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) o [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) per annullare il resto di un set di risultati in attesa, non **SQLCancel**.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un'applicazione driver ODBC di SQL Server Native Client](../../../relational-databases/native-client/odbc/creating-a-driver-application.md)  
  
  
