---
title: Eseguire l'override di precisione in secondi e leader per i tipi di dati di intervallo | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fdab9e6e60311aca4ce0ae35f92e38c45fdf3702
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63018476"
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>Override della precisione iniziale e in secondi predefinita per i tipi di dati intervallo
Quando il campo SQL_DESC_TYPE di un ARD è impostato su un tipo C datetime o intervallo, tramite la chiamata a **SQLBindCol** oppure **SQLSetDescField**, il campo SQL_DESC_PRECISION (che contiene l'intervallo (secondi) la precisione) è impostata per i valori predefiniti seguenti:  
  
-   6 per timestamp e tutti i tipi di dati di intervallo con un componente relativo ai secondi.  
  
-   0 per tutti gli altri tipi di dati.  
  
 Per tutti i tipi di dati di intervallo, il campo di descrizione SQL_DESC_DATETIME_INTERVAL_PRECISION, che contiene la precisione di campo intervallo iniziale, è impostato su un valore predefinito di 2.  
  
 Quando il campo SQL_DESC_TYPE in un APD è impostato su un tipo C datetime o intervallo, tramite la chiamata a **SQLBindParameter** oppure **SQLSetDescField**, di SQL_DESC_PRECISION e SQL_DESC_DATETIME_INTERVAL_ Campi di precisione in APD vengono impostati sul valore predefinito specificato in precedenza. Questo vale per i parametri di input ma non per i parametri di input/output o di output.  
  
 Una chiamata a **SQLSetDescRec** imposta l'intervallo di precisione iniziale per l'impostazione predefinita, ma imposta la precisione dei secondi di intervallo (nel campo SQL_DESC_PRECISION) il valore della relativa *precisione* argomento.  
  
 Se uno dei valori predefiniti assegnati in precedenza non è accettabile a un'applicazione, l'applicazione deve impostare il campo SQL_DESC_PRECISION o SQL_DESC_DATETIME_INTERVAL_PRECISION chiamando **SQLSetDescField**.  
  
 Se l'applicazione chiama **SQLGetData** per restituire i dati in un valore datetime o intervallo di tipo C, vengono utilizzate la precisione iniziale intervallo predefinita e precisione dei secondi di intervallo. Se l'impostazione predefinita non è accettabile, l'applicazione deve chiamare **SQLSetDescField** per impostare dei campi del descrittore, o **SQLSetDescRec** impostare SQL_DESC_PRECISION. La chiamata a **SQLGetData** deve avere una *TargetType* di SQL_ARD_TYPE per utilizzare i valori nei campi del descrittore.  
  
 Quando **SQLPutData** viene chiamato, l'intervallo iniziale intervallo e precisione secondi precisione vengono letti dai campi dei record del descrittore che corrispondono al parametro data-at-execution o della colonna, ovvero APD campi per le chiamate per **SQLExecute** oppure **SQLExecDirect**, o ARD campi per le chiamate a **SQLBulkOperations** oppure **SQLSetPos**.
