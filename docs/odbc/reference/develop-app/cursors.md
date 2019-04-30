---
title: Cursori | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91765f0572d8c880f7505948f7756b373fe28f62
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042127"
---
# <a name="cursors"></a>Cursori
Un'applicazione recupera i dati con un *cursore*. Un cursore è diverso da un set di risultati: Un set di risultati è il set di righe che corrisponde ai criteri di ricerca specifico, mentre un cursore è il software che restituisce le righe per l'applicazione. Il nome *cursore,* applicato ai database, probabilmente provenienti dal cursore intermittente in un computer terminal. Come tale cursore indica la posizione corrente nella schermata e in cui le parole digitate apparirà successive, un cursore su un set di risultati indica la posizione corrente nel set di risultati e quali righe verrà restituiti successivamente.  
  
 Il modello di cursore in ODBC si basa sul modello di cursore in embedded SQL. Una differenza fondamentale tra questi modelli è che il modo di cursori viene aperti. In embedded SQL, un cursore debba essere esplicitamente dichiarato e aperti prima che possa essere utilizzato. In ODBC un cursore è aperto in modo implicito quando viene eseguita un'istruzione che crea un set di risultati. Quando il cursore è aperto, viene posizionato prima la prima riga del set di risultati. In entrambi embedded SQL e ODBC, è necessario chiudere un cursore dopo l'applicazione ha finito di usarlo.  
  
 I cursori diversi hanno caratteristiche diverse. Il tipo più comune di cursore, che viene chiamato un *cursori forward-only,* possibile solo spostare in avanti attraverso il set di risultati. Per tornare a una riga precedente, l'applicazione deve chiudere e riaprire il cursore e quindi leggere righe dall'inizio del gruppo di risultati fino a raggiungere la riga necessaria. I cursori forward-only forniscono un meccanismo veloce per l'esecuzione di una singola iterazione di un set di risultati.  
  
 I cursori forward-only sono meno utile per le applicazioni basate su schermo, in cui l'utente scorre all'indietro e avanti tramite i dati. Tali applicazioni possono utilizzare un cursore forward-only leggendo il risultato impostato al termine, la memorizzazione nella cache i dati in locale e l'esecuzione di scorrimento se stessi. Tuttavia, ciò funziona anche solo con piccole quantità di dati. Una soluzione migliore consiste nell'usare un *cursori scorrevoli,* che fornisce accesso casuale al set di risultati. Tali applicazioni possono inoltre aumentare le prestazioni mediante il recupero di più righe di dati alla volta, tramite il cosiddetto un *cursore a blocchi.* Per altre informazioni sui cursori a blocchi, vedere [cursori a blocchi usando](../../../odbc/reference/develop-app/using-block-cursors.md).  
  
 I cursori forward-only sono il tipo di cursore predefinito in ODBC e viene illustrato nelle sezioni seguenti. Per altre informazioni sui cursori a blocchi e i cursori scorrevoli, vedere [cursori rettangolari](../../../odbc/reference/develop-app/block-cursors.md) e [cursori scorrevoli](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
> [!IMPORTANT]  
>  Eseguire il commit o rollback di una transazione, in modo esplicito chiamando **SQLEndTran** o da opera in modalità autocommit, fa sì che alcune origini dati chiudere tutti i cursori su tutte le istruzioni in una connessione. Per altre informazioni, vedere gli attributi SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR nel [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrizione della funzione.
