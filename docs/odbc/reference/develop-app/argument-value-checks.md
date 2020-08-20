---
description: Controlli del valore dell'argomento
title: Controlli del valore dell'argomento | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5dac29eea6c9a2b5f178aa233520674ea466cf48
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465953"
---
# <a name="argument-value-checks"></a>Controlli del valore dell'argomento
Gestione driver controlla i seguenti tipi di argomenti. Se non specificato diversamente, gestione driver restituisce SQL_ERROR per gli errori nei valori degli argomenti.  
  
-   Gli handle di ambiente, di connessione e di istruzione in genere non possono essere puntatori null. Gestione driver restituisce SQL_INVALID_HANDLE quando viene trovato un handle null.  
  
-   Gli argomenti del puntatore necessari, ad esempio *OutputHandlePtr* in **SQLAllocHandle** e *CursorName* in **SQLSetCursorName**, non possono essere puntatori null.  
  
-   I flag di opzione che non supportano valori specifici del driver devono essere un valore valido. L' *operazione* in **SQLSetPos** , ad esempio, deve essere SQL_POSITION, SQL_REFRESH, SQL_UPDATE, SQL_DELETE o SQL_ADD.  
  
-   I flag di opzione devono essere supportati nella versione di ODBC supportata dal driver. Ad esempio, *InfoType* in **SQLGetInfo** non può essere SQL_ASYNC_MODE (introdotto in ODBC 3,0) quando si chiama un driver ODBC 2,0.  
  
-   I numeri di colonna e di parametro devono essere maggiori di 0 oppure maggiori o uguali a 0, a seconda della funzione. Il driver deve controllare il limite superiore di questi valori di argomento in base al set di risultati o all'istruzione SQL corrente.  
  
-   Gli argomenti relativi a lunghezza/indicatore e lunghezza del buffer di dati devono contenere valori appropriati. Ad esempio, l'argomento che specifica la lunghezza di un nome di tabella in **SQLColumns** (*NameLength3*) deve essere SQL_NTS o un valore maggiore di 0; *BufferLength* in **SQLDescribeCol** deve essere maggiore o uguale a 0. Il driver potrebbe anche dover controllare questi argomenti. Ad esempio, potrebbe verificare che *NameLength3* sia minore o uguale alla lunghezza massima di un nome di tabella nell'origine dati.
