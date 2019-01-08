---
title: Creazione di un'applicazione di Driver ODBC di SQL Server Native Client | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, architecture
- SQL Server Native Client ODBC driver, creating applications
- ODBC function calls
- ODBC, header files
- ODBC applications
- ODBC applications, creating
- SQL Server Native Client ODBC driver, extensions
- applications [SQL Server Native Client]
- SQL Server Native Client ODBC driver, ODBC architecture
- extensions [ODBC]
- ODBC, driver extensions
- function calls [ODBC]
ms.assetid: c83c36e2-734e-4960-bc7e-92235910bc6f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db71e2ca03cbefdccf0bdf879fdb43d775125064
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53362173"
---
# <a name="creating-a-sql-server-native-client-odbc-driver-application"></a>Creazione di un'applicazione driver ODBC di SQL Server Native Client
  L'architettura ODBC include quattro componenti che eseguono le funzioni seguenti.  
  
|Componente|Funzione|  
|---------------|--------------|  
|Applicazione|Chiama funzioni ODBC per comunicare con un'origine dati ODBC, invia istruzioni SQL ed elabora set di risultati.|  
|Gestione driver|Gestisce la comunicazione tra un'applicazione e tutti i driver ODBC utilizzati dall'applicazione.|  
|Driver|Elabora tutte le chiamate di funzioni ODBC dall'applicazione, si connette a un'origine dati, passa istruzioni SQL dall'applicazione all'origine dati e restituisce risultati all'applicazione. Se necessario, il driver converte dati ODBC SQL dall'applicazione al formato SQL nativo utilizzato dall'origine dati.|  
|Origine dati|Contiene tutte le informazioni di cui necessita un driver per accedere a un'istanza specifica di dati in un DBMS.|  
  
 Un'applicazione che utilizza il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client per comunicare con un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esegue le attività seguenti:  
  
-   Si connette a un'origine dati  
  
-   Invia istruzioni SQL all'origine dati  
  
-   Elabora i risultati delle istruzioni dall'origine dati  
  
-   Elabora errori e messaggi  
  
-   Termina la connessione all'origine dati  
  
 Un'applicazione più complessa per la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client è possibile che anche le seguenti operazioni:  
  
-   Utilizzare cursori per controllare la posizione in un set di risultati  
  
-   Richiedere operazioni di commit o rollback per il controllo delle transazioni  
  
-   Eseguire transazioni distribuite che interessano due o più server  
  
-   Eseguire stored procedure nel server remoto  
  
-   Chiamare funzioni di catalogo per richiedere informazioni sugli attributi di un set di risultati  
  
-   Eseguire operazioni di copia bulk  
  
-   Gestire i dati di grandi dimensioni (**varchar (max)**, **nvarchar (max)**, e **varbinary (max)** colonne) operazioni  
  
-   Utilizzare logica di riconnessione per semplificare il failover quando è configurato il mirroring del database  
  
-   Registrare dati relativi alle prestazioni e query con esecuzione prolungata  
  
 Per eseguire chiamate di funzioni ODBC, un'applicazione C o C++ deve includere i file di intestazione sql.h, sqlext.h e sqltypes.h. Per eseguire chiamate alle funzioni API del programma di installazione ODBC, un'applicazione deve includere il file di intestazione odbcinst.h. Un'applicazione ODBC Unicode deve includere il file di intestazione sqlucode.h. Le applicazioni ODBC devono essere collegate con il file odbc32.lib. Le applicazioni ODBC che chiamano funzioni API del programma di installazione ODBC devono essere collegate con il file odbccp32.lib. Tali file sono inclusi in Windows Platform SDK.  
  
 Molti driver ODBC, tra cui la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] il driver ODBC Native Client, offrire estensioni ODBC driver specifici. Per poter sfruttare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] estensioni specifiche del driver ODBC Native Client, un'applicazione devono includere il file di intestazione sqlncli.h. Questo file di intestazione contiene gli elementi seguenti:  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Attributi di connessione specifiche del driver Client ODBC nativi.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Attributi di istruzione specifica del driver Client ODBC nativi.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Attributi di colonna specifici del driver Client ODBC nativi.  
  
-   Tipi di dati specifici di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Tipi di dati definiti dall'utente specifici di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC specifiche [SQLGetInfo](../../native-client-odbc-api/sqlgetinfo.md) tipi.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Campi di diagnostica driver Client ODBC nativi.  
  
-   Codici di funzioni dinamiche di diagnostica specifiche di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Definizioni di tipi C/C++ per tipi di dati C nativi specifici di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (restituite quando le colonne sono associate al tipo di dati C SQL_C_BINARY).  
  
-   Definizione del tipo per la struttura di dati SQLPERF.  
  
-   Macro e prototipi di copia bulk per supportare l'utilizzo di API per la copia bulk tramite una connessione ODBC.  
  
-   Chiamata delle funzioni API dei metadati delle query distribuite per ottenere elenchi di server collegati e dei relativi cataloghi.  
  
 Qualsiasi applicazione C o C++ ODBC che utilizza la funzione di copia di massa di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client deve essere collegato con il file sqlncli11.lib. Le applicazioni che chiamano le funzioni API dei metadati delle query distribuite devono anch'esse essere collegate con sqlncli11.lib. I file sqlncli.h e sqlncli11.lib vengono distribuiti come parte del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gli strumenti per gli sviluppatori. Le directory Include e Lib di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devono essere incluse nei percorsi INCLUDE e LIB del compilatore, come illustrato di seguito:  
  
```  
LIB=c:\Program Files\Microsoft Data Access SDK 2.8\Libs\x86\lib;C:\Program Files\Microsoft SQL Server\100\Tools\SDK\Lib;  
INCLUDE=c:\Program Files\Microsoft Data Access SDK 2.8\inc;C:\Program Files\Microsoft SQL Server\100\Tools\SDK\Include;  
```  
  
 Una decisione di progettazione da adottare nelle fasi iniziali del processo di compilazione di un'applicazione consiste nello stabilire se l'applicazione debba supportare più chiamate ODBC in sospeso simultaneamente. Per supportare più chiamate ODBC simultanee, sono disponibili due metodi, descritti più avanti in questa sezione. Per ulteriori informazioni, vedere la [di riferimento del programmatore di ODBC](https://go.microsoft.com/fwlink/?LinkId=45250).  
  
## <a name="in-this-section"></a>In questa sezione  
  
-   [Modalità asincrona e SQLCancel](../../native-client-odbc-api/sqlcancel.md)  
  
-   [Applicazioni a thread multipli](creating-a-driver-application-multithreaded-applications.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)  
  
  
