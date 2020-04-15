---
title: 'Appendice D: Tipi di dati Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], defined
- SQL data types [ODBC], defined
- data types [ODBC]
- data types [ODBC], about data types
ms.assetid: 981d49c3-3531-4543-aa75-5bd9e4f67000
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c1abadb962e3a1ee9327bbb8d84e52d180b4a7e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292461"
---
# <a name="appendix-d-data-types"></a>Appendice D: Tipi di dati
ODBC definisce due set di tipi di dati: i tipi di dati SQL e i tipi di dati C. I tipi di dati SQL indicano il tipo di dati dei dati archiviati nell'origine dati. I tipi di dati C indicano il tipo di dati dei dati archiviati nei buffer dell'applicazione.  
  
 I tipi di dati SQL vengono definiti da ogni DBMS in conformità con lo standard SQL-92. Per ogni tipo di dati SQL specificato nello standard SQL-92, ODBC definisce un identificatore di tipo, ovvero un valore **di #define** che viene passato come argomento nelle funzioni ODBC o restituito nei metadati di un set di risultati. Gli unici tipi di dati SQL-92 non supportati da ODBC sono BIT (il tipo ODBC SQL_BIT ha caratteristiche diverse), BIT_VARYING, TIME_WITH_TIMEZONE, TIMESTAMP_WITH_TIMEZONE e NATIONAL_CHARACTER. I driver sono responsabili del mapping dei tipi di dati SQL specifici dell'origine dati agli identificatori dei tipi di dati SQL ODBC e agli identificatori dei tipi di dati SQL specifici del driver. Il tipo di dati SQL viene specificato nel campo SQL_DESC_CONCISE_TYPE di un descrittore di implementazione.  
  
 ODBC definisce i tipi di dati C e gli identificatori di tipo ODBC corrispondenti. Un'applicazione specifica il tipo di dati C del buffer che riceverà i dati del set di risultati passando l'identificatore di tipo C appropriato nell'argomento *TargetType* in una chiamata a **SQLBindCol** o **SQLGetData**. Specifica il tipo C del buffer contenente un parametro di istruzione passando l'identificatore di tipo C appropriato nell'argomento *ValueType* in una chiamata a **SQLBindParameter**. Il tipo di dati C è specificato nel campo SQL_DESC_CONCISE_TYPE di un descrittore dell'applicazione.  
  
> [!NOTE]  
>  Non sono presenti tipi di dati C specifici del driver.  
  
 Ogni tipo di dati SQL corrisponde a un tipo di dati C ODBC. Prima di restituire dati dall'origine dati, il driver li converte nel tipo di dati C specificato. Prima di inviare dati all'origine dati, il driver li converte dal tipo di dati C specificato.  
  
 Questa appendice contiene i seguenti argomenti.  
  
-   [Uso degli identificatori dei tipi di dati](../../../odbc/reference/appendixes/using-data-type-identifiers.md)  
  
-   [Tipi di dati SQLSQL Data Types](../../../odbc/reference/appendixes/sql-data-types.md)  
  
-   [Tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md)  
  
-   [Identificatori e descrittori del tipo di dati](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)  
  
-   [Identificatori di pseudo-tipo](../../../odbc/reference/appendixes/pseudo-type-identifiers.md)  
  
-   [Trasferimento dei dati in forma binaria](../../../odbc/reference/appendixes/transferring-data-in-its-binary-form.md)  
  
-   [Linee guida per i tipi di dati intervallo e numerici](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md)  
  
-   [Vincoli del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)  
  
-   [Dimensione colonna, cifre decimali, lunghezza trasferimento in ottetti e dimensioni visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)  
  
-   [Conversione di dati da SQL ai tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)  
  
-   [Conversione di dati da C ai tipi di dati SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)  
  
 Per una spiegazione dei tipi di dati ODBC, vedere [Tipi di dati in ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md). Per informazioni sui tipi di dati SQL specifici del driver, vedere la documentazione del driver.
