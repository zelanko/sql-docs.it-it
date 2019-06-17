---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d1c31ef622281b4f52f62ca3867c5afa7dcae8ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194421"
---
# <a name="updating-data-with-sqlsetpos"></a>Aggiornamento dati con SQLSetPos
Le applicazioni possono aggiornare o eliminare qualsiasi riga nel set di righe con **SQLSetPos**. La chiamata **SQLSetPos** rappresenta un'alternativa utile alla creazione ed esecuzione di un'istruzione SQL. In questo modo, un driver ODBC supportano gli aggiornamenti posizionati anche quando l'origine dati non supporta le istruzioni SQL posizionate. Fa parte del paradigma di ottenere accesso completo al database tramite le chiamate di funzione.  
  
 **SQLSetPos** agisce sui set di righe corrente e può essere usato solo dopo una chiamata a **SQLFetchScroll**. L'applicazione specifica il numero di riga da aggiornare, eliminare o inserire i nuovi dati di tale riga vengono recuperati dai buffer di set di righe. **SQLSetPos** inoltre consente di designare una riga specificata come riga corrente o per aggiornare una determinata riga nel set di righe dall'origine dati.  
  
 Dimensioni del set di righe vengono impostate tramite una chiamata a **SQLSetStmtAttr** con un *attributo* argomento di SQL_ATTR_ROW_ARRAY_SIZE. **SQLSetPos** Usa una nuova dimensione di set di righe, tuttavia, solo dopo una chiamata a **SQLFetch** oppure **SQLFetchScroll**. Se vengono modificate le dimensioni del set di righe, ad esempio **SQLSetPos** viene chiamato e quindi **SQLFetch** oppure **SQLFetchScroll** viene chiamato e la chiamata a **SQLSetPos** Usa le dimensioni del set di righe precedente durante **SQLFetch** oppure **SQLFetchScroll** Usa le nuove dimensioni del set di righe.  
  
 La prima riga nel set di righe è il numero di riga 1. Il *RowNumber* argomento nella **SQLSetPos** deve identificare una riga nel set di righe; vale a dire, il valore deve essere compreso nell'intervallo compreso tra 1 e il numero di righe recuperate più di recente (che può essere minore di dimensioni del set di righe). Se *RowNumber* è 0, l'operazione viene applicata a ogni riga nel set di righe.  
  
 Poiché tramite SQL, viene eseguita la maggior parte delle interazioni con i database relazionali **SQLSetPos** non è supportato. Tuttavia, un driver può facilmente emulare, costruendo e l'esecuzione di un' **UPDATE** oppure **eliminare** istruzione.  
  
 Per determinare quali operazioni **SQLSetPos** supporta, un'applicazione chiama **SQLGetInfo** con SQL_DYNAMIC_CURSOR_ATTRIBUTES1 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ Cursore1 o l'opzione di informazioni SQL_STATIC_CURSOR_ATTRIBUTES1 (a seconda del tipo di cursore).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Aggiornamento delle righe nel set di righe con SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [Eliminazione di righe nel set di righe con SQLSetPos](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
