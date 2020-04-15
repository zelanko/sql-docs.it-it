---
title: Scorrimento relativo e assoluto Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- absolute scrolling [ODBC]
- relative scrolling [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 3d0ff48d-fef5-4c01-bb1d-a583e6269b66
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae0ed5af8d116a3038b55b1e3d68231154c2a35c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300101"
---
# <a name="relative-and-absolute-scrolling"></a>Scorrimento relativo e assoluto
La maggior parte delle opzioni di scorrimento in **SQLFetchScroll** posiziona il cursore rispetto alla posizione corrente o a una posizione assoluta. **SQLFetchScroll** supporta il recupero dei set di righe successivo, precedente, primo e ultimo, nonché il recupero relativo (recupero del set di righe *n* dall'inizio del set di righe corrente) e il recupero assoluto (recupero del set di righe a partire dalla riga *n*). Se *n* è negativo in un recupero assoluto, le righe vengono conteggiate dalla fine del set di risultati. Pertanto, un recupero assoluto della riga -1 significa recuperare il set di righe che inizia con l'ultima riga nel set di risultati.  
  
 I cursori dinamici rilevano le righe inserite ed eliminate dal set di risultati, pertanto non esiste un modo semplice per i cursori dinamici recuperare la riga in corrispondenza di un numero specifico oltre alla lettura dall'inizio del set di risultati, che probabilmente sarà lenta. Inoltre, il recupero assoluto non è molto utile nei cursori dinamici perché i numeri di riga cambiano quando le righe vengono inserite ed eliminate; pertanto, il recupero successivo dello stesso numero di riga può produrre righe diverse.  
  
 Le applicazioni che utilizzano **SQLFetchScroll** solo per le funzionalità del cursore a blocchi, ad esempio i report, probabilmente passerà attraverso il set di risultati una sola volta, usando solo l'opzione per recuperare il set di righe successivo. Le applicazioni basate su schermo, d'altra parte, possono sfruttare tutte le funzionalità di **SQLFetchScroll**. Se l'applicazione imposta la dimensione del set di righe sul numero di righe visualizzate sullo schermo e associa i buffer dello schermo al set di risultati, può convertire le operazioni della barra di scorrimento direttamente nelle chiamate a **SQLFetchScroll**.  
  
|Operazione della barra di scorrimento|Opzione di scorrimento SQLFetchScroll|  
|--------------------------|-------------------------------------|  
|Su di una pagina|SQL_FETCH_PRIOR|  
|Giù di una pagina|SQL_FETCH_NEXT|  
|Su di una riga|SQL_FETCH_RELATIVE con *FetchOffset* uguale a -1|  
|Giù di una riga|SQL_FETCH_RELATIVE con *FetchOffset* uguale a 1|  
|Casella di scorrimento in alto|SQL_FETCH_FIRST|  
|Casella di scorrimento in basso|SQL_FETCH_LAST|  
|Posizione casuale della casella di scorrimento|SQL_FETCH_ABSOLUTE|  
  
 Tali applicazioni devono anche posizionare la casella di scorrimento dopo un'operazione di scorrimento, che richiede il numero di riga corrente e il numero di righe. Per il numero di riga corrente, le applicazioni possono tenere traccia del numero di riga corrente o chiamare **SQLGetStmtAttr** con l'attributo SQL_ATTR_ROW_NUMBER per recuperarlo.  
  
 Il numero di righe nel cursore, ovvero la dimensione del set di risultati, è disponibile come campo SQL_DIAG_CURSOR_ROW_COUNT dell'intestazione diagnostica. Il valore di questo campo viene definito solo dopo la chiamata a **SQLExecute**, **SQLExecDirect**o **SQLMoreResult** . Questo conteggio può essere un conteggio approssimativo o un conteggio esatto, a seconda delle funzionalità del driver. Il supporto del driver può essere determinato chiamando **SQLGetInfo** con i tipi di informazioni sugli attributi del cursore e controllando se viene restituito il bit SQL_CA2_CRC_APPROXIMATE o SQL_CA2_CRC_EXACT per il tipo di cursore.  
  
 Un conteggio esatto delle righe non è mai supportato per un cursore dinamico. Per altri tipi di cursori, il driver può supportare conteggi di righe esatti o approssimativi, ma non entrambi. Se il driver non supporta i conteggi delle righe esatte né approssimative per un tipo di cursore specifico, il campo SQL_DIAG_CURSOR_ROW_COUNT contiene il numero di righe che sono state recuperate finora. Indipendentemente da ciò che il driver supporta, **SQLFetchScroll** con un *Operazione* di SQL_FETCH_LAST causerà il SQL_DIAG_CURSOR_ROW_COUNT campo per contenere il conteggio esatto delle righe.
