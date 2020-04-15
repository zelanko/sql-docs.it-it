---
title: Compatibilità dei cursori di blocco e scorrevole per ODBC 3.x . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- SQLExtendedFetch function [ODBC], block cursors
- cursors [ODBC], compatibility issues
- SQLFetchScroll function [ODBC], block cursors
ms.assetid: 82f6cf68-cfde-4417-9788-d6382ca14bf8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c526eff6e19014c923f05ad91551a7d7c66f5294
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306342"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>Cursori rettangolari, cursori scorrevoli e compatibilità con le versioni precedenti per le applicazioni ODBC 3.x
L'esistenza di **SQLFetchScroll** e **SQLExtendedFetch** rappresenta la prima netta divisione in ODBC tra l'API (Application Programming Interface), ovvero l'insieme di funzioni chiamate dall'applicazione, e l'interfaccia del provider di servizi (SPI), ovvero l'insieme di funzioni implementate dal driver. Questa divisione è necessaria per bilanciare il requisito in ODBC *3.x*, che utilizza **SQLFetchScroll**, per allinearsi agli standard ed essere compatibile con ODBC *2.x*, che utilizza **SQLExtendedFetch**.  
  
 L'API ODBC *3.x,* ovvero il set di funzioni chiamate dall'applicazione, include **SQLFetchScroll** e gli attributi dell'istruzione correlata. ODBC *3.x* SPI, che è l'insieme di funzioni implementato dal driver, include **SQLFetchScroll**, **SQLExtendedFetch**e gli attributi dell'istruzione correlata. Poiché ODBC non applica formalmente questa divisione tra l'API e spi, è possibile che le applicazioni ODBC *3.x* chiamino **SQLExtendedFetch** e gli attributi di istruzione correlati. Tuttavia, non vi è alcun motivo per le applicazioni ODBC *3.x* per eseguire questa operazione. Per ulteriori informazioni su API e IPO, vedere l'introduzione [all'architettura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Per informazioni su come Il Gestore Driver ODBC *3.x* esegue il mapping delle chiamate ai driver ODBC *2.x* e ODBC *3.x* e sulle funzioni e gli attributi dell'istruzione che un driver ODBC *3.x* deve implementare per i cursori a blocchi e scorrevoli, vedere [Che cosa fa il driver](../../../odbc/reference/appendixes/what-the-driver-does.md) nell'appendice G: Linee guida del driver per la compatibilità con le versioni precedenti.  
  
 Nella tabella seguente vengono riepilogate le funzioni e gli attributi di istruzione che un'applicazione ODBC *3.x* deve utilizzare con i cursori di blocco e scorrevole. Vengono inoltre elencate le modifiche tra ODBC *2.x* e ODBC *3.x* in quest'area che le applicazioni ODBC *3.x* devono essere consapevoli per essere compatibili con i driver ODBC *2.x.*  
  
