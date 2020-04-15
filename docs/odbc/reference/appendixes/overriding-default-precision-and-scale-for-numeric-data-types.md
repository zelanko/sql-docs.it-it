---
title: Override di precisione e scala predefiniti per i tipi di dati numerici Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], precision and scale
- precision [ODBC], numeric data types
- data types [ODBC], numeric data types
- numeric data type [ODBC]
- numeric literals [ODBC]
ms.assetid: 84292334-0e33-4a1b-84de-8c018dd787f3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 365c5f69d21dd3a4ad8e89805d81f1b3b0c9dcba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303592"
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>Override della precisione predefinita e della scala per i tipi di dati numerici
Quando il campo SQL_DESC_TYPE in un ARD è impostato su SQL_C_NUMERIC, chiamando **SQLBindCol** o **SQLSetDescField**, il campo SQL_DESC_SCALE nell'ARD è impostato su 0 e il campo SQL_DESC_PRECISION è impostato su una precisione predefinita definita dal driver. Ciò è vero anche quando il campo SQL_DESC_TYPE in un aPD è impostato su SQL_C_NUMERIC, chiamando **SQLBindParameter** o **SQLSetDescField**. Questo è vero per i parametri di input, input/output o output.  
  
 Se una delle impostazioni predefinite descritte in precedenza non è accettabile per un'applicazione, l'applicazione deve impostare il campo SQL_DESC_SCALE o SQL_DESC_PRECISION chiamando **SQLSetDescField** o **SQLSetDescRec**.  
  
 Se l'applicazione chiama **SQLGetData** per restituire i dati in una struttura SQL_C_NUMERIC, vengono utilizzati i campi SQL_DESC_SCALE e SQL_DESC_PRECISION predefiniti. Se i valori predefiniti non sono accettabili, l'applicazione deve chiamare **SQLSetDescRec** o **SQLSetDescField** per impostare i campi e quindi chiamare **SQLGetData** con un *TargetType* di SQL_ARD_TYPE per utilizzare i valori nei campi del descrittore.  
  
 Quando **SQLPutData** viene chiamato, la chiamata utilizza i campi SQL_DESC_SCALE e SQL_DESC_PRECISION del record del descrittore che corrisponde al parametro o alla colonna data-at-execution, ovvero campi APD per le chiamate a **SQLExecute** o **SQLExecDirect**, o ARD per le chiamate a **SQLBulkOperations** o **SQLSetPos**.
