---
title: Compatibilità tra cursori e blocchi scorrevoli per ODBC 3. x | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7d12906f8dec0bfb12fc861c067e6e615e758a3b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68134993"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>Cursori rettangolari, cursori scorrevoli e compatibilità con le versioni precedenti per le applicazioni ODBC 3.x
L'esistenza di **SQLFetchScroll** e **SQLExtendedFetch** rappresenta la prima suddivisione chiara in ODBC tra l'API (Application Programming Interface), ovvero il set di funzioni chiamate dall'applicazione, e l'interfaccia del provider di servizi (SPI), ovvero il set di funzioni implementate dal driver. Questa suddivisione è necessaria per bilanciare il requisito in ODBC *3. x*, che usa **SQLFetchScroll**, per allinearsi agli standard ed essere compatibile con ODBC *2. x*, che usa **SQLExtendedFetch**.  
  
 L'API ODBC *3. x* , ovvero il set di funzioni chiamate dall'applicazione, include **SQLFetchScroll** e gli attributi dell'istruzione correlati. ODBC *3. x* SPI, ovvero il set di funzioni implementate dal driver, include **SQLFetchScroll**, **SQLExtendedFetch**e gli attributi di istruzione correlati. Poiché ODBC non impone formalmente questa suddivisione tra l'API e il SPI, è possibile che le applicazioni ODBC *3. x* chiamino **SQLExtendedFetch** e gli attributi dell'istruzione correlati. Tuttavia, non esiste alcun motivo per le applicazioni ODBC *3. x* a tale scopo. Per ulteriori informazioni sulle API e SPIs, vedere Introduzione all' [architettura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Per informazioni sul modo in cui il gestore di driver ODBC *3. x* esegue il mapping delle chiamate ai driver ODBC *2. x* e ODBC *3. x* e sulle funzioni e sugli attributi di istruzioni che devono essere implementati da un driver ODBC *3. x* per i cursori Block e scroll, vedere la pagina relativa alle linee guida per la compatibilità con le versioni precedenti [del](../../../odbc/reference/appendixes/what-the-driver-does.md) driver.  
  
 Nella tabella seguente sono riepilogate le funzioni e gli attributi di istruzione che un'applicazione ODBC *3. x* deve utilizzare con i cursori Block e scroll. Vengono inoltre elencate le modifiche tra ODBC *2. x* e ODBC *3. x* in quest'area in cui le applicazioni ODBC *3. x* devono essere consapevoli di essere compatibili con i driver ODBC *2. x* .  
  
|Funzione or<br /><br /> attributo di istruzione|Commenti|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|Punta al segnalibro da usare con **SQLFetchScroll**.<br /><br /> Quando un'applicazione imposta questa impostazione in un driver ODBC *2. x* , deve puntare a un segnalibro a lunghezza fissa.|  
|SQL_ATTR_ROW_STATUS_PTR|Punta alla matrice di stato della riga compilata da **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**e **SQLSetPos**.<br /><br /> Se un'applicazione imposta questa impostazione in un driver ODBC *2. x* e chiama **SQLBulkOperation** con un' *operazione* di SQL_ADD prima della chiamata a **SQLFetchScroll**, **SQLFetch**o **SQLExtendedFetch**, viene restituito SQLState HY011 (l'attributo non può essere impostato adesso).<br /><br /> Quando un'applicazione chiama **SQLFetch** in un driver ODBC *2. x* , viene eseguito il mapping di **SQLFetch** a **SQLExtendedFetch** e pertanto restituisce i valori in questa matrice.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Punta al buffer in cui **SQLFetch** e **SQLFetchScroll** restituiscono il numero di righe recuperate.<br /><br /> Quando un'applicazione chiama **SQLFetch** in un driver ODBC *2. x* , viene eseguito il mapping di **SQLFetch** a **SQLExtendedFetch** e pertanto viene restituito un valore in questo buffer.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Imposta la dimensione del set di righe.<br /><br /> Se un'applicazione chiama **SQLBulkOperations** con un' *operazione* di SQL_ADD in un driver ODBC *2. x* , SQL_ROWSET_SIZE verrà usato per la chiamata, non SQL_ATTR_ROW_ARRAY_SIZE, perché la chiamata viene mappata a **SQLSetPos** con un' *operazione* di SQL_ADD, che usa SQL_ROWSET_SIZE.<br /><br /> La chiamata di **SQLSetPos** con un' *operazione* di SQL_ADD o **SQLExtendedFetch** in un driver ODBC *2. x* USA SQL_ROWSET_SIZE.<br /><br /> La chiamata a **SQLFetch** o **SQLFetchScroll** in un driver ODBC *2. x* utilizza SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLBulkOperations**|Esegue operazioni di inserimento e segnalibro. Quando **SQLBulkOperations** con un' *operazione* di SQL_ADD viene chiamato in un driver ODBC *2. x* , viene eseguito il mapping a **SQLSetPos** con un' *operazione* di SQL_ADD. Di seguito sono riportati i dettagli di implementazione:<br /><br /> -Quando si utilizza un driver ODBC *2. x* , un'applicazione deve utilizzare solo l'ARD allocato in modo implicito a *statementHandle*; non è possibile allocare un altro ARD per l'aggiunta di righe, perché le operazioni di descrittore esplicite non sono supportate in un driver ODBC *2. x* . Un'applicazione deve usare **SQLBindCol** per eseguire l'associazione a Ard, non a **SQLSetDescField** o **SQLSetDescRec**.<br />-Quando si chiama un driver ODBC *3. x* , un'applicazione può chiamare **SQLBulkOperations** con un' *operazione* di SQL_ADD prima di chiamare **SQLFetch** o **SQLFetchScroll**. Quando si chiama un driver ODBC *2. x* , un'applicazione deve chiamare **SQLFetchScroll** prima di chiamare **SQLBulkOperations** con un'operazione di SQL_ADD.|  
|**SQLFetch**|Restituisce il set di righe successivo. Di seguito sono riportati i dettagli di implementazione:<br /><br /> -Quando un'applicazione chiama **SQLFetch** in un driver ODBC *2. x* , viene eseguito il mapping a **SQLExtendedFetch**.<br />-Quando un'applicazione chiama **SQLFetch** in un driver ODBC *3. x* , restituisce il numero di righe specificate con l'attributo dell'istruzione SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLFetchScroll**|Restituisce il set di righe specificato. Di seguito sono riportati i dettagli di implementazione:<br /><br /> -Quando un'applicazione chiama **SQLFetchScroll** in un driver ODBC *2. x* , restituisce SQLSTATE 01S01 (errore nella riga) prima di ogni errore che si applica a una singola riga. Questa operazione viene eseguita solo perché Gestione driver ODBC *3. x* esegue il mapping a **SQLExtendedFetch** e **SQLExtendedFetch** restituisce questo SQLSTATE. Quando un'applicazione chiama **SQLFetchScroll** in un driver ODBC *3. x* , non restituisce mai SQLSTATE 01S01 (errore nella riga).<br />-Quando un'applicazione chiama **SQLFetchScroll** in un driver ODBC *2. x* con *FetchOrientation* impostato su SQL_FETCH_BOOKMARK, l'argomento *FetchOffset* deve essere impostato su 0. SQLSTATE HYC00 (funzionalità facoltativa non implementata) viene restituito se si tenta il recupero di segnalibri basato su offset con un driver ODBC *2. x* .|  
  
> [!NOTE]  
>  Le applicazioni ODBC *3. x* non devono utilizzare **SQLExtendedFetch** o l'attributo dell'istruzione SQL_ROWSET_SIZE. Devono invece usare **SQLFetchScroll** e l'attributo dell'istruzione SQL_ATTR_ROW_ARRAY_SIZE. Le applicazioni ODBC *3. x* non devono usare **SQLSetPos** con un' *operazione* di SQL_ADD ma devono usare **SQLBulkOperations** con un' *operazione* di SQL_ADD.
