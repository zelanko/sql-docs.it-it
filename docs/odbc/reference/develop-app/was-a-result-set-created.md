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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81294549"
---
# <a name="was-a-result-set-created"></a>Verifica della creazione di un set di risultati
Nella maggior parte dei casi, i programmatori di applicazioni sanno se le istruzioni eseguite dall'applicazione creeranno un set di risultati. Questa situazione si verifica se l'applicazione usa istruzioni SQL hardcoded scritte dal programmatore. Si tratta in genere del caso in cui l'applicazione costruisce istruzioni SQL in fase di esecuzione: il programmatore può includere facilmente il codice che contrassegna se viene costruita un'istruzione **Select** o un'istruzione **Insert** . In alcune situazioni, il programmatore non può sapere se un'istruzione creerà un set di risultati. Questo vale se l'applicazione consente all'utente di immettere ed eseguire un'istruzione SQL. È anche vero quando l'applicazione crea un'istruzione in fase di esecuzione per eseguire una procedura.  
  
 In questi casi, l'applicazione chiama **SQLNumResultCols** per determinare il numero di colonne nel set di risultati. Se è 0, l'istruzione non ha creato un set di risultati. Se si tratta di un altro numero, l'istruzione ha creato un set di risultati.  
  
 L'applicazione può chiamare **SQLNumResultCols** in qualsiasi momento dopo che l'istruzione è stata preparata o eseguita. Tuttavia, poiché alcune origini dati non possono descrivere facilmente i set di risultati che verranno creati dalle istruzioni preparate, le prestazioni risulteranno ridotte se **SQLNumResultCols** viene chiamato dopo che un'istruzione viene preparata ma prima che venga eseguita.  
  
 Alcune origini dati supportano anche la determinazione del numero di righe restituite da un'istruzione SQL in un set di risultati. A tale scopo, l'applicazione chiama **SQLRowCount**. Il conteggio delle righe rappresenta esattamente l'impostazione dell'opzione SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 o SQL_STATIC_CURSOR_ATTRIBUTES2 (a seconda del tipo di cursore) restituito da una chiamata a **SQLGetInfo**. Questa maschera di maschera indica per ogni tipo di cursore se il conteggio delle righe restituito è esatto, approssimativo o non è disponibile. Il conteggio delle righe per i cursori statici o gestiti da keyset è influenzato dalle modifiche apportate tramite **SQLBulkOperations** o **SQLSetPos**o dalle istruzioni Update o DELETE posizionate, a seconda degli altri bit restituiti dagli stessi argomenti di opzione elencati in precedenza. Per ulteriori informazioni, vedere la descrizione della funzione [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) .
