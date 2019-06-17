---
title: Recupero di una riga di dati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetch function [ODBC], fetching a row of data
- cursors [ODBC], fetching rows
- result sets [ODBC], fetching
- fetches [ODBC], row of data
ms.assetid: 16d4a380-0d83-456b-aeee-f10738944e86
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 012e454d03a0eb4ad16095353351d67e50d9586a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061519"
---
# <a name="fetching-a-row-of-data"></a>Recupero di una riga di dati
Per recuperare una riga di dati, un'applicazione chiama **SQLFetch**. **SQLFetch** possono essere chiamati con qualsiasi tipo di cursore, ma viene solo spostato nel set di righe in una direzione di tipo forward-only. **SQLFetch** sposta il cursore alla riga successiva e restituisce i dati per tutte le colonne che sono state associate con chiamate a **SQLBindCol**. Quando il cursore raggiunge la fine del risultato impostato, **SQLFetch** restituisce SQL_NO_DATA. Per esempi di chiamata **SQLFetch**, vedere [SQLBindCol usando](../../../odbc/reference/develop-app/using-sqlbindcol.md).  
  
 Esattamente come **SQLFetch** viene implementata è specifico del driver, ma generali modello è per il driver recuperare i dati per qualsiasi associato colonne dall'origine dati, convertirlo in base ai tipi di variabili associate e posizionare il dati convertiti nelle variabili stesse. Se il driver non è possibile convertire qualsiasi dato, **SQLFetch** restituisce un errore. L'applicazione può continuare il recupero di righe, ma i dati per la riga corrente vanno persi. Cosa accade ai dati delle colonne non associate dipende dal driver, ma la maggior parte dei driver di recuperare e rimuoverlo o mai recuperarla affatto.  
  
 Il driver imposta anche i valori di qualsiasi buffer di lunghezza/indicatore che sono stati associati. Se il valore dei dati per una colonna è NULL, il driver imposta il buffer di lunghezza/indicatore corrispondente su SQL_NULL_DATA. Se il valore dei dati non è NULL, il driver imposta il buffer di lunghezza/indicatore per la lunghezza in byte dei dati dopo la conversione. Se non è possibile determinare la lunghezza, come avviene, a volte con dati di tipo long che viene recuperati da più di una chiamata di funzione, il driver imposta il buffer di lunghezza/indicatore su SQL_NO_TOTAL. Per i tipi di dati a lunghezza fissa, ad esempio numeri interi e strutture di data, la lunghezza in byte è la dimensione del tipo di dati.  
  
 Per i dati a lunghezza variabile, ad esempio carattere e i dati binari, il driver verificherà la lunghezza in byte dei dati convertiti con la lunghezza in byte del buffer associato alla colonna; lunghezza del buffer viene specificata nella *BufferLength* nell'argomento **SQLBindCol**. Se la lunghezza in byte di dati convertiti è maggiore della lunghezza di byte del buffer, il driver tronca i dati per le dimensioni del buffer, restituisce la lunghezza non troncata nel buffer di lunghezza/indicatore, viene restituito SQL_SUCCESS_WITH_INFO e SQLSTATE 01004 (dati inserisce troncato) nei dati di diagnostica. L'unica eccezione è se un segnalibro a lunghezza variabile viene troncato quando restituito da **SQLFetch**, che restituisce SQLSTATE 22001 (dati String, troncati a destra).  
  
 Dati a lunghezza fissa non viene mai troncati, perché il driver presuppone che le dimensioni del buffer associate sono le dimensioni del tipo di dati. Il troncamento dei dati tende a essere rara, perché l'applicazione viene in genere associato un buffer sufficiente per contenere l'intero valore dei dati; Determina le dimensioni necessarie dai metadati. Tuttavia, l'applicazione potrebbe associare in modo esplicito un buffer di che indicare l'origine è troppo piccolo. Ad esempio, potrebbe recuperare e visualizzare i primi 20 caratteri di una descrizione di parte o i primi 100 caratteri di una colonna di testo lungo.  
  
 Dati di tipo carattere devono essere con terminazione null dal driver prima che venga restituito all'applicazione, anche se è stato troncato. Il carattere di terminazione null non è inclusa la lunghezza di byte restituita, ma richiedono spazio nel buffer associato. Si supponga, ad esempio, un'applicazione vengono utilizzate stringhe composte da dati di tipo carattere nel set di caratteri ASCII, un driver sono 50 caratteri dei dati da restituire e buffer dell'applicazione è 25 byte. Nel buffer dell'applicazione, il driver restituisce i primi 24 caratteri seguiti da un carattere di terminazione null. Nel buffer di lunghezza/indicatore, viene restituito una lunghezza in byte pari a 50.  
  
 L'applicazione può limitare il numero di righe nel set impostando l'attributo di istruzione SQL_ATTR_MAX_ROWS prima di eseguire l'istruzione che crea il risultato di set di risultati. Ad esempio, la modalità di anteprima in un'applicazione utilizzata per formattare i report deve solo dati sufficienti per visualizzare la prima pagina del report. Limitando le dimensioni del set di risultati, tale funzionalità viene eseguita più velocemente. Questo attributo dell'istruzione è progettato per ridurre il traffico di rete e potrebbe non essere supportato da tutti i driver.
