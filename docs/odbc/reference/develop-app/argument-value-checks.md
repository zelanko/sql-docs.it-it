---
title: Controlli del valore dell'argomento Documenti Microsoft
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
ms.openlocfilehash: 6c6e4de16c4a1a80be893acbc7a1993b375f2fee
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298824"
---
# <a name="argument-value-checks"></a>Controlli del valore dell'argomento
Gestione Driver controlla i seguenti tipi di argomenti. Se non specificato diversamente, Gestione Driver restituisce SQL_ERROR per gli errori nei valori degli argomenti.  
  
-   Gli handle di ambiente, connessione e istruzione in genere non possono essere puntatori null. Gestione Driver restituisce SQL_INVALID_HANDLE quando trova un handle null.  
  
-   Gli argomenti del puntatore necessari, ad esempio *OutputHandlePtr* in **SQLAllocHandle** e *CursorName* in **SQLSetCursorName**, non possono essere puntatori null.  
  
-   I flag di opzione che non supportano valori specifici del driver devono essere un valore valido. Ad esempio, *Operazione* in **SQLSetPos** deve essere SQL_POSITION, SQL_REFRESH, SQL_UPDATE, SQL_DELETE o SQL_ADD.  
  
-   I flag di opzione devono essere supportati nella versione di ODBC supportata dal driver. Ad esempio, *InfoType* in **SQLGetInfo** non può essere SQL_ASYNC_MODE (introdotto in ODBC 3.0) quando si chiama un driver ODBC 2.0.  
  
-   I numeri di colonna e di parametro devono essere maggiori di 0 oppure maggiori o uguali a 0, a seconda della funzione. Il driver deve controllare il limite superiore di questi valori di argomento in base al set di risultati corrente o all'istruzione SQL.  
  
-   Gli argomenti di lunghezza/indicatore e gli argomenti di lunghezza del buffer di dati devono contenere valori appropriati. Ad esempio, l'argomento che specifica la lunghezza di un nome di tabella in **SQLColumns** (*NameLength3*) deve essere SQL_NTS o un valore maggiore di 0; *BufferLength* in **SQLDescribeCol** deve essere maggiore o uguale a 0. Il driver potrebbe anche essere necessario controllare questi argomenti. Ad esempio, potrebbe verificare che *NameLength3* sia minore o uguale alla lunghezza massima di un nome di tabella nell'origine dati.
