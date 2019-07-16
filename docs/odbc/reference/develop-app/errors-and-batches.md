---
title: Errori e batch | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], errors
- sql_success_with_info [ODBC]
- sql_success [ODBC]
- SQL statements [ODBC], batches
- sql_error [ODBC]
ms.assetid: 6debd41d-9f4c-4f4c-a44b-2993da5306f0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6902b82c74e953d6009d7e5352608477d92122d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051136"
---
# <a name="errors-and-batches"></a>Errori e batch
Quando si verifica un errore durante l'esecuzione di un batch di istruzioni SQL, uno dei seguenti quattro risultati sono possibili. (Ogni risultato possibili è specifiche dell'origine dati e potrebbe dipendere anche le istruzioni incluse nel batch).  
  
-   Viene eseguita alcuna istruzione nel batch.  
  
-   Viene eseguita alcuna istruzione nel batch e viene eseguito il rollback della transazione.  
  
-   Vengono eseguite tutte le istruzioni prima dell'istruzione di errore.  
  
-   Vengono eseguite tutte le istruzioni, ad eccezione dell'istruzione di errore.  
  
 Nei primi due casi **SQLExecute** e **SQLExecDirect** restituirà SQL_ERROR. Negli ultimi due casi, possono restituire SQL_SUCCESS_WITH_INFO o SQL_SUCCESS, a seconda dell'implementazione. In tutti i casi, ulteriori informazioni sull'errore possono essere recuperati con **SQLGetDiagField**, **SQLGetDiagRec**, o **SQLError**. Tuttavia, la natura e la profondità di queste informazioni è specifico dell'origine dati. Inoltre, queste informazioni sono improbabile identificare esattamente l'istruzione in errore.
