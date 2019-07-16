---
title: Sviluppo di riconoscimento dei Pool di connessioni in un Driver ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c63d5cae-24fc-4fee-89a9-ad0367cddc3e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 02577370218a799faf86a7f8986859c415962f5a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897741"
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>Sviluppo del rilevamento di pool di connessioni in un driver ODBC
Questo argomento illustra i dettagli dello sviluppo di un driver ODBC che contiene informazioni sul modo in cui il driver deve fornire i servizi del pool di connessione.  
  
## <a name="enabling-driver-aware-connection-pooling"></a>Abilitazione del pool di connessioni compatibile con il Driver  
 Un driver necessario implementare le funzioni ODBC Service Provider Interface (SPI) seguenti:  
  
-   SQLSetConnectAttrForDbcInfo  
  
-   SQLSetConnectInfo  
  
-   SQLSetDriverConnectInfo  
  
-   SQLGetPoolID  
  
-   SQLRateConnection  
  
-   SQLPoolConnect  
  
-   SQLCleanupConnectionPoolID  
  
 Visualizzare [riferimento ODBC Service Provider Interface (SPI)](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md) per altre informazioni.  
  
 Un driver deve implementare anche le seguenti funzioni esistenti in modo che il pool compatibile con il driver può essere abilitato:  
  
|Funzione|Aggiunta la funzionalità|  
|--------------|-------------------------|  
|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|Supporto per il nuovo tipo di handle: SQL_HANDLE_DBC_INFO_TOKEN (vedere la descrizione riportata di seguito).|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|Supporto per il nuovo attributo di sola connessione: SQL_ATTR_DBC_INFO_TOKEN per la reimpostazione della connessione (vedere la descrizione riportata di seguito).|  
  
> [!NOTE]  
>  Funzioni deprecate, ad esempio **SQLError** e **SQLSetConnectOption** non sono supportate per il pool di connessioni compatibile con il driver.  
  
## <a name="the-pool-id"></a>L'ID del Pool  
 L'ID del pool è un ID specifico del driver di puntatore a lunghezza per rappresentare un determinato gruppo di connessioni che possono essere usati indifferentemente. Dato un set di informazioni di connessione, un driver debba essere in grado di dedurre rapidamente il corrispondente ID del pool.  
  
 Ad esempio, l'ID del pool deve codificare le informazioni di nome e le credenziali del server. Tuttavia, il nome del database non è necessaria perché un driver potrebbe essere in grado di riutilizzare una connessione e quindi modificare il database in meno tempo rispetto alla creazione di una nuova connessione.  
  
 Un driver necessario definire un set di attributi chiave, che includerà l'ID del pool. Il valore di questi attributi chiave può provenire da attributi di connessione, la stringa di connessione e DSN. Nel caso in cui sono presenti conflitti in queste origini, usare i criteri di risoluzione esistente, specifici del driver per la compatibilità con le versioni precedenti.  
  
 Gestione Driver utilizzerà un pool diverso per gli ID del pool diversi. Tutte le connessioni nello stesso pool sono riutilizzabili. Gestione Driver mai riutilizzerà una connessione con un ID pool diversi.  
  
 Di conseguenza i driver devono assegnare un ID univoco del pool per ogni gruppo di connessioni con lo stesso valore nei relativi attributi chiave definiti. Se un driver utilizza lo stesso ID pool per due connessioni con valori diversi nei relativi attributi chiave, gestione Driver verrà comunque inserirli nello stesso pool (gestione Driver non riconosce gli attributi della chiave specifiche del driver). Ciò significa che il driver necessario per il Driver Gestione report che non è riutilizzabile all'interno di una connessione con un diverso set di attributi chiave [funzione SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md). Ciò può ridurre le prestazioni e questo non è consigliato.  
  
 Gestione Driver non riutilizzerà una connessione allocata da un altro ambiente driver anche se corrispondano a tutte le informazioni di connessione. Gestione Driver utilizzerà un pool diverso per diversi ambienti, anche quando le connessioni hanno lo stesso ID di pool. Pertanto, l'ID del pool è locale al relativo ambiente di driver.  
  
 La funzione per ottenere l'ID del pool dal driver viene [funzione SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md).  
  
