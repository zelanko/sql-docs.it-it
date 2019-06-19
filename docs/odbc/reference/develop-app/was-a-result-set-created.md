---
title: Verifica della creazione di un set di risultati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], determining if created
ms.assetid: 4a83b8cb-2d57-4e64-b497-80bd587ee1f9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db287e729678f54aaf637950c89c724724678f08
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63208392"
---
# <a name="was-a-result-set-created"></a>Verifica della creazione di un set di risultati
Nella maggior parte dei casi, i programmatori di applicazioni sapere se le istruzioni in cui che viene eseguita l'applicazione creerà un set di risultati. Questo è il caso se l'applicazione Usa istruzioni SQL hard-coded scritte dal programmatore. Di solito avviene quando l'applicazione crea istruzioni SQL in fase di esecuzione: Il programmatore può facilmente includere codice che consente di contrassegnare se un **seleziona** istruzione o un' **Inserisci** istruzione in fase di costruzione. In alcune situazioni, il programmatore non è possibile conoscere se un'istruzione creerà un set di risultati. Questo è vero se l'applicazione consente all'utente di immettere ed eseguire un'istruzione SQL. È anche true quando l'applicazione crea un'istruzione in fase di esecuzione per eseguire una procedura.  
  
 In questi casi, l'applicazione chiama **SQLNumResultCols** per determinare il numero di colonne nel set di risultati. Se è 0, l'istruzione non è stato creato un set di risultati. in caso di qualsiasi altro numero, l'istruzione è stato creato un set di risultati.  
  
 L'applicazione può chiamare **SQLNumResultCols** in qualsiasi momento dopo la preparazione o l'esecuzione dell'istruzione. Tuttavia, poiché alcune origini dati facilmente non è possibile descrivere i set di risultati che verranno creati per le istruzioni preparate, le prestazioni ne risentiranno se **SQLNumResultCols** viene chiamato dopo che un'istruzione preparata ma prima che venga eseguito.  
  
 Alcune origini dati supportano anche determinare il numero di righe che restituisce un'istruzione SQL in un set di risultati. A tale scopo, l'applicazione chiama **SQLRowCount**. Esattamente ciò che rappresenta il conteggio delle righe è indicato dall'impostazione dell'opzione SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 o SQL_STATIC_CURSOR_ATTRIBUTES2 (a seconda del tipo di cursore) restituito da una chiamata a **SQLGetInfo**. Questa maschera di bit indica per ogni tipo di cursore che specifica se il numero di righe restituito è esatto e approssimativo, o non è disponibile in tutti. Se i conteggi delle righe per statico o gestito da keyset dei cursori sono interessati dalle modifiche apportate attraverso **SQLBulkOperations** oppure **SQLSetPos**, o per gli aggiornamenti posizionati o le istruzioni delete, dipende da altri bit restituiti dagli stessi argomenti opzione elencati in precedenza. Per altre informazioni, vedere la [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrizione della funzione.
