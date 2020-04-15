---
title: La soluzione ODBC - Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286754"
---
# <a name="the-odbc-solution"></a>Soluzione ODBC
La domanda, quindi, è come ODBC standardizzare l'accesso al database? Esistono due requisiti architettonici:  
  
-   Le applicazioni devono essere in grado di accedere a più DBS utilizzando lo stesso codice sorgente senza ricompilare o ricollegare.  
  
-   Le applicazioni devono essere in grado di accedere a più DBSMO contemporaneamente.  
  
 E c'è un'altra domanda, a causa della realtà del mercato:  
  
-   Quali funzionalità DBMS devono esporre ODBC? Solo le funzionalità comuni a tutti i DBMS o a qualsiasi funzionalità disponibile in qualsiasi DBMS  
  
 ODBC risolve questi problemi nel modo seguente:  
  
-   **ODBC è un'interfaccia a livello di chiamata.** Per risolvere il problema di come le applicazioni accedono a più DBPERSIST utilizzando lo stesso codice sorgente, ODBC definisce una CLI standard. Contiene tutte le funzioni nelle specifiche CLI di Open Group e ISO/IEC e fornisce funzioni aggiuntive comunemente richieste dalle applicazioni.  
  
     Per ogni DBMS che supporta ODBC è necessaria una libreria o un driver diverso. Il driver implementa le funzioni nell'API ODBC. Per utilizzare un driver diverso, non è necessario ricompilare o ricollegare l'applicazione. Al contrario, l'applicazione carica semplicemente il nuovo driver e chiama le funzioni in esso. Per accedere a più DBS contemporaneamente, l'applicazione carica più driver. La modalità di supportato dei driver è specifica del sistema operativo. Ad esempio, nel sistema operativo Microsoft® Windows®, i driver sono librerie a collegamento dinamico (DLL).  
  
-   **ODBC definisce una grammatica SQL standard.** Oltre a un'interfaccia a livello di chiamata standard, ODBC definisce una grammatica SQL standard. Questa grammatica è basata sulla specifica Open Group SQL CAE. Le differenze tra le due grammatiche sono minori e principalmente a causa delle differenze tra la grammatica SQL richiesta da SQL incorporato (Open Group) e una CLI (ODBC). Ci sono anche alcune estensioni alla grammatica per esporre le funzionalità linguistiche comunemente disponibili non coperte dalla grammatica Open Group.  
  
     Le applicazioni possono inviare istruzioni utilizzando ODBC o la grammatica specifica di DBMS. Se un'istruzione utilizza una grammatica ODBC diversa dalla grammatica specifica di DBMS, il driver la converte prima di inviarla all'origine dati. Tuttavia, tali conversioni sono rare perché la maggior parte dei DBS utilizza già la grammatica SQL standard.  
  
-   **ODBC fornisce una Gestione Driver per gestire l'accesso simultaneo a più DBS.** Anche se l'uso di driver risolve il problema di accedere a più DBS contemporaneamente, il codice per eseguire questa operazione può essere complesso. Le applicazioni progettate per funzionare con tutti i driver non possono essere collegate staticamente ad alcun driver. Al contrario, devono caricare i driver in fase di esecuzione e chiamare le funzioni in essi in essi tramite una tabella di puntatori a funzione. La situazione diventa più complessa se l'applicazione utilizza più driver contemporaneamente.  
  
     Anziché forzare ogni applicazione a eseguire questa operazione, ODBC fornisce un Driver Manager. Gestione Driver implementa tutte le funzioni ODBC, principalmente come chiamate pass-through alle funzioni ODBC nei driver, ed è collegato in modo statico all'applicazione o caricato dall'applicazione in fase di esecuzione. Pertanto, l'applicazione chiama le funzioni ODBC in base al nome in Gestione Driver, anziché dal puntatore in ogni driver.  
  
     Quando un'applicazione necessita di un driver specifico, richiede innanzitutto un handle di connessione con cui identificare il driver e quindi richiede che Gestione Driver caricare il driver. Gestione Driver carica il driver e memorizza l'indirizzo di ogni funzione nel driver. Per chiamare una funzione ODBC nel driver, l'applicazione chiama tale funzione in Gestione Driver e passa l'handle di connessione per il driver. Gestione Driver chiama quindi la funzione utilizzando l'indirizzo archiviato in precedenza.  
  
-   **ODBC espone un numero significativo di funzionalità DBMS, ma non richiede driver per supportarli tutti.** Se ODBC esponesse solo le funzionalità comuni a tutti i DBS, sarebbe di scarsa utilità; dopo tutto, il motivo per cui esistono così tanti DBS diversi oggi è che hanno caratteristiche diverse. Se ODBC esponesse tutte le funzionalità disponibili in qualsiasi DBMS, sarebbe impossibile per i driver da implementare.  
  
     Al contrario, ODBC espone un numero significativo di funzionalità, più di quelle supportate dalla maggior parte dei DBS, ma richiede che i driver implementino solo un sottoinsieme di tali funzionalità. I driver implementano le funzionalità rimanenti solo se sono supportate dal sistema DBMS sottostante o se scelgono di emularle. Pertanto, le applicazioni possono essere scritte per sfruttare le funzionalità di un singolo DBMS esposto dal driver per tale DBMS, per utilizzare solo le funzionalità utilizzate da tutti i DBMS o per verificare il supporto di una particolare funzionalità e reagire di conseguenza.  
  
     In modo che un'applicazione possa determinare quali funzionalità sono supportate da un driver e dal supporto DBMS, ODBC fornisce due funzioni (**SQLGetInfo** e **SQLGetFunctions**) che restituiscono informazioni generali sulle funzionalità del driver e DBMS e un elenco di funzioni supportate dal driver. ODBC definisce anche i livelli di conformità grammaticale API e SQL, che specificano ampi intervalli di funzionalità supportate dal driver. Per ulteriori informazioni, consultate [Livelli di conformità.](../../odbc/reference/develop-app/conformance-levels.md)  
  
     È importante ricordare che ODBC definisce un'interfaccia comune per tutte le funzionalità che espone. Per questo motivo, le applicazioni contengono codice specifico della funzionalità, non codice specifico DBMS, e possono utilizzare qualsiasi driver che espongono tali funzionalità. Uno dei vantaggi è che le applicazioni non devono essere aggiornate quando le funzionalità supportate da un DBMS sono migliorate; al contrario, quando viene installato un driver aggiornato, l'applicazione utilizza automaticamente le funzionalità perché il codice è specifico delle funzionalità, non specifico del driver o DBMS.Instead, when an updated driver is installed, the application automatically uses the features because its code is feature-specific, not driver-specific or DBMS-specific.
