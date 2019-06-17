---
title: Determinazione della funzionalità del cursore | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 716471786400c030febb62ebf41c8422770a8c09
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62744385"
---
# <a name="determining-cursor-capabilities"></a>Determinazione delle funzionalità del cursore
Le quattro opzioni seguenti in **SQLGetInfo** descrivono i tipi di cursori supportati e quali sono le relative funzionalità:  
  
-   SQL_CURSOR_SENSITIVITY. Indica se un cursore è sensibile alle modifiche apportate da un altro cursore.  
  
-   SQL_SCROLL_OPTIONS. Elenca i tipi di cursore supportato (forward-only, statici, gestito da keyset, dinamici o misti). Tutte le origini dati devono supportare i cursori forward-only.  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 (a seconda del tipo di cursore). Elenca i tipi di istruzione fetch supportati dai cursori scorrevoli. I bit nel valore restituito corrispondono ai tipi di operazione di recupero nella **SQLFetchScroll**.  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 o SQL_STATIC_CURSOR_ATTRIBUTES2 (a seconda del tipo di cursore). Indica se i cursori statici e gestito da keyset possono rilevare i propri aggiornamenti, eliminazioni e inserimenti.  
  
 Un'applicazione può determinare le funzionalità di cursore in fase di esecuzione chiamando **SQLGetInfo** con queste opzioni. Questa operazione viene eseguita in genere da applicazioni generiche. Funzionalità del cursore inoltre può essere determinata durante lo sviluppo di applicazioni e il relativo utilizzo hardcoded nell'applicazione. Questa viene eseguita in genere da applicazioni personalizzate e verticale, ma è anche possibile da applicazioni generiche che usano un'implementazione di cursore lato client, ad esempio la libreria di cursori ODBC.
