---
title: SqlRateConnection (funzione) . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLRateConnection function [ODBC]
ms.assetid: e8da2ffb-d6ef-4ca7-824f-57afd29585d8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d29033460a7f89fc4a8b1c371a4d32bdf94a2a05
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288881"
---
# <a name="sqlrateconnection-function"></a>Funzione SQLRateConnection
**Conformità**  
 Versione introdotta: ODBC 3.81 Standards Compliance: ODBC  
  
 **Riepilogo**  
 **SQLRateConnection** determina se un driver può riutilizzare una connessione esistente nel pool di connessioni.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp
  
SQLRETURN  SQLRateConnection(  
                SQLHDBC_INFO_TOKEN   hRequest,  
                SQLHDBC              hCandidateConnection,  
                BOOL                 fRequiredTransactionEnlistment,  
                TRANSID              transId,  
                DWORD *              pRating );  
```  
  
## <a name="arguments"></a>Argomenti  
 *hRichiesta*  
 [Ingresso] Handle di token che rappresenta la nuova richiesta di connessione dell'applicazione.  
  
 *hCandidateConnection*  
 [Ingresso] Connessione esistente nel pool di connessioni. La connessione deve essere in uno stato aperto.  
  
 *fRequiredTransactionEnlistment*  
 [Ingresso] Se TRUE, riutilizzare *hCandidateConnection* della connessione esistente per la nuova richiesta di connessione (*hRequest*) richiede un ulteriore elenco.  
  
 *transId*  
 [Ingresso] Se *fRequiredTransactionEnlistment* è TRUE, *transId* rappresenta la transazione DTC che verrà analizzata dalla richiesta. Se *fRequiredTransactionEnlistment* è FALSE, *transId* verrà ignorato.  
  
 *pValutazione*  
 [Uscita] *hCandidateConnection*'riutilizzare la classificazione per *hRequest*. Questa valutazione sarà compresa tra 0 e 100 (incluso).  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Gestione Driver non elaborerà le informazioni diagnostiche restituite da questa funzione.  
  
## <a name="remarks"></a>Osservazioni  
 **SQLRateConnection** produce un punteggio compreso tra 0 e 100 (incluso) che indica quanto una connessione esistente corrisponde alla richiesta.  
  
|Punteggio|Significato (quando viene restituito SQL_SUCCESS)|  
|-----------|-----------------------------------------------|  
|0|*hCandidateConnection* non deve essere riutilizzato per *hRequest*.|  
|Qualsiasi valore compreso tra 1 e 98 (incluso)|Maggiore è il punteggio, più vicino a *hCandidateConnection* corrispondono a *hRequest*.|  
|99|Sono presenti solo mancate corrispondenze negli attributi non significativi.  Gestione Driver deve arrestare il ciclo di classificazione.|  
|100|Corrispondenza perfetta.  Gestione Driver deve arrestare il ciclo di classificazione.|  
|Qualsiasi altro valore maggiore di 100|*hCandidateConnection* è contrassegnato come morto e non verrà riutilizzato nemmeno in una richiesta di connessione futura.|  
  
 Gestione Driver contrassegnerà una connessione come morta se il codice di ritorno è diverso da SQL_SUCCESS (inclusi SQL_SUCCESS_WITH_INFO) o la valutazione è maggiore di 100. Tale connessione inattiva non verrà riutilizzata (anche nelle richieste di connessione future) e alla fine verrà stesa dopo il passaggio di CPTimeout. Gestione Driver continuerà a trovare un'altra connessione dal pool per valutare.  
  
 Se Gestione Driver riutilizzato una connessione il cui punteggio è strettamente inferiore a 100 (incluso 99), Gestione Driver chiamerà SQLSetConnectAttr(SQL_ATTR_DBC_INFO_TOKEN) per reimpostare la connessione nello stato richiesto dall'applicazione. Il driver non deve reimpostare la connessione in questa chiamata di funzione.  
  
 Se *fRequiredTransactionEnlistment* è TRUE, il riutilizzo di *hCandidateConnection* richiede un ulteriore elenco*transId* *(transId* ! Ciò indica il costo del riutilizzo di una connessione e se il driver deve eseguire l'arruolazione/ disinuscitare la connessione se intende riutilizzare la connessione. Se *fRequireTransactionEnlistment* è FALSE, driver deve ignorare il valore di *transId*.  
  
 Gestione Driver garantisce che l'handle HENV padre di *hRequest* e *hCandidateConnection* sono uguali. Gestione Driver garantisce che l'ID del pool associato a *hRequest* e *hCandidateConnection* sono uguali.  
  
 Le applicazioni non devono chiamare direttamente questa funzione. Un driver ODBC che supporta il pool di connessioni in grado di riconoscere i driver deve implementare questa funzione.  
  
 Includere sqlspi.h per lo sviluppo di driver ODBC.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBCDeveloping an ODBC Driver](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pool di connessioni in grado di riconoscere i driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Sviluppo del rilevamento di pool di connessioni in un driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
