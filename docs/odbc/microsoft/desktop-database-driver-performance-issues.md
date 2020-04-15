---
title: Problemi di prestazioni dei driver di database desktop Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], performance
- desktop database drivers [ODBC], performance
- Jet-based ODBC drivers [ODBC], performance
ms.assetid: 1a4c4b7e-9744-411f-9b6e-06dfdad92cf7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a819d99a995fd7b287beb66b94f1df526e05f201
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303502"
---
# <a name="desktop-database-driver-performance-issues"></a>Problemi di prestazioni dei driver di database desktop
Per garantire la compatibilità con le applicazioni ANSI esistenti, i tipi di dati SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR vengono esposti come SQL_CHAR, SQL_VARCHAR e SQL_LONGVARCHAR per origini dati Microsoft Access 4.0 o versioni successive. Le origini dati non restituiscono tipi di dati WIDE CHAR, ma i dati devono comunque essere inviati a Jet in formato Wide Char. È importante comprendere che la conversione verrà eseguita se un parametro di SQL_C_CHAR o una colonna di risultati è associata a un SQL_CHAR tipo di dati in un'applicazione ANSI.  
  
 Questa conversione può essere particolarmente inefficiente in termini di memoria quando un tipo SQL_C_CHAR è associato a un parametro di tipo LONGVARCHAR.This conversion can be especially inefficient in terms of memory when a SQL_C_CHAR type is bound to a parameter of type LONGVARCHAR. Poiché il modulo di gestione Jet 4.0 non è in grado di trasmettere i dati dei parametri LONGTEXT, è necessario allocare un buffer di conversione UNICODE pari al doppio della dimensione del buffer ANSI SQL_C_CHAR. Il meccanismo più efficiente è che l'applicazione esegua la conversione UNICODE e associa il parametro come tipo SQL_C_WCHAR. Quando un parametro è contrassegnato come data-at-execution e i dati vengono forniti in più chiamate a SQLPutData, viene aumentato un buffer di dati longtext. Un modo per evitare il costo della crescita di questo buffer "Put Data" consiste nel fornire una lunghezza facoltativa tramite SQL_DATA_AT_EXEC_LEN(x), dove *x* è la lunghezza prevista di byte. In questo modo verranno inizializzate le dimensioni di un buffer PutData interno su *x* byte.  
  
> [!NOTE]  
>  Un modo efficiente per inserire o aggiornare dati lunghi può essere ottenuto utilizzando **SQLBulkOperations()** o **SQLSetPos()** e impostando i dati long su SQL_DATA_AT_EXEC. (EXEC_LEN viene ignorata in questo caso.) I dati possono essere trasmessi in blocchi chiamando **SQLPutData** più volte, che aggiungerà effettivamente i dati alla tabella.  
  
 Quando un'applicazione che utilizza un database Jet 3.5 tramite i driver di database desktop di Microsoft ODBC viene aggiornata alla versione 4.0, potrebbe verificarsi una riduzione delle prestazioni e un aumento delle dimensioni del working set. Questo perché quando una versione 3. *x* database viene aperto utilizzando il nuovo driver versione 4.0, carica Jet 4.0. Quando Jet 4.0 apre il database e vede che il database è un 3. *x* versione, carica un driver ISAM installabile che equivale a caricare il motore Jet 3.5 pure. Per rimuovere la penalità di prestazioni e dimensioni, il Jet 3. *x* database deve essere compattato in un database di formato Jet 4.0. Ciò eliminerà il caricamento di due motori Jet e ridurrà al minimo il percorso del codice dei dati.  
  
 Inoltre, il motore Jet 4.0 è un motore Unicode. Tutte le stringhe vengono archiviate e modificate in Unicode.All strings are stored and manipulated in Unicode. Quando un'applicazione ANSI accede a un Jet 3. *x* tramite il motore Jet 4.0, i dati vengono convertiti da ANSI a Unicode e di nuovo in ANSI. Se il database viene aggiornato al formato della versione 4.0, le stringhe vengono convertite in Unicode, rimuovendo un livello di conversione delle stringhe e riducendo al minimo il percorso del codice ai dati passando attraverso un solo motore Jet.
