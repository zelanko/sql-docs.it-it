---
title: Esempio di esplorazione SQL Server | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114334"
---
# <a name="sql-server-browsing-example"></a>Esempio di esplorazione di SQL Server
Nell'esempio seguente viene illustrato come utilizzare **SQLBrowseConnect** per esplorare le connessioni disponibili con un driver per SQL Server. Per prima cosa, l'applicazione richiede un handle di connessione:  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 Successivamente, l'applicazione chiama **SQLBrowseConnect** e specifica il driver SQL Server, usando la descrizione del driver restituita da **SQLDrivers**:  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Poiché si tratta della prima chiamata a **SQLBrowseConnect**, gestione driver carica il driver SQL Server e chiama la funzione **SQLBrowseConnect** del driver con gli stessi argomenti ricevuti dall'applicazione.  
  
> [!NOTE]  
>  Se ci si connette a un provider dell'origine dati che supporta l'autenticazione di Windows, `Trusted_Connection=yes` è necessario specificare al posto delle informazioni sull'ID utente e sulla password nella stringa di connessione.  
  
 Il driver determina che si tratta della prima chiamata a **SQLBrowseConnect** e restituisce il secondo livello degli attributi di connessione: Server, nome utente, password, nome dell'applicazione e ID workstation. Per l'attributo Server restituisce un elenco di nomi di server validi. Il codice restituito da **SQLBrowseConnect** è SQL_NEED_DATA. Ecco la stringa di risultato Browse:  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 Ogni parola chiave nella stringa di risultato Browse è seguita da due punti e da una o più parole prima del segno di uguale. Queste parole rappresentano il nome descrittivo che un'applicazione può usare per compilare una finestra di dialogo. Le parole chiave **app** e **WSID** sono precedute da un asterisco, il che significa che sono facoltative. Le parole chiave **Server**, **UID**e **pwd** non sono precedute da un asterisco. è necessario specificare i valori nella stringa della richiesta browse successiva. Il valore della parola chiave **Server** può essere uno dei server restituiti da **SQLBrowseConnect** o un nome fornito dall'utente.  
  
 L'applicazione chiama di nuovo **SQLBrowseConnect** , specificando il server verde e omettendo le parole chiave **app** e **WSID** e i nomi descrittivi dopo ogni parola chiave:  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Il driver tenta di connettersi al server verde. Se sono presenti errori non irreversibili, ad esempio una coppia parola chiave/valore mancante, **SQLBrowseConnect** restituisce SQL_NEED_DATA e rimane nello stesso stato in cui si trovava prima dell'errore. L'applicazione può chiamare **SQLGetDiagField** o **SQLGetDiagRec** per determinare l'errore. Se la connessione ha esito positivo, il driver restituisce SQL_NEED_DATA e restituisce la stringa di risultato Browse:  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 Poiché gli attributi in questa stringa sono facoltativi, l'applicazione può ometterli. Tuttavia, l'applicazione deve chiamare nuovamente **SQLBrowseConnect** . Se l'applicazione sceglie di omettere il nome e la lingua del database, specifica una stringa di richiesta di esplorazione vuota. In questo esempio, l'applicazione sceglie il database pubs e chiama **SQLBrowseConnect** per l'ultima volta, omettendo la parola chiave del **linguaggio** e l'asterisco prima della parola chiave **database** :  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Poiché l'attributo **database** è l'attributo di connessione finale richiesto dal driver, il processo di esplorazione è completo, l'applicazione è connessa all'origine dati e **SQLBrowseConnect** restituisce SQL_SUCCESS. **SQLBrowseConnect** restituisce inoltre la stringa di connessione completa come stringa di risultato Browse:  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 La stringa di connessione finale restituita dal driver non contiene i nomi descrittivi dopo ogni parola chiave, né contiene parole chiave facoltative non specificate dall'applicazione. L'applicazione può utilizzare questa stringa con **SQLDriverConnect** per ristabilire la connessione all'origine dati nell'handle di connessione corrente (dopo la disconnessione) o per connettersi all'origine dati in un handle di connessione diverso. Ad esempio:  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```
