---
title: Costruzione di istruzioni ricercate Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8b9a27aa9fc84aadc6659993de3e12e269631d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284741"
---
# <a name="constructing-searched-statements"></a>Costruzione di istruzioni di ricerca
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 Per supportare le istruzioni di aggiornamento ed eliminazione posizionate, la libreria di cursori crea un'istruzione **UPDATE** o **DELETE** cercata dall'istruzione posizionata. Per supportare le chiamate a **SQLGetData** in un blocco di dati, la libreria di cursori crea un'istruzione **SELECT** ricercata per creare un set di risultati contenente la riga di dati corrente. In ognuna di queste istruzioni, la clausola **WHERE** enumera i valori archiviati nella cache per ogni colonna associata che restituisce SQL_PRED_SEARCHABLE o SQL_PRED_BASIC per l'identificatore di campo SQL_DESC_SEARCHABLE in **SQLColAttribute**.  
  
> [!CAUTION]  
>  La clausola **WHERE** costruita dalla libreria di cursori per identificare la riga corrente può non riuscire a identificare righe, identificare una riga diversa o identificare più di una riga.  
  
 Se un'istruzione update o delete posizionata ha effetto su più righe, la libreria di cursori aggiorna la matrice di stato della riga solo per la riga in cui è posizionato il cursore e restituisce SQL_SUCCESS_WITH_INFO e SQLSTATE 01001 (conflitto di operazioni cursore). Se l'istruzione non identifica alcuna riga, la libreria di cursori non aggiorna la matrice di stato della riga e restituisce SQL_SUCCESS_WITH_INFO e SQLSTATE 01001 (conflitto di operazioni cursore). Un'applicazione può chiamare **SQLRowCount** per determinare il numero di righe che sono state aggiornate o eliminate.  
  
 Se la clausola **SELECT** utilizzata per posizionare il cursore per una chiamata a **SQLGetData** identifica più di una riga, non è garantito che **SQLGetData** restituisca i dati corretti. Se non identifica alcuna riga, **SQLGetData** restituisce SQL_NO_DATA.  
  
 Se un'applicazione è conforme alle linee guida seguenti, la clausola **WHERE** costruita dalla libreria di cursori deve identificare in modo univoco la riga corrente, tranne quando ciò è impossibile, ad esempio quando l'origine dati contiene righe duplicate.  
  
-   **Associare colonne che identificano in modo univoco la riga.** Se le colonne associate non identificano in modo univoco la riga, la clausola **WHERE** costruita dalla libreria di cursori potrebbe identificare più di una riga. In un'istruzione di aggiornamento o eliminazione posizionata, una clausola di questo tipo può causare l'aggiornamento o l'eliminazione di più righe. In una chiamata a **SQLGetData**, una clausola di questo tipo potrebbe causare la restituzione dei dati per la riga errata. L'associazione di tutte le colonne in una chiave univoca garantisce che ogni riga venga identificata in modo univoco.  
  
-   **Allocare buffer di dati sufficientemente grandi da non eseguire troncamenti.** La cache della libreria di cursori è una copia dei valori nei buffer del set di righe associati al set di risultati con **SQLBindCol**. Se i dati vengono troncati quando vengono inseriti in questi buffer, verranno troncati anche nella cache. Una clausola **WHERE** costruita da valori troncati potrebbe non identificare correttamente la riga sottostante nell'origine dati.  
  
-   **Specificare buffer di lunghezza non Null per i dati binari C.** La libreria di cursori alloca i buffer di lunghezza nella cache solo se l'argomento *StrLen_or_IndPtr* in **SQLBindCol** è diverso da null. Quando l'argomento *TargetType* è SQL_C_BINARY, la libreria di cursori richiede la lunghezza dei dati binari per costruire una clausola **WHERE** dai dati. Se non è presente alcun buffer di lunghezza per una colonna SQL_C_BINARY e l'applicazione chiama **SQLGetData** o tenta di eseguire un aggiornamento posizionato o eliminare istruzione, la libreria di cursori restituisce SQL_ERROR e SQLSTATE SL014 (è stata emessa una richiesta posizionata e non tutti i campi conteggio delle colonne sono stati memorizzati nel buffer).  
  
-   **Specificare buffer di lunghezza non Null per le colonne nullable.** La libreria di cursori alloca i buffer di lunghezza nella cache solo se l'argomento *StrLen_or_IndPtr* in **SQLBindCol** è diverso da null. Poiché SQL_NULL_DATA viene archiviata nel buffer di lunghezza, la libreria di cursori presuppone che qualsiasi colonna per cui non è specificato alcun buffer di lunghezza non è nullable. Se non viene specificata alcuna colonna di lunghezza per una colonna nullable, la libreria di cursori crea una clausola **WHERE** che utilizza il valore di dati per la colonna. Questa clausola non identificherà correttamente la riga.
