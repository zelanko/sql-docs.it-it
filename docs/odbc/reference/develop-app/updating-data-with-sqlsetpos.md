---
description: Aggiornamento dati con SQLSetPos
title: Aggiornamento dei dati con SQLSetPos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating data
ms.assetid: e9625b59-06a0-4883-b155-b932ba7528d9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eccc08e7af81b2b2b13dd50b2cfb0f5701174e70
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476283"
---
# <a name="updating-data-with-sqlsetpos"></a>Aggiornamento dati con SQLSetPos
Le applicazioni possono aggiornare o eliminare qualsiasi riga del set di righe con **SQLSetPos**. La chiamata di **SQLSetPos** è una pratica alternativa alla costruzione e all'esecuzione di un'istruzione SQL. Consente a un driver ODBC di supportare gli aggiornamenti posizionati anche quando l'origine dati non supporta istruzioni SQL posizionate. Fa parte del paradigma di ottenere l'accesso completo al database per mezzo di chiamate di funzione.  
  
 **SQLSetPos** opera sul set di righe corrente e può essere utilizzato solo dopo una chiamata a **SQLFetchScroll**. L'applicazione specifica il numero della riga da aggiornare, eliminare o inserire e il driver recupera i nuovi dati per la riga dai buffer dei set di righe. **SQLSetPos** può essere utilizzato anche per definire una riga specificata come riga corrente o per aggiornare una determinata riga del set di righe dall'origine dati.  
  
 Le dimensioni del set di righe vengono impostate da una chiamata a **SQLSetStmtAttr** con un argomento *attribute* di SQL_ATTR_ROW_ARRAY_SIZE. **SQLSetPos** utilizza una nuova dimensione del set di righe, tuttavia, solo dopo una chiamata a **SQLFetch** o **SQLFetchScroll**. Se, ad esempio, le dimensioni del set di righe vengono modificate, viene chiamato **SQLSetPos** , viene chiamato **SQLFetch** o **SQLFetchScroll** e la chiamata a **SQLSetPos** usa le dimensioni del set di righe precedenti mentre **SQLFetch** o **SQLFetchScroll** usa le nuove dimensioni del set di righe.  
  
 La prima riga nel set di righe è il numero di riga 1. L'argomento *RowNumber* in **SQLSetPos** deve identificare una riga nel set di righe; ovvero, il valore deve essere compreso tra 1 e il numero di righe recuperate più di recente, che possono essere inferiori alle dimensioni del set di righe. Se *RowNumber* è 0, l'operazione viene applicata a ogni riga nel set di righe.  
  
 Poiché la maggior parte dell'interazione con i database relazionali viene eseguita tramite SQL, **SQLSetPos** non è ampiamente supportato. Tuttavia, un driver può emularlo facilmente costruendo ed eseguendo un'istruzione **Update** o **Delete** .  
  
 Per determinare le operazioni supportate da **SQLSetPos** , un'applicazione chiama **SQLGetInfo** con l'opzione SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 Information (a seconda del tipo di cursore).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Aggiornamento delle righe nel set di righe con SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [Eliminazione di righe nel set di righe con SQLSetPos](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
