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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68061481"
---
# <a name="sqlgetpoolid-function"></a>Funzione SQLGetPoolID
**Conformità**  
 Versione introdotta: ODBC 3,81 Standard Compliance: ODBC  
  
 **Summary**  
 **SQLGetPoolID** recupera l'ID del pool.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp
  
SQLRETURN  SQLGetPoolID (  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                POOLID *              pPoolID );  
```  
  
## <a name="arguments"></a>Argomenti  
 *hDbcInfoToken*  
 Input Handle di token che contiene tutte le informazioni di connessione.  
  
 *pPoolID*  
 Output ID del pool, usato per identificare un set di connessioni che possono essere usate in modo intercambiabile (eventualmente richiedendo una reimpostazione aggiuntiva).  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetPoolID** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, gestione driver utilizzerà un **HandleType** di SQL_HANDLE_DBC_INFO_TOKEN e un **handle** di *hDbcInfoToken*.  
  
## <a name="remarks"></a>Osservazioni  
 **SQLGetPoolID** viene usato per ottenere l'ID del pool in base a un set di informazioni di connessione (da **SQLSetConnectAttrForDbcInfo**, **SQLSetDriverConnectInfo**e **SQLSetConnectInfo**). Questo ID del pool viene usato per identificare un set di connessioni che possono essere usate in modo interscambiabile (probabilmente richiedendo una reimpostazione aggiuntiva). L'ID del pool verrà usato per identificare il pool di connessioni per il gruppo di connessioni.  
  
 Ogni volta che un driver restituisce SQL_ERROR o SQL_INVALID_HANDLE, gestione driver restituisce l'errore all'applicazione (in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Ogni volta che un driver restituisce SQL_SUCCESS_WITH_INFO, gestione driver otterrà le informazioni di diagnostica da *hDbcInfoToken*e restituirà SQL_SUCCESS_WITH_INFO all'applicazione in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Le applicazioni non devono chiamare direttamente questa funzione. Un driver ODBC che supporta il pool di connessioni compatibile con il driver deve implementare questa funzione.  
  
 Includere sqlspi. h per lo sviluppo di driver ODBC.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pool di connessioni compatibile con il driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Sviluppo del rilevamento di pool di connessioni in un driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
