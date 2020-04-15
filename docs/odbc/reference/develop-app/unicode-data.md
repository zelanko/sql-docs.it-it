---
title: 'Proprietà Unicode Data : Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73ea9035b05f04fec1527ca2aa98531a807db8cf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307398"
---
# <a name="unicode-data"></a>Dati Unicode
I tipi di dati Unicode SQL vengono forniti per descrivere i dati che risiedono in Unicode in modo nativo nel dbMS. Viene fornito un tipo di dati Unicode C per consentire a un'applicazione di associare dati a un buffer Unicode. Gestione Driver può convertire i dati da un tipo Unicode C (SQL_C_WCHAR) per farlo funzionare con un driver ANSI.  
  
 Un ODBC 3.0 o 2. *X* l'applicazione verrà sempre associata ai tipi di dati ANSI. Per ottenere prestazioni ottimali, un'applicazione ODBC 3.5 (o successiva) deve essere associata al tipo di dati C ANSI se il tipo di colonna SQL è ANSI e deve essere associata al tipo di dati Unicode C se il tipo di colonna SQL è Unicode.  
  
 Gli indicatori di tipo Unicode SQL sono SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR. SQL_WCHAR dati ha una lunghezza di stringa fissa, mentre SQL_WVARCHAR ha una lunghezza variabile con un massimo dichiarato e SQL_WLONGVARCHAR ha una lunghezza variabile con un massimo che dipende dall'origine dati.  
  
 L'indicatore di tipo Unicode C è SQL_C_WCHAR. Questa è l'impostazione predefinita per ognuno degli indicatori di tipo Unicode SQL. Tutti i tipi SQL possono essere convertiti in SQL_C_WCHAR e SQL_C_WCHAR possono essere convertiti in tutti i tipi SQL. Un'applicazione può recuperare i dati in uno dei tre modi seguenti:An application can retrieve data in one of three ways:  
  
-   Recuperare i dati come SQL_C_CHAR.  
  
-   Recuperare i dati come SQL_C_WCHAR.  
  
-   Dichiarare i dati come SQL_C_TCHAR. Si tratta di una macro che inserisce SQL_C_WCHAR se l'applicazione viene compilata come un'applicazione Unicode o inserisce SQL_C_CHAR se viene compilata come applicazione ANSI.  
  
 SQL_C_TCHAR è dichiarata in una funzione come segue:  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 Quando l'applicazione viene compilata come applicazione Unicode, l'argomento *ValueType* verrebbe modificato da SQL_C_TCHAR a SQL_C_WCHAR. Quando l'applicazione viene compilata come applicazione ANSI, l'argomento *ValueType* viene modificato in SQL_C_CHAR.  
  
 I driver Unicode devono comunque supportare i tipi di dati ANSI, incluse le SQL_CHAR. Se un'applicazione che utilizza un driver Unicode viene associata a SQL_CHAR, Gestione Driver non verrà eseguito il mapping dei dati SQL_CHAR a SQL_WCHAR. Il driver Unicode deve accettare i dati SQL_CHAR.  
  
 Gestione Driver archivia i nomi dei driver e DSN in Unicode e li esegue il mapping ad ANSI in base alle esigenze. Se non è possibile eseguire il mapping di un carattere Unicode a un carattere ANSI (come può verificarsi se i caratteri di una tabella codici che non è la tabella codici nativa del computer vengono utilizzati nei nomi di driver e DSN), i caratteri che non è possibile convertire sono rappresentati da un carattere predefinito fornito dal sistema.
