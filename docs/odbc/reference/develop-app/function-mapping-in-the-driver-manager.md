---
title: Mappatura delle funzioni in Gestione Driver Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db8e525bb7e8f3e167deb8061a4dd5b75073933c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305582"
---
# <a name="function-mapping-in-the-driver-manager"></a>Mapping di funzioni in Gestione driver
Gestione driver supporta due punti di ingresso per le funzioni che accettano argomenti stringa. La funzione non decorata (**SQLDriverConnect**) è il formato ANSI della funzione. Il formato Unicode è decorato con una *W* (**SQLDriverConnectW**.)  
  
 Il file di intestazione ODBC supporta anche le funzioni decorate con *un A,* (**SQLDriverConnectA**) per la comodità di applicazioni miste ANSI/Unicode. Le chiamate effettuate alle funzioni **A** sono in realtà chiamate nel punto di ingresso non decorato (**SQLDriverConnect**.)  
  
 Se l'applicazione viene compilata con il _UNICODE **#define**, il file di intestazione ODBC esegua il mapping delle chiamate di funzione non decorate (**SQLDriverConnect**) alla versione Unicode (**SQLDriverConnectW**).  
  
 Gestione Driver riconosce un driver come driver Unicode se **SQLConnectW** è supportato dal driver.  
  
 Se il driver è un driver Unicode, Gestione Driver effettua chiamate di funzione come segue:  
  
-   Passa una funzione senza argomenti stringa o parametri direttamente tramite il driver.  
  
-   Passa le funzioni Unicode (con il suffisso *W)* direttamente al driver.  
  
-   Converte una funzione ANSI (con il suffisso *A)* in una funzione Unicode (con il suffisso *W)* convertendo gli argomenti di stringa in caratteri Unicode e passa la funzione Unicode al driver.  
  
 Se il driver è un driver ANSI, Gestione Driver effettua chiamate di funzione come segue:  
  
-   Passa le funzioni senza argomenti stringa o parametri direttamente tramite il driver.  
  
-   Converte le funzioni Unicode (con il suffisso *W)* in una chiamata di funzione ANSI e la passa al driver.  
  
-   Passa una funzione ANSI direttamente al driver.  
  
 Gestione Driver è abilitato per Unicode internamente. Di conseguenza, le prestazioni ottimali vengono ottenute da un'applicazione Unicode che utilizza un driver Unicode, perché Gestione Driver passa semplicemente le funzioni Unicode al driver. Quando un'applicazione ANSI utilizza un driver ANSI, Gestione Driver deve convertire le stringhe da ANSI a Unicode durante l'elaborazione di alcune funzioni, ad esempio **SQLDriverConnect**. Dopo l'elaborazione della funzione, Gestione Driver deve quindi convertire la stringa Unicode in ANSI prima di inviare la funzione al driver ANSI.  
  
 Un'applicazione non deve modificare o leggere i buffer di parametri associati quando il driver restituisce SQL_STILL_EXECUTING o SQL_NEED_DATA. Gestione Driver lascia i buffer associati ad ANSI fino a quando il driver restituisce SQL_SUCCESS, SQL_SUCCESS_WITH_INFO o SQL_ERROR. Un'applicazione multithreading non deve accedere ai valori dei parametri associati su cui un altro thread sta eseguendo un'istruzione SQL. Gestione Driver converte i dati da Unicode ad ANSI "sul posto" e l'altro thread potrebbe visualizzare i dati ANSI in questi buffer mentre il driver sta ancora elaborando l'istruzione SQL. Le applicazioni che associano dati Unicode a un driver ANSI non devono associare due colonne diverse allo stesso indirizzo.
