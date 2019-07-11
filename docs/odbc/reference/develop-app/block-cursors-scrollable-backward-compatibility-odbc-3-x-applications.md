---
title: Blocco e la compatibilità di cursori scorrevoli per ODBC 3.x | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 49a7a1af0f4b487baddfffa3e4f14d2a148b7a1d
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794044"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>Cursori rettangolari, cursori scorrevoli e compatibilità con le versioni precedenti per le applicazioni ODBC 3.x
La presenza di entrambe **SQLFetchScroll** e **SQLExtendedFetch** rappresenta cancellare le prima di tutto è suddiviso in ODBC tra l'interfaccia API (Application Programming), ovvero il set di funzioni di le chiamate dell'applicazione e il servizio Provider di interfaccia (SPI), ovvero il set di funzioni il driver implementa. Questa suddivisione deve bilanciare l'esigenza in ODBC *3.x*, che usa **SQLFetchScroll**, per allineare con gli standard e di essere compatibile con ODBC *2.x*, che usa **SQLExtendedFetch**.  
  
 ODBC *3.x* API, ovvero il set di funzioni l'applicazione chiama, includono **SQLFetchScroll** e relativi attributi di istruzione. ODBC *3.x* SPI, ovvero il set di funzioni implementa il driver, include **SQLFetchScroll**, **SQLExtendedFetch**e i relativi attributi di istruzione. Poiché ODBC non impone formalmente questa suddivisione tra l'API e di SPI, è possibile che per ODBC *3.x* alle applicazioni di chiamare **SQLExtendedFetch** e relativi attributi di istruzione. Tuttavia, non vi è alcun motivo per ODBC *3.x* alle applicazioni di eseguire questa operazione. Per altre informazioni sulle API e SPI, vedere l'introduzione [architettura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Per informazioni su come ODBC *3.x* Driver Manager esegue il mapping di chiamate a ODBC *2.x* e ODBC *3.x* driver e le funzioni e istruzione degli attributi un ODBC *3.x* driver deve implementare per i cursori scorrevoli e blocco, vedere [il Driver del funzionamento di](../../../odbc/reference/appendixes/what-the-driver-does.md) nell'appendice g: Driver linee guida per la compatibilità con le versioni precedenti.  
  
 La tabella seguente riepiloga le funzioni e gli attributi delle istruzioni un ODBC *3.x* applicazione deve usare con i cursori scorrevoli e blocco. Sono inoltre indicate le modifiche tra ODBC *2.x* e ODBC *3.x* in quest'area che ODBC *3.x* applicazioni devono tenere presente per essere compatibile con ODBC *2.x* i driver.  
  
