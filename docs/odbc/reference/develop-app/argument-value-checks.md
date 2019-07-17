---
title: Controlli dei valori di argomento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- argument value checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 37a65f8b-83aa-456c-b7cf-500404abb38a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 013c8f80a672ed691e7519b318206c406171cfbc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077113"
---
# <a name="argument-value-checks"></a>Controlli del valore dell'argomento
Gestione Driver controlla i seguenti tipi di argomenti. Se non specificato diversamente, gestione Driver restituisce SQL_ERROR errori nei valori degli argomenti.  
  
-   Gli handle di ambiente, connessione e istruzione non sono in genere essere puntatori null. Gestione Driver non restituisca SQL_INVALID_HANDLE quando rileva un handle null.  
  
-   Argomenti di puntatore, obbligatori, ad esempio *OutputHandlePtr* nelle **SQLAllocHandle** e *Nomecursore* nel **SQLSetCursorName**, non può essere puntatori null.  
  
-   Flag di opzione che non supportano valori specifici del driver devono essere un valore valido. Ad esempio, *operazione* nelle **SQLSetPos** deve essere SQL_POSITION, SQL_REFRESH, SQL_UPDATE, SQL_DELETE o SQL_ADD.  
  
-   Flag di opzione deve essere supportato nella versione di ODBC supportati dal driver. Ad esempio, *InfoType* nelle **SQLGetInfo** non può essere SQL_ASYNC_MODE (introdotta in ODBC 3.0) quando si chiama un driver ODBC 2.0.  
  
-   I numeri di parametro e colonna devono essere maggiore di 0 oppure maggiore o uguale a 0, a seconda della funzione. Il driver deve controllare il limite massimo di questi valori di argomento in base al set di risultati corrente o l'istruzione SQL.  
  
-   Gli argomenti di lunghezza/indicatore e gli argomenti di lunghezza del buffer di dati devono contenere i valori appropriati. Ad esempio, l'argomento che specifica la lunghezza del nome di tabella nella **SQLColumns** (*NameLength3*) deve essere SQL_NTS o un valore maggiore di 0. *BufferLength* nelle **SQLDescribeCol** deve essere maggiore o uguale a 0. Il driver potrebbe essere necessario anche controllare questi argomenti. Ad esempio, potrebbero verificare che *NameLength3* è minore o uguale alla lunghezza massima di un nome di tabella nell'origine dati.
