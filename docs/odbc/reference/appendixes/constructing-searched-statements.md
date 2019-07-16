---
title: Costruzione di istruzioni di ricerca | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- searched statements [ODBC]
- ODBC cursor library [ODBC], statement processing
- ODBC cursor library [ODBC], searched statements
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
- cursor library [ODBC], searched statements
- SQL statements [ODBC], searched statements
ms.assetid: e429254c-c43f-4fbf-98b2-5f1ed53501ff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c8f24fe59da1377ea42900a8f1f0b89eb97125f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019176"
---
# <a name="constructing-searched-statements"></a>Costruzione di istruzioni di ricerca
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 Per supportare l'aggiornamento posizionato ed eliminare le istruzioni, costruisce un'avanzata libreria di cursori **aggiornare** oppure **eliminare** istruzione dall'istruzione posizionato. Per supportare le chiamate a **SQLGetData** in un blocco di dati, costruisce un'avanzata libreria di cursori **seleziona** creare un risultato dell'istruzione set che contiene la riga corrente di dati. In ognuna di queste istruzioni, il **in cui** clausola enumera i valori memorizzati nella cache per ogni colonna associata che restituisce SQL_PRED_SEARCHABLE o SQL_PRED_BASIC per l'identificatore di campo SQL_DESC_SEARCHABLE in  **SQLColAttribute**.  
  
> [!CAUTION]  
>  Il **in cui** clausola costruito dalla libreria di cursori per identificare la riga corrente può non riuscire a identificare tutte le righe, identificare una riga diversa o per identificare più di una riga.  
  
 Se un'istruzione delete o un aggiornamento posizionato interessa più righe, la libreria di cursori Aggiorna la matrice di stato di riga solo per la riga in cui è posizionato il cursore e vengono restituiti SQL_SUCCESS_WITH_INFO e SQLSTATE 01001 (conflitto dell'operazione del cursore). Se l'istruzione non identifica tutte le righe, la libreria di cursori non aggiorna la matrice di stato di riga e restituisce SQL_SUCCESS_WITH_INFO e SQLSTATE 01001 (conflitto dell'operazione del cursore). Un'applicazione può chiamare **SQLRowCount** per determinare il numero di righe che sono stati aggiornati o eliminati.  
  
 Se il **selezionate** clausola consente di posizionare il cursore per una chiamata a **SQLGetData** identifica più di una riga, **SQLGetData** non garantisce la restituzione di dati corretto. Se tutte le righe, non identifica **SQLGetData** restituisce SQL_NO_DATA.  
  
 Se un'applicazione è conforme alle linee guida seguenti, il **in cui** clausola costruito dalla libreria di cursori deve identificare in modo univoco la riga corrente, tranne quando è impossibile, ad esempio quando l'origine dati contiene duplicato righe.  
  
-   **Associare le colonne che identificano in modo univoco la riga.** Se le colonne associate identifica in modo univoco la riga, il **in cui** clausola costruito dalla libreria di cursori potrebbe identificare più di una riga. In un'istruzione delete o update posizionata, questa clausola può causare più di una riga deve essere aggiornato o eliminato. In una chiamata a **SQLGetData**, questa clausola può causare il driver restituire i dati per la riga non corretto. Associazione di tutte le colonne in una chiave univoca garantisce che ogni riga viene identificata.  
  
-   **Allocare buffer di dati sufficientemente grande che si verifica nessun troncamento.** Cache della libreria di cursori è una copia dei valori nei buffer di set di righe associato al set di risultati **SQLBindCol**. Se i dati vengono troncati quando è inserito in questi buffer, esso verrà troncato anche nella cache. Oggetto **in cui** clausola costruito dai valori troncati potrebbe non identificare correttamente la riga sottostante nell'origine dati.  
  
-   **Specificare i buffer di lunghezza non null per i dati binari di C.** La libreria di cursori alloca i buffer di lunghezza nella relativa cache solo se il *StrLen_or_IndPtr* nell'argomento **SQLBindCol** è diverso da null. Quando la *TargetType* l'argomento è SQL_C_BINARY, la libreria di cursori richiede la lunghezza dei dati binari per costruire un **in cui** clausola dai dati. Se non vi è alcun buffer di lunghezza per una colonna SQL_C_BINARY e l'applicazione chiama **SQLGetData** o tenta di eseguire un aggiornamento posizionato o delete-istruzione, la restituisce libreria cursore SQL_ERROR e SQLSTATE SL014 (un oggetto posizionato richiesta è stata rilasciata e non tutti i campi numero di colonna sono stati memorizzati nel buffer).  
  
-   **Specificare i buffer di lunghezza non null per le colonne nullable.** La libreria di cursori alloca i buffer di lunghezza nella relativa cache solo se il *StrLen_or_IndPtr* nell'argomento **SQLBindCol** è diverso da null. Poiché SQL_NULL_DATA viene memorizzato nel buffer di lunghezza, la libreria di cursori si presuppone che qualsiasi colonna per la cui lunghezza non è specificato il buffer è non nullable. Se nessuna colonna di lunghezza per una colonna che ammette valori null, la libreria di cursori restituisce un **in cui** clausola che utilizza il valore dei dati per la colonna. Questa clausola non identificherà correttamente la riga.
