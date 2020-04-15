---
title: SqlCleanupConnectionPoolID (funzione) . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLCleanupConnectionPoolID function [ODBC]
ms.assetid: 1fc61908-e003-4587-b91a-32f40569fb99
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a74a92cc05ecd41e99ff87642c7fe3ee527e0c98
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301321"
---
# <a name="sqlcleanupconnectionpoolid-function"></a>Funzione SQLCleanupConnectionPoolID
**Conformità**  
 Versione introdotta: ODBC 3.81 Standards Compliance: ODBC  
  
 **Riepilogo**  
 **SQLCleanupConnectionPoolID** informa un driver che è stato stime di un ID pool. Un ID pool può sciare ogni volta che si scisse tutte le connessioni in un pool associate a tale ID. Per ulteriori informazioni sul timeout di connessione, vedere [Pooling in Microsoft Data Access Components.](https://msdn.microsoft.com/library/ms810829.aspx)  
  
## <a name="syntax"></a>Sintassi  
  
```cpp
  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>Argomenti  
 *EnvironmentHandle*  
 [Ingresso] Handle di ambiente del pool.  
  
 *IdPoolid*  
 [Ingresso] Pool associato all'ID del pool stimeout.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Gestione Driver non elaborerà le informazioni di diagnostica restituite da **SQLCleanupConnectionPoolID**.  
  
 Un'applicazione non può ricevere il messaggio di errore restituito dal driver.  
  
## <a name="remarks"></a>Osservazioni  
 **SQLCleanupConnectionPoolID** può essere chiamato in qualsiasi momento, ma Gestione Driver garantisce che nessun altro thread chiama contemporaneamente **SQLGetPoolID** e nessun altro thread chiama contemporaneamente **SQLRateConnection** e **SQLPoolConnect** con un token di informazioni di connessione assegnato con tale ID del pool. Pertanto, il driver deve assicurarsi che questa funzione è thread-safe.  
  
 Un driver può pulire le risorse associate all'ID pool.  
  
 Le applicazioni non devono chiamare direttamente questa funzione. Un driver ODBC che supporta il pool di connessioni in grado di riconoscere i driver deve implementare questa funzione.  
  
 Includere sqlspi.h per lo sviluppo di driver ODBC.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBCDeveloping an ODBC Driver](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pool di connessioni in grado di riconoscere i driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Sviluppo del rilevamento di pool di connessioni in un driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
