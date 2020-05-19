---
title: Creazione di un SQL Server Native Client applicazione driver ODBC | Microsoft Docs
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4c5dc6e2452ea538f30e9ac10fa27b051aba13a1
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707100"
---
# <a name="creating-a-sql-server-native-client-odbc-driver-application"></a>Creazione di un'applicazione driver ODBC di SQL Server Native Client
  L'architettura ODBC include quattro componenti che eseguono le funzioni seguenti.  
  
|Componente|Funzione|  
|---------------|--------------|  
|Applicazione|Chiama funzioni ODBC per comunicare con un'origine dati ODBC, invia istruzioni SQL ed elabora set di risultati.|  
|Gestione driver|Gestisce la comunicazione tra un'applicazione e tutti i driver ODBC utilizzati dall'applicazione.|  
|Driver|Elabora tutte le chiamate di funzioni ODBC dall'applicazione, si connette a un'origine dati, passa istruzioni SQL dall'applicazione all'origine dati e restituisce risultati all'applicazione. Se necessario, il driver converte dati ODBC SQL dall'applicazione al formato SQL nativo utilizzato dall'origine dati.|  
|Origine dati|Contiene tutte le informazioni di cui necessita un driver per accedere a un'istanza specifica di dati in un DBMS.|  
  
 Un'applicazione che utilizza il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC di Native Client per comunicare con un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esegue le attività seguenti:  
  
-   Si connette a un'origine dati  
  
-   Invia istruzioni SQL all'origine dati  
  
-   Elabora i risultati delle istruzioni dall'origine dati  
  
-   Elabora errori e messaggi  
  
-   Termina la connessione all'origine dati  
  
 Un'applicazione più complessa scritta per il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC di Native client potrebbe inoltre eseguire le attività seguenti:  
  
-   Utilizzare cursori per controllare la posizione in un set di risultati  
  
-   Richiedere operazioni di commit o rollback per il controllo delle transazioni  
  
-   Eseguire transazioni distribuite che interessano due o più server  
  
-   Eseguire stored procedure nel server remoto  
  
-   Chiamare funzioni di catalogo per richiedere informazioni sugli attributi di un set di risultati  
  
-   Eseguire operazioni di copia bulk  
  
-   Gestire le operazioni di dati di grandi dimensioni (**varchar (max)**, **nvarchar (max)** e **varbinary (max)** )  
  
-   Utilizzare logica di riconnessione per semplificare il failover quando è configurato il mirroring del database  
  
-   Registrare dati relativi alle prestazioni e query con esecuzione prolungata  
  
 Per eseguire chiamate di funzioni ODBC, un'applicazione C o C++ deve includere i file di intestazione sql.h, sqlext.h e sqltypes.h. Per eseguire chiamate alle funzioni API del programma di installazione ODBC, un'applicazione deve includere il file di intestazione odbcinst.h. Un'applicazione ODBC Unicode deve includere il file di intestazione sqlucode.h. Le applicazioni ODBC devono essere collegate con il file odbc32.lib. Le applicazioni ODBC che chiamano funzioni API del programma di installazione ODBC devono essere collegate con il file odbccp32.lib. Tali file sono inclusi in Windows Platform SDK.  
  
 Molti driver ODBC, incluso il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC di Native client, offrono estensioni ODBC specifiche del driver. Per sfruttare i vantaggi delle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] estensioni specifiche del driver ODBC di Native client, un'applicazione deve includere il file di intestazione sqlncli. h. Questo file di intestazione contiene gli elementi seguenti:  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Attributi di connessione specifici del driver ODBC di Native Client.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Attributi di istruzione specifici del driver ODBC di Native Client.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Attributi di colonna specifici del driver ODBC di Native Client.  
  
-   Tipi di dati specifici di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Tipi di dati definiti dall'utente specifici di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Tipi di [SQLGetInfo](../../native-client-odbc-api/sqlgetinfo.md) specifici del driver ODBC di Native Client.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Campi di diagnostica del driver ODBC di Native Client.  
  
-   Codici di funzioni dinamiche di diagnostica specifiche di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Definizioni di tipi C/C++ per tipi di dati C nativi specifici di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (restituite quando le colonne sono associate al tipo di dati C SQL_C_BINARY).  
  
-   Definizione del tipo per la struttura di dati SQLPERF.  
  
-   Macro e prototipi di copia bulk per supportare l'utilizzo di API per la copia bulk tramite una connessione ODBC.  
  
-   Chiamata delle funzioni API dei metadati delle query distribuite per ottenere elenchi di server collegati e dei relativi cataloghi.  
  
 Qualsiasi applicazione ODBC C o C++ che utilizza la funzionalità di copia bulk del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC di Native client deve essere collegata con il file sqlncli11. lib. Le applicazioni che chiamano le funzioni API dei metadati delle query distribuite devono anch'esse essere collegate con sqlncli11.lib. I file sqlncli. h e sqlncli11. lib vengono distribuiti come parte degli [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] strumenti di sviluppo. Le directory Include e Lib di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devono essere incluse nei percorsi INCLUDE e LIB del compilatore, come illustrato di seguito:  
  
```  
LIB=c:\Program Files\Microsoft Data Access SDK 2.8\Libs\x86\lib;C:\Program Files\Microsoft SQL Server\100\Tools\SDK\Lib;  
INCLUDE=c:\Program Files\Microsoft Data Access SDK 2.8\inc;C:\Program Files\Microsoft SQL Server\100\Tools\SDK\Include;  
```  
  
 Una decisione di progettazione da adottare nelle fasi iniziali del processo di compilazione di un'applicazione consiste nello stabilire se l'applicazione debba supportare più chiamate ODBC in sospeso simultaneamente. Per supportare più chiamate ODBC simultanee, sono disponibili due metodi, descritti più avanti in questa sezione. Per ulteriori informazioni, vedere [ODBC Programmer ' s Reference](https://go.microsoft.com/fwlink/?LinkId=45250).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Modalità asincrona e SQLCancel](../../native-client-odbc-api/sqlcancel.md)  
  
-   [Applicazioni a thread multipli](creating-a-driver-application-multithreaded-applications.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)  
  
  
