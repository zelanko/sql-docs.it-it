---
title: Libreria di cursori ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], library
- SQL_CUR_USE_DRIVER option
- ODBC applications, cursors
- ODBC cursors, library
- SQL_CUR_USE_IF_NEEDED option
- SQLSetConnectAttr function
- SQL_CUR_USE_ODBC option
ms.assetid: 3c610d3d-6e06-49cf-9a40-05b6a1c83a32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b81a7871434691a5940a04c7c60aaad9254b645
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63201164"
---
# <a name="odbc-cursor-library"></a>Libreria di cursori ODBC
  Alcuni driver ODBC supportano solo le impostazioni di cursore predefinito. tali driver inoltre non supportano operazioni del cursore posizionate, ad esempio **SQLSetPos**. La libreria di cursori ODBC è un componente di Microsoft Data Access Components (MDAC) utilizzato per implementare cursori a blocchi o statici in un driver che generalmente non li supporta. La libreria di cursori implementa anche le istruzioni UPDATE e DELETE posizionate e **SQLSetPos** per i cursori che crea.  
  
 La libreria di cursori ODBC viene implementata come livello tra Gestione driver ODBC e il driver ODBC. Se la libreria viene caricata, a questa, e non al driver, vengono indirizzati tutti i comandi correlati al cursore. La libreria di cursori implementa un cursore mediante il recupero dell'intero set di risultati dal driver sottostante e la memorizzazione nella cache del client del set di risultati. Quando si utilizza la libreria di cursori ODBC, nell'applicazione sono disponibili solo le funzionalità di cursore della libreria di cursori e non funzionalità di cursore aggiuntive del driver sottostante.  
  
 Con il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client non esiste l'esigenza di utilizzare la libreria di cursori ODBC, in quanto il driver supporta un numero maggiore di funzionalità di cursore rispetto alla libreria. L'unico motivo per usare la libreria di cursori ODBC con il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client è perché il driver implementa il supporto per i cursori tramite i cursori del server e i cursori del server non supportano tutte le istruzioni SQL. È pertanto consigliabile utilizzare la libreria di cursori ODBC ogni volta che si richiede un cursore statico con stored procedure, batch o istruzioni SQL contenenti COMPUTE, COMPUTE BY, FOR BROWSE o INTO. È tuttavia necessario prestare attenzione nell'utilizzo della libreria in quanto memorizza nella cache del client l'intero set di risultati con conseguente impiego di grandi quantità di memoria e rallentamento delle prestazioni.  
  
 Un'applicazione richiama la libreria di cursori in modo da connessioni utilizzando [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) per impostare l'attributo di connessione SQL_ATTR_ODBC_CURSORS prima della connessione a un'origine dati. L'attributo SQL_ATTR_ODBC_CURSORS può essere impostato su uno di tre valori seguenti:  
  
 SQL_CUR_USE_ODBC  
 Quando questa opzione è impostata con il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client, la libreria di cursori ODBC sostituisce il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporto nativo dei cursori del driver ODBC di Native Client. Solo i tipi di cursore supportati dalla libreria di cursori possono essere utilizzati per la connessione. Non è invece possibile utilizzare i cursori server a questo scopo.  
  
 SQL_CUR_USE_DRIVER  
 Quando questa opzione è impostata, tutte del cursore del supporto nativo per il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC di Native Client può essere utilizzato per la connessione. Non è possibile utilizzare la libreria di cursori ODBC. Tutti i cursori vengono implementati come cursori server.  
  
 SQL_CUR_USE_IF_NEEDED  
 Quando questa opzione è impostata, l'effetto è identico a SQL_CUR_USE_DRIVER con il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client. In fase di connessione, verifica se il driver ODBC cui si è connessi supporta l'opzione SQL_FETCH_PRIOR di gestione Driver ODBC [SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md). Se il driver non supporta l'opzione, Gestione driver ODBC carica la libreria di cursori ODBC. In caso contrario, Gestione driver ODBC non carica la libreria in questione e l'applicazione utilizza il supporto nativo del driver. Poiché il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client supporta SQL_FETCH_PRIOR, gestione Driver ODBC non carica la libreria di cursori ODBC.  
  
 La libreria di cursori consente alle applicazioni di utilizzare più istruzioni attive in una connessione, nonché cursori scorrevoli aggiornabili. Per il supporto di tale funzionalità è necessario caricare la libreria di cursori. Uso [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) per specificare come usare la libreria di cursori e [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) per specificare la dimensione di tipo, concorrenza e del set di righe del cursore.  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità di implementazione dei cursori](how-cursors-are-implemented.md)  
  
  
