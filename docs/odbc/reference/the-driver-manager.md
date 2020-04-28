---
title: Gestione driver | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286795"
---
# <a name="the-driver-manager"></a>Gestione driver
*Gestione driver* è una libreria che gestisce la comunicazione tra le applicazioni e i driver. In Microsoft® Windows® Platforms, ad esempio, gestione driver è una libreria di collegamento dinamico (DLL), scritta da Microsoft, che può essere ridistribuita dagli utenti di MDAC 2,8 SP1 SDK ridistribuibile.  
  
 Gestione driver è particolarmente utile per gli sviluppatori di applicazioni e risolve diversi problemi comuni a tutte le applicazioni. Sono incluse la determinazione del driver da caricare in base a un nome di origine dati, il caricamento e lo scaricamento di driver e la chiamata di funzioni nei driver.  
  
 Per capire il motivo per cui quest'ultimo è un problema, considerare cosa accadrebbe se l'applicazione chiamasse direttamente funzioni nel driver. A meno che l'applicazione non sia stata collegata direttamente a un driver specifico, sarebbe necessario compilare una tabella di puntatori alle funzioni in tale driver e chiamare tali funzioni in base al puntatore. L'utilizzo dello stesso codice per più di un driver alla volta aggiungerebbe un ulteriore livello di complessità. Per prima cosa, l'applicazione deve impostare un puntatore a funzione per puntare alla funzione corretta nel driver corretto e quindi chiamare la funzione tramite tale puntatore.  
  
 Gestione driver risolve questo problema fornendo un'unica posizione per chiamare ogni funzione. L'applicazione è collegata a gestione driver e chiama le funzioni ODBC in Gestione driver, non nel driver. L'applicazione identifica il driver e l'origine dati di destinazione con un *handle di connessione*. Quando carica un driver, gestione driver compila una tabella di puntatori alle funzioni in tale driver. Usa l'handle di connessione passato dall'applicazione per trovare l'indirizzo della funzione nel driver di destinazione e chiama tale funzione per indirizzo.  
  
 Nella maggior parte dei casi, gestione driver passa semplicemente le chiamate di funzione dall'applicazione al driver corretto. Implementa tuttavia anche alcune funzioni (**SQLDataSources**, **SQLDrivers**e **SQLGetFunctions**) ed esegue il controllo degli errori di base. Gestione driver, ad esempio, verifica che gli handle non siano puntatori null, che le funzioni vengano chiamate nell'ordine corretto e che alcuni argomenti della funzione siano validi. Per una descrizione completa degli errori controllati da Gestione driver, vedere la sezione di riferimento per ogni funzione e [Appendice B: tabelle di transizione dello stato ODBC](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Il ruolo principale finale di gestione driver è il caricamento e lo scaricamento dei driver. L'applicazione carica e Scarica solo Gestione driver. Quando si desidera utilizzare un determinato driver, viene chiamata una funzione di connessione (**SQLConnect**, **SQLDriverConnect**o **SQLBrowseConnect**) in Gestione driver e viene specificato il nome di un'origine dati o di un driver specifico, ad esempio "contabilità" o "SQL Server". Con questo nome, gestione driver esegue la ricerca delle informazioni sull'origine dati per il nome file del driver, ad esempio sqlsrvr. dll. Viene quindi caricato il driver (presupponendo che non sia già caricato), viene archiviato l'indirizzo di ogni funzione nel driver e viene chiamata la funzione di connessione nel driver, che quindi si inizializza e si connette all'origine dati.  
  
 Quando l'applicazione viene eseguita utilizzando il driver, viene chiamato **SQLConnect** in Gestione driver. Gestione driver chiama questa funzione nel driver, che si disconnette dall'origine dati. Tuttavia, gestione driver mantiene il driver in memoria nel caso in cui l'applicazione si riconnetta. Scarica il driver solo quando l'applicazione libera la connessione utilizzata dal driver o utilizza la connessione per un driver diverso e nessuna altra connessione utilizza il driver. Per una descrizione completa del ruolo di gestione driver per il caricamento e lo scaricamento dei driver, vedere [ruolo di gestione driver nel processo di connessione](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md).
