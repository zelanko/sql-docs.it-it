---
title: Aggiornamento dei dati con SQLSetPos Documenti Microsoft
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
ms.openlocfilehash: 16476a1e1007905f34ec2e70ce6032eb8d81fe7a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286161"
---
# <a name="updating-data-with-sqlsetpos"></a>Aggiornamento dati con SQLSetPos
Le applicazioni possono aggiornare o eliminare qualsiasi riga nel set di righe con **SQLSetPos**. La chiamata a **SQLSetPos** è una comoda alternativa alla costruzione e all'esecuzione di un'istruzione SQL. Consente a un driver ODBC di supportare gli aggiornamenti posizionati anche quando l'origine dati non supporta le istruzioni SQL posizionate. Fa parte del paradigma di ottenere l'accesso completo al database tramite chiamate di funzione.  
  
 **SQLSetPos** opera sul set di righe corrente e può essere utilizzato solo dopo una chiamata a **SQLFetchScroll**. L'applicazione specifica il numero della riga da aggiornare, eliminare o inserire e il driver recupera i nuovi dati per tale riga dai buffer del set di righe. **SQLSetPos** può essere utilizzato anche per designare una riga specificata come riga corrente o per aggiornare una determinata riga nel set di righe dall'origine dati.  
  
 La dimensione del set di righe viene impostata da una chiamata a **SQLSetStmtAttr** con un argomento *Attribute* di SQL_ATTR_ROW_ARRAY_SIZE. **SQLSetPos** utilizza una nuova dimensione del set di righe, tuttavia, solo dopo una chiamata a **SQLFetch** o **SQLFetchScroll**. Ad esempio, se la dimensione del set di righe viene modificata, **SQLSetPos** viene chiamato e quindi **SQLFetcho** o **SQLFetchScroll** viene chiamato e la chiamata a **SQLSetPos** utilizza la dimensione del set di righe precedente mentre **SQLFetch** o **SQLFetchScroll** utilizza la nuova dimensione del set di righe.  
  
 La prima riga nel set di righe è il numero di riga 1. *L'argomento RowNumber* in **SQLSetPos** deve identificare una riga nel set di righe. vale a dire, il valore deve essere compreso nell'intervallo compreso tra 1 e il numero di righe che sono state recuperate più di recente (che può essere inferiore alla dimensione del set di righe). Se *RowNumber* è 0, l'operazione si applica a ogni riga del set di righe.  
  
 Poiché la maggior parte delle interazioni con i database relazionali viene eseguita tramite SQL, **SQLSetPos** non è ampiamente supportato. Tuttavia, un driver può facilmente emularlo costruendo ed eseguendo **un'istruzione UPDATE** o **DELETE.**  
  
 Per determinare le operazioni supportate da **SQLSetPos,** un'applicazione chiama **SQLGetInfo** con l'opzione SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 informazioni (a seconda del tipo di cursore).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Aggiornamento delle righe nel set di righe con SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [Eliminazione di righe nel set di righe con SQLSetPos](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
