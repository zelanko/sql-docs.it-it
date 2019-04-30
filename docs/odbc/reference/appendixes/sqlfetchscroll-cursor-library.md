---
title: SQLFetchScroll (libreria di cursori) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db7dc5482347ad9b7f194b3c9c8c6cd7fc3f9f6a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199591"
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 In questo argomento viene illustrato l'utilizzo dei **SQLFetchScroll** funzione nella libreria di cursori. Per informazioni generali sul **SQLFetchScroll**, vedere [funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
 La libreria di cursori implementa **SQLFetchScroll** chiamando ripetutamente **SQLFetch** nel driver. Trasferire i dati che viene recuperato dal driver ai buffer di set di righe fornito dall'applicazione. Inoltre memorizza nella cache i dati nei file di memoria e disco. Quando un'applicazione richiede un nuovo set di righe, la libreria di cursori si recupera in base alle esigenze dal driver (se si è non stato recuperato in precedenza) o dalla cache (se si è stato recuperato in precedenza). Infine, la libreria di cursori mantiene lo stato dei dati memorizzati nella cache e restituisce queste informazioni per l'applicazione della matrice di stato di riga.  
  
 Quando viene usata la libreria di cursori, le chiamate a **SQLFetchScroll** ReadContentAsBase64 e ReadContentAsBinHex con chiamate a uno **SQLFetch** oppure **SQLExtendedFetch**.  
  
 Quando viene usata la libreria di cursori, le chiamate a **SQLFetchScroll** sono supportati sia per ODBC 2. *x* e per ODBC 3. *x* driver.  
  
## <a name="rowset-buffers"></a>Buffer di righe  
 La libreria di cursori consente di ottimizzare il trasferimento dei dati dal driver per il buffer di set di righe fornito dall'applicazione se:  
  
-   L'applicazione usa l'associazione per riga.  
  
-   Esistono byte inutilizzate tra i campi della struttura che dell'applicazione dichiara per includere una riga di dati.  
  
-   I campi in cui **SQLFetch** oppure **SQLFetchScroll** restituisce la lunghezza/indicatore per una colonna segue il buffer per tale colonna e precede il buffer per la colonna successiva. Questi campi sono facoltativi.  
  
 Quando l'applicazione richiede un nuovo set di righe, la libreria di cursori recupera i dati dalla cache e dal driver, se necessario. Se i set di righe nuove e obsolete si sovrappongono, la libreria di cursori possa ottimizzarne le prestazioni usando di nuovo i dati dalle sezioni dei buffer di righe sovrapposti. Di conseguenza, le modifiche non salvate ai buffer di set di righe vengono perse a meno che non si sovrappongono i set di righe nuove e obsolete e le modifiche sono nelle sezioni dei buffer di righe sovrapposte. Per salvare le modifiche, un'applicazione invia un'istruzione per gli aggiornamenti posizionati.  
  
 Si noti che la libreria di cursori Aggiorna sempre il buffer di set di righe con i dati dalla cache quando un'applicazione chiama **SQLFetchScroll** con il *FetchOrientation* argomento impostato su SQL_FETCH_RELATIVE e il *FetchOffset* argomento impostato su 0.  
  
 La libreria di cursori supporta la chiamata **SQLSetStmtAttr** con un *attributo* di SQL_ATTR_ROW_ARRAY_SIZE per modificare le dimensioni del set di righe mentre è aperto un cursore. La nuova dimensione di set di righe sarà effettive la volta successiva **SQLFetchScroll** viene chiamato.  
  
## <a name="result-set-membership"></a>Appartenenza al Set di risultati  
 La libreria di cursori recupera i dati del driver solo quando viene richiesto dall'applicazione. A seconda dell'origine dati e l'impostazione dell'attributo di istruzione SQL_CONCURRENCY, ciò comporta le conseguenze seguenti:  
  
-   I dati recuperati dalla libreria di cursori potrebbero essere diversi dai dati che erano disponibili al momento che è stata eseguita l'istruzione. Ad esempio, dopo l'apertura del cursore, le righe inserite in un punto oltre la posizione corrente del cursore possono essere recuperate da alcuni driver.  
  
