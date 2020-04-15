---
title: SQLGetData (libreria di cursori) Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07200d48f439c97003da7062fc218cd2f3081d1b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307842"
---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo della funzione **SQLGetData** nella libreria di cursori. Per informazioni generali su **SQLGetData**, vedere [Funzione SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).  
  
 La libreria di cursori implementa **SQLGetData** creando innanzitutto un'istruzione **SELECT** con una clausola **WHERE** che enumera i valori archiviati nella cache per ogni colonna associata nella riga corrente. Viene quindi eseguita l'istruzione **SELECT** per riselezionare la riga e viene chiamato **SQLGetData** nel driver per recuperare i dati dall'origine dati (anziché dalla cache).  
  
> [!CAUTION]  
>  La clausola **WHERE** costruita dalla libreria di cursori per identificare la riga corrente può non riuscire a identificare righe, identificare una riga diversa o identificare più di una riga. Per ulteriori informazioni, vedere [Creazione di istruzioni ricercate](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Se l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS è impostato su SQL_UB_VARIABLE, **SQLGetData** può essere chiamato sulla colonna 0 per restituire i dati del segnalibro.  
  
 Le chiamate a SQLGetData sono soggette alle restrizioni seguenti:Calls to **SQLGetData** are subject to the following restrictions:  
  
-   **Impossibile chiamare SQLGetData** per i cursori forward-only.  
  
-   **SQLGetData** può essere chiamato solo quando vengono soddisfatte le condizioni seguenti: un'istruzione **SELECT** ha generato il set di risultati. l'istruzione **SELECT** non contiene un join, una clausola **UNION** o una clausola **GROUP BY.** e tutte le colonne che utilizzavano un alias o un'espressione nell'elenco di selezione non erano associate a **SQLBindCol**.  
  
-   Se il driver supporta una sola istruzione attiva, la libreria di cursori recupera il resto del set di risultati prima di eseguire l'istruzione **SELECT** e chiamare **SQLGetData**.
