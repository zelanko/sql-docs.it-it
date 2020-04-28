---
title: Soluzione ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], using ODBC
ms.assetid: 34b80790-e010-4b90-8eaa-03189f5d8986
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2b35883ff4d621f0ecc092020ad744455281dd63
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286754"
---
# <a name="the-odbc-solution"></a>Soluzione ODBC
La domanda, quindi, è in che modo ODBC standardizza l'accesso al database? Esistono due requisiti architetturali:  
  
-   Le applicazioni devono essere in grado di accedere a più DBMS utilizzando lo stesso codice sorgente senza ricompilare o ricollegare.  
  
-   Le applicazioni devono essere in grado di accedere contemporaneamente a più DBMS.  
  
 E c'è un'altra domanda, a causa della realtà del Marketplace:  
  
-   Quali funzionalità DBMS devono essere esposte da ODBC? Solo le funzionalità comuni a tutti i DBMS o a qualsiasi funzionalità disponibile in qualsiasi sistema DBMS?  
  
 ODBC risolve questi problemi nel modo seguente:  
  
-   **ODBC è un'interfaccia a livello di chiamata.** Per risolvere il problema del modo in cui le applicazioni accedono a più DBMS utilizzando lo stesso codice sorgente, ODBC definisce un'interfaccia della riga di comando standard. Sono incluse tutte le funzioni nelle specifiche dell'interfaccia della riga di comando di Open Group e ISO/IEC e fornisce funzioni aggiuntive comunemente richieste dalle applicazioni.  
  
     Per ogni DBMS che supporta ODBC è necessaria una libreria o un driver diverso. Il driver implementa le funzioni nell'API ODBC. Per usare un driver diverso, non è necessario ricompilare o ricollegare l'applicazione. Al contrario, l'applicazione carica semplicemente il nuovo driver e chiama le funzioni al suo interno. Per accedere simultaneamente a più DBMS, l'applicazione carica più driver. Il modo in cui sono supportati i driver è specifico del sistema operativo. Ad esempio, nel sistema operativo Microsoft® Windows®, i driver sono librerie a collegamento dinamico (dll).  
  
-   **ODBC definisce una grammatica SQL standard.** Oltre a un'interfaccia standard a livello di chiamata, ODBC definisce una grammatica SQL standard. Questa grammatica è basata sulla specifica SQL CAE del gruppo aperto. Le differenze tra le due grammatiche sono minime e principalmente a causa delle differenze tra la grammatica SQL richiesta da Embedded SQL (Open Group) e un'interfaccia della riga di comando (ODBC). Esistono inoltre alcune estensioni della grammatica per esporre le funzionalità del linguaggio comunemente disponibili non coperte dalla grammatica dei gruppi aperti.  
  
     Le applicazioni possono inviare istruzioni utilizzando una grammatica specifica ODBC o DBMS. Se un'istruzione utilizza la grammatica ODBC diversa dalla grammatica specifica di DBMS, il driver la converte prima di inviarla all'origine dati. Tuttavia, tali conversioni sono rare perché la maggior parte dei DBMS usa già la grammatica SQL standard.  
  
-   **ODBC fornisce una gestione driver per gestire l'accesso simultaneo a più DBMS.** Anche se l'uso dei driver risolve il problema dell'accesso simultaneo a più DBMS, il codice per eseguire questa operazione può risultare complesso. Le applicazioni progettate per funzionare con tutti i driver non possono essere collegate in modo statico ad alcun driver. Devono invece caricare i driver in fase di esecuzione e chiamare le funzioni in essi tramite una tabella di puntatori a funzione. La situazione diventa più complessa se l'applicazione usa più driver contemporaneamente.  
  
     Anziché forzare ogni applicazione, ODBC fornisce una gestione driver. Gestione driver implementa tutte le funzioni ODBC, principalmente come chiamate pass-through alle funzioni ODBC nei driver, ed è collegata in modo statico all'applicazione o caricata dall'applicazione in fase di esecuzione. Pertanto, l'applicazione chiama le funzioni ODBC in base al nome in Gestione driver, anziché in base al puntatore in ogni driver.  
  
     Quando un'applicazione necessita di un driver specifico, richiede prima di tutto un handle di connessione con il quale identificare il driver e quindi le richieste di caricamento del driver da parte di gestione driver. Gestione driver carica il driver e archivia l'indirizzo di ogni funzione nel driver. Per chiamare una funzione ODBC nel driver, l'applicazione chiama tale funzione in Gestione driver e passa l'handle di connessione per il driver. Gestione driver chiama quindi la funzione utilizzando l'indirizzo archiviato in precedenza.  
  
-   **ODBC espone un numero significativo di funzionalità DBMS ma non richiede che i driver li supportino tutti.** Se ODBC esponeva solo le funzionalità comuni a tutti i DBMS, sarebbe poco utile. Dopo tutto, il motivo per cui esistono molti sistemi DBMS diversi è che hanno diverse funzionalità. Se ODBC ha esposto tutte le funzionalità disponibili in un sistema DBMS, non sarebbe possibile che i driver implementino.  
  
     ODBC, invece, espone un numero significativo di funzionalità: più che sono supportate dalla maggior parte dei DBMS, ma richiede che i driver implementino solo un subset di tali funzionalità. I driver implementano le funzionalità rimanenti solo se sono supportati dal sistema DBMS sottostante o se scelgono di emularli. In questo modo, le applicazioni possono essere scritte per sfruttare le funzionalità di un singolo sistema DBMS esposto dal driver per tale DBMS, per usare solo le funzionalità usate da tutti i DBMS o per verificare il supporto di una particolare funzionalità e rispondere di conseguenza.  
  
     In modo che un'applicazione possa determinare quali funzionalità sono supportate da un driver e da DBMS, ODBC fornisce due funzioni (**SQLGetInfo** e **SQLGetFunctions**) che restituiscono informazioni generali sulle funzionalità del driver e del sistema DBMS e un elenco di funzioni supportate dal driver. ODBC definisce inoltre i livelli di conformità dell'API e della grammatica SQL, che specificano ampi intervalli di funzionalità supportate dal driver. Per altre informazioni, vedere [livelli di conformità](../../odbc/reference/develop-app/conformance-levels.md).  
  
     È importante ricordare che ODBC definisce un'interfaccia comune per tutte le funzionalità che espone. Per questo motivo, le applicazioni contengono codice specifico della funzionalità, non codice specifico di DBMS e possono usare qualsiasi driver che esponga tali funzionalità. Un vantaggio è che non è necessario aggiornare le applicazioni quando le funzionalità supportate da un sistema DBMS sono migliorate; al contrario, quando viene installato un driver aggiornato, l'applicazione usa automaticamente le funzionalità perché il codice è specifico della funzionalità, non specifico del driver o DBMS.
