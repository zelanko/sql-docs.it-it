---
title: Determinazione delle funzionalità del cursore . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], capabilities
- cursors [ODBC], scrollable
ms.assetid: 35be486c-8f2d-4cec-beb8-df14151abfef
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 984ad8302f2e1695c8df84a64a18042f4cc9e364
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305882"
---
# <a name="determining-cursor-capabilities"></a>Determinazione delle funzionalità del cursore
Le quattro opzioni seguenti in **SQLGetInfo** descrivono quali tipi di cursori sono supportati e quali sono le relative funzionalità:  
  
-   SQL_CURSOR_SENSITIVITY. Indica se un cursore è sensibile alle modifiche apportate da un altro cursore.  
  
-   SQL_SCROLL_OPTIONS. Elenca i tipi di cursore supportati (forward-only, static, keyset-driven, dynamic o mixed). Tutte le origini dati devono supportare i cursori forward-only.  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 (a seconda del tipo di cursore). Elenca i tipi di recupero supportati dai cursori scorrevoli. I bit nel valore restituito corrispondono ai tipi di recupero in **SQLFetchScroll**.  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 o SQL_STATIC_CURSOR_ATTRIBUTES2 (a seconda del tipo di cursore). Indica se i cursori statici e basati su keyset possono rilevare i propri aggiornamenti, eliminazioni e inserimenti.  
  
 Un'applicazione può determinare le funzionalità del cursore in fase di esecuzione chiamando **SQLGetInfo** con queste opzioni. Questa operazione viene in genere eseguita da applicazioni generiche. Le funzionalità del cursore possono essere determinate anche durante lo sviluppo dell'applicazione e il loro utilizzo hardcoded nell'applicazione. Questa operazione viene in genere eseguita da applicazioni verticali e personalizzate, ma può essere eseguita anche da applicazioni generiche che utilizzano un'implementazione del cursore sul lato client, ad esempio la libreria di cursori ODBC.
