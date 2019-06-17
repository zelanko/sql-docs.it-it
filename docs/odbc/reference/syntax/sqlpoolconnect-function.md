---
title: Funzione SQLPoolConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPoolConnect function [ODBC]
ms.assetid: 41322737-890d-4a81-aed2-06cc3d546962
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 297c856cc2481a6d3266d7654797f81b9b9f5c11
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536603"
---
# <a name="sqlpoolconnect-function"></a>Funzione SQLPoolConnect
**Conformità**  
 Versione introdotta: Conformità agli standard 3,8 ODBC: ODBC  
  
 **Riepilogo**  
 **SQLPoolConnect** consente di creare una nuova connessione se nessuna connessione nel pool può essere riutilizzata.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp
  
SQLRETURN  SQLPoolConnect(  
                SQLHDBC              hDbc,  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              wszOutConnectString,  
                SQLSMALLINT          cchConnectStringBuffer,  
                SQLSMALLINT *        cchConnectStringLen );  
```  
  
## <a name="arguments"></a>Argomenti  
 *hDbc*  
 [Input] L'handle di connessione.  
  
 *hDbcInfoToken*  
 [Input] L'handle del token per la nuova richiesta di connessione dell'applicazione.  
  
 *wszOutConnectString*  
 [Output] Puntatore a un buffer per la stringa di connessione completata. Connessione all'origine dati di destinazione, questo buffer contiene la stringa di connessione completata. Le applicazioni è consigliabile allocare almeno 1.024 caratteri per questo buffer.  
  
 Se *wszOutConnectString* sia impostato su NULL *cchConnectStringLen* continuerà a restituire il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibili per restituire il buffer a cui punta *wszOutConnectString*.  
  
 *cchConnectStringBuffer*  
 [Input] Lunghezza di **wszOutConnectString* buffer, in caratteri.  
  
 *cchConnectStringLen*  
 [Output] Puntatore a un buffer in cui restituire il numero totale di caratteri (escluso il carattere di terminazione null) disponibili per restituire \* *wszOutConnectString*. Se il numero di caratteri disponibili da restituire è maggiore o uguale a *cchConnectStringBuffer*, il completamento stringa di connessione nel \* *wszOutConnectString* viene troncato a *cchConnectStringBuffer* meno la lunghezza di un carattere di terminazione null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, or, SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Simile a [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) per qualsiasi input errore di convalida, ad eccezione del fatto che la gestione di Driver utilizzerà un **HandleType** di SQL_HANDLE_DBC_INFO_TOKEN e un **gestire** di *hDbcInfoToken*.  
  
## <a name="remarks"></a>Note  
 Gestione Driver garantisce che padre gestire HENV *hDbc* e *hDbcInfoToken* sono uguali.  
  
 A differenza [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md), è presente alcun *DriverCompletion* argomento per richiedere agli utenti di immettere le informazioni di connessione. Una finestra di dialogo richiesta non è consentito nello scenario del pool di connessioni.  
  
 Le applicazioni non devono chiamare direttamente questa funzione. Un driver ODBC che supporta il pool di connessioni compatibile con il driver deve implementare questa funzione.  
  
 Ogni volta che un driver restituisce SQL_ERROR o SQL_INVALID_HANDLE, gestione Driver restituisce l'errore all'applicazione (in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) oppure [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Ottiene le informazioni di diagnostica da ogni volta che un driver restituisce SQL_SUCCESS_WITH_INFO, gestione Driver *hDbcInfoToken*e restituiscono SQL_SUCCESS_WITH_INFO all'applicazione in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Quando un'applicazione usa [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md), *wszOutConnectString* sarà un buffer NULL (gli ultimi tre parametri verranno tutti impostati su NULL, 0, NULL). In caso contrario, il driver deve restituire la stringa di connessione di output, che sarà restituita all'applicazione [funzione SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) chiamare.  
  
 Includere sqlspi.h per lo sviluppo di driver ODBC.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pool di connessioni compatibile con il driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Sviluppo del rilevamento di pool di connessioni in un driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
