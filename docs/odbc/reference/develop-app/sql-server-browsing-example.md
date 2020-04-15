---
title: Esempio di esplorazione di SQL Server Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBrowseConnect function [ODBC], example
- connecting to data source [ODBC], SqlBrowseConnect
- connecting to driver [ODBC], SQLBrowseConnect
ms.assetid: 6e0d5fd1-ec93-4348-a77a-08f5ba738bc6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7b15aa8e3d573660a312fceb5b9100a41f0384d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301982"
---
# <a name="sql-server-browsing-example"></a>Esempio di esplorazione di SQL Server
Nell'esempio seguente viene illustrato come SQLBrowseConnect può essere utilizzato per esplorare le connessioni disponibili con un driver per SQL Server.The following example shows how **SQLBrowseConnect** might be used to browse the connections available with a driver for SQL Server. In primo luogo, l'applicazione richiede un handle di connessione:First, the application requests a connection handle:  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 Successivamente, l'applicazione chiama **SQLBrowseConnect** e specifica il driver di SQL Server, utilizzando la descrizione del driver restituito da **SQLDrivers**:  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Poiché si tratta della prima chiamata a **SQLBrowseConnect**, Gestione Driver carica il driver di SQL Server e chiama la funzione **SQLBrowseConnect** del driver con gli stessi argomenti ricevuti dall'applicazione.  
  
> [!NOTE]  
>  Se ci si connette a un provider di origini `Trusted_Connection=yes` dati che supporta l'autenticazione di Windows, è necessario specificare al posto delle informazioni relative all'ID utente e alla password nella stringa di connessione.  
  
 Il driver determina che si tratta della prima chiamata a **SQLBrowseConnect** e restituisce il secondo livello di attributi di connessione: server, nome utente, password, nome dell'applicazione e ID workstation. Per l'attributo server, restituisce un elenco di nomi di server validi. Il codice restituito da **SQLBrowseConnect** è SQL_NEED_DATA. Di seguito è riportata la stringa di risultato di sfoglia:Here is the browse result string:  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 Ogni parola chiave nella stringa di risultato Sfoglia è seguita da due punti e da una o più parole prima del segno di uguale. Queste parole sono il nome descrittivo che un'applicazione può utilizzare per compilare una finestra di dialogo. Le parole chiave **APP** e **WSID** sono precedute da un asterisco, ovvero sono facoltative. Le parole chiave **SERVER**, **UID**e **PWD** non sono precedute da un asterisco; i valori devono essere forniti per loro nella stringa di richiesta Sfoglia successiva. Il valore per la parola chiave **SERVER** può essere uno dei server restituiti da **SQLBrowseConnect** o un nome fornito dall'utente.  
  
 L'applicazione chiama nuovamente **SQLBrowseConnect,** specificando il server verde e omettendo le parole **chiave APP** e **WSID** e i nomi descrittivi dopo ogni parola chiave:  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Il driver tenta di connettersi al server verde. Se sono presenti errori non irreversibili, ad esempio una coppia parola chiave-valore mancante, **SQLBrowseConnect** restituisce SQL_NEED_DATA e rimane nello stesso stato in cui si trovava prima dell'errore. L'applicazione può chiamare **SQLGetDiagField** o **SQLGetDiagRec** per determinare l'errore. Se la connessione ha esito positivo, il driver restituisce SQL_NEED_DATA e restituisce la stringa di risultato Sfoglia:If the connection is successful, the driver returns SQL_NEED_DATA and returns the browse result string:  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 Poiché gli attributi in questa stringa sono facoltativi, l'applicazione può ometterli. Tuttavia, l'applicazione deve chiamare **SQLBrowseConnect** nuovamente. Se l'applicazione sceglie di omettere il nome e la lingua del database, specifica una stringa di richiesta di esplorazione vuota. In questo esempio, l'applicazione sceglie il database pubs e chiama **SQLBrowseConnect** un'ultima volta, omettendo la parola chiave **LANGUAGE** e l'asterisco prima della parola chiave **DATABASE:**  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Poiché l'attributo **DATABASE** è l'attributo di connessione finale richiesto dal driver, il processo di esplorazione è completo, l'applicazione è connessa all'origine dati e **SQLBrowseConnect** restituisce SQL_SUCCESS. **SQLBrowseConnect** restituisce anche la stringa di connessione completa come stringa di risultato sfoglia:SQLBrowseConnect also returns the complete connection string as the browse result string:  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 La stringa di connessione finale restituita dal driver non contiene i nomi descrittivi dopo ogni parola chiave, né contiene parole chiave facoltative non specificate dall'applicazione. L'applicazione può usare questa stringa con **SQLDriverConnect** per riconnettersi all'origine dati sull'handle di connessione corrente (dopo la disconnessione) o per connettersi all'origine dati su un handle di connessione diverso. Ad esempio:  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```
