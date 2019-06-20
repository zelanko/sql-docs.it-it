---
title: Funzioni API di livello 1 (Driver ODBC per Oracle) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 6a70116fb0e8ef1236b18cb478184e96fe08fce5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63262224"
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>Funzioni API di livello 1 (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 Supporta le funzioni in questo livello forniscono conformità di interfaccia Core oltre a funzionalità aggiuntive, ad esempio delle transazioni.  
  
|Funzione dell'API|Note|  
|------------------|-----------|  
|**SQLColumns**|Crea un set di risultati per una tabella, ovvero l'elenco di colonne per la tabella specificata o tabelle. Quando si richiedono le colonne per un sinonimo PUBLIC, è necessario avere impostato l'attributo di connessione SYNONYMCOLUMNS e specificata una stringa vuota come la *szTableOwner* argomento. Quando si restituiscono le colonne per il sinonimo PUBLIC, il driver imposta la colonna nome della tabella in una stringa vuota. Il set di risultati contiene una colonna aggiuntiva, posizione ORDINALE, alla fine di ogni riga. Questo valore è la posizione ordinale della colonna nella tabella.|  
|**SQLDriverConnect**|Si connette a un'origine dati esistente. Per informazioni dettagliate, vedere [formato stringa di connessione e gli attributi](../../odbc/microsoft/connection-string-format-and-attributes.md).|  
|**SQLGetConnectOption**|Restituisce l'impostazione corrente dell'opzione di connessione. Questa funzione è supportata parzialmente. Il driver supporta tutti i valori per il *fOption* argomento, ma non supporta alcuni *vParam* valori per il *fOption* argomento [SQL_TXN_ISOLATION ](../../odbc/microsoft/connect-options.md). Per altre informazioni, vedere [opzioni di connessione](../../odbc/microsoft/connect-options.md).|  
|**SQLGetData**|Recupera il valore di un singolo campo nel record corrente del set di risultati specificato.|  
|**SQLGetFunctions**|Restituisce TRUE per tutte le funzioni supportate. Implementata da Gestione Driver.|  
|**SQLGetInfo**|Restituisce informazioni, tra cui SQLHDBC SQLUSMALLINT, SQLPOINTER, SQLSMALLINT e SQLSMALLINT \*, riguardanti il Driver ODBC per Oracle e l'origine dati associata a un handle di connessione *hdbc*.|  
|**SQLGetStmtOption**|Restituisce l'impostazione corrente di un'opzione di istruzione. Per altre informazioni, vedere [le opzioni dell'istruzione](../../odbc/microsoft/statement-options.md).|  
|**SQLGetTypeInfo**|Restituisce informazioni sui tipi di dati supportati da un'origine dati. Il driver restituisce le informazioni in un set di risultati SQL.|  
|**SQLParamData**|Usato in combinazione con **SQLPutData** per specificare i dati dei parametri in fase di esecuzione di istruzione.|  
|**SQLPutData**|Consente a un'applicazione inviare i dati per un parametro o della colonna per il driver in fase di esecuzione di istruzione.|  
|**SQLSetConnectOption**|Fornisce l'accesso alle opzioni che determinano gli aspetti della connessione. Questa funzione è supportata parzialmente: Il driver supporta tutti i valori per il *fOption* argomento, ma non supporta alcuni *vParam* valori per il *fOption* argomento [SQL_TXN_ISOLATION ](../../odbc/microsoft/connect-options.md). Per altre informazioni, vedere [opzioni di connessione](../../odbc/microsoft/connect-options.md).|  
|**SQLSetStmtOption**|Imposta le opzioni relative a un handle di istruzione *hstmt*. Per altre informazioni, vedere [le opzioni dell'istruzione](../../odbc/microsoft/statement-options.md).|  
|**SQLSpecialColumns**|Recupera il set di colonne ottimale che identifica in modo univoco una riga nella tabella.|  
|**SQLStatistics**|Recupera un elenco delle statistiche su una singola tabella e indici o i nomi dei tag, associati alla tabella. Il driver restituisce le informazioni come set di risultati.|  
|**SQLTables**|Restituisce l'elenco di nomi di tabella specificato dal parametro di **SQLTables** istruzione. Se si specifica alcun parametro, restituisce i nomi di tabella archiviati nell'origine dati corrente. Il driver restituisce le informazioni come set di risultati.<br /><br /> Le chiamate di tipo di enumerazione non riceveranno una voce del set di risultati per visualizzazioni remote o locale con parametri. Tuttavia, una chiamata a **SQLTables** con una tabella univoca identificatore di nome verrà trovata una corrispondenza per una vista, se presente, con lo stesso nome; in questo modo l'API per verificare la presenza di conflitti di nome prima della creazione di una nuova tabella.<br /><br /> Il sinonimo PUBLIC viene restituito con il valore TABLE_OWNER "".<br /><br /> Le viste SYS o sistema di proprietà vengono identificate come vista di sistema.|
