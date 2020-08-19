---
description: Esempio di diagnostica di Gestione driver
title: Esempio di diagnostica di gestione driver | Microsoft Docs
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
ms.openlocfilehash: b1d852436600ffb3ce5258e731d23c4579bf8964
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483064"
---
# <a name="driver-manager-diagnostic-example"></a>Esempio di diagnostica di Gestione driver
Gestione driver può inoltre generare messaggi di diagnostica. Se, ad esempio, un'applicazione ha passato un'opzione di direzione non valida a **SQLDataSources**, gestione driver potrebbe formattare e restituire i valori seguenti da **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 Poiché l'errore si è verificato in Gestione driver, i prefissi sono stati aggiunti al messaggio di diagnostica per il fornitore ([Microsoft]) e al relativo identificatore ([Gestione driver ODBC]).
