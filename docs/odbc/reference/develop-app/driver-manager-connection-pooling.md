---
title: Pool di connessioni di Gestione driver - Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 84ccc0db8f9a54eecc8337ca5efbc7b4c4baa239
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305822"
---
# <a name="driver-manager-connection-pooling"></a>Pool di connessioni di Gestione driver
Il pool di connessioni consente a un'applicazione di utilizzare una connessione da un pool di connessioni che non è necessario ristabilire per ogni utilizzo. Dopo aver creato una connessione e inserito in un pool, un'applicazione può riutilizzare tale connessione senza eseguire il processo di connessione completo.  
  
 L'utilizzo di una connessione in pool può comportare miglioramenti significativi delle prestazioni, poiché le applicazioni possono risparmiare l'overhead necessario per creare una connessione. Ciò può essere particolarmente significativo per le applicazioni di livello intermedio che si connettono in rete o per le applicazioni che si connettono e si disconnettono ripetutamente, ad esempio le applicazioni Internet.This can be particularly significant for middle-tier applications that connect over a network or for applications that repeatedly connect and disconnect, such as Internet applications.  
  
 Oltre a migliorare le prestazioni, l'architettura del pool di connessioni consente a un ambiente e alle connessioni associate di essere utilizzati da più componenti in un unico processo. Ciò significa che i componenti autonomi nello stesso processo possono interagire tra loro senza essere consapevoli l'uno dell'altro. Una connessione in un pool di connessioni può essere utilizzata ripetutamente da più componenti.  
  
> [!NOTE]
>  Il pool di connessioni può essere utilizzato da un'applicazione ODBC che ospita ODBC 2. *x,* purché l'applicazione possa chiamare *SQLSetEnvAttr*. Quando si utilizza il pool di connessioni, l'applicazione non deve eseguire istruzioni SQL \<che modificano il database o il contesto del database, ad esempio la modifica del nome del *database*>, che modifica il catalogo utilizzato da un'origine dati.  


 Un driver ODBC deve essere completamente thread-safe e le connessioni non devono avere affinità di thread per supportare il pool di connessioni. Ciò significa che il driver è in grado di gestire una chiamata su qualsiasi thread in qualsiasi momento ed è in grado di connettersi su un thread, di utilizzare la connessione su un altro thread e di disconnettersi su un terzo thread.  
  
 Il pool di connessioni viene gestito da Gestione Driver. Le connessioni vengono disegnate dal pool quando l'applicazione chiama **SQLConnect** o **SQLDriverConnect** e vengono restituite al pool quando l'applicazione chiama **SQLDisconnect**. La dimensione del pool aumenta in modo dinamico, in base alle allocazioni di risorse richieste. Si riduce in base al timeout di inattività: se una connessione è inattiva per un periodo di tempo (non è stata utilizzata in una connessione), viene rimossa dal pool. La dimensione del pool è limitata solo da vincoli di memoria e limiti sul server.  
  
 Gestione Driver determina se una connessione specifica in un pool deve essere utilizzata in base agli argomenti passati in **SQLConnect** o **SQLDriverConnect**e in base agli attributi di connessione impostati dopo l'allocazione della connessione.  
  
 Quando Gestione Driver sta pooling connessioni, deve essere in grado di determinare se una connessione è ancora funzionante prima di distribuire la connessione. In caso contrario, Gestione Driver continua a distribuire la connessione inattiva all'applicazione ogni volta che si verifica un errore di rete temporaneo. In ODBC 3 *.x*SQL_ATTR_CONNECTION_DEAD . Si tratta di un attributo di connessione di sola lettura che restituisce SQL_CD_TRUE o SQL_CD_FALSE. Il valore SQL_CD_TRUE indica che la connessione è stata persa, mentre il valore SQL_CD_FALSE significa che la connessione è ancora attiva. Anche i driver conformi alle versioni precedenti di ODBC possono supportare questo attributo.  
  
 Un driver deve implementare questa opzione in modo efficiente o comprometterà le prestazioni del pool di connessioni. In particolare, una chiamata per ottenere questo attributo di connessione non deve causare un round trip al server. Al contrario, un driver deve restituire semplicemente l'ultimo stato noto della connessione. La connessione è morta se l'ultimo viaggio al server non è riuscito e non è morto se l'ultimo viaggio ha avuto esito positivo.  
  
## <a name="remarks"></a>Osservazioni  
 Se una connessione è stata persa (segnalato tramite SQL_ATTR_CONNECTION_DEAD), Gestione Driver ODBC distruggerà tale connessione chiamando SQLDisconnect nel driver. Le nuove richieste di connessione potrebbero non trovare una connessione utilizzabile nel pool. Alla fine Gestione Driver potrebbe effettuare una nuova connessione, presupponendo che il pool è vuoto.  
  
 Per utilizzare un pool di connessioni, un'applicazione esegue i passaggi seguenti:To use a connection pool, an application performs the following steps:  
  
