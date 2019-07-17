---
title: La connessione a un'origine dati (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- checking connection states
- ODBC data sources, connections
- data sources [SQL Server Native Client]
- SQLBrowseConnect function
- ODBC applications, connections
- ODBC applications, data sources
- connections [SQL Server Native Client]
- SQLConnect function
- SQLDriveConnect function
- verifying connection states
- SQL Server Native Client ODBC driver, data sources
- SQL Server Native Client ODBC driver, connections
ms.assetid: ae30dd1d-06ae-452b-9618-8fd8cd7ba074
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 092ff6fc878f9a53e6b39e4ca9e4ac1c348ffb83
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68134194"
---
# <a name="connecting-to-a-data-source-odbc"></a>Connessione a un'origine dati (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Dopo avere allocato handle di ambiente e di connessione e avere impostato tutti gli attributi di connessione, l'applicazione si connette all'origine dati o al driver. È possibile utilizzare tre funzioni per connettersi:  
  
-   **SQLConnect**  
  
-   **SQLDriverConnect**  
  
-   **SQLBrowseConnect**  
  
 Per altre informazioni sull'esecuzione di connessioni a un'origine dati, tra cui le diverse opzioni di stringa di connessione disponibili, vedere [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
## <a name="sqlconnect"></a>SQLConnect  
 **SQLConnect** è la più semplice funzione di connessione. La funzione accetta tre parametri: un nome di origine dati, un ID utente e una password. Uso **SQLConnect** quando questi tre parametri contengono tutte le informazioni necessarie per connettersi al database. A tale scopo, compilare un elenco di origini dati usando **SQLDataSources**; Richiedi all'utente un'origine dati, l'ID utente e password; e chiamare **SQLConnect**.  
  
 **SQLConnect** presuppone che un nome dell'origine dati, l'ID utente e password siano sufficienti per connettersi a un'origine dati e che l'origine dati ODBC contenga tutte le altre informazioni, il driver ODBC deve effettuare la connessione. A differenza [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) e [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md), **SQLConnect** non usa una stringa di connessione.  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
 **SQLDriverConnect** viene usato quando sono necessarie ulteriori informazioni rispetto il nome dell'origine dati, l'ID utente e password. Uno dei parametri **SQLDriverConnect** è una stringa di connessione contenente informazioni specifiche del driver. È possibile usare **SQLDriverConnect** invece di **SQLConnect** per i motivi seguenti:  
  
-   Per immettere informazioni specifiche del driver in fase di connessione.  
  
-   Per specificare che il driver deve richiedere all'utente le informazioni di connessione.  
  
-   Per connettersi senza utilizzare un'origine dati ODBC.  
  
 Il **SQLDriverConnect** stringa di connessione contiene una serie di coppie valore-parola chiave che specificano tutte le informazioni di connessione supportate da un driver ODBC. Ogni driver supporta le parole chiave ODBC standard (DSN, FILEDSN, DRIVER, UID, PWD e SAVEFILE) oltre a parole chiave specifiche del driver per tutte le informazioni di connessione supportate dal driver stesso. **SQLDriverConnect** può essere usato per connettersi senza un'origine dati. Ad esempio, un'applicazione progettata per stabilire una connessione "Senza DSN" a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può chiamare **SQLDriverConnect** con una stringa di connessione che definisce l'ID di accesso, la password, libreria di rete, nome del server connettersi a e del database predefinito da usare.  
  
 Quando si usa **SQLDriverConnect**, sono disponibili due opzioni per richiedere all'utente eventuali necessarie le informazioni di connessione:  
  
-   Finestra di dialogo dell'applicazione  
  
     È possibile creare una finestra di dialogo dell'applicazione che richiede le informazioni di connessione e quindi chiama **SQLDriverConnect** con un handle di finestra NULL e *DriverCompletion* impostato su SQL_DRIVER_NOPROMPT. Queste impostazioni impediscono di aprire la finestra di dialogo del driver ODBC. Questo metodo viene utilizzato quando è importante controllare l'interfaccia utente dell'applicazione.  
  
-   Finestra di dialogo del driver  
  
     È possibile codificare l'applicazione da passare a un handle di finestra valido **SQLDriverConnect** e impostare le *DriverCompletion* parametro SQL_DRIVER_COMPLETE, SQL_DRIVER_PROMPT o SQL_DRIVER_COMPLETE_ Obbligatorio. Il driver genera quindi una finestra di dialogo per richiedere all'utente le informazioni di connessione. Questo metodo semplifica il codice dell'applicazione.  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
 **SQLBrowseConnect**, ad esempio **SQLDriverConnect**, Usa una stringa di connessione. Tuttavia, utilizzando **SQLBrowseConnect**, un'applicazione può costruire una stringa di connessione completa in maniera iterativa con l'origine dati in fase di esecuzione. In questo modo, l'applicazione può eseguire due operazioni:  
  
-   Compilare finestre di dialogo proprie per richiedere tali informazioni, mantenendo in tal modo il controllo sull'interfaccia utente.  
  
-   Esplorare il sistema per individuare origini dati che possano essere utilizzate da un driver specifico, possibilmente in diversi passaggi.  
  
     L'utente, ad esempio, potrebbe esplorare innanzitutto la rete per individuare i server e, dopo averne scelto uno, esplorare il server per individuare i database accessibili dal driver.  
  
 Quando **SQLBrowseConnect** completa correttamente una connessione, viene restituita una stringa di connessione che può essere utilizzata nelle chiamate successive a **SQLDriverConnect**.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client restituisce sempre SQL_SUCCESS_WITH_INFO in un esito positivo **SQLConnect**, **SQLDriverConnect**, oppure **SQLBrowseConnect**. Quando un'applicazione ODBC chiama **SQLGetDiagRec** dopo avere ottenuto SQL_SUCCESS_WITH_INFO, può ricevere i messaggi seguenti:  
  
 5701  
 Indica che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha inserito il contesto dell'utente nel database predefinito specificato nell'origine dati o nel database predefinito specificato per l'ID di accesso utilizzato nella connessione se l'origine dati non dispone di un database predefinito.  
  
 5703  
 Indica la lingua utilizzata nel server.  
  
 Nell'esempio seguente viene riportato il messaggio restituito in una connessione eseguita correttamente dall'amministratore di sistema:  
  
```  
szSqlState = "01000", *pfNativeError = 5701,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
       Changed database context to 'pubs'."  
szSqlState = "01000", *pfNativeError = 5703,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
       Changed language setting to 'us_english'."  
```  
  
 È possibile ignorare i messaggi 5701 e 5703, in quanto di natura esclusivamente informativa. Non è consigliabile, tuttavia, ignorare un codice restituito di SQL_SUCCESS_WITH_INFO, in quanto è possibile che vengano generati messaggi diversi da 5701 o 5703. Se, ad esempio, un driver si connette a un server che esegue un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con le procedure di catalogo non aggiornate memorizzata, uno degli errori restituiti tramite **SQLGetDiagRec** dopo SQL_SUCCESS_WITH_INFO è:  
  
```  
SqlState:   01000  
pfNative:   0  
szErrorMsg: "[Microsoft][SQL Server Native Client]The ODBC  
            catalog stored procedures installed on server  
            my65server are version 06.50.0193; version 07.00.0205  
            or later is required to ensure proper operation.  
            Please contact your system administrator."  
```  
  
 L'errore di un'applicazione per funzione di gestione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] connessioni devono chiamare **SQLGetDiagRec** fino a quando non viene restituito SQL_NO_DATA. Deve quindi intervenire su qualsiasi messaggio diverso da quelli con un *pfNative* codice 5701 o 5703.  
  
## <a name="see-also"></a>Vedere anche  
 [Comunicazione con SQL Server &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
