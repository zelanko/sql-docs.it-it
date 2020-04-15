---
title: Funzione SQLSetDriverConnectInfo . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetDriverConnectInfo function [ODBC]
ms.assetid: bfd4dfc2-fbca-4ef3-81e5-2706f2389256
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 10336475e39598161126c13771ad822de0d5f7d8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298801"
---
# <a name="sqlsetdriverconnectinfo-function"></a>Funzione SQLSetDriverConnectInfo
**Conformità**  
 Versione introdotta: ODBC 3.81 Standards Compliance: ODBC  
  
 **Riepilogo**  
 **SQLSetDriverConnectInfo** viene utilizzato per impostare la stringa di connessione nel token di informazioni di connessione per la chiamata **SQLDriverConnect** di un'applicazione.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp
  
SQLRETURN SQLSetDriverConnectInfo(  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              InConnectionString,  
                SQLSMALLINT          StringLength1 );  
```  
  
## <a name="arguments"></a>Argomenti  
 *TokenHandle*  
 [Ingresso] Handle di token.  
  
 *InConnectionStringInConnectionString (Informazioni in stringa)*  
 [Ingresso] Stringa di connessione completa (vedere la sintassi in "Commenti" in [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)), una stringa di connessione parziale o una stringa vuota.  
  
 *LunghezzaStringa1*  
 [Ingresso] Lunghezza di ,*InConnectionString*, in caratteri se la stringa è Unicode o byte se string è ANSI o DBCS.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Uguale a [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) correlato a qualsiasi errore di convalida dell'input, ad eccezione del fatto che Gestione Driver utilizzerà un **HandleType** di SQL_HANDLE_DBC_INFO_TOKEN e un **handle** di *hDbcInfoToken*.  
  
## <a name="remarks"></a>Osservazioni  
 Ogni volta che un driver restituisce SQL_ERROR o SQL_INVALID_HANDLE, Gestione Driver restituisce l'errore all'applicazione (in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Ogni volta che un driver restituisce SQL_SUCCESS_WITH_INFO, Gestione Driver otterrà le informazioni di diagnostica da *hDbcInfoToken*e restituirà SQL_SUCCESS_WITH_INFO all'applicazione in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Le applicazioni non devono chiamare direttamente questa funzione. Un driver ODBC che supporta il pool di connessioni in grado di riconoscere i driver deve implementare questa funzione.  
  
 Includere sqlspi.h per lo sviluppo di driver ODBC.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBCDeveloping an ODBC Driver](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pool di connessioni in grado di riconoscere i driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Sviluppo del rilevamento di pool di connessioni in un driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