1.  Abilita il pool di connessioni chiamando **SQLSetEnvAttr** per impostare l'attributo di ambiente SQL_ATTR_CONNECTION_POOLING su SQL_CP_ONE_PER_DRIVER o SQL_CP_ONE_PER_HENV. Questa chiamata deve essere effettuata prima che l'applicazione allochi l'ambiente condiviso per il quale deve essere abilitato il pool di connessioni. L'handle di ambiente nella chiamata a **SQLSetEnvAttr** deve essere impostato su null, il che rende SQL_ATTR_CONNECTION_POOLING un attributo a livello di processo. Se l'attributo è impostato su SQL_CP_ONE_PER_DRIVER, per ogni driver è supportato un singolo pool di connessioni. Se un'applicazione funziona con molti driver e pochi ambienti, potrebbe essere più efficiente perché potrebbero essere necessari meno confronti. Se impostato su SQL_CP_ONE_PER_HENV, è supportato un singolo pool di connessioni per ogni ambiente. Se un'applicazione funziona con molti ambienti e pochi driver, questo potrebbe essere più efficiente perché potrebbe essere necessario un minor numero di confronti. Il pool di connessioni viene disabilitato impostando SQL_ATTR_CONNECTION_POOLING su SQL_CP_OFF.  
  
2.  Alloca un ambiente chiamando **SQLAllocHandle** con il *HandleType* argomento impostato su SQL_HANDLE_ENV. L'ambiente allocato da questa chiamata sarà un ambiente condiviso implicito perché il pool di connessioni è stato abilitato. L'ambiente da utilizzare non viene tuttavia determinato fino a quando **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_DBC viene chiamato su questo ambiente.  
  
3.  Alloca una connessione chiamando **SQLAllocHandle** con *InputHandle* impostato su SQL_HANDLE_DBC e *InputHandle* impostato sull'handle di ambiente allocato per il pool di connessioni. Gestione Driver tenta di trovare un ambiente esistente che corrisponde agli attributi di ambiente impostati dall'applicazione. Se tale ambiente non esiste, ne viene creato uno, con un conteggio dei riferimenti (mantenuto da Gestione Driver) pari a 1. Se viene trovato un ambiente condiviso corrispondente, l'ambiente viene restituito all'applicazione e il conteggio dei riferimenti viene incrementato. La connessione effettiva da utilizzare non è determinata da Gestione Driver fino a quando non viene chiamato **SQLConnect** o **SQLDriverConnect.**  
  
4.  Chiama **SQLConnect** o **SQLDriverConnect** per effettuare la connessione. Gestione Driver utilizza le opzioni di connessione nella chiamata a **SQLConnect** (o le parole chiave di connessione nella chiamata a **SQLDriverConnect**) e gli attributi di connessione impostati dopo l'allocazione di connessione per determinare quale connessione nel pool deve essere utilizzata.  
  
    > [!NOTE]  
    >  Il modo in cui una connessione richiesta corrisponde a una connessione in pool è determinato dall'attributo di ambiente SQL_ATTR_CP_MATCH. Per ulteriori informazioni, vedere [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
     Le applicazioni ODBC che utilizzano il pool di connessioni devono chiamare [CoInitializeEx](https://go.microsoft.com/fwlink/?LinkID=116307) durante l'inizializzazione dell'applicazione e [CoUninitialize](https://go.microsoft.com/fwlink/?LinkId=116310) alla chiusura dell'applicazione.  
  
5.  Chiama **SQLDisconnect** al termine della connessione. La connessione viene restituita al pool di connessioni e diventa disponibile per il riutilizzo.  
  
 Per una discussione approfondita, vedere [Pooling in Microsoft Data Access Components](https://go.microsoft.com/fwlink/?LinkId=120776).  
  
## <a name="connection-pooling-considerations"></a>Considerazioni sul pool di connessioniConnection Pooling Considerations  
 L'esecuzione di una delle seguenti azioni utilizzando un comando SQL (anziché tramite l'API ODBC) può influire sullo stato della connessione e causare problemi imprevisti quando è attivo il pool di connessioni:  
  
-   Apertura di una connessione e modifica del database predefinito.  
  
-   Utilizzo dell'istruzione SET per modificare le opzioni configurabili (inclusi SET ROWCOUNT, ANSI_NULL, IMPLICIT_TRANSACTIONS, SHOWPLAN, STATISTICS, TEXTSI-E e DATEFORMAT).  
  
-   Creazione di tabelle temporanee e stored procedure.  
  
 Se una di queste azioni viene eseguita all'esterno dell'API ODBC, la persona successiva che utilizza la connessione erediterà automaticamente le impostazioni, le tabelle o le procedure precedenti.  
  
> [!NOTE]  
>  Non aspettatevi che alcune impostazioni siano presenti nello stato di connessione. È sempre necessario impostare lo stato della connessione nell'applicazione e assicurarsi che l'applicazione rimuova le impostazioni del pool di connessioni inutilizzate.  
  
## <a name="driver-aware-connection-pooling"></a>Pool di connessioni compatibile con il driver  
 A partire da Windows 8, un driver ODBC può utilizzare le connessioni nel pool in modo più efficiente. Per ulteriori informazioni, vedere [Pool di connessioni in base](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)al driver .  
  
## <a name="see-also"></a>Vedere anche  
 [Connessione a un'origine dati o a un driverConnecting to a Data Source or Driver](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [Sviluppo di un driver ODBCDeveloping an ODBC Driver](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Raggruppamento in Microsoft Data Access Components](https://go.microsoft.com/fwlink/?LinkId=120776)
