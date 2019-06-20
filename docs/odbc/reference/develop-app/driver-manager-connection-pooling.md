---
title: Pool di connessioni di Gestione driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- pooled connections [ODBC]
- connecting to driver [ODBC], connection pooling
- connecting to data source [ODBC], connection pooling
ms.assetid: ee95ffdb-5aa1-49a3-beb2-7695b27c3df9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: efcd4c4b3dabc82b30d5b0e903dd8937ad3a7ce3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280422"
---
# <a name="driver-manager-connection-pooling"></a>Pool di connessioni di Gestione driver
Pool di connessioni consente a un'applicazione usare una connessione da un pool di connessioni che non è necessario stabilire nuovamente per ogni uso. Una volta una connessione sia stata creata e inserita in un pool, un'applicazione può riutilizzare la connessione senza eseguire il processo di connessione completa.  
  
 Usando una connessione in pool può causare miglioramenti significativi delle prestazioni, poiché le applicazioni possono salvare l'overhead causato dalla creazione di una connessione. Ciò risulta particolarmente significativo per le applicazioni di livello intermedio che si connettono tramite una rete o per le applicazioni che si connettono più volte e disconnettersi, ad esempio le applicazioni Internet.  
  
 Oltre a miglioramenti delle prestazioni, il pool di connessioni architettura consente a un ambiente e le connessioni associate a essere utilizzata da più componenti in un unico processo. Ciò significa che i componenti autonomi nello stesso processo possono interagire tra loro senza tener conto uno da altro. Una connessione in un pool di connessioni può essere utilizzata ripetutamente per più componenti.  
  
> [!NOTE]
>  Pool di connessioni può essere utilizzato da un'applicazione ODBC che esibisce ODBC 2. *x* comportamento, a condizione che l'applicazione può chiamare *SQLSetEnvAttr*. Quando si usa il pool di connessioni, l'applicazione non deve eseguire le istruzioni SQL che modificano il database o il contesto del database, ad esempio la modifica di \< *database * * nome*>, che viene modificato il catalogo utilizzato da un origine dati.  


 Un driver ODBC deve essere completamente thread-safe e connessioni devono non presentano affinità di thread per supportare il pool di connessioni. Ciò significa che il driver è in grado di gestire una chiamata in qualsiasi thread in qualsiasi momento ed è in grado di connettersi su un singolo thread, usare la connessione in un altro thread e disconnettere in un thread terzo.  
  
 Il pool di connessioni viene gestito da Gestione Driver. Le connessioni vengono recuperate dal pool quando l'applicazione chiama **SQLConnect** oppure **SQLDriverConnect** e restituiti al pool quando l'applicazione chiama **SQLDisconnect**. Le dimensioni del pool aumentano in modo dinamico, le allocazioni di risorse richiesto in base. Si riduce in base al timeout di inattività: Se una connessione rimane inattiva per un periodo di tempo (non è stato usato in una connessione), viene rimossa dal pool. Le dimensioni del pool sono limitata solo da vincoli di memoria e i limiti sul server.  
  
 Gestione Driver determina se una connessione specifica in un pool deve essere utilizzata secondo gli argomenti passati **SQLConnect** oppure **SQLDriverConnect**e in base agli attributi di connessione impostare dopo la connessione è stata allocata.  
  
 Quando Gestione Driver è il pool di connessioni, deve essere in grado di determinare se una connessione sta ancora lavorando prima di passare il timeout della connessione. In caso contrario, gestione Driver tiene d' passando il timeout della connessione inutilizzata per l'applicazione ogni volta che si verifica un errore di rete temporanei. Un nuovo attributo di connessione è stato definito in ODBC 3*x*: SQL_ATTR_CONNECTION_DEAD. Si tratta di un attributo di connessione di sola lettura che restituisce un oggetto SQL_CD_TRUE o SQL_CD_FALSE. Il valore SQL_CD_TRUE significa che la connessione è stata persa, mentre il valore SQL_CD_FALSE significa che la connessione è ancora attiva. (Driver conforme a versioni precedenti di ODBC possono anche supportare questo attributo.)  
  
 Un driver necessario implementare questa opzione in modo efficiente o rallenta le prestazioni di pool di connessioni. In particolare, una chiamata per ottenere questo attributo di connessione non dovrebbe provocare un round trip al server. Al contrario, un driver deve restituire l'ultimo stato noto della connessione. La connessione è inattivo se non è riuscita l'ultima trip al server e non inattivo se ha esito positivo l'ultima ottimizzazione dei viaggi.  
  
## <a name="remarks"></a>Note  
 Se una connessione è stata interrotta (segnalato tramite SQL_ATTR_CONNECTION_DEAD), gestione Driver ODBC comporta l'eliminazione della connessione tramite la chiamata delle SQLDisconnect nel driver. Le nuove richieste di connessione potrebbero non trovare una connessione usabile nel pool. Alla fine gestione Driver potrebbe creare una nuova connessione, supponendo che il pool è vuoto.  
  
 Per usare un pool di connessioni, un'applicazione esegue i passaggi seguenti:  
  
