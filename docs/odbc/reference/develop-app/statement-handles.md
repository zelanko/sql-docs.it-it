---
title: Gli handle di istruzione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 65d6d78b-a8c8-489a-9dad-f8d127a44882
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6f249bb13ece6382e96dfe953b1d3c1d96c7bf65
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63148997"
---
# <a name="statement-handles"></a>Handle di istruzione
Oggetto *istruzione* è più facilmente considerato come un'istruzione SQL, ad esempio **seleziona \* dipendente da**. Tuttavia, un'istruzione è solo un'istruzione SQL: è costituito da tutte le informazioni associate a tale istruzione SQL, ad esempio qualsiasi set di risultati creati tramite l'istruzione e i parametri usati nell'esecuzione dell'istruzione. Un'istruzione non è neanche necessario disporre di un'istruzione SQL definito dall'applicazione. Ad esempio, quando una funzione di catalogo, ad esempio **SQLTables** viene eseguita in un'istruzione, viene eseguita un'istruzione SQL predefinita che restituisce un elenco di nomi di tabella.  
  
 Ogni istruzione viene identificata da un handle di istruzione. Un'istruzione è associata a una singola connessione, e possono essere presenti più istruzioni in tale connessione. Alcuni driver limitare il numero di istruzioni attive che supportano; opzione il SQL_MAX_CONCURRENT_ACTIVITIES **SQLGetInfo** specifica quanti istruzioni attive supporta un driver in un'unica connessione. Viene definita come un'istruzione *active* se è presente in attesa di risultati, in cui risultati sono un set di risultati o conteggio delle righe interessate da un' **Inserisci**, **UPDATE**, o **Eliminare** istruzione o i dati viene inviato con più chiamate a **SQLPutData**.  
  
 All'interno di un frammento di codice che implementa ODBC (gestione Driver o un driver), l'handle di istruzione identifica una struttura che contiene informazioni di istruzione, ad esempio:  
  
-   Stato dell'istruzione  
  
-   La diagnostica a livello di istruzione corrente  
  
-   Gli indirizzi delle variabili di applicazione associati ai parametri dell'istruzione e le colonne del set di risultati  
  
-   Le impostazioni correnti di ogni attributo di istruzione  
  
 Gli handle di istruzione vengono utilizzati nella maggior parte delle funzioni ODBC. In particolare, vengono usati nelle funzioni per associare i parametri e le colonne del set di risultati (**SQLBindParameter** e **SQLBindCol**), preparare ed eseguire le istruzioni (**SQLPrepare** **SQLExecute**, e **SQLExecDirect**), recuperare i metadati (**SQLColAttribute** e **SQLDescribeCol**), recupero i risultati (**SQLFetch**) e recuperare dati diagnostici (**SQLGetDiagField** e **SQLGetDiagRec**). Vengono usati anche nelle funzioni di catalogo (**SQLColumns**, **SQLTables**e così via) e un numero di altre funzioni.  
  
 Gli handle di istruzione vengono allocati con **SQLAllocHandle** e liberati con **SQLFreeHandle**.
