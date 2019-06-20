---
title: 'Passaggio 4a: Recuperare i risultati | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cad33f1ccf798a08ef1f11667e59b4d5fb4888d8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149203"
---
# <a name="step-4a-fetch-the-results"></a>Passaggio 4a: Recuperare i risultati
Il passaggio successivo è per recuperare i risultati, come illustrato nella figura seguente.  
  
 ![Recupero di risultati in un'applicazione ODBC](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 Se l'istruzione eseguita "passaggio 3: Compilare ed eseguire un'istruzione SQL"è stata una **selezionate** istruzione o una funzione di catalogo, l'applicazione chiama innanzitutto **SQLNumResultCols** per determinare il numero di colonne nel set di risultati. Questo passaggio non è necessario se l'applicazione ha già conosce il numero di risultati set di colonne, ad esempio quando l'istruzione SQL è hardcoded in un'applicazione personalizzata o verticale.  
  
 Successivamente, l'applicazione recupera il nome, tipo di dati, precisione e scala di ogni colonna del set di risultati con **SQLDescribeCol**. Anche in questo caso, non necessario per le applicazioni, ad esempio applicazioni verticali e personalizzate che già conoscono tali informazioni. L'applicazione passa queste informazioni per **SQLBindCol**, che si associa una variabile di applicazione a una colonna nel set di risultati.  
  
 L'applicazione viene ora chiamato **SQLFetch** per recuperare la prima riga di dati e inserire i dati da tale riga nelle variabili associate con **SQLBindCol**. Se sono presenti dati lungo nella riga, quindi chiama **SQLGetData** per recuperare i dati. L'applicazione continua a chiamare **SQLFetch** e **SQLGetData** per recuperare dati aggiuntivi. Dopo avere completato il recupero dei dati, viene chiamato **SQLCloseCursor** per chiudere il cursore.  
  
 Per una descrizione completa del recupero dei risultati, vedere [recupero di risultati (Basic)](../../../odbc/reference/develop-app/retrieving-results-basic.md) e [il recupero dei risultati (avanzate)](../../../odbc/reference/develop-app/retrieving-results-advanced.md).  
  
 A questo punto l'applicazione torna al "passaggio 3: Compilare ed eseguire un'istruzione SQL"per eseguire un'altra istruzione nella stessa transazione; o procede al "passaggio 5: Eseguire il commit della transazione"per eseguire il commit o rollback della transazione.
