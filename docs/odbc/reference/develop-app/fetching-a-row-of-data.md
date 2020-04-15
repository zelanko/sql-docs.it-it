---
title: Recupero di una riga di dati Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a702f561b756d5305020df9f015d3ea4b444caa6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305672"
---
# <a name="fetching-a-row-of-data"></a>Recupero di una riga di dati
Per recuperare una riga di dati, un'applicazione chiama **SQLFetch**. **SQLFetch** può essere chiamato con qualsiasi tipo di cursore, ma sposta solo il cursore del set di righe in una direzione forward-only. **SQLFetch** sposta il cursore alla riga successiva e restituisce i dati per tutte le colonne associate con chiamate a **SQLBindCol**. Quando il cursore raggiunge la fine del set di risultati, **SQLFetch** restituisce SQL_NO_DATA. Per esempi di chiamata a **SQLFetch**, vedere Utilizzo di [SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).  
  
 Esattamente come **SQLFetch** viene implementato è specifico del driver, ma il modello generale è per il driver per recuperare i dati per tutte le colonne associate dall'origine dati, convertirli in base ai tipi delle variabili associate e inserire i dati convertiti in tali variabili. Se il driver non è in grado di convertire i dati, **SQLFetch** restituisce un errore. L'applicazione può continuare a recuperare righe, ma i dati per la riga corrente vengono persi. Ciò che accade ai dati per le colonne non associate dipende dal driver, ma la maggior parte dei driver lo recupera ed elimina o non li recupera mai affatto.  
  
 Il driver imposta anche i valori di qualsiasi buffer di lunghezza/indicatore che sono stati associati. Se il valore dei dati per una colonna è NULL, il driver imposta il buffer di lunghezza/indicatore corrispondente su SQL_NULL_DATA. Se il valore dei dati non è NULL, il driver imposta il buffer di lunghezza/indicatore sulla lunghezza in byte dei dati dopo la conversione. Se questa lunghezza non può essere determinata, come talvolta accade con i dati long recuperati da più chiamate di funzione, il driver imposta il buffer di lunghezza/indicatore su SQL_NO_TOTAL. Per i tipi di dati a lunghezza fissa, ad esempio numeri interi e strutture di data, la lunghezza in byte è la dimensione del tipo di dati.  
  
 Per i dati a lunghezza variabile, ad esempio i dati di tipo carattere e binario, il driver controlla la lunghezza in byte dei dati convertiti rispetto alla lunghezza in byte del buffer associata alla colonna. la lunghezza del buffer è specificata nell'argomento *BufferLength* in **SQLBindCol**. Se la lunghezza in byte dei dati convertiti è maggiore della lunghezza in byte del buffer, il driver tronca i dati per adattarli al buffer, restituisce la lunghezza non troncata nel buffer di lunghezza/indicatore, restituisce SQL_SUCCESS_WITH_INFO e inserisce SQLSTATE 01004 (dati troncati) nella diagnostica. L'unica eccezione è se un segnalibro di lunghezza variabile viene troncato quando viene restituito da **SQLFetch**, che restituisce SQLSTATE 22001 (dati stringa troncati a destra).  
  
 I dati a lunghezza fissa non vengono mai troncati, perché il driver presuppone che la dimensione del buffer associato sia la dimensione del tipo di dati. Il troncamento dei dati tende ad essere raro, perché l'applicazione associa in genere un buffer sufficientemente grande da contenere l'intero valore dei dati. determina le dimensioni necessarie dai metadati. Tuttavia, l'applicazione potrebbe associare in modo esplicito un buffer che sa essere troppo piccolo. Ad esempio, potrebbe recuperare e visualizzare i primi 20 caratteri di una descrizione di parte o i primi 100 caratteri di una colonna di testo lunga.  
  
 I dati di tipo carattere devono essere con terminazione null dal driver prima di essere restituiti all'applicazione, anche se è stato troncato. Il carattere di terminazione null non è incluso nella lunghezza dei byte restituita, ma richiede spazio nel buffer associato. Si supponga, ad esempio, che un'applicazione utilizzi stringhe composte da dati di tipo carattere nel set di caratteri ASCII, che un driver abbia 50 caratteri di dati da restituire e che il buffer dell'applicazione sia lungo 25 byte. Nel buffer dell'applicazione, il driver restituisce i primi 24 caratteri seguiti da un carattere di terminazione null. Nel buffer di lunghezza/indicatore, restituisce una lunghezza in byte di 50.  
  
 L'applicazione può limitare il numero di righe nel set di risultati impostando l'attributo dell'istruzione SQL_ATTR_MAX_ROWS prima di eseguire l'istruzione che crea il set di risultati. Ad esempio, la modalità di anteprima in un'applicazione utilizzata per formattare i report richiede solo dati sufficienti per visualizzare la prima pagina del report. Limitando le dimensioni del set di risultati, tale funzionalità verrebbe eseguita più velocemente. Questo attributo di istruzione ha lo scopo di ridurre il traffico di rete e potrebbe non essere supportato da tutti i driver.
