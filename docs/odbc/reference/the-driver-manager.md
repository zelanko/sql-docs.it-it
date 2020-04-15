---
title: Gestione driver Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 686a2b9673fb392f969a42f4cc86dd95a95668a6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286795"
---
# <a name="the-driver-manager"></a>Gestione driver
*Gestione Driver* è una libreria che gestisce la comunicazione tra applicazioni e driver. Ad esempio, su Microsoft® piattaforme Windows®, Gestione Driver è una libreria a collegamento dinamico (DLL) che viene scritta da Microsoft e può essere ridistribuita dagli utenti di MDAC 2.8 SP1 SDK ridistribuibile.  
  
 Gestione Driver esiste principalmente per comodità per gli autori di applicazioni e risolve una serie di problemi comuni a tutte le applicazioni. Questi includono la determinazione del driver da caricare in base al nome di un'origine dati, il caricamento e lo scaricamento dei driver e la chiamata di funzioni nei driver.  
  
 Per capire perché quest'ultimo è un problema, considerare cosa accadrebbe se l'applicazione ha chiamato funzioni nel driver direttamente. A meno che l'applicazione non sia collegata direttamente a un driver specifico, sarebbe necessario compilare una tabella di puntatori alle funzioni in tale driver e chiamare tali funzioni tramite puntatore. L'utilizzo dello stesso codice per più di un driver alla volta aggiungerebbe un altro livello di complessità. L'applicazione deve prima impostare un puntatore a funzione in modo che punti alla funzione corretta nel driver corretto e quindi chiamare la funzione tramite tale puntatore.  
  
 Gestione Driver risolve questo problema fornendo un'unica posizione per chiamare ogni funzione. L'applicazione è collegata a Gestione Driver e chiama le funzioni ODBC in Gestione Driver, non il driver. L'applicazione identifica il driver di destinazione e l'origine dati con un handle di *connessione*. Quando viene caricato un driver, Gestione Driver crea una tabella di puntatori alle funzioni in tale driver. Utilizza l'handle di connessione passato dall'applicazione per trovare l'indirizzo della funzione nel driver di destinazione e chiama tale funzione in base all'indirizzo.  
  
 Per la maggior parte, Gestione Driver passa semplicemente le chiamate di funzione dall'applicazione al driver corretto. Tuttavia, implementa anche alcune funzioni (**SQLDataSources**, **SQLDrivers**e **SQLGetFunctions**) ed esegue il controllo degli errori di base. Ad esempio, Gestione Driver controlla che gli handle non sono puntatori null, che le funzioni vengono chiamate nell'ordine corretto e che alcuni argomenti di funzione sono validi. Per una descrizione completa degli errori controllati da Gestione Driver, vedere la sezione di riferimento per ogni funzione e [Appendice B: Tabelle](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)di transizione dello stato ODBC .  
  
 Il ruolo principale finale di Gestione Driver è il caricamento e lo scaricamento dei driver. L'applicazione carica e scarica solo Gestione Driver. Quando si desidera utilizzare un driver specifico, chiama una funzione di connessione (**SQLConnect**, **SQLDriverConnect**o **SQLBrowseConnect**) in Gestione Driver e specifica il nome di una determinata origine dati o driver, ad esempio "Contabilità" o "SQL Server". Utilizzando questo nome, Gestione Driver cerca le informazioni sull'origine dati per il nome del file del driver, ad esempio Sqlsrvr.dll. Carica quindi il driver (presupponendo che non sia già caricato), archivia l'indirizzo di ogni funzione nel driver e chiama la funzione di connessione nel driver, che quindi si inizializza e si connette all'origine dati.  
  
 Al termine dell'applicazione utilizzando il driver, chiama **SQLDisconnect** in Gestione Driver. Gestione Driver chiama questa funzione nel driver, che si disconnette dall'origine dati. Tuttavia, Gestione Driver mantiene il driver in memoria nel caso in cui l'applicazione si riconnette ad esso. Scarica il driver solo quando l'applicazione libera la connessione utilizzata dal driver o utilizza la connessione per un driver diverso e nessun'altra connessione utilizza il driver. Per una descrizione completa del ruolo di Gestione Driver nel caricamento e nello scaricamento dei driver, vedere [Gestione Driver nel processo](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)di connessione .
