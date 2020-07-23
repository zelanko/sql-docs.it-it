---
title: Cursori (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- forward-only cursors [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], about cursors
- cursors [ODBC]
- fetches [ODBC], cursors
- result sets [ODBC], fetching
- block cursors [ODBC]
ms.assetid: 0b114352-3c63-4d33-9220-182ede90e4aa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3a7484de48edaecea56fc135ca3b803875f9557c
ms.sourcegitcommit: 08f331b6a5fe72d68ef1b2eccc5d16cb80c6ee39
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "86977778"
---
# <a name="cursors"></a>Cursori
Un'applicazione recupera i dati con un *cursore*. Un cursore è diverso da un set di risultati: un set di risultati è il set di righe che corrisponde a criteri di ricerca specifici, mentre un cursore è il software che restituisce tali righe all'applicazione. Il cursore del nome *,* come si applica ai database, probabilmente è stato originato dal cursore lampeggiante su un terminale del computer. Così come il cursore indica la posizione corrente sullo schermo e il punto in cui le parole digitate verranno visualizzate successivamente, un cursore in un set di risultati indicherà la posizione corrente nel set di risultati e la riga che verrà restituita successivamente.  
  
 Il modello di cursore in ODBC è basato sul modello di cursore in SQL incorporato. Una differenza rilevante tra questi modelli è la modalità di apertura dei cursori. In Embedded SQL un cursore deve essere dichiarato e aperto in modo esplicito prima di poter essere utilizzato. In ODBC un cursore viene aperto in modo implicito quando viene eseguita un'istruzione che crea un set di risultati. Quando viene aperto, il cursore viene posizionato prima della prima riga del set di risultati. In SQL incorporato e ODBC è necessario chiudere un cursore dopo che l'applicazione ha terminato di utilizzarla.  
  
 Cursori diversi hanno caratteristiche diverse. Il tipo di cursore più comune, denominato cursore di tipo " *Avanti",* può essere spostato in avanti solo attraverso il set di risultati. Per tornare a una riga precedente, l'applicazione deve chiudere e riaprire il cursore, quindi leggere le righe dall'inizio del set di risultati finché non raggiunge la riga richiesta. I cursori di sola trasmissione forniscono un meccanismo rapido per l'esecuzione di un singolo passaggio tramite un set di risultati.  
  
 I cursori di sola trasmissione sono meno utili per le applicazioni basate su schermo, in cui l'utente scorre in avanti e indietro nei dati. Tali applicazioni possono utilizzare un cursore di tipo "di sola lettura" leggendo il set di risultati una sola volta, memorizzando nella cache i dati in locale ed eseguendo lo scorrimento. Tuttavia, questo funziona bene solo con piccole quantità di dati. Una soluzione migliore consiste nell'usare un *cursore scorrevole,* che consente l'accesso casuale al set di risultati. Tali applicazioni possono inoltre migliorare le prestazioni recuperando più di una riga di dati alla volta, utilizzando il cosiddetto cursore a *blocchi.* Per ulteriori informazioni sui cursori a blocchi, vedere [utilizzo di cursori a blocchi](../../../odbc/reference/develop-app/using-block-cursors.md).  
  
 Il cursore di sola trasmissione è il tipo di cursore predefinito in ODBC e viene descritto nelle sezioni seguenti. Per ulteriori informazioni sui cursori a blocchi e i cursori scorrevoli, vedere [blocchi cursori](../../../odbc/reference/develop-app/block-cursors.md) e [cursori scorrevoli](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
> [!IMPORTANT]  
>  Per eseguire il commit o il rollback di una transazione, chiamando in modo esplicito **SQLEndTran** o operando in modalità autocommit, alcune origini dati possono chiudere tutti i cursori in tutte le istruzioni di una connessione. Per ulteriori informazioni, vedere gli attributi SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR nella descrizione della funzione [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) .
