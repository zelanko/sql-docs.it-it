---
description: 'Passaggio 4a: Recuperare i risultati'
title: 'Passaggio 4a: recuperare i risultati | Microsoft Docs'
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
ms.openlocfilehash: 91a81809d07faafac6511bb5ec96c97d4f59d654
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491358"
---
# <a name="step-4a-fetch-the-results"></a>Passaggio 4a: Recuperare i risultati
Il passaggio successivo consiste nel recuperare i risultati, come illustrato nella figura seguente.  
  
 ![Recupero di risultati in un'applicazione ODBC](../../../odbc/reference/develop-app/media/pr14.gif "PR14")  
  
 Se l'istruzione eseguita in "passaggio 3: compilare ed eseguire un'istruzione SQL" era un'istruzione **Select** o una funzione di catalogo, l'applicazione chiama prima **SQLNumResultCols** per determinare il numero di colonne nel set di risultati. Questo passaggio non è necessario se l'applicazione conosce già il numero di colonne del set di risultati, ad esempio quando l'istruzione SQL è hardcoded in un'applicazione verticale o personalizzata.  
  
 Successivamente, l'applicazione recupera il nome, il tipo di dati, la precisione e la scala di ogni colonna del set di risultati con **SQLDescribeCol**. Anche in questo caso non è necessario per le applicazioni, ad esempio applicazioni verticali e personalizzate che già conoscono queste informazioni. L'applicazione passa queste informazioni a **SQLBindCol**, che associa una variabile dell'applicazione a una colonna nel set di risultati.  
  
 Ora l'applicazione chiama **SQLFetch** per recuperare la prima riga di dati e inserire i dati da tale riga nelle variabili associate a **SQLBindCol**. Se nella riga sono presenti dati Long, viene chiamato **SQLGetData** per recuperare i dati. L'applicazione continua a chiamare **SQLFetch** e **SQLGetData** per recuperare dati aggiuntivi. Al termine del recupero dei dati, chiama **SQLCloseCursor** per chiudere il cursore.  
  
 Per una descrizione completa del recupero dei risultati, vedere [recupero di risultati (di base)](../../../odbc/reference/develop-app/retrieving-results-basic.md) e [recupero dei risultati (avanzate)](../../../odbc/reference/develop-app/retrieving-results-advanced.md).  
  
 L'applicazione ora torna a "passaggio 3: compilare ed eseguire un'istruzione SQL" per eseguire un'altra istruzione nella stessa transazione. in alternativa, procedere con "passaggio 5: eseguire il commit della transazione" per eseguire il commit o il rollback della transazione.
