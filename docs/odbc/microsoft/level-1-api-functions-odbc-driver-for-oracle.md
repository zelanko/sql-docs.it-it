---
title: Funzioni API di livello 1 (driver ODBC per Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC level 1 API functions [ODBC]
- ODBC driver for Oracle [ODBC], functions
- level 1 API functions [ODBC]
- API functions [ODBC]
ms.assetid: 98cced6f-41b8-43c1-a3cd-f4ea1615c0af
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cb1771f88987073b1ef0bcc106f8de28549affe6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085468"
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>Funzioni API di livello 1 (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Le funzioni a questo livello forniscono la conformità dell'interfaccia principale, oltre a funzionalità aggiuntive, ad esempio il supporto delle transazioni.  
  
|Funzione API|Note|  
|------------------|-----------|  
|**SQLColumns**|Consente di creare un set di risultati per una tabella, ovvero l'elenco di colonne per la tabella o le tabelle specificate. Quando si richiedono colonne per un sinonimo PUBLIC, è necessario impostare l'attributo di connessione SYNONYMCOLUMNS e specificare una stringa vuota come argomento *szTableOwner* . Quando si restituiscono colonne per i sinonimi pubblici, il driver imposta la colonna nome tabella su una stringa vuota. Il set di risultati contiene una colonna aggiuntiva, posizione ORDINAle, alla fine di ogni riga. Questo valore è la posizione ordinale della colonna nella tabella.|  
|**SQLDriverConnect**|Consente di connettersi a un'origine dati esistente. Per informazioni dettagliate, vedere [formato e attributi della stringa di connessione](../../odbc/microsoft/connection-string-format-and-attributes.md).|  
|**SQLGetConnectOption**|Restituisce l'impostazione corrente di un'opzione di connessione. Questa funzione è parzialmente supportata. Il driver supporta tutti i valori per l'argomento *fOption* , ma non supporta alcuni valori *parametro vParam* per l'argomento *fOption* [SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md). Per altre informazioni, vedere [Opzioni di connessione](../../odbc/microsoft/connect-options.md).|  
|**SQLGetData**|Recupera il valore di un singolo campo nel record corrente del set di risultati specificato.|  
|**SQLGetFunctions**|Restituisce TRUE per tutte le funzioni supportate. Implementato da Gestione driver.|  
|**SQLGetInfo**|Restituisce informazioni, tra cui SQLHDBC, SQLUSMALLINT, SQLPOINTER, SQLSMALLINT e SQLSMALLINT \*, sul driver ODBC per Oracle e l'origine dati associata a un handle di connessione, *HDBC*.|  
|**SQLGetStmtOption**|Restituisce l'impostazione corrente di un'opzione dell'istruzione. Per ulteriori informazioni, vedere [Opzioni dell'istruzione](../../odbc/microsoft/statement-options.md).|  
|**SQLGetTypeInfo**|Restituisce informazioni sui tipi di dati supportati da un'origine dati. Il driver restituisce le informazioni in un set di risultati SQL.|  
|**SQLParamData**|Utilizzato insieme a **SQLPutData** per specificare i dati dei parametri in fase di esecuzione dell'istruzione.|  
|**SQLPutData**|Consente a un'applicazione di inviare i dati per un parametro o una colonna al driver al momento dell'esecuzione dell'istruzione.|  
|**SQLSetConnectOption**|Consente di accedere alle opzioni che regolano gli aspetti della connessione. Questa funzione è parzialmente supportata: il driver supporta tutti i valori per l'argomento *fOption* , ma non supporta alcuni valori *parametro vParam* per l'argomento *fOption* [SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md). Per altre informazioni, vedere [Opzioni di connessione](../../odbc/microsoft/connect-options.md).|  
|**SQLSetStmtOption**|Imposta le opzioni correlate a un handle di istruzione, *HSTMT*. Per ulteriori informazioni, vedere [Opzioni dell'istruzione](../../odbc/microsoft/statement-options.md).|  
|**SQLSpecialColumns**|Recupera il set ottimale di colonne che identifica in modo univoco una riga nella tabella.|  
|**SQLStatistics**|Recupera un elenco di statistiche relative a una singola tabella e agli indici o ai nomi di tag associati alla tabella. Il driver restituisce le informazioni come un set di risultati.|  
|**SQLTables**|Restituisce l'elenco dei nomi di tabella specificati dal parametro nell'istruzione **SQLTables** . Se non viene specificato alcun parametro, restituisce i nomi di tabella archiviati nell'origine dati corrente. Il driver restituisce le informazioni come un set di risultati.<br /><br /> Le chiamate al tipo di enumerazione non riceveranno una voce del set di risultati per le visualizzazioni remote o le visualizzazioni con parametri locali. Tuttavia, una chiamata a **SQLTables** con un identificatore di nome di tabella univoco troverà una corrispondenza per tale visualizzazione, se presente, con lo stesso nome; Ciò consente all'API di verificare la presenza di conflitti di nome prima della creazione di una nuova tabella.<br /><br /> I sinonimi pubblici vengono restituiti con un valore TABLE_OWNER "".<br /><br /> Le visualizzazioni di proprietà di SYS o SYSTEM vengono identificate come viste di sistema.|
