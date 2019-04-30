---
title: Override della precisione predefinita e la scalabilità per tipi di dati numerici | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f071cf4391c760f7d269382537c3cd4f2b758c3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278304"
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>Override della precisione predefinita e della scala per i tipi di dati numerici
Quando il campo SQL_DESC_TYPE in un ARD è impostato per SQL_C_NUMERIC, tramite la chiamata a **SQLBindCol** oppure **SQLSetDescField**, il campo SQL_DESC_SCALE il ARD è impostato su 0 e viene impostato il campo SQL_DESC_PRECISION per una precisione predefinito definito dal driver. Questo vale anche quando il campo SQL_DESC_TYPE in un APD è impostato su SQL_C_NUMERIC, tramite la chiamata a **SQLBindParameter** oppure **SQLSetDescField**. Questo vale per l'input, input/output o i parametri di output.  
  
 Se uno dei valori predefiniti descritti in precedenza non sono accettabile per un'applicazione, l'applicazione deve impostare il campo SQL_DESC_PRECISION o SQL_DESC_SCALE chiamando **SQLSetDescField** o **SQLSetDescRec**.  
  
 Se l'applicazione chiama **SQLGetData** per restituire i dati in una struttura SQL_C_NUMERIC, vengono usati i campi SQL_DESC_PRECISION e SQL_DESC_SCALE predefiniti. Se le impostazioni predefinite non sono accettabili, l'applicazione deve chiamare **SQLSetDescRec** oppure **SQLSetDescField** per impostare i campi e quindi chiamare **SQLGetData** con un *TargetType* di SQL_ARD_TYPE per utilizzare i valori nei campi del descrittore.  
  
 Quando **SQLPutData** viene chiamato, la chiamata Usa i campi SQL_DESC_SCALE e SQL_DESC_PRECISION di record del descrittore che corrisponde al parametro data-at-execution o della colonna, che sono campi APD per le chiamate a  **SQLExecute** oppure **SQLExecDirect**, o ARD campi per le chiamate ai **SQLBulkOperations** oppure **SQLSetPos**.
