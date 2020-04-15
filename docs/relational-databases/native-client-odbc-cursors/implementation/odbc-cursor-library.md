---
title: Libreria di cursori ODBC - Documenti Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 93c85bc943d1a6a081cbea6bbeae40ba85aeffc5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305399"
---
# <a name="odbc-cursor-library"></a>Libreria di cursori ODBC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Alcuni driver ODBC supportano solo le impostazioni predefinite del cursore; questi driver inoltre non supportano le operazioni del cursore posizionato, ad esempio **SQLSetPos**. La libreria di cursori ODBC è un componente di Microsoft Data Access Components (MDAC) utilizzato per implementare cursori a blocchi o statici in un driver che generalmente non li supporta. La libreria di cursori implementa anche le istruzioni UPDATE e DELETE posizionate e **SQLSetPos** per i cursori creati.  
  
 La libreria di cursori ODBC viene implementata come livello tra Gestione driver ODBC e il driver ODBC. Se la libreria viene caricata, a questa, e non al driver, vengono indirizzati tutti i comandi correlati al cursore. La libreria di cursori implementa un cursore mediante il recupero dell'intero set di risultati dal driver sottostante e la memorizzazione nella cache del client del set di risultati. Quando si utilizza la libreria di cursori ODBC, nell'applicazione sono disponibili solo le funzionalità di cursore della libreria di cursori e non funzionalità di cursore aggiuntive del driver sottostante.  
  
 Con il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client non esiste l'esigenza di utilizzare la libreria di cursori ODBC, in quanto il driver supporta un numero maggiore di funzionalità di cursore rispetto alla libreria. L'unico motivo per utilizzare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] la libreria di cursori ODBC con il driver ODBC Native Client è perché il driver implementa il supporto del cursore tramite i cursori del server e i cursori del server non supportano tutte le istruzioni SQL. È pertanto consigliabile utilizzare la libreria di cursori ODBC ogni volta che si richiede un cursore statico con stored procedure, batch o istruzioni SQL contenenti COMPUTE, COMPUTE BY, FOR BROWSE o INTO. È tuttavia necessario prestare attenzione nell'utilizzo della libreria in quanto memorizza nella cache del client l'intero set di risultati con conseguente impiego di grandi quantità di memoria e rallentamento delle prestazioni.  
  
 Un'applicazione richiama la libreria di cursori in base alla connessione utilizzando [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) per impostare l'attributo di connessione SQL_ATTR_ODBC_CURSORS prima della connessione a un'origine dati. L'attributo SQL_ATTR_ODBC_CURSORS può essere impostato su uno di tre valori seguenti:  
  
 SQL_CUR_USE_ODBC  
 Quando questa opzione è [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] impostata con il driver ODBC [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, la libreria di cursori ODBC esegue l'override del supporto del cursore nativo del driver ODBC native del driver Native Client. Solo i tipi di cursore supportati dalla libreria di cursori possono essere utilizzati per la connessione. Non è invece possibile utilizzare i cursori server a questo scopo.  
  
 SQL_CUR_USE_DRIVER  
 Quando questa opzione è impostata, tutto [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] il cursore supporta nativo per il driver ODBC Native Client può essere utilizzato per la connessione. Non è possibile utilizzare la libreria di cursori ODBC. Tutti i cursori vengono implementati come cursori server.  
  
 SQL_CUR_USE_IF_NEEDED  
 Quando questa opzione è impostata, l'effetto è [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] lo stesso di SQL_CUR_USE_DRIVER quando viene utilizzato con il driver ODBC Native Client. In fase di connessione, Gestione Driver ODBC verifica se il driver ODBC a cui si è connessi supporta l'opzione SQL_FETCH_PRIOR di [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md). Se il driver non supporta l'opzione, Gestione driver ODBC carica la libreria di cursori ODBC. In caso contrario, Gestione driver ODBC non carica la libreria in questione e l'applicazione utilizza il supporto nativo del driver. Poiché [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] il driver ODBC Native Client supporta SQL_FETCH_PRIOR, Gestione Driver ODBC non carica la libreria di cursori ODBC.  
  
 La libreria di cursori consente alle applicazioni di utilizzare più istruzioni attive in una connessione, nonché cursori scorrevoli aggiornabili. Per il supporto di tale funzionalità è necessario caricare la libreria di cursori. Utilizzare [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) per specificare come deve essere utilizzata la libreria di cursori e [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) per specificare il tipo di cursore, la concorrenza e le dimensioni del set di righe.  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità di implementazione dei cursori](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
