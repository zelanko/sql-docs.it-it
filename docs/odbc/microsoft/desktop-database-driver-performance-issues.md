---
description: Problemi di prestazioni dei driver di database desktop
title: Problemi di prestazioni del driver del database desktop | Microsoft Docs
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
ms.openlocfilehash: 20c21c493d81df6afb4a338675f86ad96ccfab68
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449553"
---
# <a name="desktop-database-driver-performance-issues"></a>Problemi di prestazioni dei driver di database desktop
Per garantire la compatibilità con le applicazioni ANSI esistenti, i tipi di dati SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR vengono esposti come SQL_CHAR, SQL_VARCHAR e SQL_LONGVARCHAR per le origini dati Microsoft Access 4,0 o versioni successive. Le origini dati non restituiscono tipi di dati CHAR di grandi dimensioni, ma i dati devono comunque essere inviati a Jet in formato carattere wide. È importante comprendere che la conversione verrà eseguita se un SQL_C_CHAR parametro o una colonna risultato è associato a un tipo di dati SQL_CHAR in un'applicazione ANSI.  
  
 Questa conversione può essere particolarmente inefficiente in termini di memoria quando un tipo di SQL_C_CHAR è associato a un parametro di tipo LONGVARCHAR. Poiché il motore Jet 4,0 non è in grado di trasmettere i dati del parametro LONGTEXT, è necessario allocare un buffer di conversione UNICODE che sia il doppio delle dimensioni del SQL_C_CHAR buffer ANSI. Il meccanismo più efficiente prevede che l'applicazione esegua la conversione UNICODE e associ il parametro come tipo SQL_C_WCHAR. Quando un parametro è contrassegnato come data-at-execution e i dati vengono forniti in più chiamate a SQLPutData, viene aumentato il buffer dei dati LONGTEXT. Un modo per evitare i costi legati alla crescita del buffer "put data" consiste nel fornire una lunghezza facoltativa tramite SQL_DATA_AT_EXEC_LEN (x), dove *x* è la lunghezza prevista di byte. In questo modo, le dimensioni di un buffer PutData interno vengono inizializzate su *x* byte.  
  
> [!NOTE]  
>  Un modo efficiente per inserire o aggiornare i dati di tipo Long può essere eseguito tramite **SQLBulkOperations ()** o **SQLSetPos ()** e impostando i dati lunghi su SQL_DATA_AT_EXEC. In questo caso EXEC_LEN viene ignorato. I dati possono essere trasmessi in blocchi chiamando più volte **SQLPutData** , che aggiungerà i dati alla tabella in modo efficace.  
  
 Quando un'applicazione che utilizza un database Jet 3,5 tramite i driver di database di Microsoft ODBC desktop viene aggiornata alla versione 4,0, potrebbe verificarsi una riduzione delle prestazioni e un aumento delle dimensioni del working set. Questo è dovuto al fatto che quando si usa una versione 3. il database *x* viene aperto usando il nuovo driver della versione 4,0, carica Jet 4,0. Quando Jet 4,0 apre il database e rileva che il database è un 3. *x* versione, carica un driver ISAM installabile che equivale a caricare anche il motore Jet 3,5. Per rimuovere le prestazioni e le dimensioni rigore, Jet 3. il database *x* deve essere compresso in un database in formato Jet 4,0. In questo modo si eliminerà il caricamento di due motori jet e il percorso del codice ai dati verrà ridotto.  
  
 Inoltre, il motore Jet 4,0 è un motore Unicode. Tutte le stringhe vengono archiviate e modificate in Unicode. Quando un'applicazione ANSI accede a un Jet 3. *x* database tramite il motore Jet 4,0, i dati vengono convertiti da ANSI a Unicode e viceversa. Se il database viene aggiornato al formato della versione 4,0, le stringhe vengono convertite in Unicode, rimuovendo un livello di conversione di stringa e riducendo al minimo il percorso del codice ai dati attraverso un solo motore Jet.
