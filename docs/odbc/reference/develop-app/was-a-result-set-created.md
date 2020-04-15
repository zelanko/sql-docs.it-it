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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c171a154dd16a291c5dbe1dcade8c01ea95fb084
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294549"
---
# <a name="was-a-result-set-created"></a>Verifica della creazione di un set di risultati
Nella maggior parte dei casi, i programmatori di applicazioni sanno se le istruzioni eseguite dall'applicazione creeranno un set di risultati. Questo è il caso se l'applicazione utilizza istruzioni SQL hardcoded scritte dal programmatore. In genere è il caso quando l'applicazione costruisce istruzioni SQL in fase di esecuzione: il programmatore può facilmente includere il codice che contrassegna se un'istruzione **SELECT** o **un'istruzione INSERT** viene costruita. In alcune situazioni, il programmatore non è in grado di sapere se un'istruzione creerà un set di risultati. Questo è vero se l'applicazione fornisce un modo per l'utente di immettere ed eseguire un'istruzione SQL. È anche vero quando l'applicazione costruisce un'istruzione in fase di esecuzione per eseguire una routine.  
  
 In questi casi, l'applicazione chiama **SQLNumResultCols** per determinare il numero di colonne nel set di risultati. Se è 0, l'istruzione non ha creato un set di risultati; se si tratta di qualsiasi altro numero, l'istruzione ha creato un set di risultati.  
  
 L'applicazione può chiamare **SQLNumResultCols** in qualsiasi momento dopo la preparazione o l'esecuzione dell'istruzione. Tuttavia, poiché alcune origini dati non possono descrivere facilmente i set di risultati che verranno creati da istruzioni preparate, le prestazioni risentiranno se **SQLNumResultCols** viene chiamato dopo la preparazione di un'istruzione ma prima dell'esecuzione.  
  
 Alcune origini dati supportano anche la determinazione del numero di righe restituite da un'istruzione SQL in un set di risultati. A tale scopo, l'applicazione chiama **SQLRowCount**. Ciò che rappresenta il conteggio delle righe è indicato dall'impostazione dell'opzione SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 o SQL_STATIC_CURSOR_ATTRIBUTES2 (a seconda del tipo di cursore) restituito da una chiamata a **SQLGetInfo**. Questa maschera di bit indica per ogni tipo di cursore se il conteggio delle righe restituito è esatto, approssimativo o non è disponibile affatto. Se i conteggi delle righe per i cursori statici o basati su keyset sono influenzati dalle modifiche apportate tramite **SQLBulkOperations** o **SQLSetPos**o dalle istruzioni di aggiornamento o eliminazione posizionate, dipende da altri bit restituiti dagli stessi argomenti di opzione elencati in precedenza. Per altre informazioni, vedere la descrizione della funzione [SQLGetInfo.For](../../../odbc/reference/syntax/sqlgetinfo-function.md) more information, see the SQLGetInfo function description.