## <a name="the-connection-rating"></a>La classificazione di connessione  
 Rispetto a una nuova connessione, è possibile ottenere prestazioni migliori reimpostando alcune informazioni di connessione (ad esempio, DATABASE) in una connessione in pool. Pertanto, è possibile non il nome del database sia nel set di attributi chiave. In caso contrario, è possibile avere un pool separato per ogni database, che potrebbe non essere ottimale in applicazioni di livello intermedio, in cui i clienti di usano varie stringhe di connessione diversa.  
  
 Ogni volta che si riutilizza una connessione con alcuni attributi non corrispondenti, è consigliabile reimpostare gli attributi non corrispondenti in base alla nuova richiesta di applicazione, in modo che la connessione restituita è identica alla richiesta dell'applicazione (vedere la discussione dell'attributo SQL_ATTR In _DBC_INFO_TOKEN [funzione SQLSetConnectAttr](https://go.microsoft.com/fwlink/?LinkId=59368)). Tuttavia, la reimpostazione di tali attributi potrebbe ridurre le prestazioni. Ad esempio, la reimpostazione di un database richiede una chiamata di rete al server. Riutilizzare una connessione perfettamente corrispondente, di conseguenza, se disponibile.  
  
 Una funzione di classificazione nel driver può restituire una connessione esistente con una nuova richiesta di connessione. Ad esempio, è possibile determinare la funzione del driver classificazione:  
  
-   Se la connessione esistente è perfettamente corrispondente con la richiesta.  
  
-   Se ci sono solo alcuni non significativi le mancate corrispondenze, ad esempio timeout di connessione, che non richiedono la comunicazione con il server per reimpostare.  
  
-   Se sono presenti alcuni attributi non corrispondenti che richiedono una comunicazione con il server per reimpostare ma sarebbero comunque comportare prestazioni migliori rispetto a una nuova connessione.  
  
-   Se la mancata corrispondenza si è verificato per un attributo che richiede molto tempo reimpostare (lo sviluppatore del driver potrebbe prendere in considerazione l'aggiunta di questo attributo nel set di attributi chiave, che viene usato per generare l'ID del pool).  
  
 Un punteggio compreso tra 0 e 100 viene possibile, dove 0 indica che non riutilizzare e 100 indica che perfettamente corrispondente. [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md) è la funzione per la valutazione di una connessione.  
  
## <a name="new-odbc-handle---sqlhandledbcinfotoken"></a>Nuovo Handle ODBC - SQL_HANDLE_DBC_INFO_TOKEN  
 Per supportare i pool di connessioni compatibile con il driver, il driver ha bisogno delle informazioni di connessione per calcolare l'ID del Pool. Il driver deve anche le informazioni di connessione per confrontare le nuove richieste di connessione con le connessioni del pool.  Quando nessuna connessione nel pool può essere riutilizzata, il driver deve stabilire una nuova connessione, richiedendo pertanto le informazioni di connessione.  
  
 Poiché le informazioni di connessione possono provenire da più origini (stringa di connessione, gli attributi di connessione e DSN), il driver potrebbe essere necessario analizzare la stringa di connessione e risolvere il conflitto tra le origini dati in ogni chiamata di funzione precedente.  
  
 Pertanto, è stato introdotto un nuovo handle ODBC: SQL_HANDLE_DBC_INFO_TOKEN. Con SQL_HANDLE_DBC_INFO_TOKEN, un driver non è necessario analizzare la stringa di connessione e risolvere i conflitti nelle informazioni di connessione più volte. Poiché si tratta di una struttura di dati specifici del driver, il driver può archiviare i dati, ad esempio le informazioni di connessione o pool di ID.  
  
 Questo handle viene usato solo come un'interfaccia tra il gestore dei Driver e il driver. Un'applicazione non è possibile allocare l'handle direttamente.  
  
 Handle padre di questo handle è di tipo SQL_HANDLE_ENV, vale a dire che il driver può ottenere le informazioni sull'ambiente dal punto di controllo HENV durante la risoluzione di informazioni di connessione.  
  
 Ogni volta che ricevuta una nuova richiesta di connessione, gestione Driver allocherà un handle di tipo SQL_HANDLE_DBC_INFO_TOKEN per archiviare le informazioni di connessione, dopo la conferma che il driver supporta la consapevolezza di pool di connessioni. Al termine di uso dell'handle (ma prima di restituire alcuni codici restituiti, diverso da SQL_STILL_EXECUTING dal [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) o [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)), the Driver Manager consente di liberare l'handle. Pertanto, l'handle è creato dopo la chiamata di funzione SQLAllocHandle ed eliminati definitivamente dopo la chiamata SQLFreeHandle. Gestione Driver garantisce l'handle verrà liberata prima di liberare il HENV associato (quando [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) oppure [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) restituisce un errore).  
  
 Il driver deve modificare le funzioni seguenti per accettare il nuovo tipo di handle SQL_HANDLE_DBC_INFO_TOKEN:  
  
1.  [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 Gestione Driver garantisce che più thread non utilizzerà lo stesso handle SQL_HANDLE_DBC_INFO_TOKEN contemporaneamente. Pertanto, il modello di sincronizzazione di questo handle può essere molto semplice interno al driver. Gestione Driver non avranno un blocco di ambiente prima dell'allocazione e liberazione SQL_HANDLE_DBC_INFO_TOKEN.  
  
 La gestione di Driver **SQLAllocHandle** e **SQLFreeHandle** non accetta questo nuovo tipo di handle.  
  
 SQL_HANDLE_DBC_INFO_TOKEN potrebbero contenere informazioni riservate, ad esempio le credenziali. Di conseguenza, un driver in modo protetto necessario cancellare il buffer di memoria (tramite [SecureZeroMemory](https://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx)) che contiene le informazioni sensibili prima di rilasciare l'handle con **SQLFreeHandle**. Ogni volta che viene chiuso l'handle di ambiente di un'applicazione, tutti i pool di connessione associata verranno chiusa.  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>Pool di connessioni di Gestione driver algoritmo di classificazione  
 Questa sezione descrive l'algoritmo di classificazione per il pool di connessioni di gestione Driver. Gli sviluppatori di driver possono implementare lo stesso algoritmo per la compatibilità con le versioni precedenti. Questo algoritmo potrebbe non essere quello più adatto. È necessario perfezionare questo algoritmo è basato l'implementazione (in caso contrario, non è necessario implementare questa funzionalità).  
  
 Gestione Driver restituirà un valore integrale di classificazione da 0 a 100 per ogni connessione dal pool. 0 indica che la connessione non è possibile riutilizzare e 100 indica una soluzione perfetta individuata come corrispondenza. Si supponga la richiesta di connessione è denominata hRequest e la connessione esistente dal pool come hCandidate. Se una delle condizioni seguenti è false, hCandidate la connessione in pool non può essere riutilizzata per hRequest (the Driver Manager assegnerà un punteggio pari a 0).  
  
-   hCandidate e hRequest provengono da UNICODE API (ad esempio, SQLDriverConnectW) oppure ANSI API (ad esempio, SQLDriverConnectA). (Driver di UNICODE possibile comportamento diversi dato API ANSI e UNICODE API (vedere l'attributo di connessione SQL_ATTR_ANSI_APP)).  
  
-   hCandidate e hRequest vengono creati dalla funzione stessa. SQLDriverConnect o SQLConnect.  
  
-   La stringa di connessione utilizzata per aprire hCandidate deve essere identico hRequest, quando si usa SQLDriverConnect.  
  
-   Il nome utente ServerName (o DSN), e la password utilizzata per aprire hCandidate deve essere lo stesso utilizzato per aprire hRequest quando SQLConnect viene utilizzato.  
  
-   L'ID di sicurezza (SID) del thread corrente deve essere lo stesso SID utilizzato per aprire hCandidate.  
  
-   Per il driver che è dispendioso integrare e rimuovere (vedere la discussione relativa SQL_DTC_TRANSITION_COST nelle [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)), viene riutilizzata *hRequest* non deve richiedere un elenco aggiuntivo o unenlistment.  
  
 La tabella seguente illustra l'assegnazione di punteggio per scenari diversi.  
  
|Confronto tra gli attributi di connessione tra la connessione in pool e la richiesta|Nessuna integrazione / unenlistment|Richiede l'integrazione aggiuntiva / Unenlistment|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|Catalogo (SQL_ATTR_CURRENT_CATALOG) è diverso|60|50|  
|Alcuni attributi di connessione sono diversi, ma catalogo è lo stesso|90|70|  
|Tutti gli attributi di connessione perfettamente corrispondenti|100|80|  
  
## <a name="sequence-diagram"></a>Diagramma sequenza  
 Questo diagramma di sequenza Mostra il meccanismo di pooling base descritte in questo argomento. Visualizza solo l'uso di [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) ma [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) case è simile.  
  
 ![Diagramma di sequenza](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>Diagramma di stato  
 Questo diagramma di stato Mostra l'oggetto token info connessione, descritte in questo argomento. Il diagramma mostra solo [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) ma [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) case è simile. Poiché gestione Driver potrebbe essere necessario gestire gli errori in qualsiasi momento, gestione Driver può chiamare [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md) per qualsiasi stato.  
  
 ![Diagramma di stato](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>Vedere anche  
 [Pool di connessioni compatibile con il driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Riferimento dell'interfaccia del provider di servizi (SPI) ODBC](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)
