---
title: Recupero dei dati dei risultati Documenti Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e1d9fdfcd7bcc4f86afacc75dff5b40b77bb7b2a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304613"
---
# <a name="fetching-result-data"></a>Recupero di dati dei risultati
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Un'applicazione ODBC dispone di tre opzioni per il recupero dei dati dei risultati.  
  
 La prima opzione è basata su [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md). Prima di recuperare il set di risultati, l'applicazione utilizza **SQLBindCol** per associare ogni colonna nel set di risultati a una variabile di programma. Dopo l'associazione delle colonne, il driver trasferisce i dati della riga corrente nelle variabili associate alle colonne del set di risultati ogni volta che l'applicazione chiama **SQLFetch** o [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md). Il driver gestisce le conversioni di dati se la colonna del set di risultati e la variabile di programma hanno tipi di dati diversi. Se l'applicazione dispone di SQL_ATTR_ROW_ARRAY_SIZE impostate su un valore maggiore di 1, è possibile associare le colonne dei risultati a matrici di variabili, che verranno tutte riempite a ogni chiamata a **SQLFetchScroll**.  
  
 La seconda opzione è basata su [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md). L'applicazione non utilizza **SQLBindCol** per associare le colonne del set di risultati alle variabili di programma. Dopo ogni chiamata a **SQLFetch**, l'applicazione chiama **SQLGetData** una volta per ogni colonna nel set di risultati. **SQLGetData** indica al driver di trasferire dati da una colonna del set di risultati specifico a una variabile di programma specifica e specifica i tipi di dati della colonna e della variabile. In questo modo il driver può convertire dati se la colonna dei risultati e la variabile di programma hanno tipi di dati diversi. **Le**colonne Text , **ntext**e **image** sono in genere troppo grandi per essere contenute in una variabile di programma, ma possono comunque essere recuperate utilizzando **SQLGetData**. Se i dati **text**, **ntext**o **image** nella colonna dei risultati sono più grandi della variabile di programma, **SQLGetData** restituisce SQL_SUCCESS_WITH_INFO e SQLSTATE 01004 (dati stringa troncati a destra). Le chiamate successive a **SQLGetData** restituiscono blocchi successivi dei dati di **tipo text** o **image.** Quando viene raggiunta la fine dei dati, **SQLGetData** restituisce SQL_SUCCESS. Ciascun recupero restituisce un set di righe se SQL_ATTR_ROW_ARRAY_SIZE è maggiore di 1. Prima di utilizzare **SQLGetData**, è necessario utilizzare **SQLSetPos** per specificare una riga specifica all'interno del set di righe come riga corrente.  
  
 La terza opzione consiste nell'utilizzare una combinazione di **SQLBindCol** e **SQLGetData**. Un'applicazione potrebbe, ad esempio, associare le prime dieci colonne di un set di risultati e quindi, a ogni recupero, chiamare **SQLGetData** tre volte per recuperare i dati da tre colonne non associate. Viene in genere utilizzato quando un set di risultati contiene una o più colonne di **tipo text** o **image.**  
  
 A seconda delle opzioni del cursore impostate per il set di risultati, un'applicazione può anche utilizzare le opzioni di scorrimento di **SQLFetchScroll** per scorrere il set di risultati.  
  
 L'utilizzo in eccesso di **SQLBindCol** per associare una colonna del set di risultati a una variabile di programma è costoso perché **SQLBindCol** causa l'allocazione di memoria da parte di un driver ODBC. Quando si associa una colonna risultato a una variabile, tale associazione rimane attiva fino a quando non si chiama [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) per liberare l'handle dell'istruzione o chiamare [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) con *fOption* impostato su SQL_UNBIND. Le associazioni non vengono annullate automaticamente al termine dell'istruzione.  
  
 Questa logica consente di gestire in modo efficace l'esecuzione della stessa istruzione SELECT più volte con parametri diversi. Poiché il set di risultati mantiene la stessa struttura, è possibile associare il set di risultati una sola volta, elaborare tutte le istruzioni SELECT, quindi chiamare **SQLFreeStmt** con *fOption* impostato su SQL_UNBIND dopo l'ultima esecuzione. Non è necessario chiamare **SQLBindCol** per associare le colonne in un set di risultati senza prima chiamare **SQLFreeStmt** con *fOption* impostato su SQL_UNBIND per liberare le associazioni precedenti.  
  
 Quando si utilizza **SQLBindCol**, è possibile eseguire l'associazione per riga o per colonna. L'associazione per riga è leggermente più veloce dell'associazione per colonna.  
  
 È possibile utilizzare **SQLGetData** per recuperare i dati in base alla colonna anziché associare le colonne del set di risultati tramite **SQLBindCol**. Se un set di risultati contiene solo alcune righe, l'utilizzo di **SQLGetData** anziché **SQLBindCol** è più veloce; in caso contrario, **SQLBindCol** offre le prestazioni migliori. Se non si inseriscono sempre i dati nello stesso set di variabili, è necessario usare **SQLGetData** anziché riassociare costantemente. È possibile utilizzare **SQLGetData** solo nelle colonne presenti nell'elenco di selezione dopo che tutte le colonne sono associate a **SQLBindCol**. La colonna deve essere visualizzata anche dopo tutte le colonne in cui è già stato utilizzato **SQLGetData**.  
  
 Le funzioni ODBC che gestiscono lo spostamento dei dati all'esterno o all'esterno delle variabili di programma, ad esempio **SQLGetData**, **SQLBindCol**e [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md), supportano la conversione implicita dei tipi di dati. Se, ad esempio, un'applicazione associa una colonna integer a una variabile di programma stringa di caratteri, il driver converte automaticamente i dati da integer in carattere prima di inserirli nella variabile di programma.  
  
 La conversione dei dati nelle applicazioni deve essere ridotta al minimo. A meno che la conversione dei dati non sia necessaria per l'elaborazione eseguita dall'applicazione, è preferibile che le applicazioni non associno colonne e parametri a variabili di programma dello stesso tipo di dati. Se i dati devono essere convertiti da un tipo a un altro, tuttavia, è più efficiente fare in modo che il driver esegua la conversione anziché lasciare che la conversione venga eseguita nell'applicazione. Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client trasferisce in genere i dati direttamente dai buffer di rete alle variabili dell'applicazione. La richiesta al driver di convertire i dati forza il driver a eseguire il buffer dei dati e a utilizzare cicli della CPU per la conversione dei dati.  
  
 Le variabili di programma devono essere sufficientemente grandi da contenere i dati trasferiti da una colonna, ad eccezione dei dati **text**, **ntext**e **image.** Se un'applicazione tenta di recuperare dati del set di risultati e di inserirli in una variabile di dimensioni troppo piccole per contenerli, il driver genera un avviso. Ciò forza il driver ad allocare memoria per il messaggio e il driver e l'applicazione devono entrambi impiegare cicli della CPU per l'elaborazione del messaggio e per la gestione degli errori. L'applicazione deve allocare una variabile sufficientemente grande per contenere i dati recuperati oppure utilizzare la funzione SUBSTRING nell'elenco di selezione per ridurre le dimensioni della colonna nel set di risultati.  
  
 Quando si utilizza SQL_C_DEFAULT per specificare il tipo della variabile C, è necessario procedere con cautela. SQL_C_DEFAULT specifica che il tipo della variabile C corrisponde al tipo di dati SQL della colonna o del parametro. Se SQL_C_DEFAULT viene specificato per una colonna **ntext**, **nchar**o **nvarchar** , i dati Unicode vengono restituiti all'applicazione. Ciò può provocare diversi problemi se l'applicazione non è stata codificata per la gestione di dati Unicode. Gli stessi tipi di problemi possono verificarsi con il tipo di dati **uniqueidentifier** (SQL_GUID).  
  
 **I**dati text , **ntext**e **image** sono in genere troppo grandi per essere contenuti in una singola variabile di programma e vengono in genere elaborati con **SQLGetData** anziché **con SQLBindCol**. Quando si utilizzano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursori del server, il driver ODBC Native Client è ottimizzato per non trasmettere i dati per le colonne **text,** **ntext**o **image** non associate al momento del recupero della riga. I dati **text**, **ntext**o **image** non vengono effettivamente recuperati dal server fino a quando l'applicazione non emette **SQLGetData** per la colonna.  
  
 Questa ottimizzazione può essere applicata alle applicazioni in modo che non vengano visualizzati dati di **testo**, **ntext**o **immagine** mentre un utente scorre un cursore verso l'alto e verso il basso. Dopo che l'utente seleziona una riga, l'applicazione può chiamare **SQLGetData** per recuperare i dati **text**, **ntext**o **image.** In questo modo si salva la trasmissione dei dati di **testo**, **ntext**o **immagine** per una qualsiasi delle righe che l'utente non seleziona e può salvare la trasmissione di grandi quantità di dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Elaborazione dei risultati &#40;&#41;ODBCProcessing Results &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
