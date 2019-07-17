---
title: SQLGetData (libreria di cursori) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Cursor Library
ms.assetid: ff40c9c0-b847-4426-a099-1bff47e6e872
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5962882de08712dcff75790de7c58d69f965a3bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086378"
---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 In questo argomento viene illustrato l'utilizzo dei **SQLGetData** funzione nella libreria di cursori. Per informazioni generali sul **SQLGetData**, vedere [funzione SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).  
  
 La libreria di cursori implementa **SQLGetData** costruendo prima un **seleziona** istruzione con una **dove** clausola che enumera i valori memorizzati nella cache per ogni limite colonna nella riga corrente. Ed esegue la **selezionate** istruzione per selezionare nuovamente la riga e chiama **SQLGetData** nel driver per recuperare i dati dall'origine dati (anziché la cache).  
  
> [!CAUTION]  
>  Il **in cui** clausola costruito dalla libreria di cursori per identificare la riga corrente può non riuscire a identificare tutte le righe, identificare una riga diversa o per identificare più di una riga. Per altre informazioni, vedere [costruzione di istruzioni di eseguire la ricerca](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Se l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS è impostata su, SQL_UB_VARIABLE **SQLGetData** può essere chiamato sulla colonna 0 per restituire i dati di segnalibro.  
  
 Le chiamate a **SQLGetData** sono soggetti alle restrizioni seguenti:  
  
-   **SQLGetData** non può essere chiamato per i cursori forward-only.  
  
-   **SQLGetData** può essere chiamato solo quando vengono soddisfatte le condizioni seguenti: una **seleziona** istruzione ha generato il set di risultati; il **seleziona** istruzione non contiene un join, un  **UNION** clausola, o un **GROUP BY** clausola; e tutte le colonne utilizzate di un'espressione o un alias nell'elenco di selezione non sono associate con **SQLBindCol**.  
  
-   Se il driver supporta solo un'istruzione attiva, la libreria di cursori recupera il resto del gruppo di risultati prima di eseguire la **selezionate** istruzione e chiamando il metodo **SQLGetData**.
