---
description: Tipo di buffer di dati
title: Tipo di buffer di dati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], buffers
- data buffers [ODBC], types
- buffers [ODBC], data
- C data types [ODBC], buffers
ms.assetid: 58bea3e9-d552-447f-b3ad-ce1dab213b72
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a1a3edf66a8f3684fdf8389d16c08f62682907ca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429353"
---
# <a name="data-buffer-type"></a>Tipo di buffer di dati
Il tipo di dati C di un buffer viene specificato dall'applicazione. Con una singola variabile, questo errore si verifica quando l'applicazione alloca la variabile. Con la memoria generica, ovvero la memoria a cui punta un puntatore di tipo void, questo errore si verifica quando l'applicazione esegue il cast della memoria a un particolare tipo. Il driver individua questo tipo in due modi:  
  
-   **Argomento tipo di buffer di dati.** I buffer usati per trasferire i valori di parametro e i dati del set di risultati, ad esempio il buffer associato con *TargetValuePtr* in **SQLBindCol**, in genere hanno un argomento di tipo associato, ad esempio l'argomento *targetType* in **SQLBindCol**. In questo argomento, l'applicazione passa l'identificatore del tipo C che corrisponde al tipo di buffer. Ad esempio, nella chiamata seguente a **SQLBindCol**, il valore SQL_C_TYPE_DATE indica al driver che il buffer di *data* è un SQL_DATE_STRUCT:  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     Per ulteriori informazioni sugli identificatori di tipo, vedere la sezione [tipi di dati in ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md) più avanti in questa sezione.  
  
-   **Tipo predefinito.** I buffer usati per inviare e recuperare opzioni o attributi, ad esempio il buffer a cui punta l'argomento *InfoValuePtr* in **SQLGetInfo**, hanno un tipo fisso che dipende dall'opzione specificata. Il driver presuppone che il buffer di dati sia di questo tipo. è responsabilità dell'applicazione allocare un buffer di questo tipo. Ad esempio, nella chiamata seguente a **SQLGetInfo**, il driver presuppone che il buffer sia un valore integer a 32 bit, perché questa è l'opzione SQL_STRING_FUNCTIONS richiesta:  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 Il driver usa il tipo di dati C per interpretare i dati nel buffer.
