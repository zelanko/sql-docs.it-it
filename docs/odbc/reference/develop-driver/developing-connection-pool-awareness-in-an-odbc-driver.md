---
title: Sviluppo di consapevolezza del pool di connessione in un driver ODBC Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c63d5cae-24fc-4fee-89a9-ad0367cddc3e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f77fea1d8439ac9ce7374b7dd47db5665686cfbc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283431"
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>Sviluppo del rilevamento di pool di connessioni in un driver ODBC
In questo argomento vengono illustrati i dettagli dello sviluppo di un driver ODBC che contiene informazioni su come il driver deve fornire servizi di pool di connessioni.  
  
## <a name="enabling-driver-aware-connection-pooling"></a>Abilitazione del pool di connessioni in grado di riconoscere i driver  
 Un driver deve implementare le seguenti funzioni SPI (ODBC Service Provider Interface):  
  
-   SQLSetConnectAttrForDbcInfo  
  
-   SQLSetConnectInfo (informazioni in lingua inglese)  
  
-   SQLSetDriverConnectInfo (informazioni in lingua inglese)  
  
-   SQLGetPoolID (IDSQLGetPoolID)  
  
-   SQLRateConnection (connessione SQLRateConnection)  
  
-   SQLPoolConnect (informazioni in lingua inglese)  
  
-   SQLCleanupConnectionPoolID (informazioni in lingua inglese)  
  
 Per altre informazioni, vedere Riferimento all'interfaccia del provider di servizi [ODBC (SPI, ODBC Service Provider Interface).](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)  
  
 Un driver deve inoltre implementare le seguenti funzioni esistenti in modo che sia possibile abilitare il pool in grado di riconoscere i driver:A driver must also implement the following existing functions so that the driver-aware pooling can be enabled:  
  
|Funzione|Funzionalità aggiunta|  
|--------------|-------------------------|  
|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|Supportare il nuovo tipo di maniglia: SQL_HANDLE_DBC_INFO_TOKEN (vedere la descrizione riportata di seguito).|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|Supportare il nuovo attributo di connessione set-only: SQL_ATTR_DBC_INFO_TOKEN per reimpostare la connessione (vedere la descrizione riportata di seguito).|  
  
> [!NOTE]  
>  Le funzioni deprecate come **SQLError** e **SQLSetConnectOption** non sono supportate per il pool di connessioni in grado di riconoscere i driver.  
  
## <a name="the-pool-id"></a>The Pool ID  
 L'ID del pool è un ID specifico del driver della lunghezza del puntatore per rappresentare un particolare gruppo di connessioni che può essere utilizzato in modo intercambiabile. Dato un set di informazioni di connessione, un driver deve essere in grado di dedurre rapidamente l'ID del pool corrispondente.  
  
 Ad esempio, l'ID del pool deve codificare il nome del server e le informazioni sulle credenziali. Tuttavia, il nome del database non è necessario perché un driver può essere in grado di riutilizzare una connessione e quindi modificare il database in meno tempo rispetto alla creazione di una nuova connessione.  
  
 Un driver deve definire un set di attributi chiave, che comprenderà l'ID del pool. Il valore di questi attributi chiave può provenire dagli attributi di connessione, dalla stringa di connessione e dal DSN. Nel caso in cui si verificano conflitti in queste origini, il criterio di risoluzione specifico del driver esistente deve essere utilizzato per la compatibilità con le versioni precedenti.  
  
 Gestione Driver utilizzerà un pool diverso per ID di pool diversi. Tutte le connessioni nello stesso pool sono riutilizzabili. Gestione Driver non riutilizzerà mai una connessione con un ID di pool diverso.  
  
 Pertanto, i driver devono assegnare un ID pool univoco per ogni gruppo di connessioni con lo stesso valore negli attributi chiave definiti. Se un driver utilizza lo stesso ID pool per due connessioni con valori diversi negli attributi chiave, Gestione Driver li inserirà comunque nello stesso pool (Gestione Driver non conosce gli attributi chiave specifici del driver). Ciò significa che il driver dovrà segnalare a Gestione Driver che una connessione con un diverso set di attributi chiave non è riutilizzabile all'interno della [funzione SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md). Ciò può ridurre le prestazioni e questa operazione non è consigliata.  
  
 Gestione Driver non riutilizzerà una connessione allocata da un altro ambiente driver anche se tutte le informazioni di connessione corrisponde. Gestione Driver utilizzerà un pool diverso per ambienti diversi, anche quando le connessioni hanno lo stesso ID pool. Pertanto, l'ID del pool è locale per l'ambiente del driver.  
  
 La funzione per ottenere l'ID del pool dal driver è [la funzione SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md).  
  