|Funzione o<br /><br /> attributo di istruzione|Commenti|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|Punta al segnalibro da utilizzare con **SQLFetchScroll**.<br /><br /> Quando un'applicazione imposta questo in un driver ODBC *2.x,* questo deve puntare a un segnalibro a lunghezza fissa.|  
|SQL_ATTR_ROW_STATUS_PTR|Punta alla matrice di stato della riga compilata da **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**e **SQLSetPos**.<br /><br /> Se un'applicazione imposta questo valore in un driver ODBC *2.x* e chiama **SQLBulkOperation** con *un'operazione* di SQL_ADD prima di chiamare **SQLFetchScroll**, **SQLFetch**o **SQLExtendedFetch**, viene restituito SQLSTATE HY011 (attributo non può essere impostato).<br /><br /> Quando un'applicazione chiama **SQLFetch** in un driver ODBC *2.x,* **SQLFetch** viene mappato a **SQLExtendedFetch** e pertanto restituisce valori in questa matrice.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Punta al buffer in cui **SQLFetch** e **SQLFetchScroll** restituiscono il numero di righe recuperate.<br /><br /> Quando un'applicazione chiama **SQLFetch** in un driver ODBC *2.x,* **SQLFetch** viene mappato a **SQLExtendedFetch** e pertanto restituisce un valore in questo buffer.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Imposta le dimensioni del set di righe.<br /><br /> Se un'applicazione chiama **SQLBulkOperations** con *un'operazione* di SQL_ADD in un driver ODBC *2.x,* verrà utilizzato SQL_ROWSET_SIZE per la chiamata, non SQL_ATTR_ROW_ARRAY_SIZE, perché la chiamata è mappata a **SQLSetPos** con *un'operazione* di SQL_ADD, che utilizza SQL_ROWSET_SIZE.<br /><br /> Chiamata **di SQLSetPos** con *un'operazione* di SQL_ADD o **SQLExtendedFetch** in un driver ODBC *2.x* utilizza SQL_ROWSET_SIZE.<br /><br /> La chiamata **a SQLFetch** o **SQLFetchScroll** in un driver ODBC *2.x* utilizza SQL_ATTR_ROW_ARRAY_SIZE.|  
|**Sqlbulkoperations**|Esegue operazioni di inserimento e segnalibro. Quando **SQLBulkOperations** con *un'operazione* di SQL_ADD viene chiamato in un driver ODBC *2.x,* viene eseguito il mapping a **SQLSetPos** con *un'operazione* di SQL_ADD. Di seguito sono riportati i dettagli di implementazione:The following are implementation details:<br /><br /> - Quando si utilizza un driver ODBC *2.x,* un'applicazione deve utilizzare solo l'ARD allocato in modo implicito associato a *StatementHandle*; non è possibile allocare un altro ARD per l'aggiunta di righe, perché le operazioni di descrittore esplicite non sono supportate in un driver ODBC *2.x.* Un'applicazione deve utilizzare **SQLBindCol** per l'associazione all'ARD, non **SQLSetDescField** o **SQLSetDescRec**.<br />- Quando si chiama un driver ODBC *3.x,* un'applicazione può chiamare **SQLBulkOperations** con *un'operazione* di SQL_ADD prima di chiamare **SQLFetch** o **SQLFetchScroll**. Quando si chiama un driver ODBC *2.x,* un'applicazione deve chiamare **SQLFetchScroll** prima di chiamare **SQLBulkOperations** con un'operazione di SQL_ADD.|  
|**SQLFetch**|Restituisce il set di righe successivo. Di seguito sono riportati i dettagli di implementazione:The following are implementation details:<br /><br /> - Quando un'applicazione chiama **SQLFetch** in un driver ODBC *2.x* , viene mappato a **SQLExtendedFetch**.<br />- Quando un'applicazione chiama **SQLFetch** in un driver ODBC *3.x,* restituisce il numero di righe specificato con il SQL_ATTR_ROW_ARRAY_SIZEattributo di istruzione.|  
|**SQLFetchScroll**|Restituisce il set di righe specificato. Di seguito sono riportati i dettagli di implementazione:The following are implementation details:<br /><br /> - Quando un'applicazione chiama **SQLFetchScroll** in un driver ODBC *2.x,* restituisce SQLSTATE 01S01 (errore nella riga) prima di ogni errore che si applica a una singola riga. Questa operazione viene eseguito solo perché Gestione driver ODBC *3.x* esegue il mapping a **SQLExtendedFetch** e **SQLExtendedFetch** restituisce sqlSTATE. Quando un'applicazione chiama **SQLFetchScroll** in un driver ODBC *3.x,* non restituisce mai SQLSTATE 01S01 (errore nella riga).<br />- Quando un'applicazione chiama SQLFetchScroll in un driver ODBC *2.x* con FetchOrientation impostato su SQL_FETCH_BOOKMARK, il FetchOffset argomento deve essere impostato su 0.- when an application calls **SQLFetchScroll** in an ODBC 2.x driver with *FetchOrientation* set to SQL_FETCH_BOOKMARK, the *FetchOffset* argument must be set to 0. SQLSTATE HYC00 (funzionalità facoltativa non implementata) viene restituito se si tenta di recuperare un segnalibro basato su offset con un driver ODBC *2.x.*|  
  
> [!NOTE]  
>  Le applicazioni ODBC *3.x* non devono utilizzare **SQLExtendedFetch** o l'attributo dell'istruzione SQL_ROWSET_SIZE. Al contrario, devono utilizzare **SQLFetchScroll** e l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE. Le applicazioni ODBC *3.x* non devono utilizzare **SQLSetPos** con *un'operazione* di SQL_ADD ma devono utilizzare **SQLBulkOperations** con *un'operazione* di SQL_ADD.
