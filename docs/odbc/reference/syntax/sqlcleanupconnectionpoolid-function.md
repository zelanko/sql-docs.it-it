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
ms.openlocfilehash: ee8f9b9879a3533e8196bbc89f8ae0b0a132293a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036091"
---
# <a name="sqlcleanupconnectionpoolid-function"></a>Funzione SQLCleanupConnectionPoolID
**Conformità**  
 Versione introdotta: ODBC 3,81 Standard Compliance: ODBC  
  
 **Summary**  
 **SQLCleanupConnectionPoolID** informa un driver che è stato raggiunto il timeout di un ID pool. Un ID pool può scadere ogni volta che si verifica il timeout di tutte le connessioni in un pool associato a tale ID pool. Per ulteriori informazioni sul timeout della connessione, vedere [pooling in Microsoft Data Access Components](https://msdn.microsoft.com/library/ms810829.aspx) .  
  
## <a name="syntax"></a>Sintassi  
  
```cpp
  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>Argomenti  
 *EnvironmentHandle*  
 Input Handle di ambiente del pool.  
  
 *PoolID*  
 Input Pool associato all'ID del pool scaduto.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Gestione driver non elaborerà le informazioni di diagnostica restituite da **SQLCleanupConnectionPoolID**.  
  
 Un'applicazione non può ricevere il messaggio di errore restituito dal driver.  
  
## <a name="remarks"></a>Osservazioni  
 **SQLCleanupConnectionPoolID** può essere chiamato in qualsiasi momento, ma gestione driver garantisce che nessun altro thread chiama contemporaneamente **SQLGetPoolID** e nessun altro thread chiama contemporaneamente **SQLRateConnection** e **SQLPoolConnect** con un token di informazioni di connessione assegnato a tale ID. Pertanto, è necessario che il driver assicuri che questa funzione sia thread-safe.  
  
 Un driver è in grado di pulire le risorse associate all'ID del pool.  
  
 Le applicazioni non devono chiamare direttamente questa funzione. Un driver ODBC che supporta il pool di connessioni compatibile con il driver deve implementare questa funzione.  
  
 Includere sqlspi. h per lo sviluppo di driver ODBC.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pool di connessioni compatibile con il driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Sviluppo del rilevamento di pool di connessioni in un driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