-   I dati nel set di risultati potrebbero essere bloccati da origine dati per la libreria di cursori e pertanto non essere disponibile ad altri utenti.  
  
 Dopo che la libreria di cursori ha memorizzato nella cache di una riga di dati, in grado di rilevare le modifiche a tale riga nell'origine dati sottostante (fatta eccezione per gli aggiornamenti posizionati e le eliminazioni operativo in cache del cursore stesso). Ciò si verifica perché, per le chiamate a **SQLFetchScroll**, la libreria di cursori recupera mai nuovamente i dati dall'origine dati. Al contrario, recupera nuovamente i dati dalla cache.  
  
## <a name="scrolling"></a>Lo scorrimento  
 La libreria di cursori supporta i seguenti tipi di operazione di recupero nel **SQLFetchScroll**.  
  
|Tipo di cursore|Tipi di operazione di recupero|  
|-----------------|-----------------|  
|Forward-only|SQL_FETCH_NEXT|  
|Static|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>Errori  
 Quando **SQLFetchScroll** viene chiamato e l'altra delle chiamate a **SQLFetch** restituisce SQL_ERROR, procede di libreria di cursore come indicato di seguito. Una volta completata questa procedura, la libreria di cursori continua l'elaborazione.  
  
1.  Le chiamate **SQLGetDiagRec** per ottenere informazioni sull'errore dal driver e registra ciò come un record di diagnostica in Gestione Driver.  
  
2.  Imposta il campo SQL_DIAG_ROW_NUMBER nel record di diagnostica sul valore appropriato.  
  
3.  Imposta il campo SQL_DIAG_COLUMN_NUMBER nel record di diagnostica sul valore appropriato, se applicabile; in caso contrario, impostato su 0.  
  
4.  Imposta il valore per la riga nella matrice di stato di riga da SQL_ROW_ERROR errore.  
  
 Dopo il cursore della libreria è chiamato **SQLFetch** più volte nella propria implementazione di **SQLFetchScroll**, qualsiasi errore o avviso restituito da una delle chiamate a **SQLFetch** in un record di diagnostica e possono essere recuperati da una chiamata a **SQLGetDiagRec**. Se i dati sono stati troncati durante il recupero, i dati troncati si troverà ora nella cache della libreria di cursori. Le chiamate successive a **SQLFetchScroll** scorrere fino a una riga con dati troncati verranno restituiti i dati troncati e non verrà generato alcun avviso perché i dati vengono recuperati dalla cache della libreria di cursori. Per tenere traccia della lunghezza dei dati restituiti in modo che possa determinare se i dati restituiti in un buffer sono stati troncati, un'applicazione deve essere associato il buffer di lunghezza/indicatore.  
  
## <a name="bookmark-operations"></a>Operazioni di segnalibro  
 La libreria di cursori supporta la chiamata **SQLFetchScroll** con un *FetchOrientation* impostato su sql_fetch_bookmark. Supporta anche specificando un offset espresso nel *FetchOffset* argomento che può essere utilizzato nell'operazione di segnalibro. Questo è l'unica operazione segnalibro che supporta la libreria di cursori. La libreria di cursori non supporta la chiamata **SQLBulkOperations**.  
  
 Se l'applicazione ha impostato l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS e per la colonna del segnalibro è stato associato, la libreria di cursori genera un segnalibro a lunghezza fissa e lo restituisce all'applicazione. La libreria di cursori crea e gestisce i segnalibri che usa; non usa i segnalibri gestiti all'origine dati. Quando **SQLFetchScroll** viene chiamato per recuperare un blocco di dati che sono già stati recuperati dall'origine dati, il recupero dei dati dalla cache della libreria di cursore. Di conseguenza, il segnalibro utilizzato in una chiamata a **SQLFetchScroll** con un *FetchOrientation* di SQL_FETCH_BOOKMARK devono essere creati e gestiti dalla libreria di cursori.  
  
## <a name="interaction-with-other-functions"></a>Interazione con altre funzioni  
 Un'applicazione deve chiamare **SQLFetch** oppure **SQLFetchScroll** prima che prepara o si esegue qualsiasi posizionato istruzioni update o delete.
