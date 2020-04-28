---
title: Sviluppo della consapevolezza del pool di connessioni in un driver ODBC | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283431"
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>Sviluppo del rilevamento di pool di connessioni in un driver ODBC
In questo argomento vengono illustrati i dettagli dello sviluppo di un driver ODBC che contiene informazioni sul modo in cui il driver deve fornire i servizi di pool di connessioni.  
  
## <a name="enabling-driver-aware-connection-pooling"></a>Abilitazione del pool di connessioni compatibile con il driver  
 Un driver deve implementare le seguenti funzioni di ODBC Service Provider Interface (SPI):  
  
-   SQLSetConnectAttrForDbcInfo  
  
-   SQLSetConnectInfo  
  
-   SQLSetDriverConnectInfo  
  
-   SQLGetPoolID  
  
-   SQLRateConnection  
  
-   SQLPoolConnect  
  
-   SQLCleanupConnectionPoolID  
  
 Per ulteriori informazioni, vedere Guida di [riferimento all'interfaccia del provider di servizi (SPI) ODBC](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md) .  
  
 Un driver deve implementare anche le funzioni esistenti seguenti, in modo che sia possibile abilitare il pool compatibile con i driver:  
  
|Funzione|Funzionalità aggiunta|  
|--------------|-------------------------|  
|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|Supporta il nuovo tipo di handle: SQL_HANDLE_DBC_INFO_TOKEN (vedere la descrizione riportata di seguito).|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|Supporto del nuovo attributo di connessione solo set: SQL_ATTR_DBC_INFO_TOKEN per la reimpostazione della connessione (vedere la descrizione riportata di seguito).|  
  
> [!NOTE]  
>  Le funzioni deprecate quali **SQLError** e **SQLSetConnectOption** non sono supportate per il pool di connessioni compatibile con i driver.  
  
## <a name="the-pool-id"></a>ID del pool  
 L'ID del pool è un ID specifico del driver di lunghezza puntatore per rappresentare un particolare gruppo di connessioni che possono essere usate in modo interscambiabile. Dato un set di informazioni di connessione, un driver deve essere in grado di dedurre rapidamente l'ID del pool corrispondente.  
  
 Ad esempio, l'ID del pool deve codificare il nome del server e le informazioni sulle credenziali. Tuttavia, il nome del database non è necessario perché un driver potrebbe essere in grado di riutilizzare una connessione e quindi modificare il database in meno tempo rispetto alla creazione di una nuova connessione.  
  
 Un driver deve definire un set di attributi chiave, che includerà l'ID del pool. Il valore di questi attributi chiave può provenire dagli attributi di connessione, dalla stringa di connessione e dal DSN. Se in queste origini sono presenti conflitti, i criteri di risoluzione specifici del driver esistenti devono essere usati per la compatibilità con le versioni precedenti.  
  
 Gestione driver utilizzerà un pool diverso per gli ID del pool diversi. Tutte le connessioni nello stesso pool sono riutilizzabili. Gestione driver non riutilizzerà mai una connessione con un ID pool diverso.  
  
 I driver devono pertanto assegnare un ID pool univoco per ogni gruppo di connessioni con lo stesso valore negli attributi chiave definiti. Se un driver usa lo stesso ID di pool per due connessioni con valori diversi nei rispettivi attributi chiave, gestione driver li inserirà nello stesso pool (Gestione driver non è in grado di riconoscere gli attributi chiave specifici del driver). Questo significa che il driver dovrà segnalare a gestione driver che una connessione con un diverso set di attributi chiave non è riutilizzabile all'interno della [funzione SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md). Ciò può ridurre le prestazioni e questa operazione non è consigliata.  
  
 Gestione driver non riutilizzerà una connessione allocata da un altro ambiente driver anche se tutte le informazioni di connessione corrispondono. Gestione driver utilizzerà un pool diverso per un ambiente diverso, anche quando le connessioni hanno lo stesso ID pool. L'ID del pool è quindi locale rispetto al relativo ambiente di driver.  
  
 La funzione per ottenere l'ID del pool dal driver è la [funzione SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md).  
  
## <a name="the-connection-rating"></a>Classificazione della connessione  
 Rispetto alla creazione di una nuova connessione, è possibile ottenere prestazioni migliori reimpostando alcune informazioni di connessione, ad esempio il DATABASE, in una connessione in pool. Quindi, potrebbe non essere necessario che il nome del database sia nel set di attributi chiave. In caso contrario, è possibile disporre di un pool separato per ogni database, che potrebbe non essere utile nelle applicazioni di livello intermedio, in cui i clienti utilizzano diverse stringhe di connessione.  
  
 Quando si riutilizza una connessione con alcuni attributi non corrispondenti, è necessario reimpostare gli attributi non corrispondenti basati sulla nuova richiesta dell'applicazione, in modo che la connessione restituita sia identica alla richiesta dell'applicazione (vedere la discussione sull'attributo SQL_ATTR_DBC_INFO_TOKEN nella [funzione SQLSetConnectAttr](https://go.microsoft.com/fwlink/?LinkId=59368)). La reimpostazione di tali attributi può tuttavia ridurre le prestazioni. La reimpostazione di un database, ad esempio, richiede una chiamata di rete al server. Quindi, riutilizzare una connessione perfettamente corrispondente, se disponibile.  
  
 Una funzione di classificazione nel driver può valutare una connessione esistente con una nuova richiesta di connessione. La funzione di valutazione del driver, ad esempio, può determinare:  
  
-   Se la connessione esistente è perfettamente associata alla richiesta.  
  
-   Se sono presenti solo alcune mancate corrispondenze non significative, ad esempio il timeout della connessione, che non richiedono la comunicazione con il server per la reimpostazione.  
  
-   Se sono presenti alcuni attributi non corrispondenti che richiedono una comunicazione con il server per la reimpostazione, ma possono comunque migliorare le prestazioni rispetto alla creazione di una nuova connessione.  
  
-   Se si è verificata una mancata corrispondenza per un attributo che richiede molto tempo per la reimpostazione, lo sviluppatore del driver può prendere in considerazione l'aggiunta di questo attributo nel set di attributi chiave, che viene usato per generare l'ID del pool.  
  
 È possibile un punteggio compreso tra 0 e 100. il valore 0 indica che non viene riutilizzato e 100 significa che la corrispondenza è perfetta. [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md) è la funzione per la classificazione di una connessione.  
  
## <a name="new-odbc-handle---sql_handle_dbc_info_token"></a>Nuovo handle ODBC-SQL_HANDLE_DBC_INFO_TOKEN  
 Per supportare il pool di connessioni compatibile con il driver, il driver necessita di informazioni di connessione per calcolare l'ID del pool. Il driver necessita inoltre di informazioni di connessione per confrontare le nuove richieste di connessione con le connessioni nel pool.  Ogni volta che non è possibile riutilizzare nessuna connessione nel pool, il driver deve stabilire una nuova connessione, richiedendo quindi le informazioni di connessione.  
  
 Poiché le informazioni di connessione possono provenire da più origini (stringa di connessione, attributi di connessione e DSN), il driver potrebbe dover analizzare la stringa di connessione e risolvere il conflitto tra queste origini in ognuna delle chiamate di funzione precedenti.  
  
 Viene quindi introdotto un nuovo handle ODBC: SQL_HANDLE_DBC_INFO_TOKEN. Con SQL_HANDLE_DBC_INFO_TOKEN, un driver non deve analizzare la stringa di connessione e risolvere i conflitti nelle informazioni di connessione più di una volta. Poiché si tratta di una struttura di dati specifica del driver, il driver può archiviare dati quali le informazioni di connessione o l'ID del pool.  
  
 Questo handle viene utilizzato solo come interfaccia tra il driver e la gestione driver. Un'applicazione non può allocare direttamente questo handle.  
  
 L'handle padre di questo handle è di tipo SQL_HANDLE_ENV, vale a dire che il driver può ottenere le informazioni sull'ambiente dall'handle HENV durante la risoluzione delle informazioni di connessione.  
  
 Ogni volta che viene ricevuta una nuova richiesta di connessione, gestione driver alloca un handle di tipo SQL_HANDLE_DBC_INFO_TOKEN per l'archiviazione delle informazioni di connessione, dopo la conferma che il driver supporta la consapevolezza del pool di connessioni. Al termine dell'utilizzo dell'handle (ma prima di restituire alcuni codici restituiti diversi da SQL_STILL_EXECUTING da [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) o [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)), gestione driver libererà l'handle. Pertanto, l'handle viene creato dopo la chiamata a SQLAllocHandle ed eliminato definitivamente dopo la chiamata SQLFreeHandle. Gestione driver garantisce che l'handle venga liberato prima di liberare il HENV associato (quando [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) o [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) restituisce un errore).  
  
 Il driver deve modificare le funzioni seguenti per accettare il nuovo tipo di handle SQL_HANDLE_DBC_INFO_TOKEN:  
  
1.  [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 Gestione driver garantisce che più thread non utilizzeranno contemporaneamente lo stesso handle di SQL_HANDLE_DBC_INFO_TOKEN. Pertanto, il modello di sincronizzazione di questo handle può essere molto semplice all'interno del driver. Gestione driver non accetta un blocco di ambiente prima di allocare e liberare SQL_HANDLE_DBC_INFO_TOKEN.  
  
 Il **SQLAllocHandle** e **SQLFreeHandle** di gestione driver non accetteranno questo nuovo tipo di handle.  
  
 SQL_HANDLE_DBC_INFO_TOKEN possono contenere informazioni riservate, ad esempio le credenziali. Pertanto, un driver deve cancellare in modo sicuro il buffer di memoria (usando [SecureZeroMemory](https://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx)) che contiene le informazioni riservate prima di rilasciare questo handle con **SQLFreeHandle**. Ogni volta che viene chiuso un handle di ambiente di un'applicazione, tutti i pool di connessioni associati verranno chiusi.  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>Algoritmo di classificazione pool di connessioni di gestione driver  
 In questa sezione viene descritto l'algoritmo di classificazione per il pool di connessioni di gestione driver. Gli sviluppatori di driver possono implementare lo stesso algoritmo per la compatibilità con le versioni precedenti. Questo algoritmo potrebbe non essere quello migliore. È consigliabile perfezionare questo algoritmo in base all'implementazione. in caso contrario, non esiste alcun motivo per implementare questa funzionalità.  
  
 Gestione driver restituirà una valutazione integrale da 0 a 100 per ogni connessione dal pool. 0 indica che non è possibile riutilizzare la connessione e 100 indica una corrispondenza perfetta. Si supponga che la richiesta di connessione sia denominata hRequest e che la connessione esistente dal pool sia denominata hCandidate. Se una delle condizioni seguenti è false, non è possibile riutilizzare la connessione in pool hCandidate per hRequest (Gestione driver assegnerà una classificazione pari a 0).  
  
-   hCandidate e hRequest provengono entrambi da un'API UNICODE, ad esempio SQLDriverConnectW, o da un'API ANSI, ad esempio SQLDriverConnectA. I driver UNICODE possono avere un comportamento diverso dall'API ANSI e dall'API UNICODE (vedere l'attributo di connessione SQL_ATTR_ANSI_APP).  
  
-   hCandidate e hRequest vengono creati dalla stessa funzione. SQLDriverConnect o SQLConnect.  
  
-   La stringa di connessione usata per aprire hCandidate deve essere uguale a hRequest, quando viene usato SQLDriverConnect.  
  
-   Il nomeserver (o DSN), il nome utente e la password usati per aprire hCandidate devono essere gli stessi usati per aprire hRequest quando si usa SQLConnect.  
  
-   L'ID di sicurezza (SID) del thread corrente deve essere uguale al SID usato per aprire hCandidate.  
  
-   Per i driver di cui è possibile eseguire l'integrazione e la rimozione (vedere la discussione relativa a SQL_DTC_TRANSITION_COST in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)), il riutilizzo di *hRequest* non deve richiedere un elenco o una rimozione aggiuntiva.  
  
 Nella tabella seguente viene illustrata l'assegnazione dei punteggi per diversi scenari.  
  
|Confronto sugli attributi di connessione tra la connessione in pool e la richiesta|Nessun inserimento/rimozione|Richiedi integrazione/rimozione aggiuntiva|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|Catalogo (SQL_ATTR_CURRENT_CATALOG) diverso|60|50|  
|Alcuni attributi di connessione sono diversi, ma il catalogo è lo stesso|90|70|  
|Tutti gli attributi di connessione corrispondono perfettamente|100|80|  
  
## <a name="sequence-diagram"></a>Diagramma sequenza  
 In questo diagramma di sequenza viene illustrato il meccanismo di base del pool descritto in questo argomento. Mostra solo l'uso di [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) , ma il caso di [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) è simile.  
  
 ![Diagramma sequenza](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>Diagramma di stato  
 Questo diagramma di stato Mostra l'oggetto token informazioni di connessione, descritto in questo argomento. Il diagramma mostra solo [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) , ma il caso di [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) è simile. Poiché Gestione driver potrebbe dover gestire gli errori in qualsiasi momento, gestione driver può chiamare [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md) per qualsiasi stato.  
  
 ![Diagramma di stato](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>Vedere anche  
 [Pool di connessioni compatibile con il driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Riferimento dell'interfaccia del provider di servizi (SPI) ODBC](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)
