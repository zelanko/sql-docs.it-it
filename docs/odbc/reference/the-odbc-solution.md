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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e6992e084c210cea1b95157744addfd40180fccb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039337"
---
# <a name="the-odbc-solution"></a>Soluzione ODBC
La domanda, quindi, è come ODBC standardizzare l'accesso al database? Esistono due requisiti di architettura:  
  
-   Le applicazioni devono essere in grado di accedere con lo stesso codice sorgente senza dover ricompilare o ricollegamento più DBMS.  
  
-   Le applicazioni devono essere in grado di accedere simultaneamente più DBMS.  
  
 Ed è presente un'altra domanda, a causa di realtà marketplace:  
  
-   Quali funzionalità DBMS deve esporre ODBC? Solo le funzionalità comuni a tutti i DBMS o tutte le funzionalità che sono disponibile in qualsiasi sistema DBMS?  
  
 ODBC risolve questi problemi nel modo seguente:  
  
-   **ODBC è un'interfaccia a livello di chiamata.** Per risolvere il problema di come applicazioni di accedere più DBMS usando lo stesso codice sorgente, ODBC definisce un'interfaccia della riga di comando standard. Contiene tutte le funzioni nelle specifiche dell'interfaccia della riga da Open Group e ISO/IEC e fornisce funzioni aggiuntive comunemente richieste dalle applicazioni.  
  
     Un'altra libreria o driver, è necessario per ogni sistema DBMS che supporti ODBC. Il driver implementa le funzioni dell'API ODBC. Per usare un driver diverso, l'applicazione non dovrà essere ricompilato o ricollegare. Al contrario, l'applicazione semplicemente carica il nuovo driver e chiama le funzioni in essa. Per accedere simultaneamente più DBMS, l'applicazione carica più driver. Modo in cui sono supportati i driver è specifico del sistema operativo. Ad esempio, nel sistema operativo Microsoft® Windows®, i driver sono librerie a collegamento dinamico (DLL).  
  
-   **ODBC definisce una grammatica SQL standard.** Oltre a un'interfaccia a livello di chiamata standard, ODBC definisce una grammatica SQL standard. L'espressione è basato sulla specifica Open gruppo SQL CAE. Differenze tra le grammatiche di due sono minori e principalmente a causa di differenze tra la grammatica SQL richiesto da incorporati della riga di comando (ODBC) e SQL (Open Group). Esistono anche alcune estensioni per la grammatica per esporre le funzionalità di linguaggio comunemente disponibili non coperti dalla grammatica di Open Group.  
  
     Le applicazioni possono inviare le istruzioni che utilizzano ODBC o specifici del DBMS grammatica. Se un'istruzione Usa grammatica ODBC che è diversa dalla grammatica specifici del DBMS, il driver converte prima dell'invio all'origine dati. Tuttavia, tali conversioni sono rari, poiché la maggior parte dei DBMS usano già la sintassi SQL standard.  
  
-   **ODBC fornisce un Driver Manager per gestire l'accesso simultaneo da più DBMS.** Sebbene l'utilizzo di driver risolve il problema di accedere contemporaneamente più DBMS, il codice per eseguire questa operazione può essere complesso. Le applicazioni che sono progettate per funzionare con tutti i driver non possono essere collegate staticamente per tutti i driver. Ma è necessario caricare i driver in fase di esecuzione e chiamare le funzioni in essi contenuti tramite una tabella di puntatori a funzione. La situazione diventa più complessa se l'applicazione usa più driver contemporaneamente.  
  
     Anziché richiedere ogni applicazione a tale scopo, ODBC offre una gestione Driver. Gestione Driver implementa tutte le funzioni ODBC - principalmente come pass-through delle chiamate alle funzioni ODBC driver - in ed è staticamente collegata all'applicazione o caricata dall'applicazione in fase di esecuzione. Di conseguenza, l'applicazione chiama funzioni ODBC dal nome in Gestione Driver, anziché il puntatore in tutti i driver.  
  
     Quando un'applicazione necessita di un driver specifico, verrà richiesta prima di tutto un handle di connessione con il quale identificare i driver e quindi le richieste che Gestione Driver caricare il driver. Gestione Driver viene caricato il driver e archivia l'indirizzo di ogni funzione nel driver. Per chiamare una funzione ODBC nel driver, l'applicazione chiama tale funzione in Gestione Driver e passa l'handle di connessione per il driver. Gestione Driver quindi chiama la funzione usando l'indirizzo che archiviato in precedenza.  
  
-   **ODBC espone un numero significativo di funzionalità DBMS, ma non hanno bisogno di driver per supportare tutti gli elementi.** Se ODBC esposte solo le funzionalità comuni a tutti i DBMS, sarebbe poco utili; Dopo tutto, pertanto molti diversi DBMS oggi esistono infatti che dispongono di diverse funzionalità. Se ODBC esposte tutte le funzionalità sono disponibile in qualsiasi sistema DBMS, sarebbe impossibile ritestare per implementare i driver.  
  
     Al contrario, ODBC espone un numero significativo di funzionalità - altre superiore a quello supportato dalla maggior parte dei DBMS - ma richiede che i driver per implementare solo un subset di tali funzionalità. I driver di implementano le funzionalità rimanenti solo se sono supportate dal sistema DBMS sottostante o se si sceglie di emularli. Di conseguenza, è possibile creare applicazioni di sfruttare le funzionalità del sistema DBMS per una singola come viene esposta dal driver per DBMS, usare solo le funzionalità usate dai sistemi DBMS tutti, o per verificare il supporto di una particolare funzionalità e reagire di conseguenza.  
  
     In modo che un'applicazione può determinare quali funzionalità di un driver e il supporto di DBMS, sono disponibili due funzioni ODBC (**SQLGetInfo** e **SQLGetFunctions**) che restituiscono informazioni generali sui driver e DBMS funzionalità e un elenco di funzioni il driver supporta. Anche ODBC definisce già API e SQL grammatica livelli di conformità, che specificano gli intervalli ampi di funzionalità supportato dal driver. Per altre informazioni, vedere [livelli di conformità](../../odbc/reference/develop-app/conformance-levels.md).  
  
     È importante tenere presente che ODBC definisce un'interfaccia comune per tutte le funzionalità che esposte. Per questo motivo, le applicazioni contengono funzionalità specifiche del codice, non specifici del DBMS e possono usare i driver di espongano tali funzionalità. Un vantaggio di questo approccio è che le applicazioni non sono necessario essere aggiornati quando vengono migliorate le funzionalità supportate da un sistema DBMS; al contrario, quando viene installato un driver aggiornato, l'applicazione usa automaticamente le funzionalità specifiche delle funzionalità, non specifiche del driver o specifici del DBMS poiché il relativo codice.
