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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da899e4dc47daff03c31277b3edd4d9c642b87cb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305292"
---
# <a name="cursors"></a>Cursori
Un'applicazione recupera i dati con un *cursore*. Un cursore è diverso da un set di risultati: un set di risultati è il set di righe che corrisponde a criteri di ricerca specifici, mentre un cursore è il software che restituisce tali righe all'applicazione. Il *cursore* del nome, come si applica ai database, probabilmente ha avuto origine dal cursore lampeggiante su un terminale di computer. Così come il cursore indica la posizione corrente sullo schermo e dove verranno visualizzate le parole digitate successivamente, un cursore su un set di risultati indica la posizione corrente nel set di risultati e quale riga verrà restituita successivamente.  
  
 Il modello di cursore in ODBC è basato sul modello di cursore in SQL incorporato. Una differenza notevole tra questi modelli è il modo in cui i cursori vengono aperti. In SQL incorporato, un cursore deve essere dichiarato e aperto in modo esplicito prima di poter essere utilizzato. In ODBC, un cursore viene aperto in modo implicito quando viene eseguita un'istruzione che crea un set di risultati. Quando il cursore viene aperto, viene posizionato prima della prima riga del set di risultati. In SQL incorporato e ODBC, un cursore deve essere chiuso dopo che l'applicazione ha terminato di utilizzarlo.  
  
 Cursori diversi hanno caratteristiche diverse. Il tipo più comune di cursore, denominato *cursore forward-only,* può spostarsi solo in avanti nel set di risultati. Per tornare a una riga precedente, l'applicazione deve chiudere e riaprire il cursore e quindi leggere le righe dall'inizio del set di risultati fino a raggiungere la riga richiesta. I cursori forward-only forniscono un meccanismo rapido per eseguire un singolo passaggio attraverso un set di risultati.  
  
 I cursori forward-only sono meno utili per le applicazioni basate su schermo, in cui l'utente scorre avanti e indietro tra i dati. Tali applicazioni possono utilizzare un cursore forward-only leggendo una volta il set di risultati, memorizzando i dati nella cache in locale ed eseguendo lo scorrimento. Tuttavia, questo funziona bene solo con piccole quantità di dati. Una soluzione migliore consiste nell'utilizzare un *cursore scorrevole,* che fornisce l'accesso casuale al set di risultati. Tali applicazioni possono anche aumentare le prestazioni recuperando più di una riga di dati alla volta, utilizzando quello che viene chiamato un cursore a *blocchi.* Per ulteriori informazioni sui cursori a blocchi, consultate [Utilizzo dei cursori](../../../odbc/reference/develop-app/using-block-cursors.md)a blocchi.  
  
 Il cursore forward-only è il tipo di cursore predefinito in ODBC ed è illustrato nelle sezioni seguenti. Per ulteriori informazioni sui cursori a blocchi e sui cursori scorrevoli, consultate [Cursori](../../../odbc/reference/develop-app/block-cursors.md) a blocchi e [Cursori scorrevoli.](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
> [!IMPORTANT]  
>  Il commit o il rollback di una transazione, chiamando in modo esplicito **SQLEndTran** o operando in modalità di commit automatico, fa sì che alcune origini dati chiudano tutti i cursori in tutte le istruzioni in una connessione. Per altre informazioni, vedere gli attributi SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR nella descrizione della funzione [SQLGetInfo.For](../../../odbc/reference/syntax/sqlgetinfo-function.md) more information, see the SQL_CURSOR_COMMIT_BEHAVIOR and SQL_CURSOR_ROLLBACK_BEHAVIOR attributes in the SQLGetInfo function description.