1.  Abilita il pool di connessioni tramite la chiamata **SQLSetEnvAttr** su cui impostare l'attributo di ambiente SQL_ATTR_CONNECTION_POOLING SQL_CP_ONE_PER_DRIVER o SQL_CP_ONE_PER_HENV. Prima che l'applicazione viene allocata per la connessione che il pool è necessario abilitare ambiente condiviso, è necessario effettuare questa chiamata. L'handle di ambiente nella chiamata a **SQLSetEnvAttr** deve essere impostato su null, il che rende SQL_ATTR_CONNECTION_POOLING un attributo a livello di processo. Se l'attributo è impostato su SQL_CP_ONE_PER_DRIVER, un pool di connessioni singola è supportato per ogni driver. Se un'applicazione funziona con molti driver e alcuni ambienti, ciò potrebbe essere più efficiente in quanto i confronti di un numero inferiore potrebbero essere necessari. Se impostato su SQL_CP_ONE_PER_HENV, un pool di connessioni singola è supportato per ogni ambiente. Se un'applicazione funziona con alcuni driver e molti ambienti, ciò potrebbe essere più efficiente in quanto i confronti di un numero inferiore potrebbero essere necessari. Pool di connessioni è disabilitato impostando SQL_ATTR_CONNECTION_POOLING SQL_CP_OFF.  
  
2.  Alloca un ambiente chiamando **SQLAllocHandle** con il *HandleType* argomento impostato su SQL_HANDLE_ENV. L'ambiente allocato da questa chiamata sarà un ambiente condiviso implicito perché il pool di connessioni è stato abilitato. Non viene determinato l'ambiente da utilizzare, tuttavia, finché **SQLAllocHandle** con un *HandleType* SQL_HANDLE_DBC viene chiamato su questo ambiente.  
  
3.  Alloca una connessione chiamando **SQLAllocHandle** con *InputHandle* impostato su SQL_HANDLE_DBC e il *InputHandle* impostato per l'handle di ambiente allocato per il pool di connessioni. Gestione Driver tenta di trovare un ambiente esistente che corrisponde agli attributi di ambiente impostati dall'applicazione. Se non esiste alcun ambiente di questo tipo, uno viene creato con un conteggio dei riferimenti (gestito da Gestione Driver) pari a 1. Se viene trovato un ambiente condiviso corrisponda, l'ambiente viene restituito all'applicazione e il conteggio dei riferimenti viene incrementato. (La connessione effettiva da utilizzare non è determinata da Gestione Driver finché **SQLConnect** oppure **SQLDriverConnect** viene chiamato.)  
  
4.  Le chiamate **SQLConnect** oppure **SQLDriverConnect** per stabilire la connessione. Gestione Driver utilizza le opzioni di connessione nella chiamata a **SQLConnect** (o le parole chiave di connessione nella chiamata a **SQLDriverConnect**) e impostare gli attributi di connessione dopo l'allocazione di connessione per stabilire la connessione nel pool deve essere utilizzata.  
  
    > [!NOTE]  
    >  Il modo in cui è associata una connessione richiesta per una connessione in pool è determinato dall'attributo SQL_ATTR_CP_MATCH ambiente. Per altre informazioni, vedere [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
     Le applicazioni ODBC tramite pool di connessioni devono chiamare [CoInitializeEx](https://go.microsoft.com/fwlink/?LinkID=116307) durante l'inizializzazione dell'applicazione e [CoUninitialize](https://go.microsoft.com/fwlink/?LinkId=116310) quando la chiusura dell'applicazione.  
  
5.  Le chiamate **SQLDisconnect** al termine della connessione. La connessione viene restituita al pool di connessioni e diventa disponibile per il riutilizzo.  
  
 Per un'analisi approfondita, vedere [limitazione delle richieste in Microsoft Data Access Components](https://go.microsoft.com/fwlink/?LinkId=120776).  
  
## <a name="connection-pooling-considerations"></a>Considerazioni sul pool di connessioni  
 Eseguire una delle azioni seguenti tramite un comando SQL (anziché tramite l'API ODBC) può influire sullo stato della connessione e causare problemi imprevisti quando è attivo il pool di connessioni:  
  
-   Apertura di una connessione e la modifica del database predefinito.  
  
-   Tramite l'istruzione SET per modificare le opzioni configurabili (tra cui l'opzione SET ROWCOUNT ANSI_NULL, IMPLICIT_TRANSACTIONS, SHOWPLAN, le statistiche, TEXTSIZE e DATEFORMAT).  
  
-   Creazione di tabelle e stored procedure temporanee.  
  
 Se una di queste azioni vengono eseguita di fuori dell'API ODBC, la persona successiva che usa la connessione erediterà automaticamente le impostazioni precedenti, le tabelle o procedure.  
  
> [!NOTE]  
>  Non si prevede alcune impostazioni deve essere presente nello stato della connessione. È sempre deve impostare lo stato di connessione nell'applicazione e assicurarsi che l'applicazione consente di rimuovere qualsiasi connessione inutilizzata le impostazioni di limitazione delle richieste.  
  
## <a name="driver-aware-connection-pooling"></a>Pool di connessioni compatibile con il driver  
 A partire da Windows 8, un driver ODBC può usare connessioni nel pool in modo più efficiente. Per altre informazioni, vedere [Driver-Aware Connection Pooling](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
## <a name="see-also"></a>Vedere anche  
 [La connessione a una Data sorgente o Driver](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [Sviluppo di un Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Limitazione delle richieste in Microsoft Data Access Components](https://go.microsoft.com/fwlink/?LinkId=120776)
