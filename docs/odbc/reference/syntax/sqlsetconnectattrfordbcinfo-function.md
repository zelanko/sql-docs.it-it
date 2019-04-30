---
title: Funzione SQLSetConnectAttrForDbcInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectAttrForDbcInfo function [ODBC]
ms.assetid: a28fadb9-b998-472a-b252-709507e92005
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 798f986adfeda95ef091161458d94c2ccc33b2e3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63125531"
---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>Funzione SQLSetConnectAttrForDbcInfo
**Conformità**  
 Versione introdotta: Conformità agli standard 3,81 ODBC: ODBC  
  
 **Riepilogo**  
 **SQLSetConnectAttrForDbcInfo** equivale a **SQLSetConnectAttr**, ma l'attributo viene impostato sul token di informazioni di connessione invece che nell'handle di connessione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
SQLRETURN  SQLSetConnectAttrForDbcInfo(  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                SQLINTEGER            Attribute,  
                SQLPOINTER            ValuePtr,  
                SQLINTEGER            StringLength );  
```  
  
## <a name="arguments"></a>Argomenti  
 *hDbcInfoToken*  
 [Input] Handle del token.  
  
 *Attribute*  
 [Input] Attributo da impostare. L'elenco degli attributi validi è specifici del driver e gli stessi del [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 *ValuePtr*  
 [Input] Puntatore al valore da associare *attributo*. A seconda del valore di *attributo*, *ValuePtr* sarà un valore intero senza segno a 32 bit o punterà a una stringa di caratteri con terminazione null. Si noti che se il *attributo* argomento è un valore specifico del driver, il valore nella *ValuePtr* potrebbe essere un intero con segno.  
  
 *StringLength*  
 [Input] Se *attributo* è un attributo definito da ODBC e *ValuePtr* punta a una stringa di caratteri o binario buffer, questo argomento deve essere la lunghezza di **ValuePtr*. Per i dati di stringa di caratteri, questo argomento deve contenere il numero di byte nella stringa.  
  
 Se *attributo* è un attributo definito da ODBC e *ValuePtr* è un intero *StringLength* viene ignorato.  
  
 Se *attributo* è un attributo definito dal driver, l'applicazione indica la natura dell'attributo da Gestione Driver impostando il *StringLength* argomento. *StringLength* può avere i valori seguenti:  
  
-   Se *ValuePtr* è un puntatore a una stringa di caratteri, quindi *StringLength* è la lunghezza della stringa o SQL_NTS.  
  
-   Se *ValuePtr* è un puntatore a un buffer binario, quindi l'applicazione inserisce il risultato del SQL_LEN_BINARY_ATTR (*lunghezza*) (macro) in *StringLength*. Un valore negativo in questo modo vengono inserite *StringLength*.  
  
-   Se *ValuePtr* è un puntatore a un valore diverso da una stringa di caratteri o stringa binaria, quindi *StringLength* deve avere il valore SQL_IS_POINTER.  
  
-   Se *ValuePtr* contiene un valore di lunghezza fissa, quindi *StringLength* è SQL_IS_INTEGER o SQL_IS_UINTEGER, come appropriato.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Uguale allo [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), ad eccezione del fatto che la gestione di Driver utilizzerà un **HandleType** di SQL_HANDLE_DBC_INFO_TOKEN e un **gestire** di *hDbcInfoToken* .  
  
## <a name="remarks"></a>Note  
 **SQLSetConnectAttrForDbcInfo** equivale a **SQLSetConnectAttr**, tuttavia, imposta l'attributo nel token di informazioni di connessione, anziché nell'handle di connessione. Ad esempio, se **SQLSetConnectAttr** non riconosce un attributo **SQLSetConnectAttrForDbcInfo** deve restituire anche SQL_ERROR per quell'attributo.  
  
 Ogni volta che i driver restituisce SQL_ERROR o SQL_INVALID_HANDLE, il driver deve ignorare questo attributo per calcolare l'ID del pool. Inoltre, gestione Driver otterrà le informazioni di diagnostica dal *hDbcInfoToken*e restituiscono SQL_SUCCESS_WITH_INFO all'applicazione nel [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md). Pertanto, un'applicazione può recuperare informazioni dettagliate sui motivi per cui non è possibile impostare alcuni attributi.  
  
 Le applicazioni non devono chiamare direttamente questa funzione. Un driver ODBC che supporta il pool di connessioni compatibile con il driver deve implementare questa funzione.  
  
 Includere sqlspi.h per lo sviluppo di driver ODBC.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pool di connessioni compatibile con il driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Sviluppo del rilevamento di pool di connessioni in un driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
