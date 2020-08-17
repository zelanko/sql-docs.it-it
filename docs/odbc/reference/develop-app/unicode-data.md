---
description: Dati Unicode
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f217e6b629936cc835d134c89d972bb1408b9d0b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339117"
---
# <a name="unicode-data"></a>Dati Unicode
Sono disponibili tipi di dati Unicode SQL per descrivere i dati che risiedono in Unicode in modo nativo nel sistema DBMS. Viene fornito un tipo di dati Unicode C per consentire a un'applicazione di associare i dati a un buffer Unicode. Gestione driver è in grado di convertire i dati da un tipo C Unicode (SQL_C_WCHAR) per fare in modo che funzioni con un driver ANSI.  
  
 ODBC 3,0 o 2. l'applicazione *x* viene sempre associata ai tipi di dati ANSI. Per ottenere prestazioni ottimali, un'applicazione ODBC 3,5 (o versione successiva) deve essere associata al tipo di dati ANSI di tipo C se il tipo di colonna SQL è ANSI e deve essere associato al tipo di dati C Unicode se il tipo di colonna SQL è Unicode.  
  
 Gli indicatori di tipo Unicode SQL sono SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR. SQL_WCHAR dati hanno una lunghezza di stringa fissa, mentre SQL_WVARCHAR ha una lunghezza variabile con un valore massimo dichiarato e SQL_WLONGVARCHAR ha una lunghezza variabile con un valore massimo che dipende dall'origine dati.  
  
 L'indicatore di tipo Unicode C è SQL_C_WCHAR. Si tratta dell'impostazione predefinita per ognuno degli indicatori di tipo Unicode SQL. Tutti i tipi SQL possono essere convertiti in SQL_C_WCHAR e SQL_C_WCHAR possono essere convertiti in tutti i tipi SQL. Un'applicazione può recuperare i dati in uno dei tre modi seguenti:  
  
-   Recuperare i dati come SQL_C_CHAR.  
  
-   Recuperare i dati come SQL_C_WCHAR.  
  
-   Dichiarare i dati come SQL_C_TCHAR. Si tratta di una macro che inserisce SQL_C_WCHAR se l'applicazione viene compilata come applicazione Unicode o inserisce SQL_C_CHAR se viene compilata come applicazione ANSI.  
  
 SQL_C_TCHAR viene dichiarata in una funzione come indicato di seguito:  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 Quando l'applicazione viene compilata come applicazione Unicode, l'argomento *ValueType* verrebbe modificato da SQL_C_TCHAR a SQL_C_WCHAR. Quando l'applicazione viene compilata come applicazione ANSI, l'argomento *ValueType* viene modificato in SQL_C_CHAR.  
  
 I driver Unicode devono comunque supportare i tipi di dati ANSI, incluso SQL_CHAR. Se un'applicazione che utilizza un driver Unicode viene associata a SQL_CHAR, gestione driver non eseguirà il mapping dei dati SQL_CHAR a SQL_WCHAR. Il driver Unicode deve accettare i dati SQL_CHAR.  
  
 Gestione driver archivia i nomi di driver e DSN in Unicode e li associa a ANSI in base alle esigenze. Se non è possibile eseguire il mapping di un carattere Unicode a un carattere ANSI (come può verificarsi se i caratteri di una tabella codici che non corrisponde alla tabella codici nativa del computer vengono utilizzati nei nomi di driver e DSN), i caratteri che non possono essere convertiti sono rappresentati da un carattere predefinito fornito dal sistema.
