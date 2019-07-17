---
title: Esempio di esplorazione di SQL Server | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3f3a7568c0849844526ef5f172bcecc0a5857268
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114334"
---
# <a name="sql-server-browsing-example"></a>Esempio di esplorazione di SQL Server
L'esempio seguente illustra la modalità **SQLBrowseConnect** potrebbe essere utilizzato per esplorare le connessioni disponibili con un driver per SQL Server. In primo luogo, l'applicazione richiede un handle di connessione:  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 Successivamente, l'applicazione chiama **SQLBrowseConnect** e specifica il driver SQL Server, utilizzando la descrizione del driver restituita da **SQLDrivers**:  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Poiché questa è la prima chiamata a **SQLBrowseConnect**, gestione Driver viene caricato il driver SQL Server e il driver chiama **SQLBrowseConnect** canonica con gli stessi argomenti ricevuto dal applicazione.  
  
> [!NOTE]  
>  Se ci si connette a un provider dell'origine dati che supporta l'autenticazione di Windows, è necessario specificare `Trusted_Connection=yes` anziché le informazioni utente di ID e la password nella stringa di connessione.  
  
 Il driver determina che questa è la prima chiamata a **SQLBrowseConnect** e restituisce il secondo livello di attributi di connessione: server, nome utente, password, nome dell'applicazione e ID della workstation. Per l'attributo del server, restituisce un elenco di nomi di server valido. Il codice restituito dalla **SQLBrowseConnect** è SQL_NEED_DATA. Ecco la stringa di risultato di ricerca:  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 Ogni parola chiave nella stringa di risultato Sfoglia è seguita da una virgola e uno o più parole prima del segno di uguale. Queste parole sono il nome descrittivo che un'applicazione può usare per compilare una finestra di dialogo. Il **APP** e **WSID** parole chiave sono precedute da un asterisco, ossia sono facoltativi. Il **SERVER**, **UID**, e **PWD** parole chiave non sono precedute da un asterisco; devono essere specificati per tali nella stringa di richiesta Sfoglia successiva. Il valore per il **SERVER** parola chiave può essere uno dei server restituito da **SQLBrowseConnect** o un nome fornito dall'utente.  
  
 L'applicazione chiama **SQLBrowseConnect** specificando il server di colore verde e l'omissione di nuovo, il **APP** e **WSID** parole chiave e i nomi descrittivi dopo ogni parola chiave:  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Il driver prova a connettersi al server di colore verde. Se si verificano errori non irreversibili, ad esempio una coppia parola chiave / valore mancante, **SQLBrowseConnect** restituisce SQL_NEED_DATA e rimane nello stato com'era prima dell'errore. L'applicazione può chiamare **SQLGetDiagField** oppure **SQLGetDiagRec** per determinare l'errore. Se la connessione ha esito positivo, il driver restituisce SQL_NEED_DATA e restituisce la stringa di risultato di ricerca:  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 Poiché gli attributi in questa stringa sono facoltativi, può omettere l'applicazione li. Tuttavia, l'applicazione deve chiamare **SQLBrowseConnect** nuovamente. Se l'applicazione viene scelto di omettere il nome del database e la lingua, specifica una stringa di richiesta di ricerca vuota. In questo esempio, l'applicazione sceglie il database pubs e chiama **SQLBrowseConnect** un'ultima volta, omettendo il **LANGUAGE** (parola chiave) e l'asterisco prima il **DATABASE**parola chiave:  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Poiché il **DATABASE** è l'attributo di connessione finale richiesta dal driver, il processo di esplorazione è stato completato, l'applicazione è connessa all'origine dati, e **SQLBrowseConnect** Restituisce SQL_SUCCESS. **SQLBrowseConnect** restituisce anche la stringa di connessione completa come la stringa di risultato esplorazione:  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 La stringa di connessione finale restituita dal driver non contiene i nomi descrittivi dopo ogni parola chiave, né contiene parole chiave facoltative non specificate dall'applicazione. L'applicazione può usare questa stringa con **SQLDriverConnect** per ristabilire la connessione all'origine dati nell'handle di connessione corrente (dopo la disconnessione) o per connettersi all'origine dati su un handle di connessione diversa. Ad esempio:  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```
