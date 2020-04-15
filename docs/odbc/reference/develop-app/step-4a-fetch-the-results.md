---
title: 'Passo 4a: Recuperare i risultati . Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], fetching results
- fetches [ODBC], fetching results
ms.assetid: 77d30142-c774-473c-96fb-b364bb92ac60
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c4f810e5c42b54ec871c233ab498936abae610dc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302972"
---
# <a name="step-4a-fetch-the-results"></a>Passaggio 4a: Recuperare i risultati
Il passaggio successivo consiste nel recuperare i risultati, come illustrato nella figura seguente.  
  
 ![Recupero di risultati in un'applicazione ODBC](../../../odbc/reference/develop-app/media/pr14.gif "pr14 (informazioni in questo da system")  
  
 Se l'istruzione eseguita nel "Passaggio 3: Compilare ed eseguire un'istruzione SQL" è un'istruzione **SELECT** o una funzione di catalogo, l'applicazione chiama prima **SQLNumResultCols** per determinare il numero di colonne nel set di risultati. Questo passaggio non è necessario se l'applicazione conosce già il numero di colonne del set di risultati, ad esempio quando l'istruzione SQL è hardcoded in un'applicazione verticale o personalizzata.  
  
 Successivamente, l'applicazione recupera il nome, il tipo di dati, la precisione e la scala di ogni colonna del set di risultati con **SQLDescribeCol**. Anche in questo caso, questo non è necessario per le applicazioni come le applicazioni verticali e personalizzate che già conoscono queste informazioni. L'applicazione passa queste informazioni a **SQLBindCol**, che associa una variabile di applicazione a una colonna nel set di risultati.  
  
 L'applicazione chiama ora **SQLFetch** per recuperare la prima riga di dati e inserire i dati da tale riga nelle variabili associate con **SQLBindCol**. Se sono presenti dati lunghi nella riga, chiama **SQLGetData** per recuperare i dati. L'applicazione continua a chiamare **SQLFetch** e **SQLGetData** per recuperare dati aggiuntivi. Al termine del recupero dei dati, chiama **SQLCloseCursor** per chiudere il cursore.  
  
 Per una descrizione completa del recupero dei risultati, vedere [Recupero di risultati (base)](../../../odbc/reference/develop-app/retrieving-results-basic.md) e [Recupero dei risultati (avanzato)](../../../odbc/reference/develop-app/retrieving-results-advanced.md).  
  
 L'applicazione torna ora al "Passaggio 3: compilare ed eseguire un'istruzione SQL" per eseguire un'altra istruzione nella stessa transazione; o procede al "Passaggio 5: Eseguire il commit della transazione" per eseguire il commit o il rollback della transazione.
