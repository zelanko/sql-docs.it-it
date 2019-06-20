---
title: Gestione Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC]
- ODBC architecture [ODBC], driver manager
- driver manager [ODBC], about driver manager
- ODBC driver manager [ODBC]
ms.assetid: 559e4de1-16c9-4998-94f5-6431122040cd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0c1ae3f098aea3886d5cb84a0bfcb7553a8181fa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62719735"
---
# <a name="the-driver-manager"></a>Gestione driver
Il *gestione Driver* è una libreria che gestisce la comunicazione tra applicazioni e driver. Ad esempio, su piattaforme Microsoft® Windows®, gestione Driver è una libreria di collegamento dinamico (DLL) che viene scritto da Microsoft e può essere ridistribuita dagli utenti del pacchetto ridistribuibile SP1 SDK di MDAC 2.8.  
  
 Gestione Driver esiste principalmente per motivi di praticità per gli autori di applicazioni e consente di risolvere alcuni dei problemi più comuni a tutte le applicazioni. Questi includono determinare quale driver per il caricamento basato sul nome dell'origine dati, il caricamento e lo scaricamento di driver e chiamata di funzioni nei driver.  
  
 Per visualizzare il motivo per cui quest'ultimo è un problema, si consideri cosa accadrebbe se l'applicazione ha chiamato le funzioni nel driver direttamente. A meno che l'applicazione è stata collegata direttamente a un driver specifico, sarebbe necessario creare una tabella di puntatori alle funzioni in tale driver e chiamare tali funzioni il puntatore. Con lo stesso codice per più di un driver in un momento aggiungere un ulteriore livello di complessità. L'applicazione verrebbe prima di tutto è necessario impostare un puntatore a funzione in modo da puntare alla funzione corretta nel driver corretto e quindi chiamare la funzione tramite tale puntatore.  
  
 Gestione Driver risolve questo problema, offrendo un'unica posizione per chiamare ogni funzione. L'applicazione viene collegata per le funzioni ODBC Driver Manager e le chiamate in Gestione Driver, non il driver. L'applicazione identifica l'origine di driver e i dati di destinazione con un *handle di connessione*. Quando viene caricato un driver, Driver Manager crea una tabella di puntatori alle funzioni in tale driver. Si utilizza l'handle di connessione passato dall'applicazione per trovare l'indirizzo della funzione del driver di destinazione e chiama tale funzione in base all'indirizzo.  
  
 Nella maggior parte, gestione Driver passa semplicemente le chiamate di funzione dall'applicazione per il driver corretto. Tuttavia, implementa inoltre alcune funzioni (**SQLDataSources**, **SQLDrivers**, e **SQLGetFunctions**) ed esegue il controllo degli errori di base. Gestione Driver, ad esempio, verifica che gli handle non sono puntatori null, che vengono chiamate le funzioni nell'ordine corretto e che determinati argomenti di funzione sono validi. Per una descrizione completa dei messaggi di errore controllata da Gestione Driver, vedere la sezione di riferimento per ogni funzione e [appendice b: Tabelle della transizione di stato ODBC](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Il ruolo principale finale di gestione Driver è caricamento e scaricamento di driver. L'applicazione carica e Scarica solo la gestione di Driver. Quando vuole usare un driver specifico, chiama una funzione di connessione (**SQLConnect**, **SQLDriverConnect**, o **SQLBrowseConnect**) in Gestione Driver e specifica il nome di una determinata origine dati o driver, ad esempio "Contabilità" o "SQL Server". Gestione Driver usando questo nome, cerca le informazioni di origine dati per il nome file del driver, ad esempio Sqlsrvr.dll. Quindi carica il driver (presupponendo che non sia già caricato), archivia l'indirizzo di ogni funzione nel driver e chiama la funzione di connessione nel driver, che quindi inizializza e si connette all'origine dati.  
  
 Quando viene eseguita l'applicazione usa il driver, viene chiamato **SQLDisconnect** in Gestione Driver. Gestione Driver chiama questa funzione nel driver che si disconnette dall'origine dati. Tuttavia, gestione Driver mantiene il driver in memoria nel caso in cui l'applicazione si riconnette a esso. Scarica il driver solo quando l'applicazione libera la connessione usata dal driver o utilizza la connessione per un driver diverso e non altre connessioni usano il driver. Per una descrizione completa del ruolo di gestione Driver nel caricamento e scaricamento di driver, vedere [ruolo di gestione Driver nel processo di connessione](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md).
