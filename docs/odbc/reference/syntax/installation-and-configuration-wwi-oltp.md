---
title: Funzione SQLSetDriverConnectInfo | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c344315764eac32e2e63663f07b7f797571a0e6
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53204690"
---
# <a name="sqlsetdriverconnectinfo-function"></a>Funzione SQLSetDriverConnectInfo
**Conformità**  
 Versione introdotta: Conformità agli standard 3,81 ODBC: ODBC  
  
 **Riepilogo**  
 **SQLSetDriverConnectInfo** consente di impostare la stringa di connessione in token le informazioni di connessione per un'applicazione **SQLDriverConnect** chiamare.  
  
## <a name="syntax"></a>Sintassi  
  
```  
SQLRETURN SQLSetDriverConnectInfo(  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              InConnectionString,  
                SQLSMALLINT          StringLength1 );  
```  
  
## <a name="arguments"></a>Argomenti  
 *TokenHandle*  
 [Input] Handle del token.  
  
 *InConnectionString*  
 [Input] Una stringa di connessione completa (vedere la sintassi "Commenti" nella [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)), una stringa di connessione parziale o una stringa vuota.  
  
 *StringLength1*  
 [Input] Lunghezza di **InConnectionString*, in caratteri se la stringa è Unicode, o byte se stringa ANSI o DBCS.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Uguale allo [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) correlati a qualsiasi errore di convalida dell'input, ad eccezione del fatto che verrà utilizzato Gestione Driver una **HandleType** di SQL_HANDLE_DBC_INFO_TOKEN e un **gestire** di *hDbcInfoToken*.  
  
## <a name="remarks"></a>Note  
 Ogni volta che un driver restituisce SQL_ERROR o SQL_INVALID_HANDLE, gestione Driver restituisce l'errore all'applicazione (in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) oppure [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Ottiene le informazioni di diagnostica da ogni volta che un driver restituisce SQL_SUCCESS_WITH_INFO, gestione Driver *hDbcInfoToken*e restituiscono SQL_SUCCESS_WITH_INFO all'applicazione in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Le applicazioni non devono chiamare direttamente questa funzione. Un driver ODBC che supporta il pool di connessioni compatibile con il driver deve implementare questa funzione.  
  
 Includere sqlspi.h per lo sviluppo di driver ODBC.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pool di connessioni compatibile con il driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Sviluppo del rilevamento di pool di connessioni in un driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
