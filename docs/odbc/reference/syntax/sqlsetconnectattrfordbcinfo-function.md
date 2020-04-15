---
title: SqlSetConnectAttrForDbcInfo (funzione) Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9f43a0fc6cd02fe566579a543667f9a4c4c1a108
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301888"
---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>Funzione SQLSetConnectAttrForDbcInfo
**Conformità**  
 Versione introdotta: ODBC 3.81 Standards Compliance: ODBC  
  
 **Riepilogo**  
 **SQLSetConnectAttrForDbcInfo** è uguale a **SQLSetConnectAttr**, ma imposta l'attributo sul token di informazioni di connessione anziché sull'handle di connessione.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp
  
SQLRETURN  SQLSetConnectAttrForDbcInfo(  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                SQLINTEGER            Attribute,  
                SQLPOINTER            ValuePtr,  
                SQLINTEGER            StringLength );  
```  
  
## <a name="arguments"></a>Argomenti  
 *hDbcInfoToken (informazioni in due)*  
 [Ingresso] Handle di token.  
  
 *Attributo*  
 [Ingresso] Attributo da impostare. L'elenco di attributi validi è specifico del driver e uguale a [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 *ValuePtr*  
 [Ingresso] Puntatore al valore da associare *all'attributo*. A seconda del valore di *Attribute*, *ValuePtr* sarà un valore unsigned integer a 32 bit o punterà a una stringa di caratteri con terminazione null. Si noti che se l'argomento *Attributo* è un valore specifico del driver, il valore in *ValuePtr* può essere un intero con segno.  
  
 *Lunghezza stringa*  
 [Ingresso] Se *Attribute* è un attributo definito da ODBC e *ValuePtr* punta a una stringa di caratteri o a un buffer binario, questo argomento deve essere la lunghezza di*ValuePtr*. Per i dati di stringa di caratteri, questo argomento deve contenere il numero di byte nella stringa.  
  
 Se *Attributo* è un attributo definito da ODBC e *ValuePtr* è un numero intero, *StringLength* viene ignorato.  
  
 Se *Attribute* è un attributo definito dal driver, l'applicazione indica la natura dell'attributo a Gestione Driver impostando il *StringLength* argomento. *StringLength* può avere i valori seguenti:StringLength can have the following values:  
  
-   Se *ValuePtr* è un puntatore a una stringa di caratteri, *quindi StringLength* è la lunghezza della stringa o SQL_NTS.  
  
-   Se *ValuePtr* è un puntatore a un buffer binario, l'applicazione inserisce il risultato della macro SQL_LEN_BINARY_ATTR(*length*) in *StringLength*. In questo modo un valore negativo in *StringLength*.  
  
-   Se *ValuePtr* è un puntatore a un valore diverso da una stringa di caratteri o una stringa binaria, *quindi StringLength* deve avere il valore SQL_IS_POINTER.  
  
-   Se *ValuePtr* contiene un valore a lunghezza fissa, *StringLength* è SQL_IS_INTEGER o SQL_IS_UINTEGER, a seconda dei casi.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Uguale a [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), ad eccezione del fatto che Gestione Driver utilizzerà un **HandleType** di SQL_HANDLE_DBC_INFO_TOKEN e un **handle** di *hDbcInfoToken*.  
  
## <a name="remarks"></a>Osservazioni  
 **SQLSetConnectAttrForDbcInfo** è uguale a **SQLSetConnectAttr**, ma imposta l'attributo sul token di informazioni di connessione, anziché sull'handle di connessione. Ad esempio, se **SQLSetConnectAttr** non riconosce un attributo, **SQLSetConnectAttrForDbcInfo** deve restituire anche SQL_ERROR per tale attributo.  
  
 Ogni volta che il driver restituisce SQL_ERROR o SQL_INVALID_HANDLE, il driver deve ignorare questo attributo per calcolare l'ID del pool. Inoltre, Gestione Driver otterrà le informazioni di diagnostica da *hDbcInfoToken*e restituirà SQL_SUCCESS_WITH_INFO all'applicazione in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md). Pertanto, un'applicazione può recuperare i dettagli sul motivo per cui alcuni attributi non possono essere impostati.  
  
 Le applicazioni non devono chiamare direttamente questa funzione. Un driver ODBC che supporta il pool di connessioni in grado di riconoscere i driver deve implementare questa funzione.  
  
 Includere sqlspi.h per lo sviluppo di driver ODBC.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBCDeveloping an ODBC Driver](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pool di connessioni in grado di riconoscere i driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Sviluppo del rilevamento di pool di connessioni in un driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
