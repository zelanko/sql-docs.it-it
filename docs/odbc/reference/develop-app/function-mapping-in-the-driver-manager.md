---
title: Mapping di funzioni in Gestione driver | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069695"
---
# <a name="function-mapping-in-the-driver-manager"></a>Mapping di funzioni in Gestione driver
Gestione driver supporta due punti di ingresso per le funzioni che accettano argomenti di stringa. La funzione non decorata (**SQLDriverConnect**) è il formato ANSI della funzione. Il formato Unicode è decorato con *W* (**SQLDriverConnectW**).  
  
 Il file di intestazione ODBC supporta inoltre le funzioni decorate ** con una (**SQLDriverConnectA**) per la praticità di applicazioni ANSI/Unicode miste. Le chiamate effettuate alle funzioni **a** sono in realtà chiamate al punto di ingresso non decorato (**SQLDriverConnect**).  
  
 Se l'applicazione viene compilata con il _UNICODE **#define**, il file di intestazione ODBC eseguirà il mapping delle chiamate di funzione non decorate (**SQLDriverConnect**) alla versione Unicode (**SQLDriverConnectW**).  
  
 Gestione driver riconosce un driver come driver Unicode se **SQLConnectW** è supportato dal driver.  
  
 Se il driver è un driver Unicode, gestione driver esegue le chiamate di funzione nel modo seguente:  
  
-   Passa una funzione senza argomenti o parametri stringa direttamente al driver.  
  
-   Passa le funzioni Unicode (con il suffisso *W* ) direttamente al driver.  
  
-   Converte una funzione ANSI (con *un* suffisso) in una funzione Unicode (con il suffisso *W* ) convertendo gli argomenti stringa in caratteri Unicode e passa la funzione Unicode al driver.  
  
 Se il driver è un driver ANSI, gestione driver esegue le chiamate di funzione nel modo seguente:  
  
-   Passa le funzioni senza argomenti o parametri stringa direttamente al driver.  
  
-   Converte le funzioni Unicode (con il suffisso *W* ) in una chiamata di funzione ANSI e la passa al driver.  
  
-   Passa una funzione ANSI direttamente al driver.  
  
 Gestione driver è abilitato per Unicode internamente. Di conseguenza, le prestazioni ottimali vengono ottenute da un'applicazione Unicode che utilizza un driver Unicode, perché Gestione driver passa semplicemente le funzioni Unicode al driver. Quando un'applicazione ANSI utilizza un driver ANSI, è necessario che Gestione driver converta le stringhe da ANSI a Unicode durante l'elaborazione di alcune funzioni, ad esempio **SQLDriverConnect**. Dopo l'elaborazione della funzione, gestione driver deve quindi convertire la stringa Unicode nuovamente in ANSI prima di inviare la funzione al driver ANSI.  
  
 Un'applicazione non deve modificare o leggere i buffer dei parametri associati quando il driver restituisce SQL_STILL_EXECUTING o SQL_NEED_DATA. Gestione driver lascia i buffer associati a ANSI fino a quando il driver non restituisce SQL_SUCCESS, SQL_SUCCESS_WITH_INFO o SQL_ERROR. Un'applicazione multithreading non deve accedere a tutti i valori dei parametri associati su cui è in esecuzione un'istruzione SQL in un altro thread. Gestione driver converte i dati da Unicode ad ANSI "sul posto" e l'altro thread potrebbe visualizzare i dati ANSI in questi buffer mentre il driver sta ancora elaborando l'istruzione SQL. Le applicazioni che associano dati Unicode a un driver ANSI non devono associare due colonne diverse allo stesso indirizzo.
