---
title: Funzione SQLSetConnectInfo . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectInfo function [ODBC]
ms.assetid: 0782a1c3-c5d1-499b-a8ba-134162db9990
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b575e0d09f87ad21e1190b8081b6604349a98263
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301852"
---
# <a name="sqlsetconnectinfo-function"></a>Funzione SQLSetConnectInfo
**Conformità**  
 Versione introdotta: ODBC 3.81 Standards Compliance: ODBC  
  
 **Riepilogo**  
 **SQLSetConnectInfo** viene utilizzato per impostare l'origine dati, l'ID utente e la password nel token di informazioni di connessione per la chiamata [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) di un'applicazione.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp
  
SQLRETURN  SQLSetConnectInfo(  
                SQLHDBC_INFO_TOKEN   TokenHandle,  
                WCHAR *              ServerName,  
                SQLSMALLINT          NameLength1,  
                WCHAR *              UserName,  
                SQLSMALLINT          NameLength2,  
                WCHAR *              Authentication,  
                SQLSMALLINT          NameLength3 );  
```  
  
## <a name="arguments"></a>Argomenti  
 *TokenHandle*  
 [Ingresso] Handle di token.  
  
 *ServerName*  
 [Ingresso] Nome dell'origine dati. I dati potrebbero trovarsi sullo stesso computer del programma o su un altro computer da qualche parte in una rete. Per informazioni sulla scelta di un'origine dati da parte di un'applicazione, vedere [Scelta di un'origine dati o](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)di un driver .  
  
 *NameLength1*  
 [Ingresso] Lunghezza di :*NomeServer* in caratteri.  
  
 *Nome utente*  
 [Ingresso] Identificatore utente.  
  
 *NameLength2*  
 [Ingresso] Lunghezza di :*UserName* in caratteri.  
  
 *autenticazione*  
 [Ingresso] Stringa di autenticazione (in genere la password).  
  
 *NameLength3*  
 [Ingresso] Lunghezza*dell'autenticazione* in caratteri.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Uguale a [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) per gli errori di convalida dell'input, ad eccezione del fatto che Gestione Driver utilizzerà un **HandleType** di SQL_HANDLE_DBC_INFO_TOKEN e un **handle** di *hDbcInfoToken*.  
  
## <a name="remarks"></a>Osservazioni  
 Ogni volta che un driver restituisce SQL_ERROR o SQL_INVALID_HANDLE, Gestione Driver restituisce l'errore all'applicazione (in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Ogni volta che un driver restituisce SQL_SUCCESS_WITH_INFO, Gestione Driver otterrà le informazioni di diagnostica da *hDbcInfoToken*e restituirà SQL_SUCCESS_WITH_INFO all'applicazione in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Le applicazioni non devono chiamare direttamente questa funzione. Un driver ODBC che supporta il pool di connessioni in grado di riconoscere i driver deve implementare questa funzione.  
  
 Includere sqlspi.h per lo sviluppo di driver ODBC.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBCDeveloping an ODBC Driver](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pool di connessioni in grado di riconoscere i driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Sviluppo del rilevamento di pool di connessioni in un driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
