---
title: Problemi di prestazioni del Driver di Database desktop | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b4d92d2784649e4366113b3070b54598df585370
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240311"
---
# <a name="desktop-database-driver-performance-issues"></a>Problemi di prestazioni dei driver di database desktop
Per garantire la compatibilità con le applicazioni ANSI esistenti, i tipi di dati SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR vengono esposte come SQL_CHAR e SQL_VARCHAR, SQL_LONGVARCHAR per Microsoft Access 4.0 o successiva zdroje dat. Le origini dati non restituiscono i tipi di dati carattere WIDE, ma i dati ancora devono essere inviati a Jet in formato carattere Wide. È importante comprendere che la conversione verrà eseguita se una colonna di parametri o risultati SQL_C_CHAR è associata a un tipo di dati SQL_CHAR nelle applicazioni ANSI.  
  
 Quando un tipo SQL_C_CHAR viene associato a un parametro di tipo LONGVARCHAR, questa conversione può essere particolarmente efficiente in termini di memoria. Poiché il motore Jet 4.0 non riesce a flusso di dati del parametro LONGTEXT, deve essere allocato un buffer di conversione UNICODE che è due volte la dimensione del buffer SQL_C_CHAR ANSI. Il meccanismo più efficiente è per l'applicazione eseguire la conversione di UNICODE e associare il parametro come tipo SQL_C_WCHAR. Quando un parametro è contrassegnato come data-at-execution e i dati vengono forniti in più chiamate a SQLPutData, un buffer di dati longtext verrà incrementato. Per evitare il costo dell'aumento delle dimensioni in questo buffer "Inserire dei dati" è possibile specificare una lunghezza facoltativa tramite SQL_DATA_AT_EXEC_LEN(x), dove *x* è la lunghezza prevista di byte. In tal modo inizializzata la dimensione di un buffer interno PutData da *x* byte.  
  
> [!NOTE]  
>  Un modo efficiente per inserire o aggiornare dati lungo può essere effettuato utilizzando **SQLBulkOperations()** oppure **SQLSetPos()** e impostando i dati di tipo long a SQL_DATA_AT_EXEC. (EXEC_LEN viene ignorato in questo caso). I dati possono essere trasmessi in blocchi chiamando **SQLPutData** più volte, che in modo efficace i dati verranno aggiunti alla tabella.  
  
 Quando un'applicazione usando un database Jet 3.5 tramite i driver di Database Desktop ODBC Microsoft viene aggiornata alla versione 4.0, potrebbe verificarsi un peggioramento delle prestazioni e una maggiore dimensione del working set. Infatti, quando una versione 3. *x* database viene aperta utilizzando il nuovo driver versione 4.0, vengono caricati Jet 4.0. Quando viene aperto il database Jet 4.0 e si vede che il database è 3. *x* versione, viene caricato un driver ISAM installabile che equivale a caricare anche il motore Jet 3.5. Per rimuovere la riduzione delle prestazioni e le dimensioni, il 3 di Jet. *x* database debba essere compressi in un database nel formato di Jet 4.0. Per eliminare il caricamento di due motori a reazione e ridurre al minimo il percorso del codice ai dati.  
  
 Inoltre, il motore Jet 4.0 è un motore di Unicode. Tutte le stringhe vengono memorizzate e manipolate in formato Unicode. Quando un'applicazione ANSI accede a un 3 Jet. *x* database attraverso il motore Jet 4.0, i dati viene convertito da ANSI a Unicode e tornare ad ANSI. Se il database viene aggiornato per il formato della versione 4.0, le stringhe vengono convertite in Unicode, la rimozione di un livello di conversione di stringhe, nonché di ridurre al minimo il percorso del codice ai dati tramite un solo motore Jet.
