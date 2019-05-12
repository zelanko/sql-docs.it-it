---
title: Funzione SQLCleanupConnectionPoolID | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c4d00fcff0b2fa1948f6b2f6f66b863501e12d97
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537702"
---
# <a name="sqlcleanupconnectionpoolid-function"></a>Funzione SQLCleanupConnectionPoolID
**Conformità**  
 Versione introdotta: Conformità agli standard 3,81 ODBC: ODBC  
  
 **Riepilogo**  
 **SQLCleanupConnectionPoolID** informa un driver che è stato verificato il timeout di un ID del pool. Timeout di un pool di ID possibile timeout ogni volta che sono state tutte le connessioni in un pool associato a tale ID del pool. Visualizzare [limitazione delle richieste in Microsoft Data Access Components](https://msdn.microsoft.com/library/ms810829.aspx) per altre informazioni sul timeout di connessione.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp
  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>Argomenti  
 *EnvironmentHandle*  
 [Input] L'handle di ambiente del pool.  
  
 *PoolID*  
 [Input] Il pool associato all'ID del pool che è stato verificato il timeout.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Gestione Driver non elaborerà le informazioni di diagnostica restituite da **SQLCleanupConnectionPoolID**.  
  
 Un'applicazione non può ricevere il messaggio di errore restituito dal driver.  
  
## <a name="remarks"></a>Note  
 **SQLCleanupConnectionPoolID** può essere chiamato in qualsiasi momento, ma la gestione di Driver garantisce che nessun altro thread consiste nel chiamare contemporaneamente **SQLGetPoolID** e nessun altro thread consiste nel chiamare contemporaneamente  **SQLRateConnection** e **SQLPoolConnect** con un token di informazioni di connessione assegnato con tale ID del pool. Pertanto, il driver deve assicurarsi che questa funzione è thread-safe.  
  
 Un driver possibile pulire le risorse associate con l'ID del pool.  
  
 Le applicazioni non devono chiamare direttamente questa funzione. Un driver ODBC che supporta il pool di connessioni compatibile con il driver deve implementare questa funzione.  
  
 Includere sqlspi.h per lo sviluppo di driver ODBC.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pool di connessioni compatibile con il driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Sviluppo del rilevamento di pool di connessioni in un driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
