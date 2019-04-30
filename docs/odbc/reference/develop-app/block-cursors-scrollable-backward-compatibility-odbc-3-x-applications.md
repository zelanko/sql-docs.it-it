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
ms.openlocfilehash: b0bc45169a3c5eee2e23f581a66d5232c22e89b0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199267"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>Cursori rettangolari, cursori scorrevoli e compatibilità con le versioni precedenti per le applicazioni ODBC 3.x
La presenza di entrambe **SQLFetchScroll** e **SQLExtendedFetch** rappresenta cancellare le prima di tutto è suddiviso in ODBC tra l'interfaccia API (Application Programming), ovvero il set di funzioni di le chiamate dell'applicazione e il servizio Provider di interfaccia (SPI), ovvero il set di funzioni il driver implementa. Questa suddivisione deve bilanciare l'esigenza in ODBC 3. *x*, che usa **SQLFetchScroll**, per allineare con gli standard e di essere compatibile con ODBC 2. *x*, che usa **SQLExtendedFetch**.  
  
 ODBC 3 *. x* API, ovvero il set di funzioni l'applicazione chiama, includono **SQLFetchScroll** e relativi attributi di istruzione. ODBC 3 *. x* SPI, ovvero il set di funzioni implementa il driver, include **SQLFetchScroll**, **SQLExtendedFetch**e i relativi attributi di istruzione. Poiché ODBC non impone formalmente questa suddivisione tra l'API e di SPI, è possibile che per ODBC 3 *. x* alle applicazioni di chiamare **SQLExtendedFetch** e relativi attributi di istruzione. Tuttavia, non vi è alcun motivo per ODBC 3*x* alle applicazioni di eseguire questa operazione. Per altre informazioni sulle API e SPI, vedere l'introduzione [architettura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Per informazioni su come ODBC 3. *x* Driver Manager esegue il mapping di chiamate a ODBC 2. *x* e ODBC 3. *x* i driver e le funzioni e istruzione degli attributi un'applicazione ODBC 3. *x* driver deve implementare per i cursori scorrevoli e blocco, vedere [il Driver del funzionamento di](../../../odbc/reference/appendixes/what-the-driver-does.md) nell'appendice g: Driver linee guida per la compatibilità con le versioni precedenti.  
  
 La tabella seguente riepiloga le funzioni e gli attributi delle istruzioni un'applicazione ODBC 3. *x* applicazione deve usare con i cursori scorrevoli e blocco. Elenca anche le modifiche tra ODBC 2. *x* e ODBC 3. *x* in questa area che ODBC 3. *x* le applicazioni devono tenere presente per essere compatibile con ODBC 2. *x* driver.  
  