## <a name="the-connection-rating"></a>La classificazione della connessione  
 Rispetto alla creazione di una nuova connessione, è possibile ottenere prestazioni migliori reimpostando alcune informazioni di connessione (ad esempio DATABASE) in una connessione in pool. Pertanto, è possibile che non si desideri che il nome del database sia presente nel set di attributi chiave. In caso contrario, è possibile disporre di un pool separato per ogni database, che potrebbe non essere valido nelle applicazioni di livello intermedio, in cui i clienti usano diverse stringhe di connessione.  
  
 Ogni volta che si riutilizza una connessione con alcuni attributi non corrispondenti, è necessario reimpostare gli attributi non corrispondenti in base alla nuova richiesta dell'applicazione, in modo che la connessione restituita sia identica alla richiesta dell'applicazione (vedere la discussione dell'attributo SQL_ATTR_DBC_INFO_TOKEN nella [funzione SQLSetConnectAttr](https://go.microsoft.com/fwlink/?LinkId=59368)). Tuttavia, la reimpostazione di tali attributi può ridurre le prestazioni. Ad esempio, la reimpostazione di un database richiede una chiamata di rete al server. Pertanto, riutilizzare una connessione che corrisponde perfettamente, se disponibile.  
  
 Una funzione di classificazione nel driver può valutare una connessione esistente con una nuova richiesta di connessione. Ad esempio, la funzione di classificazione del conducente può determinare:  
  
-   Se la connessione esistente è perfettamente abbinata alla richiesta.  
  
-   Se sono presenti solo alcune mancate corrispondenze insignificanti, ad esempio il timeout di connessione, che non richiedono la comunicazione con il server per la reimpostazione.  
  
-   Se sono presenti alcuni attributi non corrispondenti che richiedono una comunicazione con il server da reimpostare, ma si tradurrà comunque in prestazioni migliori rispetto alla creazione di una nuova connessione.  
  
-   Se la mancata corrispondenza si è verificata per un attributo che richiede molto tempo per la reimpostazione (lo sviluppatore del driver può prendere in considerazione l'aggiunta di questo attributo nel set di attributi chiave, che viene utilizzato per generare l'ID del pool).  
  
 Un punteggio compreso tra 0 e 100 è possibile, dove 0 significa non riutilizzare e 100 significa perfettamente abbinato. [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md) è la funzione per la valutazione di una connessione.  
  
## <a name="new-odbc-handle---sql_handle_dbc_info_token"></a>Nuovo handle ODBC - SQL_HANDLE_DBC_INFO_TOKEN  
 Per supportare il pool di connessioni in grado di riconoscere i driver, il driver necessita di informazioni di connessione per calcolare l'ID pool. Il driver necessita inoltre di informazioni di connessione per confrontare le nuove richieste di connessione con le connessioni nel pool.  Ogni volta che nessuna connessione nel pool può essere riutilizzata, il driver deve stabilire una nuova connessione, richiedendo quindi informazioni di connessione.  
  
 Poiché le informazioni di connessione possono provenire da più origini (stringa di connessione, attributi di connessione e DSN), il driver potrebbe essere necessario analizzare la stringa di connessione e risolvere il conflitto tra queste origini in ognuna delle chiamate di funzione sopra.  
  
 Pertanto, viene introdotto un nuovo handle ODBC: SQL_HANDLE_DBC_INFO_TOKEN. Con SQL_HANDLE_DBC_INFO_TOKEN, un driver non è necessario analizzare la stringa di connessione e risolvere i conflitti nelle informazioni di connessione più di una volta. Poiché si tratta di una struttura di dati specifica del driver, il driver può archiviare dati quali informazioni di connessione o ID pool.  
  
 Questo handle viene utilizzato solo come interfaccia tra Gestione Driver e driver. Un'applicazione non può allocare direttamente questo handle.  
  
 L'handle padre di questo handle è di tipo SQL_HANDLE_ENV, vale a dire che il driver può ottenere le informazioni sull'ambiente dall'handle HENV durante la risoluzione delle informazioni di connessione.  
  
 Ogni volta che riceve una nuova richiesta di connessione, Gestione Driver allocherà un handle di tipo SQL_HANDLE_DBC_INFO_TOKEN per l'archiviazione delle informazioni di connessione, dopo aver confermato che il driver supporta il riconoscimento del pool di connessioni. Al termine dell'utilizzo dell'handle , ma prima di restituire alcuni codici restituiti diversi da SQL_STILL_EXECUTING da [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) o [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)), Gestione Driver libererà l'handle. Pertanto, l'handle viene creato dopo il SQLAllocHandle chiamare ed eliminare dopo il SQLFreeHandle chiamare. Gestione Driver garantisce che l'handle verrà liberato prima di liberare l'HENV associato (quando [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) o [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) restituisce un errore).  
  
 Il driver deve modificare le seguenti funzioni per accettare il nuovo tipo di handle SQL_HANDLE_DBC_INFO_TOKEN:  
  
1.  [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 Gestione Driver garantisce che più thread non utilizzerà lo stesso SQL_HANDLE_DBC_INFO_TOKEN gestire contemporaneamente. Pertanto, il modello di sincronizzazione di questo handle può essere molto semplice all'interno del driver. Gestione Driver non accetta un blocco dell'ambiente prima di allocare e liberare SQL_HANDLE_DBC_INFO_TOKEN.  
  
 **SQLAllocHandle** di Gestione Driver e **SQLFreeHandle** non accetterà questo nuovo tipo di handle.  
  
 SQL_HANDLE_DBC_INFO_TOKEN possono contenere informazioni riservate, ad esempio credenziali. Pertanto, un driver deve cancellare in modo sicuro il buffer di memoria (utilizzando [Secure'eroMemory](https://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx)) che contiene le informazioni riservate prima di rilasciare l'handle con **SQLFreeHandle**. Ogni volta che l'handle di ambiente di un'applicazione viene chiuso, tutti i pool di connessioni associati verranno chiusi.  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>Algoritmo di classificazione del pool di connessioni di Gestione driver  
 In questa sezione viene illustrato l'algoritmo di classificazione per il pool di connessioni di Gestione Driver. Gli sviluppatori di driver possono implementare lo stesso algoritmo per la compatibilità con le versioni precedenti. Questo algoritmo potrebbe non essere il migliore. È necessario perfezionare questo algoritmo in base all'implementazione (in caso contrario, non vi è alcun motivo per implementare questa funzionalità).  
  
 Gestione Driver restituirà una classificazione integrale da 0 a 100 per ogni connessione dal pool. 0 indica che la connessione non può essere riutilizzata e 100 indica un abbinamento perfetto. Si supponga che la richiesta di connessione è denominata hRequest e la connessione esistente dal pool è denominata come hCandidate. Se una delle seguenti condizioni è false, la connessione in pool hCandidate non può essere riutilizzata per hRequest (Gestione Driver assegnerà una classificazione pari a 0).  
  
-   hCandidate e hRequest provengono entrambi da API UNICODE (ad esempio SQLDriverConnectW) o dall'API ANSI (ad esempio SQLDriverConnectA). I driver UNICODE possono avere un comportamento diverso in base all'API ANSI e all'API UNICODE (vedere l'attributo di connessione SQL_ATTR_ANSI_APP).  
  
-   hCandidate e hRequest vengono creati dalla stessa funzione; SQLDriverConnect o SQLConnect.  
  
-   La stringa di connessione utilizzata per aprire hCandidate deve essere uguale a hRequest, quando viene usato SQLDriverConnect.The connection string used to open hCandidate should be the same as hRequest, when SQLDriverConnect is used.  
  
-   Il ServerName (o DSN), nome utente e password utilizzati per aprire hCandidate devono essere gli stessi utilizzati per aprire hRequest quando viene utilizzato SQLConnect.  
  
-   L'identificatore di sicurezza (SID) del thread corrente deve essere lo stesso del SID utilizzato per aprire hCandidate.  
  
-   Per i driver che sono costosi da aggiungere e diseseguire l'elenco (vedere la discussione di SQL_DTC_TRANSITION_COST in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)), il riutilizzo di *hRequest* non deve richiedere un ulteriore elenco o unenlistment.  
  
 Nella tabella seguente viene illustrata l'assegnazione del punteggio per scenari diversi.  
  
|Confronto sugli attributi di connessione tra la connessione in pool e la richiesta|Nessun arruolamento / annullamento dell'arruolamento|Richiedi arruolamento aggiuntivo / Unenlistment|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|Catalogo (SQL_ATTR_CURRENT_CATALOG) è diverso|60|50|  
|Alcuni attributi di connessione sono diversi, ma il catalogo è lo stesso|90|70|  
|Tutti gli attributi di connessione perfettamente abbinati|100|80|  
  
## <a name="sequence-diagram"></a>Diagramma sequenza  
 Questo diagramma di sequenza mostra il meccanismo di pooling di base descritto in questo argomento. Mostra solo l'uso di [SQLDriverConnect,](../../../odbc/reference/syntax/sqldriverconnect-function.md) ma il caso [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) è simile.  
  
 ![Diagramma sequenza](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>Diagramma di stato  
 Questo diagramma di stato mostra l'oggetto token di informazioni di connessione, descritto in questo argomento. Il diagramma mostra solo [SQLDriverConnect,](../../../odbc/reference/syntax/sqldriverconnect-function.md) ma il caso [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) è simile. Poiché Gestione Driver potrebbe essere necessario gestire gli errori in qualsiasi momento, Gestione Driver può chiamare [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md) per qualsiasi stato.  
  
 ![Diagramma di stato](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>Vedere anche  
 [Pool di connessioni in grado di riconoscere i driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Riferimento dell'interfaccia del provider di servizi (SPI) ODBC](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)
