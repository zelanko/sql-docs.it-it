---
title: Identificatori e descrittori dei tipi di dati Documenti Microsoft
ms.custom: ''
ms.date: 02/02/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
- descriptors [ODBC], data types
- verbose data types [ODBC]
- data types [ODBC], descriptors
- concise data types [ODBC]
ms.assetid: f0077c9b-8eb2-4b5f-8c4c-7436fdef37ab
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f65bc86213f99112daf17c67a4ca522490d32149
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284484"
---
# <a name="data-type-identifiers-and-descriptors"></a>Identificatori e descrittori del tipo di dati
I tipi di dati elencati nelle sezioni [Tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md) e Tipi di dati [C](../../../odbc/reference/appendixes/c-data-types.md) riportati in precedenza in questa appendice sono tipi di dati "concisi": ogni identificatore fa riferimento a un singolo tipo di dati. Esiste una corrispondenza uno-a-uno tra l'identificatore e il tipo di dati. I descrittori, tuttavia, non in tutti i casi utilizzano un singolo valore per identificare i tipi di dati. In alcuni casi, usano un tipo di dati "verbose" e un sottocodice di tipo. Per tutti i tipi di dati, ad eccezione dei tipi di dati datetime e interval, l'identificatore di tipo dettagliato corrisponde all'identificatore di tipo conciso e il valore in SQL_DESC_DATETIME_INTERVAL_CODE è uguale a 0. Per i tipi di dati datetime e interval, tuttavia, un tipo dettagliato (SQL_DATETIME o SQL_INTERVAL) viene archiviato in SQL_DESC_TYPE, un tipo conciso viene archiviato in SQL_DESC_CONCISE_TYPE e un sottocodice per ogni tipo conciso viene archiviato in SQL_DESC_DATETIME_INTERVAL_CODE. L'impostazione di uno di questi campi influisce sugli altri. Per altre informazioni su questi campi, vedere la descrizione della funzione [SQLSetDescField.For](../../../odbc/reference/syntax/sqlsetdescfield-function.md) more information about these fields, see the SQLSetDescField function description.  
  
 Quando il campo SQL_DESC_TYPE o SQL_DESC_CONCISE_TYPE è impostato per alcuni tipi di dati, i campi SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_LENGTH, SQL_DESC_PRECISION e SQL_DESC_SCALE vengono impostati automaticamente sui valori predefiniti, come applicabile per il tipo di dati. Per ulteriori informazioni, vedere la descrizione del campo SQL_DESC_TYPE in [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Se uno dei valori predefiniti impostati non è appropriato, l'applicazione deve impostare in modo esplicito il campo del descrittore tramite una chiamata a **SQLSetDescField**.  
  
 Nella tabella seguente vengono illustrati l'identificatore di tipo conciso, l'identificatore di tipo dettagliato e il sottocodice del tipo per ogni identificatore di tipo SQL e C di tipo datetime e intervallo. Come indica questa tabella, per i tipi di dati datetime e interval, i campi SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE hanno le stesse costanti manifesto sia per i tipi di dati SQL (nei descrittori di implementazione) che per i tipi di dati C (nei descrittori dell'applicazione).  
  
|Tipo SQL conciso|Tipo C conciso|Tipo dettagliato|DATETIME_INTERVAL_CODE|  
|----------------------|--------------------|------------------|------------------------------|  
|SQL_TYPE_DATE|SQL_C_TYPE_DATE|SQL_DATETIME|SQL_CODE_DATE|  
|SQL_TYPE_TIME|SQL_C_TYPE_TIME|SQL_DATETIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_DATETIME|SQL_CODE_TIMESTAMP|  
|SQL_INTERVAL_MONTH|SQL_C_INTERVAL_MONTH|SQL_INTERVAL|SQL_CODE_MONTH|  
|SQL_INTERVAL_YEAR|SQL_C_INTERVAL_YEAR|SQL_INTERVAL|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_INTERVAL|SQL_CODE_YEAR_TO_MONTH|  
|SQL_INTERVAL_DAY|SQL_C_INTERVAL_DAY|SQL_INTERVAL|SQL_CODE_DAY|  
|SQL_INTERVAL_HOUR|SQL_C_INTERVAL_HOUR|SQL_INTERVAL|SQL_CODE_HOUR|  
|SQL_INTERVAL_MINUTE|SQL_C_INTERVAL_MINUTE|SQL_INTERVAL|SQL_CODE_MINUTE|  
|SQL_INTERVAL_SECOND|SQL_C_INTERVAL_SECOND|SQL_INTERVAL|SQL_CODE_SECOND|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_C_INTERVAL_DAY_TO_HOUR|SQL_INTERVAL|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE|SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_INTERVAL|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND|SQL_C_INTERVAL_DAY_TO_SECOND|SQL_INTERVAL|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR_TO_MINUTE|SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_INTERVAL|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND|SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_INTERVAL|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE_TO_SECOND|SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_INTERVAL|SQL_CODE_MINUTE_TO_SECOND|
