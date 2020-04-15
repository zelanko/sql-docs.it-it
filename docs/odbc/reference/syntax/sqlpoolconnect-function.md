---
title: Funzione SQLPoolConnect . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5045fe47683529f858b01e69f6af696e2821ca4c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306902"
---
# <a name="sqlpoolconnect-function"></a>Funzione SQLPoolConnect
**Conformità**  
 Versione introdotta: ODBC 3.8 Standards Compliance: ODBC  
  
 **Riepilogo**  
 **SQLPoolConnect** viene utilizzato per creare una nuova connessione se nessuna connessione nel pool può essere riutilizzata.  
  
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
 *Hdbc*  
 [Ingresso] Handle di connessione.  
  
 *hDbcInfoToken (informazioni in due)*  
 [Ingresso] Handle di token per la nuova richiesta di connessione dell'applicazione.  
  
 *wszOutConnectString (informazioni in base al valore dei valori wszOutConnect*  
 [Uscita] Puntatore a un buffer per la stringa di connessione completata. Una volta stabilita la connessione all'origine dati di destinazione, questo buffer contiene la stringa di connessione completata. Le applicazioni devono allocare almeno 1.024 caratteri per questo buffer.  
  
 Se *wszOutConnectString* è NULL, *cchConnectStringLen* restituirà comunque il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile per la restituzione nel buffer a cui punta *wszOutConnectString*.  
  
 *cchConnectStringBuffer (informazioni in inglese)*  
 [Ingresso] Lunghezza del buffer*wszOutConnectString,* in caratteri.  
  
 *cchConnectStringLen*  
 [Uscita] Puntatore a un buffer in cui restituire il numero totale di caratteri (escluso il carattere di terminazione null) disponibili per la restituzione in \* *wszOutConnectString*. Se il numero di caratteri disponibili per la restituzione è maggiore o \*uguale a *cchConnectStringBuffer*, la stringa di connessione completata in *wszOutConnectString* viene troncata in *cchConnectStringBuffer* meno la lunghezza di un carattere di terminazione null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Simile a [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) per qualsiasi errore di convalida dell'input, ad eccezione del fatto che Gestione Driver utilizzerà un **HandleType** di SQL_HANDLE_DBC_INFO_TOKEN e un **handle** di *hDbcInfoToken*.  
  
## <a name="remarks"></a>Osservazioni  
 Gestione Driver garantisce che l'handle HENV padre di *hDbc* e *hDbcInfoToken* sono uguali.  
  
 A differenza [di SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md), non è disponibile alcun argomento *DriverCompletion* per richiedere agli utenti di immettere le informazioni di connessione. Una finestra di dialogo di richiesta di conferma non è consentita nello scenario di pooling.  
  
 Le applicazioni non devono chiamare direttamente questa funzione. Un driver ODBC che supporta il pool di connessioni in grado di riconoscere i driver deve implementare questa funzione.  
  
 Ogni volta che un driver restituisce SQL_ERROR o SQL_INVALID_HANDLE, Gestione Driver restituisce l'errore all'applicazione (in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Ogni volta che un driver restituisce SQL_SUCCESS_WITH_INFO, Gestione Driver otterrà le informazioni di diagnostica da *hDbcInfoToken*e restituirà SQL_SUCCESS_WITH_INFO all'applicazione in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Quando un'applicazione utilizza [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md), *wszOutConnectString* sarà un buffer NULL (gli ultimi tre parametri saranno tutti impostati su NULL, 0, NULL). In caso contrario, il driver deve restituire la stringa di connessione di output, che verrà restituita alla chiamata [di funzione SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) dell'applicazione.  
  
 Includere sqlspi.h per lo sviluppo di driver ODBC.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBCDeveloping an ODBC Driver](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pool di connessioni in grado di riconoscere i driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Sviluppo del rilevamento di pool di connessioni in un driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
