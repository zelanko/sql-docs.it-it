---
title: Dati Unicode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], data
- data types [ODBC], Unicode
- C data types [ODBC], Unicode
- SQL data types [ODBC], Unicode
ms.assetid: abc28718-e6d9-49fb-97ff-402d50c3c375
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74de6c44aaf109a434f0cf76c6902abfba92efe1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305766"
---
# <a name="unicode-data"></a>Dati Unicode
Tipi di dati SQL Unicode vengono forniti per descrivere i dati che si trovano in formato Unicode in modo nativo nel sistema DBMS. Un tipo di dati Unicode C viene fornito per consentire a un'applicazione associare dati a un buffer di Unicode. Gestione Driver può convertire i dati da un tipo C Unicode (SQL_C_WCHAR) per renderla funzione con un driver ANSI.  
  
 Un database ODBC 3.0 o 2. *x* applicazione eseguirà sempre l'associazione ai tipi di dati ANSI. Per ottenere prestazioni ottimali, un'applicazione ODBC 3.5 (o versione successiva) deve essere associato al tipo di dati C ANSI se il tipo di colonna SQL ANSI e deve essere associato al tipo di dati Unicode C se il tipo di colonna SQL è un file Unicode.  
  
 Gli indicatori di tipo SQL Unicode sono SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR. I dati SQL_WCHAR ha una lunghezza di stringa fissa, SQL_WVARCHAR ha una lunghezza variabile con un massimo dichiarato e SQL_WLONGVARCHAR presenta una lunghezza variabile con un valore massimo che dipende dall'origine dati.  
  
 L'indicatore di tipo C Unicode è SQL_C_WCHAR. Questo è il valore predefinito per ognuno degli indicatori di tipo SQL Unicode. Tutti i tipi SQL può essere convertiti in SQL_C_WCHAR, e SQL_C_WCHAR può essere convertito in tutti i tipi SQL. Un'applicazione può recuperare i dati in uno dei tre modi:  
  
-   Recuperare i dati come SQL_C_CHAR.  
  
-   Come SQL_C_WCHAR, recuperare i dati.  
  
-   Dichiarare i dati come SQL_C_TCHAR. Si tratta di una macro che inserisce SQL_C_WCHAR se l'applicazione viene compilata come un'applicazione Unicode oppure ne inserisce SQL_C_CHAR se viene compilato come applicazioni ANSI.  
  
 SQL_C_TCHAR viene dichiarato in una funzione come indicato di seguito:  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 Quando viene compilata l'applicazione come applicazione a Unicode, il *ValueType* argomento potrebbe essere modificato da SQL_C_TCHAR in SQL_C_WCHAR. Quando l'applicazione viene compilata come applicazioni ANSI, il *ValueType* argomento verrà modificato da SQL_C_CHAR.  
  
 Driver di Unicode deve comunque supportare tipi di dati ANSI, tra cui SQL_CHAR. Se un'applicazione che utilizza un driver di Unicode associa al SQL_CHAR, gestione Driver non assocerà i dati SQL_CHAR SQL_WCHAR. Il driver di Unicode debba accettare i dati SQL_CHAR.  
  
 Gestione Driver archivia driver e i nomi DSN in formato Unicode e ne esegue il mapping ad ANSI in base alle esigenze. Se un carattere Unicode non può essere mappato a un carattere ANSI (come può verificarsi se caratteri da una pagina di codice che non è la pagina di codice nativo del computer vengono utilizzati nei nomi DSN e driver), i caratteri che non possono essere convertiti sono rappresentati da un sup di carattere predefinito plied dal sistema.
