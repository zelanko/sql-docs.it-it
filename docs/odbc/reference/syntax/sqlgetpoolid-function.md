---
title: Funzione SQLGetPoolID | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetPoolID function [ODBC]
ms.assetid: 95a8666a-ad68-4d89-bf65-f2cc797f8820
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7daef4785a77df294a831d69089108cbb1d88489
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061481"
---
# <a name="sqlgetpoolid-function"></a>Funzione SQLGetPoolID
**Conformità**  
 Versione introdotta: Conformità agli standard 3,81 ODBC: ODBC  
  
 **Riepilogo**  
 **SQLGetPoolID** recupera l'ID del pool.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp
  
SQLRETURN  SQLGetPoolID (  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                POOLID *              pPoolID );  
```  
  
## <a name="arguments"></a>Argomenti  
 *hDbcInfoToken*  
 [Input] Handle del token che contiene tutte le informazioni di connessione.  
  
 *pPoolID*  
 [Output] L'ID del pool, che viene usato per identificare un set di connessioni che possono essere usati indifferentemente (l'operazione può richiedere una reimpostazione aggiuntiva).  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetPoolID** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, gestione Driver userà una **HandleType** di SQL_HANDLE_DBC_INFO_TOKEN e un **gestire** del *hDbcInfoToken*.  
  
## <a name="remarks"></a>Note  
 **SQLGetPoolID** viene usato per ottenere l'ID del pool in base a un insieme di informazioni di connessione (da **SQLSetConnectAttrForDbcInfo**, **SQLSetDriverConnectInfo**, e  **SQLSetConnectInfo**). Questo pool di ID viene usato per identificare un set di connessioni che possono essere usati indifferentemente (l'operazione può richiedere una reimpostazione aggiuntiva). L'ID del pool da utilizzare per identificare il pool di connessioni per il gruppo di connessioni.  
  
 Ogni volta che un driver restituisce SQL_ERROR o SQL_INVALID_HANDLE, gestione Driver restituisce l'errore all'applicazione (in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) oppure [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Ottiene le informazioni di diagnostica da ogni volta che un driver restituisce SQL_SUCCESS_WITH_INFO, gestione Driver *hDbcInfoToken*e restituiscono SQL_SUCCESS_WITH_INFO all'applicazione in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Le applicazioni non devono chiamare direttamente questa funzione. Un driver ODBC che supporta il pool di connessioni compatibile con il driver deve implementare questa funzione.  
  
 Includere sqlspi.h per lo sviluppo di driver ODBC.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pool di connessioni compatibile con il driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Sviluppo del rilevamento di pool di connessioni in un driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
