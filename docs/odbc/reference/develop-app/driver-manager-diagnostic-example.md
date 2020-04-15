---
title: Esempio di diagnostica di Gestione driver - Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 839095e5544cab73cdddd4f4b17a3d8d52136c9c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305812"
---
# <a name="driver-manager-diagnostic-example"></a>Esempio di diagnostica di Gestione driver
Gestione Driver può anche generare messaggi di diagnostica. Ad esempio, se un'applicazione ha passato un'opzione di direzione non valida a **SQLDataSources**, Gestione Driver potrebbe formattare e restituire i seguenti valori da **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 Poiché l'errore si è verificato in Gestione Driver, ha aggiunto prefissi al messaggio di diagnostica per il relativo fornitore ([Microsoft]) e il relativo identificatore ([Gestione driver ODBC]).
