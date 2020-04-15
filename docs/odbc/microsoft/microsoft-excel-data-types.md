---
title: Tipi di dati di Microsoft Excel - Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], Excel driver
- Excel data types [ODBC]
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], data types
ms.assetid: 7b44c8e5-0bc3-4912-8a5d-56f4d5562fe6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8574985e10e5aaa3ae5431af7ee1245643e20b60
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283771"
---
# <a name="microsoft-excel-data-types"></a>Tipi di dati Microsoft Excel
Nella tabella seguente viene illustrato il mapping dei tipi di dati dei driver di Microsoft Excel ai tipi di dati SQL ODBC. Il driver di Microsoft Excel assegna questi tipi di dati alle colonne nelle tabelle di Microsoft Excel in base ai dati nella colonna.  
  
|Tipo di dati di Microsoft Excel|Tipo di dati ODBC|  
|-------------------------------|--------------------|  
|CURRENCY|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|Logico|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** restituisce i tipi di dati SQL ODBC. Tutte le conversioni nell'Appendice D di *ODBC Programmer's Reference* sono supportate per i tipi di dati SQL ODBC elencati in precedenza in questo argomento.  
  
 Nella tabella seguente vengono illustrate le limitazioni relative ai tipi di dati di Microsoft Excel.  
  
|Tipo di dati|Descrizione|  
|---------------|-----------------|  
|Dati crittografati|Il driver di Microsoft Excel non è in grado di leggere i dati crittografati.|  
|Stringhe di errore|Il driver di Microsoft Excel non può restituire una stringa di caratteri per i valori di errore di Microsoft Excel (#N/A!, #VALUE!, #REF!, #DIV/0!, #NUM!, #NAME?, e #NULL!), ma restituisce un valore NULL.|  
|Logico|Il valore in una colonna LOGICAL viene restituito in un SQL_C_CHAR buffer come 0 o 1.|  
|NUMBER|Se viene creata una colonna integer, è possibile immettere numeri troppo grandi per il tipo di dati integer e inserire dati contenenti valori non interi, con il risultato che la colonna può essere convertita in SQL_DOUBLE.|  
|TEXT|Quando le righe di una colonna contengono più di un tipo di dati di Microsoft Excel, il driver ODBC di Microsoft Excel assegna il tipo di dati SQL_VARCHAR alla colonna. Esiste un'eccezione: se la colonna contiene solo due o tre dei tipi di dati datetime (DATE, TIME e DATETIME), il driver ODBC di Microsoft Excel assegna il tipo di dati SQL_TIMESTAMP alla colonna.<br /><br /> La creazione di una colonna TEXT di lunghezza zero o non specificata restituisce in realtà una colonna di 255 byte.<br /><br /> Un valore letterale stringa di caratteri può contenere qualsiasi carattere ANSI (1-255 decimale). Utilizzare due virgolette singole consecutive (") per rappresentare una virgoletta singola (').<br /><br /> L'inserimento di un valore NULL in una colonna con un tipo di dati diverso da SQL_VARCHAR causerà la modifica del tipo di dati della colonna SQL_VARCHAR.|  
  
 Ulteriori limitazioni sui tipi di dati sono disponibili in [Limitazioni dei tipi](../../odbc/microsoft/data-type-limitations.md)di dati .
