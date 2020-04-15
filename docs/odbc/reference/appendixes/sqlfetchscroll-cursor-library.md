---
title: SQLFetchScroll (libreria di cursori) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetchScroll function [ODBC], Cursor Library
ms.assetid: 4417e57c-31dd-475e-8fe9-eab00a459c80
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e5573b8afc49afec8b7afa4fc52590e7a6a9e2fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302052"
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo della funzione **SQLFetchScroll** nella libreria di cursori. Per informazioni generali su **SQLFetchScroll**, vedere [Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
 La libreria di cursori implementa **SQLFetchScroll** chiamando ripetutamente **SQLFetch** nel driver. Trasferisce i dati recuperati dal driver ai buffer di set di righe forniti dall'applicazione. Inoltre, memorizza nella cache i dati nei file di memoria e su disco. Quando un'applicazione richiede un nuovo set di righe, la libreria di cursori lo recupera in base alle esigenze dal driver (se non è stato recuperato in precedenza) o dalla cache (se è stato recuperato in precedenza). Infine, la libreria di cursori mantiene lo stato dei dati memorizzati nella cache e restituisce queste informazioni all'applicazione nella matrice di stato della riga.  
  
 Quando viene utilizzata la libreria di cursori , le chiamate a **SQLFetchScroll** non possono essere mescolate con chiamate a **SQLFetch** o **SQLExtendedFetch**.  
  
 Quando viene utilizzata la libreria di cursori, le chiamate a **SQLFetchScroll** sono supportate sia per ODBC 2. *x* e per ODBC 3. *x* driver.  
  
## <a name="rowset-buffers"></a>Buffer del set di righeRowset Buffers  
 La libreria di cursori ottimizza il trasferimento dei dati dal driver al buffer del set di righe fornito dall'applicazione se:  
  
-   L'applicazione utilizza l'associazione per riga.  
  
-   Non sono presenti byte inutilizzati tra i campi nella struttura che l'applicazione dichiara di contenere una riga di dati.  
  
-   I campi in cui **SQLFetch** o **SQLFetchScroll** restituisce la lunghezza/indicatore per una colonna seguono il buffer per tale colonna e precedono il buffer per la colonna successiva. Questi campi sono facoltativi.  
  
 Quando l'applicazione richiede un nuovo set di righe, la libreria di cursori recupera i dati dalla cache e dal driver in base alle esigenze. Se i set di righe nuovi e precedenti si sovrappongono, la libreria di cursori può ottimizzare le prestazioni riutilizzando i dati delle sezioni sovrapposte dei buffer del set di righe. Di conseguenza, le modifiche non salvate ai buffer del set di righe vengono perse a meno che i set di righe nuovi e precedenti non si sovrappongano e le modifiche si trovino nelle sezioni sovrapposte dei buffer del set di righe. Per salvare le modifiche, un'applicazione invia un'istruzione di aggiornamento posizionata.  
  
 Si noti che la libreria di cursori aggiorna sempre i buffer del set di righe con i dati della cache quando un'applicazione chiama **SQLFetchScroll** con l'argomento *FetchOrientation* impostato su SQL_FETCH_RELATIVE e l'argomento *FetchOffset* impostato su 0.  
  
 La libreria di cursori supporta la chiamata **sqlSetStmtAttr** con un *attributo* di SQL_ATTR_ROW_ARRAY_SIZE per modificare la dimensione del set di righe mentre un cursore è aperto. La nuova dimensione del set di righe avrà effetto alla successiva chiamata a **SQLFetchScroll.The** new rowset size will take effect the next time SQLFetchScroll is called.  
  
## <a name="result-set-membership"></a>Appartenenza al set di risultatiResult Set Membership  
 La libreria di cursori recupera i dati dal driver solo quando l'applicazione lo richiede. A seconda dell'origine dati e dell'impostazione dell'attributo statement SQL_CONCURRENCY , ciò ha le seguenti conseguenze:  
  
-   I dati recuperati dalla libreria di cursori potrebbero essere diversi dai dati disponibili al momento dell'esecuzione dell'istruzione. Ad esempio, dopo l'apertura del cursore, le righe inserite in un punto oltre la posizione corrente del cursore possono essere recuperate da alcuni driver.  
  
-   I dati nel set di risultati potrebbero essere bloccati dall'origine dati per la libreria di cursori e pertanto non essere disponibili per altri utenti.  
  
 Dopo che la libreria di cursori ha memorizzato nella cache una riga di dati, non è in grado di rilevare le modifiche apportate a tale riga nell'origine dati sottostante (ad eccezione degli aggiornamenti posizionati e delle eliminazioni che operano sulla cache dello stesso cursore). Ciò si verifica perché, per le chiamate a **SQLFetchScroll**, la libreria di cursori non recupera mai i dati dall'origine dati. Al contrario, recupera i dati dalla cache.  
  
## <a name="scrolling"></a>Scorrimento  
 La libreria di cursori supporta i seguenti tipi di recupero in **SQLFetchScroll**.  
  
|Tipo di cursore|Tipi di recupero|  
|-----------------|-----------------|  
|Forward-only|SQL_FETCH_NEXT|  
|Statico|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>Errors  
 Quando **SQLFetchScroll** viene chiamato e una delle chiamate a **SQLFetch** restituisce SQL_ERROR, la libreria di cursori procede come segue. Dopo aver completato questi passaggi, la libreria di cursori continua l'elaborazione.  
  
1.  Chiama **SQLGetDiagRec** per ottenere informazioni sull'errore dal driver e invia come record di diagnostica in Gestione Driver.  
  
2.  Imposta il campo SQL_DIAG_ROW_NUMBER nel record di diagnostica sul valore appropriato.  
  
3.  Imposta il campo SQL_DIAG_COLUMN_NUMBER nel record di diagnostica sul valore appropriato, se applicabile; in caso contrario, lo imposta su 0.  
  
4.  Imposta su SQL_ROW_ERROR il valore della riga in errore nella matrice di stato della riga.  
  
 Dopo che la libreria di cursori ha chiamato **SQLFetch** più volte nell'implementazione di **SQLFetchScroll**, qualsiasi errore o avviso restituito da una delle chiamate a **SQLFetch** sarà in un record di diagnostica e può essere recuperato da una chiamata a **SQLGetDiagRec**. Se i dati sono stati troncati durante il recupero, i dati troncati ora risiederanno nella cache della libreria di cursori. Le chiamate successive a **SQLFetchScroll** per scorrere fino a una riga con dati troncati restituiranno i dati troncati e non verrà generato alcun avviso perché i dati vengono recuperati dalla cache della libreria di cursori. Per tenere traccia della lunghezza dei dati restituiti in modo che possa determinare se i dati restituiti in un buffer sono stati troncati, un'applicazione deve associare il buffer di lunghezza/indicatore.  
  
## <a name="bookmark-operations"></a>Operazioni sui segnalibri  
 La libreria di cursori supporta la chiamata **SQLFetchScroll** con un *FetchOrientation* di SQL_FETCH_BOOKMARK. Supporta inoltre la specifica di un offset nell'argomento *FetchOffset* che può essere utilizzato nell'operazione di segnalibro. Questa è l'unica operazione di segnalibro supportata dalla libreria di cursori. La libreria di cursori non supporta la chiamata di **SQLBulkOperations**.  
  
 Se l'applicazione ha impostato l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS ed è associata alla colonna del segnalibro, la libreria di cursori genera un segnalibro a lunghezza fissa e lo restituisce all'applicazione. La libreria di cursori crea e gestisce i segnalibri che utilizza; non utilizza segnalibri mantenuti nell'origine dati. Quando **SQLFetchScroll** viene chiamato per recuperare un blocco di dati che è già stato recuperato dall'origine dati, recupera i dati dalla cache della libreria di cursori. Di conseguenza, il segnalibro utilizzato in una chiamata a **SQLFetchScroll** con un *FetchOrientation* di SQL_FETCH_BOOKMARK deve essere creato e gestito dalla libreria di cursori.  
  
## <a name="interaction-with-other-functions"></a>Interazione con altre funzioni  
 Un'applicazione deve chiamare **SQLFetch** o **SQLFetchScroll** prima di preparare o eseguire qualsiasi istruzione di aggiornamento o eliminazione posizionata.
