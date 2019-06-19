---
title: Funzione SQLSetConnectInfo | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 448b0f5e34a6b7421c23a1267dd9cd68bd93ca6f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537174"
---
# <a name="sqlsetconnectinfo-function"></a>Funzione SQLSetConnectInfo
**Conformità**  
 Versione introdotta: Conformità agli standard 3,81 ODBC: ODBC  
  
 **Riepilogo**  
 **SQLSetConnectInfo** utilizzato per impostare l'origine dati, l'ID utente e password in token le informazioni di connessione per un'applicazione [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) chiamare.  
  
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
 [Input] Handle del token.  
  
 *ServerName*  
 [Input] Nome dell'origine dati. I dati potrebbero trovarsi nello stesso computer del programma, o in un altro computer in una posizione in una rete. Per informazioni sulla modalità con cui un'applicazione sceglie un'origine dati, vedere [scelta di un'origine dati o Driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 *NameLength1*  
 [Input] Lunghezza di **ServerName* in caratteri.  
  
 *UserName*  
 [Input] Identificatore dell'utente.  
  
 *NameLength2*  
 [Input] Lunghezza di **UserName* in caratteri.  
  
 *Autenticazione*  
 [Input] Stringa di autenticazione (in genere la password).  
  
 *NameLength3*  
 [Input] Lunghezza di **autenticazione* in caratteri.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Uguale allo [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) per input errori di convalida, ad eccezione del fatto che la gestione di Driver utilizzerà un **HandleType** di SQL_HANDLE_DBC_INFO_TOKEN e un **gestire** di *hDbcInfoToken*.  
  
## <a name="remarks"></a>Note  
 Ogni volta che un driver restituisce SQL_ERROR o SQL_INVALID_HANDLE, gestione Driver restituisce l'errore all'applicazione (in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) oppure [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Ottiene le informazioni di diagnostica da ogni volta che un driver restituisce SQL_SUCCESS_WITH_INFO, gestione Driver *hDbcInfoToken*e restituiscono SQL_SUCCESS_WITH_INFO all'applicazione in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Le applicazioni non devono chiamare direttamente questa funzione. Un driver ODBC che supporta il pool di connessioni compatibile con il driver deve implementare questa funzione.  
  
 Includere sqlspi.h per lo sviluppo di driver ODBC.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pool di connessioni compatibile con il driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Sviluppo del rilevamento di pool di connessioni in un driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
