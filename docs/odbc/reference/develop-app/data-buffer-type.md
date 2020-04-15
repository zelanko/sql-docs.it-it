---
title: 'Tipo di buffer di dati : Documenti Microsoft'
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305247"
---
# <a name="data-buffer-type"></a>Tipo di buffer di dati
Il tipo di dati C di un buffer viene specificato dall'applicazione. Con una singola variabile, ciò si verifica quando l'applicazione alloca la variabile. Con la memoria generica, ovvero la memoria a cui punta un puntatore di tipo void, ciò si verifica quando l'applicazione esegue il cast della memoria a un determinato tipo. Il driver rileva questo tipo in due modi:  
  
-   **Argomento di tipo buffer di dati.** I buffer utilizzati per trasferire i valori dei parametri e i dati del set di risultati, ad esempio il buffer associato a *TargetValuePtr* in **SQLBindCol**, dispongono in genere di un argomento di tipo associato, ad esempio l'argomento *TargetType* in **SQLBindCol**. In questo argomento, l'applicazione passa l'identificatore di tipo C che corrisponde al tipo del buffer. Ad esempio, nella seguente chiamata a **SQLBindCol**, il valore SQL_C_TYPE_DATE indica al driver che il buffer *di data* è un SQL_DATE_STRUCT:  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     Per ulteriori informazioni sugli identificatori di tipo, vedere la sezione [Tipi di dati in ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md) più avanti in questa sezione.  
  
-   **Tipo predefinito.** I buffer utilizzati per inviare e recuperare opzioni o attributi, ad esempio il buffer a cui punta l'argomento *InfoValuePtr* in **SQLGetInfo**, hanno un tipo fisso che dipende dall'opzione specificata. Il driver presuppone che il buffer di dati è di questo tipo. è responsabilità dell'applicazione allocare un buffer di questo tipo. Ad esempio, nella seguente chiamata a **SQLGetInfo**, il driver presuppone che il buffer sia un numero intero a 32 bit perché questo è ciò che richiede l'opzione SQL_STRING_FUNCTIONS:  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 Il driver utilizza il tipo di dati C per interpretare i dati nel buffer.
