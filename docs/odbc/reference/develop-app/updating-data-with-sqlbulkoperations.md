---
description: Aggiornamento dei dati con SQLBulkOperations
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6c8626a0925d0f30792ed92332c0f96efd23f62e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465535"
---
# <a name="updating-data-with-sqlbulkoperations"></a>Aggiornamento dei dati con SQLBulkOperations
Le applicazioni possono eseguire operazioni di aggiornamento, eliminazione, recupero o inserimento bulk sulla tabella sottostante nell'origine dati con una chiamata a **SQLBulkOperations**. La chiamata di **SQLBulkOperations** è una pratica alternativa alla costruzione e all'esecuzione di un'istruzione SQL. Consente a un driver ODBC di supportare gli aggiornamenti posizionati anche quando l'origine dati non supporta istruzioni SQL posizionate. Fa parte del paradigma di ottenere l'accesso completo al database per mezzo di chiamate di funzione.  
  
 **SQLBulkOperations** opera sul set di righe corrente e può essere utilizzato solo dopo una chiamata a **SQLFetch** o **SQLFetchScroll**. L'applicazione specifica le righe da aggiornare, eliminare o aggiornare memorizzando nella cache i segnalibri. Il driver recupera i nuovi dati per le righe da aggiornare o i nuovi dati da inserire nella tabella sottostante, dai buffer del set di righe.  
  
 Le dimensioni del set di righe che devono essere utilizzate da **SQLBulkOperations** vengono impostate da una chiamata a **SQLSetStmtAttr** con un argomento di *attributo* SQL_ATTR_ROW_ARRAY_SIZE. A differenza di **SQLSetPos**, che usa una nuova dimensione del set di righe solo dopo una chiamata a **SQLFetch** o **SQLFetchScroll**, **SQLBulkOperations** usa le nuove dimensioni del set di righe dopo la chiamata a **SQLSetStmtAttr**.  
  
 Poiché la maggior parte dell'interazione con i database relazionali viene eseguita tramite SQL, **SQLBulkOperations** non è ampiamente supportato. Tuttavia, un driver può emularlo facilmente costruendo ed eseguendo un'istruzione **Update**, **Delete**o **Insert** .  
  
 Per determinare le operazioni supportate da **SQLBulkOperation** , un'applicazione chiama **SQLGetInfo** con l'opzione SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 Information (a seconda del tipo di cursore).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Aggiornamento delle righe tramite segnalibro con SQLBulkOperations](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Eliminazione di righe tramite segnalibro con SQLBulkOperations](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Inserimento di righe con SQLBulkOperations](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [Recupero di righe con SQLBulkOperations](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
