---
title: Mapping in Gestione Driver di funzioni | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], functions
- driver manager [ODBC], function mapping
- functions [ODBC], Unicode functions
ms.assetid: ff093b29-671a-4fc0-86c9-08a311a98e54
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2bfa535d4175c109e96098dd1e40e93be9521de2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069695"
---
# <a name="function-mapping-in-the-driver-manager"></a>Mapping di funzioni in Gestione driver
Gestione driver supporta due punti di ingresso per le funzioni che accettano argomenti stringa. La funzione non decorata (**SQLDriverConnect**) è il formato ANSI della funzione. Il formato Unicode è decorato con un *W* (**SQLDriverConnectW**.)  
  
 Il file di intestazione ODBC supporta anche funzioni decorate con un *A,* (**SQLDriverConnectA**) per semplificare il lavoro delle applicazioni ANSI o Unicode miste. Le chiamate effettuate per la **un** le funzioni sono effettivamente chiamate nel punto di ingresso non decorato (**SQLDriverConnect**.)  
  
 Se l'applicazione viene compilata con Unicode **#define**, il file di intestazione ODBC verrà eseguito il mapping le chiamate di funzione non decorati (**SQLDriverConnect**) per la versione Unicode (**SQLDriverConnectW** .)  
  
 Gestione Driver riconosce un driver come driver Unicode se **SQLConnectW** è supportata dal driver.  
  
 Se il driver è un driver di Unicode, gestione Driver effettua le chiamate di funzione come indicato di seguito:  
  
-   Restituisce una funzione senza parametri o gli argomenti di stringa direttamente tramite il driver.  
  
-   Passa le funzioni Unicode (con il *W* suffisso) direttamente tramite il driver.  
  
-   Converte una funzione di ANSI (con il *un'* suffisso) a una funzione Unicode (con il *W* suffisso) convertendo gli argomenti stringa in Unicode caratteri e restituisce la funzione Unicode al driver.  
  
 Se il driver è un driver ANSI, gestione Driver effettua le chiamate di funzione come indicato di seguito:  
  
-   Restituisce le funzioni senza argomenti di tipo stringa o i parametri direttamente tramite il driver.  
  
-   Converte le funzioni Unicode (con il *W* suffisso) in un formato ANSI chiamata di funzione e lo passa al driver.  
  
-   Restituisce una funzione di ANSI direttamente al driver.  
  
 Gestione Driver è abilitata per Unicode internamente. Di conseguenza, le prestazioni ottimali sono ottenuta da un'applicazione Unicode utilizzo di un driver di Unicode, perché Gestione Driver passa semplicemente le funzioni Unicode tramite il driver. Quando un'applicazione ANSI funziona con un driver ANSI, gestione Driver deve convertire le stringhe da ANSI in Unicode durante l'elaborazione di alcune funzioni, ad esempio **SQLDriverConnect**. Dopo la funzione di elaborazione, gestione Driver necessario riconvertire quindi la stringa Unicode in ANSI prima dell'invio la funzione al driver ANSI.  
  
 Un'applicazione non deve modificare o leggere propri buffer di parametri associati quando il driver restituisce SQL_NEED_DATA o SQL_STILL_EXECUTING. Gestione Driver lascia il buffer associato a ANSI fino a quando il driver restituisce SQL_SUCCESS, SQL_SUCCESS_WITH_INFO o SQL_ERROR. Un'applicazione multithreading non è consigliabile concedere l'accesso a tutti i valori di parametri associati che un altro thread è in esecuzione in un'istruzione SQL. Gestione Driver converte i dati da Unicode ad ANSI "sul posto" e l'altro thread potrebbe visualizzare dati ANSI tali buffer mentre il driver sta ancora elaborando l'istruzione SQL. Le applicazioni che associano i dati Unicode a un driver ANSI non necessario associare due colonne diverse per lo stesso indirizzo.
