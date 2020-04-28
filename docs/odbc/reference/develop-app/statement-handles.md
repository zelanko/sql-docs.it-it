---
title: Handle di istruzione | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1be90fe10d10a0b087d1c9724fed249805eb4dba
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299677"
---
# <a name="statement-handles"></a>Handle di istruzione
Un' *istruzione* è più facilmente pensata come istruzione SQL, ad esempio **Select \* from Employee**. Tuttavia, un'istruzione non è solo un'istruzione SQL, bensì tutte le informazioni associate a tale istruzione SQL, ad esempio i set di risultati creati dall'istruzione e i parametri utilizzati nell'esecuzione dell'istruzione. Un'istruzione non deve nemmeno avere un'istruzione SQL definita dall'applicazione. Quando, ad esempio, una funzione di catalogo come **SQLTables** viene eseguita su un'istruzione, viene eseguita un'istruzione SQL predefinita che restituisce un elenco di nomi di tabella.  
  
 Ogni istruzione è identificata da un handle di istruzione. Un'istruzione è associata a una singola connessione e possono essere presenti più istruzioni su tale connessione. Alcuni driver limitano il numero di istruzioni attive supportate; l'opzione SQL_MAX_CONCURRENT_ACTIVITIES in **SQLGetInfo** specifica il numero di istruzioni attive supportate da un driver in una singola connessione. Un'istruzione è definita come *attiva* se presenta risultati in sospeso, in cui i risultati sono un set di risultati o il numero di righe interessate da un'istruzione **Insert**, **Update**o **Delete** oppure se i dati vengono inviati con più chiamate a **SQLPutData**.  
  
 All'interno di un frammento di codice che implementa ODBC (Gestione driver o driver), l'handle di istruzione identifica una struttura che contiene informazioni sull'istruzione, ad esempio:  
  
-   Stato dell'istruzione  
  
-   Diagnostica a livello di istruzione corrente  
  
-   Indirizzi delle variabili dell'applicazione associati ai parametri dell'istruzione e alle colonne del set di risultati  
  
-   Impostazioni correnti di ogni attributo di istruzione  
  
 Gli handle di istruzione vengono utilizzati nella maggior parte delle funzioni ODBC. In particolare, vengono utilizzate nelle funzioni per associare i parametri e le colonne del set di risultati **(SQLBindParameter** e **SQLBindCol**), le istruzioni di preparazione ed esecuzione (**SQLPrepare**, **SQLExecute**e **SQLExecDirect**), il recupero dei metadati (**SQLColAttribute** e **SQLDescribeCol**), il recupero dei risultati (**SQLFetch**) e il recupero della diagnostica (**SQLGetDiagField** e **SQLGetDiagRec**). Vengono inoltre utilizzati nelle funzioni di catalogo (**SQLColumns**, **SQLTables**e così via) e in alcune altre funzioni.  
  
 Gli handle di istruzione vengono allocati con **SQLAllocHandle** e liberati con **SQLFreeHandle**.
