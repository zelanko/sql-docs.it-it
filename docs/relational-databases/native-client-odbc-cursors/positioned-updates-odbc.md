---
title: Aggiornamenti posizionati (ODBC) Documenti Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- SQLSetPos function
- SQLSetCursorName function
- ODBC applications, cursors
- cursors [ODBC], positioned updates
- positioned updates [ODBC]
- ODBC cursors, positioned updates
ms.assetid: ff404e02-630f-474d-b5d4-06442b756991
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 52495f670986638cac02661240e349713424256e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305325"
---
# <a name="positioned-updates-odbc"></a>Aggiornamenti posizionati (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In ODBC sono supportati due metodi per eseguire gli aggiornamenti posizionati in un cursore:  
  
-   **SQLSetPos**  
  
-   Clausola WHERE CURRENT OF  
  
 L'approccio più comune consiste nell'utilizzare **SQLSetPos**. che dispone delle opzioni seguenti.  
  
 SQL_POSITION  
 Posiziona il cursore in una riga specifica del set di righe corrente.  
  
 SQL_REFRESH  
 Aggiorna le variabili di programma associate alle colonne del set di risultati in base ai valori della riga su cui è posizionato il cursore.  
  
 SQL_UPDATE  
 Aggiorna la riga corrente del cursore con i valori archiviati nelle variabili di programma associate alle colonne del set di risultati.  
  
 SQL_DELETE  
 Elimina la riga corrente dal cursore.  
  
 **SQLSetPos** può essere utilizzato con qualsiasi set di risultati dell'istruzione quando gli attributi del cursore dell'handle dell'istruzione sono impostati per utilizzare i cursori del server. Le colonne del set di risultati devono essere associate a variabili di programma. Non appena l'applicazione ha recuperato una riga chiama **SQLSetPos**(SQL_POSTION) per posizionare il cursore sulla riga. È possibile quindi chiamare SQLSetPos (SQL_DELETE) per eliminare la riga corrente o spostare i nuovi valori dei dati nelle variabili di programma associate e chiamare SQLSetPos (SQL_UPDATE) per aggiornare la riga corrente.  
  
 Le applicazioni possono aggiornare o eliminare qualsiasi riga nel set di righe con **SQLSetPos**. La chiamata a **SQLSetPos** è una comoda alternativa alla costruzione e all'esecuzione di un'istruzione SQL. **SQLSetPos** opera sul set di righe corrente e può essere utilizzato solo dopo una chiamata a [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md).  
  
 La dimensione del set di righe viene impostata da una chiamata a [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) con un argomento di attributo SQL_ATTR_ROW_ARRAY_SIZE. **SQLSetPos** utilizza una nuova dimensione del set di righe, ma solo dopo una chiamata a **SQLFetch** o **SQLFetchScroll**. Ad esempio, se la dimensione del set di righe viene modificata, **SQLSetPos** viene chiamato e quindi **SQLFetch** o **SQLFetchScroll** viene chiamato. La chiamata a **SQLSetPos** utilizza la dimensione del set di righe precedente, ma **SQLFetch** o **SQLFetchScroll** utilizza la nuova dimensione del set di righe.  
  
 La prima riga nel set di righe è il numero di riga 1. L'argomento RowNumber in **SQLSetPos** deve identificare una riga nel set di righe. vale a dire, il valore deve essere compreso nell'intervallo compreso tra 1 e il numero di righe che sono state recuperate più di recente. Questo valore potrebbe essere inferiore alle dimensioni del set di righe. Se RowNumber è 0, l'operazione viene applicata a ogni riga nel set di righe.  
  
 L'operazione di eliminazione di **SQLSetPos** consente all'origine dati di eliminare una o più righe selezionate di una tabella. Per eliminare righe con **SQLSetPos**, l'applicazione chiama **SQLSetPos** con Operation impostato su SQL_DELETE e RowNumber impostato sul numero della riga da eliminare. Se RowNumber è 0, tutte le righe nel set di righe vengono eliminate.  
  
 Dopo la restituzione **di SQLSetPos,** la riga eliminata è la riga corrente e il relativo stato è SQL_ROW_DELETED. La riga non può essere utilizzata in operazioni posizionate aggiuntive, ad esempio chiamate a [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) o **SQLSetPos**.  
  
 Quando si eliminano tutte le righe del set di righe (RowNumber è uguale a 0), l'applicazione può impedire al driver di eliminare determinate righe utilizzando la matrice di operazioni di riga come per l'operazione di aggiornamento di **SQLSetPos**.  
  
 Ogni riga eliminata deve essere una riga che esiste nel set di risultati. Se dopo il recupero i buffer dell'applicazione risultano pieni e se è stata conservata una matrice di stato della riga, i valori in ognuna di queste posizioni delle righe non devono essere SQL_ROW_DELETED, SQL_ROW_ERROR o SQL_ROW_NOROW.  
  
 Gli aggiornamenti posizionati possono inoltre essere eseguiti utilizzando la clausola WHERE CURRENT OF nelle istruzioni UPDATE, DELETE e INSERT. WHERE CURRENT OF richiede un nome di cursore che VERRÀ generato da ODBC quando viene chiamata la funzione [SQLGetCursorName](../../relational-databases/native-client-odbc-api/sqlgetcursorname.md) o che è possibile specificare chiamando **SQLSetCursorName**. Di seguito sono riportati i passaggi generali utilizzati per eseguire un aggiornamento di WHERE CURRENT OF in un'applicazione ODBC:  
  
-   Chiamare **SQLSetCursorName** per stabilire un nome di cursore per l'handle dell'istruzione.  
  
-   Compilare un'istruzione SELECT con una clausola FOR UPDATE OF ed eseguirla.  
  
-   Chiamare **SQLFetchScroll** per recuperare un set di righe o **SQLFetch** per recuperare una riga.  
  
-   Chiamare **SQLSetPos** (SQL_POSITION) per posizionare il cursore sulla riga.  
  
-   Compilare ed eseguire un'istruzione UPDATE con una clausola WHERE CURRENT OF utilizzando il nome del cursore impostato con **SQLSetCursorName**.  
  
 In alternativa, è possibile chiamare **SQLGetCursorName** dopo aver eseguito l'istruzione SELECT anziché chiamare **SQLSetCursorName** prima di eseguire l'istruzione SELECT. **SQLGetCursorName** restituisce un nome di cursore predefinito assegnato da ODBC se non si imposta un nome di cursore utilizzando **SQLSetCursorName**.  
  
 **SQLSetPos** è preferibile rispetto a WHERE CURRENT OF quando si utilizzano i cursori del server. Se si utilizza un cursore statico aggiornabile con la libreria di cursore ODBC, la libreria di cursori implementa gli aggiornamenti di WHERE CURRENT OF aggiungendo una clausola WHERE con i valori chiave per la tabella sottostante. Se le chiavi nella tabella non sono univoche, possono verificarsi aggiornamenti non desiderati.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo dei cursori &#40;&#41;ODBC](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
