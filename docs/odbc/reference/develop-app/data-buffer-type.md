---
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
ms.openlocfilehash: 9b98ed2ab0865b98884f6dfa1ff20142540ff314
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305247"
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
