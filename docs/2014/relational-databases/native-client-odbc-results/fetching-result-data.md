---
title: Il recupero dei dati dei risultati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLFetchScroll function
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC], fetching
- SQLBindCol function
- result sets [ODBC], fetching
- fetching [ODBC]
- ODBC data types, fetching
- SQLFetch function
- SQL Server Native Client ODBC driver, data types
- SQLGetData function
ms.assetid: b289c7fb-5017-4d7e-a2d3-19401e9fc4cd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b803ca3742f9cb831e51105aab9d0ed75ad78e16
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200075"
---
# <a name="fetching-result-data"></a>Recupero di dati dei risultati
  Un'applicazione ODBC dispone di tre opzioni per il recupero dei dati dei risultati.  
  
 La prima opzione basa [SQLBindCol](../native-client-odbc-api/sqlbindcol.md). Prima di recuperare il risultato impostato, l'applicazione utilizza **SQLBindCol** per associare ogni colonna nel risultato impostato su una variabile di programma. Dopo che le colonne sono state associate, il driver trasferisce i dati della riga corrente nelle variabili associati per il set di colonne di risultati ogni volta che l'applicazione chiama **SQLFetch** oppure [SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md). Il driver gestisce le conversioni di dati se la colonna del set di risultati e la variabile di programma hanno tipi di dati diversi. Se l'applicazione ha SQL_ATTR_ROW_ARRAY_SIZE set maggiore di 1, può associare le colonne di risultati a matrici di variabili, che verranno tutte specificate a ogni chiamata a **SQLFetchScroll**.  
  
 La seconda opzione è basata sul [SQLGetData](../native-client-odbc-api/sqlgetdata.md). L'applicazione non usa **SQLBindCol** per associare i risultati set di colonne alle variabili di programma. Dopo ogni chiamata a **SQLFetch**, l'applicazione chiama **SQLGetData** una sola volta per ogni colonna nel risultato impostato. **SQLGetData** indica al driver di trasferire i dati da una colonna del set di risultati specifico per una determinata variabile di programma e specifica i tipi di dati della colonna e della variabile. In questo modo il driver può convertire dati se la colonna dei risultati e la variabile di programma hanno tipi di dati diversi. **Testo**, **ntext**, e **immagine** colonne in genere sono troppo grandi per rientrare in una variabile di programma, ma possono comunque essere recuperate tramite **SQLGetData**. Se il **testo**, **ntext**, o **immagine** nella colonna dei risultati sono maggiori di variabile di programma **SQLGetData** restituisce SQL_SUCCESS_ WITH_INFO e SQLSTATE 01004 (dati string, troncati a destra). Le chiamate successive a **SQLGetData** restituiscono blocchi successivi delle **testo** oppure **immagine** dati. Quando viene raggiunta la fine dei dati, **SQLGetData** restituisce SQL_SUCCESS. Ciascun recupero restituisce un set di righe se SQL_ATTR_ROW_ARRAY_SIZE è maggiore di 1. Prima di usare **SQLGetData**, è necessario utilizzare innanzitutto **SQLSetPos** per specificare una riga specifica all'interno del set di righe come riga corrente.  
  
 La terza opzione consiste nell'utilizzare una combinazione di **SQLBindCol** e **SQLGetData**. Un'applicazione potrebbe, ad esempio, associare le prime dieci colonne di un set di risultati e quindi, per ogni operazione di recupero, chiamare **SQLGetData** tre volte per recuperare i dati da tre colonne non associate. Ciò in genere vengono usato quando un set di risultati contiene uno o più **testo** oppure **immagine** colonne.  
  
 A seconda delle opzioni del cursore impostate per il set di risultati, un'applicazione può inoltre utilizzare le opzioni di scorrimento **SQLFetchScroll** per scorrere il set di risultati.  
  
 Utilizzo eccessivo di **SQLBindCol** per associare un risultato di colonna del set a una variabile di programma è costoso perché **SQLBindCol** fa sì che un driver ODBC allocare memoria. Quando si associa una colonna di risultati a una variabile, tale associazione rimane effettiva fino a quando non si chiama [SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md) per liberare l'handle di istruzione o chiamata [SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md) con *fOption* impostato su SQL_UNBIND. Le associazioni non vengono annullate automaticamente al termine dell'istruzione.  
  
 Questa logica consente di gestire in modo efficace l'esecuzione della stessa istruzione SELECT più volte con parametri diversi. Poiché il set di risultati mantiene la stessa struttura, è possibile associare il set di risultati una sola volta, elaborare tutte le istruzioni SELECT, quindi chiamare **SQLFreeStmt** con *fOption* impostato su SQL_UNBIND dopo l'ultima esecuzione. Non è necessario chiamare **SQLBindCol** per associare le colonne in un set di risultati senza prima chiamare **SQLFreeStmt** con *fOption* impostato su SQL_UNBIND per rilasciare qualsiasi associazione precedente.  
  
 Quando si usa **SQLBindCol**, è possibile eseguire l'associazione per riga o per colonna. L'associazione per riga è leggermente più veloce dell'associazione per colonna.  
  
 È possibile usare **SQLGetData** per recuperare i dati in una colonna per colonna anziché associare risultato set di colonne mediante **SQLBindCol**. Se un set di risultati contiene solo alcune righe, utilizzando **SQLGetData** invece di **SQLBindCol** risulta più veloce; in caso contrario, **SQLBindCol** offre prestazioni migliori. Se non si inserisce sempre i dati nello stesso set di variabili, è consigliabile usare **SQLGetData** anziché ripetere l'associazione continuamente. È possibile usare solo **SQLGetData** sulle colonne presenti nell'elenco di selezione dopo che tutte le colonne sono associate **SQLBindCol**. La colonna deve inoltre essere visualizzata dopo tutte le colonne in cui è già stato utilizzato **SQLGetData**.  
  
 Le funzioni ODBC che gestiscono lo spostamento dei dati da e verso le variabili di programma, ad esempio **SQLGetData**, **SQLBindCol**, e [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md), supporta il tipo di dati implicite conversione. Se, ad esempio, un'applicazione associa una colonna integer a una variabile di programma stringa di caratteri, il driver converte automaticamente i dati da integer in carattere prima di inserirli nella variabile di programma.  
  
 La conversione dei dati nelle applicazioni deve essere ridotta al minimo. A meno che la conversione dei dati non sia necessaria per l'elaborazione eseguita dall'applicazione, è preferibile che le applicazioni non associno colonne e parametri a variabili di programma dello stesso tipo di dati. Se i dati devono essere convertiti da un tipo a un altro, tuttavia, è più efficiente fare in modo che il driver esegua la conversione anziché lasciare che la conversione venga eseguita nell'applicazione. Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client trasferisce in genere i dati direttamente dai buffer di rete alle variabili dell'applicazione. La richiesta al driver di convertire i dati forza il driver a eseguire il buffer dei dati e a utilizzare cicli della CPU per la conversione dei dati.  
  
 Devono essere sufficientemente grande per contenere i dati trasferiti da una colonna, ad eccezione di variabili di programma **testo**, **ntext**, e **immagine** dei dati. Se un'applicazione tenta di recuperare dati del set di risultati e di inserirli in una variabile di dimensioni troppo piccole per contenerli, il driver genera un avviso. Ciò forza il driver ad allocare memoria per il messaggio e il driver e l'applicazione devono entrambi impiegare cicli della CPU per l'elaborazione del messaggio e per la gestione degli errori. L'applicazione deve allocare una variabile sufficientemente grande per contenere i dati recuperati oppure utilizzare la funzione SUBSTRING nell'elenco di selezione per ridurre le dimensioni della colonna nel set di risultati.  
  
 Quando si utilizza SQL_C_DEFAULT per specificare il tipo della variabile C, è necessario procedere con cautela. SQL_C_DEFAULT specifica che il tipo della variabile C corrisponde al tipo di dati SQL della colonna o del parametro. Se si specifica SQL_C_DEFAULT per una **ntext**, **nchar**, o **nvarchar** colonna di dati Unicode viene restituiti all'applicazione. Ciò può provocare diversi problemi se l'applicazione non è stata codificata per la gestione di dati Unicode. Possono verificarsi gli stessi tipi di problemi con il **uniqueidentifier** tipo di dati (SQL_GUID).  
  
 **testo**, **ntext**, e **immagine** dati in genere è troppo grandi per rientrare in una singola variabile di programma e solitamente vengono elaborati con **SQLGetData** invece di **SQLBindCol**. Quando si utilizzano i cursori server, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client è ottimizzato per non trasmettere i dati per annullare l'associazione **testo**, **ntext**, o **immagine** colonne di tempo di che recupero della riga. Il **testo**, **ntext**, o **immagine** dati non vengono effettivamente recuperati dal server finché i problemi dell'applicazione **SQLGetData** per il colonna.  
  
 Questa ottimizzazione può essere applicata alle applicazioni in modo che nessun **testo**, **ntext**, o **immagine** mentre viene effettuato uno scorrimento di un utente su un cursore e visualizzazione dei dati. Dopo che l'utente ha selezionato una riga, l'applicazione può chiamare **SQLGetData** per recuperare le **testo**, **ntext**, oppure **immagine** dati. Ciò consente di risparmiare la trasmissione di **testo**, **ntext**, o **immagine** dati per tutte le righe l'utente non seleziona e consente di risparmiare la trasmissione di quantità elevate di dati.  
  
## <a name="see-also"></a>Vedere anche  
 [L'elaborazione dei risultati &#40;ODBC&#41;](processing-results-odbc.md)  
  
  
