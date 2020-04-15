---
title: Eseguire l'override della precisione iniziale e dei secondi per i tipi di dati intervallo Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: 3d65493f-dce7-4d29-9f59-c63a4e47918c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1e60d5d8fc696ad8e2bd4cfb0c082ff214e066d0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303602"
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>Override della precisione iniziale e in secondi predefinita per i tipi di dati intervallo
Quando il campo SQL_DESC_TYPE di un ARD è impostato su un tipo datetime o intervallo C, chiamando **SQLBindCol** o **SQLSetDescField**, il campo SQL_DESC_PRECISION (che contiene la precisione dei secondi dell'intervallo) viene impostato sui seguenti valori predefiniti:  
  
-   6 per timestamp e tutti i tipi di dati intervallo con un secondo componente.  
  
-   0 per tutti gli altri tipi di dati.  
  
 Per tutti i tipi di dati intervallo, il campo descrittore SQL_DESC_DATETIME_INTERVAL_PRECISION, che contiene la precisione del campo iniziale dell'intervallo, è impostato su un valore predefinito pari a 2.  
  
 Quando il campo SQL_DESC_TYPE in un aPD è impostato su un tipo datetime o intervallo C, chiamando **SQLBindParameter** o **SQLSetDescField**, i campi SQL_DESC_PRECISION e SQL_DESC_DATETIME_INTERVAL_PRECISION in APD vengono impostati sul valore predefinito specificato in precedenza. Questo è vero per i parametri di input, ma non per i parametri di input/output o di output.  
  
 Una chiamata a **SQLSetDescRec** imposta la precisione di interlinea dell'intervallo sul valore predefinito, ma imposta la precisione dei secondi dell'intervallo (nel campo SQL_DESC_PRECISION) sul valore del relativo argomento *Precision.*  
  
 Se uno dei valori predefiniti specificato in precedenza non è accettabile per un'applicazione, l'applicazione deve impostare il campo SQL_DESC_PRECISION o SQL_DESC_DATETIME_INTERVAL_PRECISION chiamando **SQLSetDescField**.  
  
 Se l'applicazione chiama **SQLGetData** per restituire dati in un tipo datetime o intervallo C, vengono utilizzate la precisione di intervallo iniziale predefinita e la precisione dei secondi di intervallo. Se l'impostazione predefinita non è accettabile, l'applicazione deve chiamare **SQLSetDescField** per impostare il campo del descrittore o **SQLSetDescRec** per impostare SQL_DESC_PRECISION. La chiamata a **SQLGetData** deve avere un *TargetType* di SQL_ARD_TYPE per utilizzare i valori nei campi del descrittore.  
  
 Quando **SQLPutData** viene chiamato, la precisione interlinea dell'intervallo e la precisione dei secondi di intervallo vengono lette dai campi del record del descrittore che corrispondono al parametro o alla colonna data-at-execution, ovvero campi APD per le chiamate **aSQLExecute** o **SQLExecDirect**o ai campi ARD per le chiamate a **SQLBulkOperations** o **SQLSetPos**.
