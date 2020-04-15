---
title: "Maniglie dell'istruzione : Documenti Microsoft"
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299677"
---
# <a name="statement-handles"></a>Handle di istruzione
*Un'istruzione* è più facilmente considerata come un'istruzione SQL, ad esempio **SELECT \* FROM Employee**. Tuttavia, un'istruzione è più di una semplice istruzione SQL: è costituita da tutte le informazioni associate a tale istruzione SQL, ad esempio qualsiasi set di risultati creato dall'istruzione e i parametri utilizzati nell'esecuzione dell'istruzione. Un'istruzione non ha nemmeno bisogno di avere un'istruzione SQL definita dall'applicazione. Ad esempio, quando una funzione di catalogo, ad esempio **SQLTables** viene eseguita su un'istruzione, viene eseguita un'istruzione SQL predefinita che restituisce un elenco di nomi di tabella.  
  
 Ogni istruzione è identificata da un handle di istruzione. Un'istruzione è associata a una singola connessione e possono essere presenti più istruzioni su tale connessione. Alcuni driver limitano il numero di istruzioni attive supportate; l'opzione SQL_MAX_CONCURRENT_ACTIVITIES in **SQLGetInfo** specifica il numero di istruzioni attive supportate da un driver in una singola connessione. Un'istruzione è definita come *attiva* se contiene risultati in sospeso, dove i risultati sono un set di risultati o il conteggio delle righe interessate da un'istruzione **INSERT**, **UPDATE**o **DELETE** oppure se i dati vengono inviati con più chiamate a **SQLPutData**.  
  
 All'interno di una parte di codice che implementa ODBC (Gestione Driver o un driver), l'handle di istruzione identifica una struttura che contiene informazioni sull'istruzione, ad esempio:In a piece of code that implements ODBC (the Driver Manager or a driver), the statement handle identifies a structure that contains statement information, such as:  
  
-   Lo stato della dichiarazione  
  
-   La diagnostica a livello di istruzione corrente  
  
-   Gli indirizzi delle variabili di applicazione associate ai parametri dell'istruzione e alle colonne del set di risultati  
  
-   Le impostazioni correnti di ogni attributo di istruzione  
  
 Gli handle di istruzione vengono utilizzati nella maggior parte delle funzioni ODBC. In particolare, vengono utilizzati nelle funzioni per associare parametri e colonne del set di risultati (**SQLBindParameter** e **SQLBindCol**), preparare ed eseguire istruzioni (**SQLPrepare**, **SQLExecute**e **SQLExecDirect**), recuperare i metadati (**SQLColAttribute** e **SQLDescribeCol**), recuperare i risultati (**SQLFetch**) e recuperare la diagnostica (**SQLGetDiagField** e **SQLGetDiagRec**). Vengono inoltre utilizzati nelle funzioni di catalogo (**SQLColumns**, **SQLTables**e così via) e in numerose altre funzioni.  
  
 Gli handle di istruzione vengono allocati con **SQLAllocHandle** e liberati con **SQLFreeHandle**.