|Funzione o<br /><br /> attributo di istruzione|Commenti|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|Punta al segnalibro da usare con **SQLFetchScroll**.<br /><br /> Quando un'applicazione imposta questo in un'API ODBC 2. *x* driver, questa deve puntare a un segnalibro a lunghezza fissa.|  
|SQL_ATTR_ROW_STATUS_PTR|I punti nella matrice di stato di riga vengono immesse **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, e **SQLSetPos**.<br /><br /> Se un'applicazione configura questa impostazione in un ODBC 2. *x* driver e le chiamate **SQLBulkOperation** con un *operazione* di SQL_ADD prima di chiamare **SQLFetchScroll**,  **SQLFetch**, oppure **SQLExtendedFetch**, SQLSTATE HY011 (attributo non può essere impostato a questo punto) viene restituito.<br /><br /> Quando un'applicazione chiama **SQLFetch** in un'API ODBC 2. *x* driver **SQLFetch** viene mappato a **SQLExtendedFetch** , quindi restituisce i valori in questa matrice.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Fa riferimento al buffer in cui **SQLFetch** e **SQLFetchScroll** restituiscono il numero di righe recuperate.<br /><br /> Quando un'applicazione chiama **SQLFetch** in un'API ODBC 2. *x* driver **SQLFetch** viene mappato a **SQLExtendedFetch** e pertanto restituisce un valore di questo buffer.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Imposta le dimensioni del set di righe.<br /><br /> Se un'applicazione chiama **SQLBulkOperations** con un *operazione* di SQL_ADD in un'API ODBC 2. *x* driver, SQL_ROWSET_SIZE verrà usato per la chiamata, non SQL_ATTR_ROW_ARRAY_SIZE, perché la chiamata viene eseguito il mapping a **SQLSetPos** con un *operazione* di SQL_ADD, che usa SQL_ROWSET_SIZE.<br /><br /> La chiamata **SQLSetPos** con un *operazione* di SQL_ADD oppure **SQLExtendedFetch** in un database ODBC 2. *x* SQL_ROWSET_SIZE utilizzato dal driver.<br /><br /> La chiamata **SQLFetch** oppure **SQLFetchScroll** in un database ODBC 2. *x* driver utilizza SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLBulkOperations**|Esegue le operazioni insert e del segnalibro. Quando **SQLBulkOperations** con un *operazione* di SQL_ADD viene chiamato in un'API ODBC 2. *x* driver, ne viene eseguito il mapping a **SQLSetPos** con un *operazione* di SQL_ADD. Di seguito sono i dettagli di implementazione:<br /><br /> -Quando si lavora con un'API ODBC 2. *x* driver, un'applicazione deve usare solo il ARD allocati in modo implicito associato con il *StatementHandle*; non è possibile allocare ARD un'altra per l'aggiunta di righe, poiché le operazioni esplicite descrittore sono non è supportato in un'API ODBC 2. *x* driver. Un'applicazione deve utilizzare **SQLBindCol** da associare alla ARD, non **SQLSetDescField** oppure **SQLSetDescRec**.<br />-Quando si chiama un'applicazione ODBC 3. *x* driver, un'applicazione può chiamare **SQLBulkOperations** con un *operazione* di SQL_ADD prima di chiamare **SQLFetch** o**SQLFetchScroll**. Quando si chiama un'API ODBC 2. *x* driver, un'applicazione deve chiamare **SQLFetchScroll** prima di chiamare **SQLBulkOperations** con un'operazione di SQL_ADD.|  
|**SQLFetch**|Restituisce il successivo set di righe. Di seguito sono i dettagli di implementazione:<br /><br /> -Quando un'applicazione chiama **SQLFetch** in un'API ODBC 2. *x* driver, ne viene eseguito il mapping a **SQLExtendedFetch**.<br />-Quando un'applicazione chiama **SQLFetch** in un'applicazione ODBC 3. *x* driver, restituisce il numero di righe specificato con l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLFetchScroll**|Restituisce il set di righe specificato. Di seguito sono i dettagli di implementazione:<br /><br /> -Quando un'applicazione chiama **SQLFetchScroll** in un'API ODBC 2. *x* driver, restituisce SQLSTATE 01S01 (errore nella riga) prima di ogni errore che si applica a una singola riga. Ciò avviene perché solo il 3 di ODBC *. x* Driver Manager esegue il mapping di questa opzione per **SQLExtendedFetch** e **SQLExtendedFetch** restituisce questo valore SQLSTATE di. Quando un'applicazione chiama **SQLFetchScroll** in un'applicazione ODBC 3. *x* driver, non restituisce mai SQLSTATE 01S01 (errore nella riga).<br />-Quando un'applicazione chiama **SQLFetchScroll** in un'API ODBC 2. *x* driver con *FetchOrientation* impostato su SQL_FETCH_BOOKMARK, il *FetchOffset* argomento deve essere impostato su 0. SQLSTATE HYC00 (funzionalità facoltativa non implementata) viene restituito se il recupero di offset in base al segnalibro viene tentato con un'API ODBC 2. *x* driver.|  
  
> [!NOTE]  
>  ODBC 3. *x* le applicazioni non devono utilizzare **SQLExtendedFetch** o l'attributo di istruzione SQL_ROWSET_SIZE. È necessario utilizzare invece **SQLFetchScroll** e l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE. ODBC 3. *x* le applicazioni non devono utilizzare **SQLSetPos** con un *operazione* di SQL_ADD è invece necessario utilizzare **SQLBulkOperations** con un *Operazione* di SQL_ADD.