|Funzione o<br /><br /> attributo di istruzione|Commenti|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|Punta al segnalibro da usare con **SQLFetchScroll**.<br /><br /> Quando un'applicazione imposta questo in un database ODBC *2.x* driver, questa deve puntare a un segnalibro a lunghezza fissa.|  
|SQL_ATTR_ROW_STATUS_PTR|I punti nella matrice di stato di riga vengono immesse **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, e **SQLSetPos**.<br /><br /> Se si imposta un'applicazione in un database ODBC *2.x* driver e le chiamate **SQLBulkOperation** con un *operazione* di SQL_ADD prima di chiamare **SQLFetchScroll**, **SQLFetch**, o **SQLExtendedFetch**, SQLSTATE HY011 (attributo non può essere impostato a questo punto) viene restituito.<br /><br /> Quando un'applicazione chiama **SQLFetch** in un database ODBC *2.x* driver **SQLFetch** è mappato alla **SQLExtendedFetch** e pertanto restituisce valori in questa matrice.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Fa riferimento al buffer in cui **SQLFetch** e **SQLFetchScroll** restituiscono il numero di righe recuperate.<br /><br /> Quando un'applicazione chiama **SQLFetch** in un database ODBC *2.x* driver **SQLFetch** è mappato alla **SQLExtendedFetch** e pertanto restituisce un valore di questo buffer.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Imposta le dimensioni del set di righe.<br /><br /> Se un'applicazione chiama **SQLBulkOperations** con un *operazione* di SQL_ADD in un database ODBC *2.x* driver, SQL_ROWSET_SIZE verrà usato per la chiamata, non SQL_ATTR_ROW_ARRAY_ Modificare le dimensioni, perché la chiamata viene mappata a **SQLSetPos** con un *operazione* di SQL_ADD, che usa SQL_ROWSET_SIZE.<br /><br /> La chiamata **SQLSetPos** con un *operazione* di SQL_ADD oppure **SQLExtendedFetch** in un database ODBC *2.x* SQL_ROWSET_SIZE utilizzato dal driver.<br /><br /> La chiamata **SQLFetch** oppure **SQLFetchScroll** in un database ODBC *2.x* driver utilizza SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLBulkOperations**|Esegue le operazioni insert e del segnalibro. Quando **SQLBulkOperations** con un *operazione* di SQL_ADD viene chiamato in un database ODBC *2.x* driver, ne viene eseguito il mapping a **SQLSetPos** con un  *Operazione* di SQL_ADD. Di seguito sono i dettagli di implementazione:<br /><br /> -Quando si lavora con un database ODBC *2.x* driver, un'applicazione deve usare solo il ARD allocati in modo implicito associato con il *StatementHandle*; non è possibile allocare un altro ARD per l'aggiunta di righe, perché esplicita operazioni di descrittore non sono supportate in un database ODBC *2.x* driver. Un'applicazione deve utilizzare **SQLBindCol** da associare alla ARD, non **SQLSetDescField** oppure **SQLSetDescRec**.<br />-Quando si chiama un ODBC *3.x* driver, un'applicazione può chiamare **SQLBulkOperations** con un *operazione* di SQL_ADD prima di chiamare **SQLFetch**oppure **SQLFetchScroll**. Quando si chiama un ODBC *2.x* driver, un'applicazione deve chiamare **SQLFetchScroll** prima di chiamare **SQLBulkOperations** con un'operazione di SQL_ADD.|  
|**SQLFetch**|Restituisce il successivo set di righe. Di seguito sono i dettagli di implementazione:<br /><br /> -Quando un'applicazione chiama **SQLFetch** in un database ODBC *2.x* driver, ne viene eseguito il mapping a **SQLExtendedFetch**.<br />-Quando un'applicazione chiama **SQLFetch** in un database ODBC *3.x* driver, restituisce il numero di righe specificato con l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLFetchScroll**|Restituisce il set di righe specificato. Di seguito sono i dettagli di implementazione:<br /><br /> -Quando un'applicazione chiama **SQLFetchScroll** in un database ODBC *2.x* driver, restituisce SQLSTATE 01S01 (errore nella riga) prima di ogni errore che si applica a una singola riga. Ciò avviene solo perché ODBC *3.x* Driver Manager esegue il mapping allo **SQLExtendedFetch** e **SQLExtendedFetch** restituisce questo valore SQLSTATE. Quando un'applicazione chiama **SQLFetchScroll** in un database ODBC *3.x* driver, non restituisce mai SQLSTATE 01S01 (errore nella riga).<br />-Quando un'applicazione chiama **SQLFetchScroll** in un database ODBC *2.x* driver con *FetchOrientation* impostato su SQL_FETCH_BOOKMARK, il *FetchOffset* argomento deve essere impostato su 0. SQLSTATE HYC00 (funzionalità facoltativa non implementata) viene restituito se si tenta il recupero di offset in base al segnalibro con un database ODBC *2.x* driver.|  
  
> [!NOTE]  
>  ODBC *3.x* le applicazioni non devono utilizzare **SQLExtendedFetch** o l'attributo di istruzione SQL_ROWSET_SIZE. È necessario utilizzare invece **SQLFetchScroll** e l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE. ODBC *3.x* le applicazioni non devono utilizzare **SQLSetPos** con un *operazione* di SQL_ADD è invece necessario utilizzare **SQLBulkOperations** con un  *Operazione* di SQL_ADD.
