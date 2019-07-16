---
title: Scorrimento relativo e assoluto | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e2034a3922dcd3db77113e08a6c48fe7ac39457f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138064"
---
# <a name="relative-and-absolute-scrolling"></a>Scorrimento relativo e assoluto
La maggior parte delle opzioni di scorrimento nella **SQLFetchScroll** posizionare il cursore rispetto alla posizione corrente o a una posizione assoluta. **SQLFetchScroll** supporta il recupero successivo, precedente, primo e ultimo set di righe, come il recupero anche come relativo (recuperare il set di righe *n* righe dall'inizio del set di righe corrente) e il recupero assoluto (recupero di inizio del set di righe nella riga *n*). Se *n* è negativo in un recupero assoluto, le righe vengono conteggiate dalla fine del set di risultati. Di conseguenza, un recupero assoluto della riga -1 significa che recuperare il set di righe che inizia con l'ultima riga nel set di risultati.  
  
 I cursori dinamici rilevano righe inserite ed eliminate dal set di risultati, in modo che non esiste un modo semplice per i cursori dinamici recuperare la riga in corrispondenza di un particolare numero diverso da leggere dall'inizio del set di risultati, è probabile che sia lento. Inoltre, il recupero assoluto non è molto utile per i cursori dinamici perché i numeri di riga è stata modificata righe vengono inserite ed eliminate; Pertanto, in successione recupero lo stesso numero di riga può generare righe diverse.  
  
 Le applicazioni che usano **SQLFetchScroll** solo per il relativo blocco di funzionalità del cursore, ad esempio report, è probabile che passano attraverso il set di risultati una sola volta, utilizzando solo l'opzione per recuperare il successivo set di righe. Le applicazioni basate su schermo, d'altra parte, possono sfruttare tutte le funzionalità di **SQLFetchScroll**. Se l'applicazione imposta le dimensioni del set di righe per il numero di righe visualizzate sullo schermo e associa i buffer dello schermo al set di risultati, può convertire operazioni della barra di scorrimento direttamente in chiamate a **SQLFetchScroll**.  
  
|Operazione della barra di scorrimento|Opzione di scorrimento SQLFetchScroll|  
|--------------------------|-------------------------------------|  
|Su di una pagina|SQL_FETCH_PRIOR|  
|Giù di una pagina|SQL_FETCH_NEXT|  
|Su di una riga|SQL_FETCH_RELATIVE con *FetchOffset* uguale a -1|  
|Giù di una riga|SQL_FETCH_RELATIVE con *FetchOffset* uguale a 1|  
|Casella di scorrimento nella parte superiore|SQL_FETCH_FIRST|  
|Casella di scorrimento nella parte inferiore|SQL_FETCH_LAST|  
|Posizione casuale della casella di scorrimento|SQL_FETCH_ABSOLUTE|  
  
 Tali applicazioni è necessario anche posizionare la casella di scorrimento dopo un'operazione di scorrimento, che richiede il numero di riga corrente e il numero di righe. Per il numero di riga corrente, le applicazioni possono essere tenere traccia del numero di riga corrente o la chiamata **SQLGetStmtAttr** con l'attributo SQL_ATTR_ROW_NUMBER per recuperarlo.  
  
 Il numero di righe nel cursore, ovvero le dimensioni del risultato impostato, è disponibile come campo SQL_DIAG_CURSOR_ROW_COUNT dell'intestazione di diagnostica. Il valore in questo campo viene definito solo dopo aver **SQLExecute**, **SQLExecDirect**, o **SQLMoreResult** è stato chiamato. Questo conteggio può essere un numero approssimativo o un conteggio esatto, a seconda delle funzionalità del driver. Supporto del driver può essere determinato chiamando **SQLGetInfo** con i tipi di informazioni di attributi del cursore e verifica se il bit SQL_CA2_CRC_APPROXIMATE o SQL_CA2_CRC_EXACT viene restituito per il tipo di cursore.  
  
 Un conteggio esatto non è mai supportato per un cursore dinamico. Per altri tipi di cursori, il driver supporta il conteggio delle righe esatto o approssimativo, ma non entrambi. Se il driver non supporta né esatta né approssimativo i conteggi delle righe per un tipo di cursore specifico, il campo SQL_DIAG_CURSOR_ROW_COUNT contiene il numero di righe che sono stati recuperati finora. Indipendentemente dal fatto che il driver supporta, **SQLFetchScroll** con un *operazione* di SQL_FETCH_LAST causerà il campo SQL_DIAG_CURSOR_ROW_COUNT contenere il numero di riga esatti.
