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
ms.openlocfilehash: 010d05990396c10836c0a2130e5d9f4392ae56ec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069864"
---
# <a name="fetching-a-row-of-data"></a>Recupero di una riga di dati
Per recuperare una riga di dati, un'applicazione chiama **SQLFetch**. **SQLFetch** può essere chiamato con qualsiasi tipo di cursore, ma sposta solo il cursore del set di righe in una direzione di solo avanzamento. **SQLFetch** sposta il cursore alla riga successiva e restituisce i dati per tutte le colonne associate alle chiamate a **SQLBindCol**. Quando il cursore raggiunge la fine del set di risultati, **SQLFetch** restituisce SQL_NO_DATA. Per esempi di chiamata a **SQLFetch**, vedere [uso di SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).  
  
 Il modo esatto in cui viene implementato **SQLFetch** è specifico del driver, ma il modello generale prevede che il driver recuperi i dati per tutte le colonne delimitate dall'origine dati, la converta in base ai tipi delle variabili delimitate e inserisce i dati convertiti in tali variabili. Se il driver non è in grado di convertire i dati, **SQLFetch** restituisce un errore. L'applicazione può continuare a recuperare le righe, ma i dati per la riga corrente andranno perduti. Ciò che accade ai dati per le colonne non vincolate dipende dal driver, ma la maggior parte dei driver li recupera e li ignora o non li recupera affatto.  
  
 Il driver imposta inoltre i valori di tutti i buffer di lunghezza/indicatore associati. Se il valore dei dati di una colonna è NULL, il driver imposta il buffer di lunghezza/indicatore corrispondente su SQL_NULL_DATA. Se il valore dei dati non è NULL, il driver imposta il buffer di lunghezza/indicatore sulla lunghezza in byte dei dati dopo la conversione. Se non è possibile determinare questa lunghezza, come accade talvolta con i dati Long recuperati da più di una chiamata di funzione, il driver imposta il buffer di lunghezza/indicatore su SQL_NO_TOTAL. Per i tipi di dati a lunghezza fissa, ad esempio gli Integer e le strutture di data, la lunghezza in byte corrisponde alla dimensione del tipo di dati.  
  
 Per i dati a lunghezza variabile, ad esempio i dati di tipo carattere e binario, il driver controlla la lunghezza in byte dei dati convertiti rispetto alla lunghezza in byte del buffer associato alla colonna. la lunghezza del buffer viene specificata nell'argomento *bufferLength* in **SQLBindCol**. Se la lunghezza in byte dei dati convertiti è maggiore della lunghezza in byte del buffer, il driver tronca i dati per adattarsi al buffer, restituisce la lunghezza non troncata nel buffer di lunghezza/indicatore, restituisce SQL_SUCCESS_WITH_INFO e inserisce SQLSTATE 01004 (dati troncati) nella diagnostica. L'unica eccezione è rappresentata dal caso in cui un segnalibro a lunghezza variabile viene troncato quando viene restituito da **SQLFetch**, che restituisce SQLState 22001 (dati stringa, troncati a destra).  
  
 I dati a lunghezza fissa non vengono mai troncati perché il driver presuppone che le dimensioni del buffer associato siano le dimensioni del tipo di dati. Il troncamento dei dati tende a essere raro, perché l'applicazione in genere associa un buffer sufficientemente grande da contenere l'intero valore dei dati; determina la dimensione necessaria per i metadati. Tuttavia, l'applicazione potrebbe associare in modo esplicito un buffer che sa essere troppo piccolo. Ad esempio, potrebbe recuperare e visualizzare i primi 20 caratteri di una descrizione della parte o i primi 100 caratteri di una colonna di testo lungo.  
  
 I dati di tipo carattere devono avere terminazione null dal driver prima che vengano restituiti all'applicazione, anche se sono stati troncati. Il carattere di terminazione null non è incluso nella lunghezza in byte restituita ma richiede spazio nel buffer associato. Si supponga, ad esempio, che un'applicazione utilizzi stringhe costituite da dati di tipo carattere nel set di caratteri ASCII, che un driver includa 50 caratteri di dati da restituire e che il buffer dell'applicazione sia lungo 25 byte. Nel buffer dell'applicazione, il driver restituisce i primi 24 caratteri seguiti da un carattere di terminazione null. Nel buffer di lunghezza/indicatore restituisce la lunghezza in byte di 50.  
  
 L'applicazione può limitare il numero di righe nel set di risultati impostando l'attributo dell'istruzione SQL_ATTR_MAX_ROWS prima di eseguire l'istruzione che crea il set di risultati. Ad esempio, la modalità di anteprima in un'applicazione utilizzata per formattare i report necessita solo di dati sufficienti per visualizzare la prima pagina del report. Limitando le dimensioni del set di risultati, una funzionalità di questo tipo verrebbe eseguita più velocemente. Questo attributo di istruzione è progettato per ridurre il traffico di rete e potrebbe non essere supportato da tutti i driver.
