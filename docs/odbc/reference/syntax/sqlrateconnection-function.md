---
title: Funzione SQLRateConnection | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d36224329fa29a54f7163cb4e1ce6228f460875
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63262500"
---
# <a name="sqlrateconnection-function"></a>Funzione SQLRateConnection
**Conformità**  
 Versione introdotta: Conformità agli standard 3,81 ODBC: ODBC  
  
 **Riepilogo**  
 **SQLRateConnection** determina se un driver può riutilizzare una connessione esistente nel pool di connessioni.  
  
## <a name="syntax"></a>Sintassi  
  
```  
SQLRETURN  SQLRateConnection(  
                SQLHDBC_INFO_TOKEN   hRequest,  
                SQLHDBC              hCandidateConnection,  
                BOOL                 fRequiredTransactionEnlistment,  
                TRANSID              transId,  
                DWORD *              pRating );  
```  
  
## <a name="arguments"></a>Argomenti  
 *hRequest*  
 [Input] Un handle del token che rappresenta la nuova richiesta di connessione dell'applicazione.  
  
 *hCandidateConnection*  
 [Input] La connessione esistente nel pool di connessioni. La connessione deve essere aperta.  
  
 *fRequiredTransactionEnlistment*  
 [Input] Se TRUE, il riutilizzo della connessione esistente *hCandidateConnection* per la nuova richiesta di connessione (*hRequest*) richiede la creazione di un'integrazione aggiuntiva.  
  
 *transId*  
 [Input] Se *fRequiredTransactionEnlistment* è TRUE, *ID transazione* rappresenta la transazione DTC che aggiungerà la richiesta. Se *fRequiredTransactionEnlistment* FALSO *ID transazione* verranno ignorati.  
  
 *pRating*  
 [Output] *hCandidateConnection*riutilizzo del punteggio per il *hRequest*. Questa valutazione è compreso tra 0 e 100 (inclusivo).  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS o SQL_ERROR, SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Gestione Driver non elaborerà le informazioni di diagnostica restituite dalla funzione.  
  
## <a name="remarks"></a>Note  
 **SQLRateConnection** produce un punteggio compreso tra 0 e 100 (inclusivo) che indica come una connessione esistente corrisponde alla richiesta.  
  
|Punteggio|Significato (quando viene restituito SQL_SUCCESS)|  
|-----------|-----------------------------------------------|  
|0|*hCandidateConnection* non deve essere riutilizzato per la *hRequest*.|  
|I valori compresi tra 1 e 98 (inclusivo)|Maggiore è il punteggio, maggiore che *hCandidateConnection* corrisponde *hRequest*.|  
|99|Sono disponibili solo le mancate corrispondenze negli attributi non significativi.  Gestione Driver deve interrompere il ciclo di valutazione.|  
|100|Corrispondenza esatta.  Gestione Driver deve interrompere il ciclo di valutazione.|  
|Qualsiasi altro valore maggiore di 100|*hCandidateConnection* viene contrassegnato come inattivo e non verrà riutilizzate anche in una richiesta di connessione future.|  
  
 Gestione Driver contrassegna una connessione come inattivo se il codice restituito è diverso da SQL_SUCCESS (inclusi SQL_SUCCESS_WITH_INFO) o la classificazione è maggiore di 100. Tale connessione inattiva non verrà riutilizzate non (ancora nelle richieste di connessione futuri) e verrà infine un timeout dopo CPTimeout passa. Gestione Driver continuerà a trovare un'altra connessione dal pool di frequenza.  
  
 Se Gestione Driver riutilizzare una connessione il cui punteggio è rigorosamente inferiore a 100 (inclusi 99), Driver Manager chiamerà SQLSetConnectAttr(SQL_ATTR_DBC_INFO_TOKEN) per reimpostare la connessione torna allo stato richiesto dall'applicazione. Il driver non reimpostare la connessione in questa chiamata di funzione.  
  
 Se *fRequiredTransactionEnlistment* è TRUE, viene riutilizzata *hCandidateConnection* richiede un'integrazione aggiuntiva (*ID transazione* ! = NULL) o unenlistment ( *ID transazione* = = NULL). Indica il costo di riutilizzare una connessione e indica se il driver deve integrare o rimuovere la connessione se sta per riutilizzare la connessione. Se *fRequireTransactionEnlistment* è FALSE, driver deve ignorare il valore di *ID transazione*.  
  
 Gestione Driver garantisce che padre gestire HENV *hRequest* e *hCandidateConnection* sono uguali. Gestione Driver garantisce che l'ID del pool associato *hRequest* e *hCandidateConnection* sono uguali.  
  
 Le applicazioni non devono chiamare direttamente questa funzione. Un driver ODBC che supporta il pool di connessioni compatibile con il driver deve implementare questa funzione.  
  
 Includere sqlspi.h per lo sviluppo di driver ODBC.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pool di connessioni compatibile con il driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Sviluppo del rilevamento di pool di connessioni in un driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
