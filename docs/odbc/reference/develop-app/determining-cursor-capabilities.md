---
title: Determinazione delle funzionalità del cursore | Microsoft Docs
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
ms.openlocfilehash: 14715e40cd99f3f1a03c2ae19e825705a8376e30
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68040001"
---
# <a name="determining-cursor-capabilities"></a>Determinazione delle funzionalità del cursore
Le quattro opzioni seguenti in **SQLGetInfo** descrivono quali tipi di cursori sono supportati e quali sono le rispettive funzionalità:  
  
-   SQL_CURSOR_SENSITIVITY. Indica se un cursore è sensibile alle modifiche apportate da un altro cursore.  
  
-   SQL_SCROLL_OPTIONS. Vengono elencati i tipi di cursore supportati (di tipo "solo", statico, gestito da keyset, dinamico o misto). Tutte le origini dati devono supportare i cursori di sola trasmissione.  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 (a seconda del tipo di cursore). Elenca i tipi di recupero supportati dai cursori scorrevoli. I bit nel valore restituito corrispondono ai tipi di recupero in **SQLFetchScroll**.  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 o SQL_STATIC_CURSOR_ATTRIBUTES2 (a seconda del tipo di cursore). Indica se i cursori statici e gestiti da keyset possono rilevare gli aggiornamenti, le eliminazioni e gli inserimenti.  
  
 Un'applicazione può determinare le funzionalità del cursore in fase di esecuzione chiamando **SQLGetInfo** con queste opzioni. Questa operazione viene eseguita comunemente dalle applicazioni generiche. Le funzionalità del cursore possono essere determinate anche durante lo sviluppo di applicazioni e il loro utilizzo hardcoded nell'applicazione. Questa operazione viene in genere eseguita da applicazioni verticali e personalizzate, ma può essere eseguita anche da applicazioni generiche che usano un'implementazione del cursore sul lato client, ad esempio la libreria di cursori ODBC.
