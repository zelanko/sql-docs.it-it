---
title: Aggiornamento dei dati con SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBulkOperations function [ODBC], updating data
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: 7645a704-341e-4267-adbe-061a9fda225b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 958514adc02452cdc75a05e7ad28cd31f4e8e0e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62632444"
---
# <a name="updating-data-with-sqlbulkoperations"></a>Aggiornamento dei dati con SQLBulkOperations
Le applicazioni possono eseguire operazioni update, delete, fetch o inserimento bulk nella tabella sottostante nell'origine dati con una chiamata a **SQLBulkOperations**. La chiamata **SQLBulkOperations** rappresenta un'alternativa utile alla creazione ed esecuzione di un'istruzione SQL. In questo modo, un driver ODBC supportano gli aggiornamenti posizionati anche quando l'origine dati non supporta le istruzioni SQL posizionate. Fa parte del paradigma di ottenere accesso completo al database tramite le chiamate di funzione.  
  
 **SQLBulkOperations** agisce sui set di righe corrente e può essere usato solo dopo una chiamata a **SQLFetch** oppure **SQLFetchScroll**. L'applicazione specifica le righe da aggiornare, eliminare o aggiornare i segnalibri di memorizzazione nella cache. Il driver può recuperare i nuovi dati per le righe da aggiornare oppure i nuovi dati da inserire nella tabella sottostante e dai buffer di set di righe.  
  
 Le dimensioni del set di righe utilizzabile dai **SQLBulkOperations** è impostata da una chiamata a **SQLSetStmtAttr** con un *attributo* argomento di SQL_ATTR_ROW_ARRAY_SIZE. A differenza **SQLSetPos**, che usa una nuova dimensione di set di righe solo dopo una chiamata a **SQLFetch** oppure **SQLFetchScroll**, **SQLBulkOperations** utilizza il nuova dimensione di set di righe dopo la chiamata a **SQLSetStmtAttr**.  
  
 Poiché tramite SQL, viene eseguita la maggior parte delle interazioni con i database relazionali **SQLBulkOperations** non è supportato. Tuttavia, un driver può facilmente emulare, costruendo e l'esecuzione di un' **UPDATE**, **eliminare**, o **Inserisci** istruzione.  
  
 Per determinare quali operazioni **SQLBulkOperation** supporta, un'applicazione chiama **SQLGetInfo** con SQL_DYNAMIC_CURSOR_ATTRIBUTES1 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR _ATTRIBUTES1 o l'opzione di informazioni SQL_STATIC_CURSOR_ATTRIBUTES1 (a seconda del tipo di cursore).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Aggiornamento delle righe tramite segnalibro con SQLBulkOperations](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Eliminazione di righe tramite segnalibro con SQLBulkOperations](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Inserimento di righe con SQLBulkOperations](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [Recupero di righe con SQLBulkOperations](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
