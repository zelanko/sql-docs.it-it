---
title: Esempio di diagnostica di Gestione driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], diagnostic messages
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: af8f2d35-d1bf-495c-af25-630654542b7d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6ad253c2d0603846d6d1f795f6115e7bb727b3da
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63238046"
---
# <a name="driver-manager-diagnostic-example"></a>Esempio di diagnostica di Gestione driver
Gestione Driver può anche generare messaggi di diagnostica. Ad esempio, se un'applicazione passata un'opzione direzione non valido per **SQLDataSources**, potrebbe essere formattare e restituire i valori seguenti da Gestione Driver **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 Perché si è verificato l'errore in Gestione Driver, aggiungere prefissi per il messaggio di diagnostica sul suo fornitore ([Microsoft]) e il relativo identificatore ([gestione Driver ODBC]).
