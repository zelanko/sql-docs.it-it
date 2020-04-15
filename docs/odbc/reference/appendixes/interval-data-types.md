---
title: Tipi di dati Interval Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- second intervals [ODBC]
- data types [ODBC], interval data types
- interval data type [ODBC]
- day-time intervals [ODBC]
- intervals [ODBC], about intervals
- minute intervals [ODBC]
- day intervals [ODBC]
- year intervals [ODBC]
- month intervals [ODBC]
- interval data type [ODBC], about interval data types
- SQL data types [ODBC], interval
- year-month intervals [ODBC]
- C data types [ODBC], interval
- interval fields [ODBC]
ms.assetid: fba93f65-c1db-44f4-91ba-532f87241cf7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee4a6e845e0bc0830f514b2e768075dd75bcf6e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304967"
---
# <a name="interval-data-types"></a>Tipi di dati intervallo
Un intervallo è definito come la differenza tra due date e ore. Gli intervalli sono espressi in uno dei due modi diversi. Uno è un intervallo *di un anno* che esprime intervalli in termini di anni e un numero integrale di mesi. L'altro è un intervallo *giorno-tempo* che esprime intervalli in termini di giorni, minuti e secondi. Questi due tipi di intervalli sono distinti e non possono essere mescolati, perché i mesi possono avere un numero variabile di giorni.  
  
 Un intervallo è costituito da un set di campi. C'è un ordinamento implicito tra i campi. Ad esempio, in un intervallo da inizio mese, l'anno viene prima, seguito dal mese. Analogamente, in un intervallo giorno per minuto, i campi sono nell'ordine giorno, ora e minuto. Il primo campo di un tipo di intervallo è denominato campo *iniziale* o campo *di ordine superiore.* L'ultimo campo è denominato campo *finale.*  
  
 In tutti gli intervalli, il campo iniziale non è vincolato dalle regole del calendario gregoriano. Ad esempio, in un intervallo da ora a minuto, il campo delle ore non è vincolato a essere compreso tra 0 e 23 (incluso). I campi finali successivi al campo iniziale seguono i soliti vincoli del calendario gregoriano. Per ulteriori informazioni, vedere [Vincoli del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)più avanti in questa appendice.  
  
 Esistono 13 tipi di dati SQL a intervalli e 13 tipi di dati a intervalli C. Ognuno dei tipi di dati di intervallo C utilizza la stessa struttura, SQL_INTERVAL_STRUCT, per contenere i dati dell'intervallo. (Per ulteriori informazioni, vedere la sezione successiva, [C Interval Structure](../../../odbc/reference/appendixes/c-interval-structure.md).) Per altre informazioni sui tipi di dati SQL, vedere [Tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md); Per ulteriori informazioni sui tipi di dati C, vedere [Tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md).  
  
|Identificatore del tipo|Classe|Descrizione|  
|---------------------|-----------|-----------------|  
|MONTH|Anno-Mese|Numero di mesi tra due date.|  
|YEAR|Anno-Mese|Numero di anni tra due date.|  
|YEAR_TO_MONTH|Anno-Mese|Numero di anni e mesi tra due date.|  
|DAY|Giorno-Ora|Numero di giorni tra due date.|  
|HOUR|Giorno-Ora|Numero di ore tra due date/ore.|  
|MINUTE|Giorno-Ora|Numero di minuti tra due date/ore.|  
|SECOND|Giorno-Ora|Numero di secondi tra due date/ore.|  
|DAY_TO_HOUR|Giorno-Ora|Numero di giorni/ore tra due date/ore.|  
|DAY_TO_MINUTE|Giorno-Ora|Numero di giorni/ore/minuti tra due date/ore.|  
|DAY_TO_SECOND|Giorno-Ora|Numero di giorni/ore/minuti/secondi tra due date/ore.|  
|HOUR_TO_MINUTE|Giorno-Ora|Numero di ore/minuti tra due date/ore.|  
|HOUR_TO_SECOND|Giorno-Ora|Numero di ore/minuti/secondi tra due date/ore.|  
|MINUTE_TO_SECOND|Giorno-Ora|Numero di minuti/secondi tra due date/ore.|  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Struttura C Interval](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [Precisione del tipo di dati intervallo](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [Lunghezza del tipo di dati intervallo](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [Valori letterali intervallo](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [Override della precisione iniziale e in secondi predefinita per i tipi di dati intervallo](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
