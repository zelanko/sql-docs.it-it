---
title: Tipo del Buffer di dati | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 615625ca396e5f2ae094962457cc9e746730ddcf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067407"
---
# <a name="data-buffer-type"></a>Tipo di buffer di dati
Il tipo di dati C di un buffer specificato dall'applicazione. Con una singola variabile, ciò si verifica quando l'applicazione alloca la variabile. Con generici per la memoria - vale a dire memoria a cui punta un puntatore di tipo void - ciò avviene quando l'applicazione viene eseguito il cast della memoria per un particolare tipo. Il driver individua questo tipo in due modi:  
  
-   **Argomento di tipo buffer di dati.** Buffer utilizzato per trasferire i valori dei parametri e dati del set di risultati, ad esempio il buffer associato a *TargetValuePtr* nelle **SQLBindCol**, in genere presente un argomento di tipo associato, ad esempio il  *TargetType* nell'argomento **SQLBindCol**. In questo argomento, l'applicazione passa l'identificatore di tipo C che corrisponde al tipo di buffer. Ad esempio, nella chiamata seguente a **SQLBindCol**, il valore SQL_C_TYPE_DATE indica al driver che la *data* buffer è un valore SQL_DATE_STRUCT:  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     Per altre informazioni sugli identificatori di tipo, vedere la [tipi di dati in ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md) più avanti in questa sezione.  
  
-   **Tipo predefinito.** Buffer usato per inviare e recuperare le opzioni o attributi, ad esempio il buffer a cui fa riferimento il *InfoValuePtr* nell'argomento **SQLGetInfo**, dispone di un tipo predefinito che dipende dall'opzione specificata. Il driver presuppone che il buffer dei dati di questo tipo. è responsabilità dell'applicazione per allocare un buffer di questo tipo. Ad esempio, nella chiamata seguente a **SQLGetInfo**, il driver presuppone che il buffer è un integer a 32 bit perché questo è ciò che l'opzione SQL_STRING_FUNCTIONS richiede:  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 Il driver Usa il tipo di dati C per interpretare i dati nel buffer.
