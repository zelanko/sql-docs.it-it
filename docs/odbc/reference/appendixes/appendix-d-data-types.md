---
title: 'Appendice D: Tipi di dati | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 75ff7e83aa87bca9f33a3a8f44447af2eb60c581
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63026766"
---
# <a name="appendix-d-data-types"></a>Appendice D: Tipi di dati
ODBC definisce due set di tipi di dati: Tipi di dati SQL e tipi di dati C. Tipi di dati SQL indicano il tipo di dati dei dati archiviati nell'origine dati. Tipi di dati C indicano il tipo di dati dei dati archiviati nel buffer dell'applicazione.  
  
 Per ogni sistema DBMS conforme allo standard SQL-92 sono definiti tipi di dati SQL. Per ogni tipo di dati SQL specificata nello standard SQL-92, ODBC definisce un identificatore di tipo, ovvero un **#define** valore che viene passato come argomento nelle funzioni ODBC o restituito nei metadati di un set di risultati. SQL-92 solo i tipi di dati non supportati da ODBC sono BIT (il tipo ODBC SQL_BIT ha caratteristiche diverse), BIT_VARYING, TIME_WITH_TIMEZONE, TIMESTAMP_WITH_TIMEZONE e NATIONAL_CHARACTER. I driver sono responsabili del mapping di tipi di dati SQL specifiche dell'origine dati per gli identificatori di tipo di dati SQL ODBC e identificatori dei tipi dati specifici del driver SQL. Il tipo di dati SQL viene specificato nel campo SQL_DESC_CONCISE_TYPE di un descrittore di implementazione.  
  
 ODBC definisce i tipi di dati C e i relativi identificatori di tipo ODBC corrispondenti. Un'applicazione specifica il tipo di dati C del buffer che riceverà i dati dei set di risultati, passando l'identificatore di tipo C appropriato nel *TargetType* argomento nella chiamata a **SQLBindCol** o  **SQLGetData**. Specifica il tipo C del buffer che contiene un parametro dell'istruzione passando l'identificatore di tipo C appropriato nel *ValueType* argomento nella chiamata a **SQLBindParameter**. Il tipo di dati C è specificato nel campo SQL_DESC_CONCISE_TYPE di un descrittore applicazione.  
  
> [!NOTE]  
>  Non sono disponibili tipi di dati C specifici del driver.  
  
 Ogni tipo di dati SQL corrisponde a un tipo di dati C ODBC. Prima di restituire dati dall'origine dati, il driver converte nel tipo di dati C specificato. Prima di inviare dati all'origine dati, il driver converte dal tipo di dati C specificato.  
  
 In questa appendice contiene gli argomenti seguenti.  
  
-   [Uso degli identificatori dei tipi di dati](../../../odbc/reference/appendixes/using-data-type-identifiers.md)  
  
-   [Tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md)  
  
-   [Tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md)  
  
-   [Identificatori e descrittori del tipo di dati](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)  
  
-   [Identificatori di pseudo-tipo](../../../odbc/reference/appendixes/pseudo-type-identifiers.md)  
  
-   [Trasferimento dei dati in forma binaria](../../../odbc/reference/appendixes/transferring-data-in-its-binary-form.md)  
  
-   [Linee guida per i tipi di dati intervallo e numerici](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md)  
  
-   [Vincoli del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)  
  
-   [Dimensione colonna, cifre decimali, lunghezza trasferimento in ottetti e dimensioni visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)  
  
-   [Conversione di dati da SQL ai tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)  
  
-   [Conversione di dati da C ai tipi di dati SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)  
  
 Per una spiegazione dei tipi di dati ODBC, vedere [tipi di dati in ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md). Per informazioni sui tipi di dati specifici del driver SQL, vedere la documentazione del driver.
