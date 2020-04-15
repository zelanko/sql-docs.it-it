---
title: Funzioni API di livello 1 (driver ODBC per Oracle) . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37305ee75ebeb0686bafe039f1102cb3c6e18674
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299951"
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>Funzioni API di livello 1 (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Le funzioni a questo livello forniscono la conformità dell'interfaccia di base e funzionalità aggiuntive, ad esempio il supporto delle transazioni.  
  
|Funzione API|Note|  
|------------------|-----------|  
|**SQLColumns**|Crea un set di risultati per una tabella, ovvero l'elenco di colonne per la tabella o le tabelle specificate. Quando si richiedono colonne per un sinonimo PUBLIC, è necessario aver impostato l'attributo di connessione SYNONYMCOLUMNS e specificato una stringa vuota come argomento *szTableOwner.* Quando si restituiscono colonne per sinonimi PUBLIC, il driver imposta la colonna TABLE NAME su una stringa vuota. Il set di risultati contiene una colonna aggiuntiva, ORDINAL POSITION, alla fine di ogni riga. Questo valore è la posizione ordinale della colonna nella tabella.|  
|**SQLDriverConnect**|Si connette a un'origine dati esistente. Per informazioni dettagliate, vedere [Formato e attributi](../../odbc/microsoft/connection-string-format-and-attributes.md)della stringa di connessione .|  
|**SQLGetConnectOption (Opzione SQLGetConnectOption)**|Restituisce l'impostazione corrente di un'opzione di connessione. Questa funzione è parzialmente supportata. Il driver supporta tutti i valori per l'argomento *fOption* ma non alcuni valori *vParam* per l'argomento *fOption* [SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md). Per ulteriori informazioni, consultate [Opzioni di connessione.](../../odbc/microsoft/connect-options.md)|  
|**SQLGetData**|Recupera il valore di un singolo campo nel record corrente del set di risultati specificato.|  
|**SQLGetFunctions**|Restituisce TRUE per tutte le funzioni supportate. Implementato da Gestione Driver.|  
|**SQLGetInfo**|Restituisce informazioni, tra cui SQLHDBC, SQLUSMALLINT, SQLPOINTER, SQLSMALLINT e SQLSMALLINT \*, sul Driver ODBC per Oracle e sull'origine dati associata a un handle di connessione, *hdbc*.|  
|**Opzione SQLGetStmtOption**|Restituisce l'impostazione corrente di un'opzione di istruzione. Per ulteriori informazioni, vedere [Opzioni dell'istruzione](../../odbc/microsoft/statement-options.md).|  
|**SQLGetTypeInfo**|Restituisce informazioni sui tipi di dati supportati da un'origine dati. Il driver restituisce le informazioni in un set di risultati SQL.|  
|**SQLParamData**|Utilizzato insieme a **SQLPutData** per specificare i dati dei parametri in fase di esecuzione dell'istruzione.|  
|**SQLPutData**|Consente a un'applicazione di inviare dati per un parametro o una colonna al driver in fase di esecuzione dell'istruzione.|  
|**Sqlsetconnectoption**|Fornisce l'accesso alle opzioni che regolano gli aspetti della connessione. Questa funzione è parzialmente supportata: il driver supporta tutti i valori per il *fOption* argomento ma non supporta alcuni valori *vParam* per il *fOption* [argomento SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md). Per ulteriori informazioni, consultate [Opzioni di connessione.](../../odbc/microsoft/connect-options.md)|  
|**Opzione SQLSetStmmtOption**|Imposta le opzioni relative a un handle di istruzione, *hstmt*. Per ulteriori informazioni, vedere [Opzioni dell'istruzione](../../odbc/microsoft/statement-options.md).|  
|**SQLSpecialColumns**|Recupera il set ottimale di colonne che identifica in modo univoco una riga nella tabella.|  
|**SQLStatistics**|Recupera un elenco di statistiche su una singola tabella e sugli indici, o nomi di tag, associati alla tabella. Il driver restituisce le informazioni come set di risultati.|  
|**SQLTables**|Restituisce l'elenco dei nomi di tabella specificati dal parametro nell'istruzione **SQLTables.** Se non viene specificato alcun parametro, restituisce i nomi delle tabelle archiviati nell'origine dati corrente. Il driver restituisce le informazioni come set di risultati.<br /><br /> Le chiamate al tipo di enumerazione non riceveranno una voce del set di risultati per le visualizzazioni remote o le visualizzazioni con parametri locali. Tuttavia, una chiamata a **SQLTables** con un identificatore nome di tabella univoco troverà una corrispondenza per tale vista, se presente, con tale nome; Ciò consente all'API di verificare la presenza di conflitti di nomi prima della creazione di una nuova tabella.<br /><br /> I sinonimi PUBLIC vengono restituiti con un valore TABLE_OWNER di "".<br /><br /> I VIEWS di proprietà di SYS o SYSTEM sono identificati come SYSTEM VIEW.|
