---
title: Tipi di dati Interval | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 930a848ea01d128cb248c7929408ce7510937ad9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188894"
---
# <a name="interval-data-types"></a>Tipi di dati intervallo
Un intervallo viene definito come la differenza tra due date e ore. Gli intervalli sono espressi in uno dei due modi diversi. Uno è un *mese anno* intervallo che esprime intervalli in termini di un numero integrale di mesi e anni. L'altro è un *diurno* intervallo che esprime intervalli in termini di giorni, minuti e secondi. Questi due tipi di intervalli sono diversi e non possono essere combinati, poiché mesi possono avere un numero variabile di giorni.  
  
 Un intervallo è costituito da un set di campi. Non vi è un ordine implicito tra i campi. Ad esempio, in un intervallo di anno per mese, anno raggiunto per primo, seguito dal mese. Analogamente, in un intervallo giorno-a-minuti, i campi sono in ordine giorno, ora e minuto. Il primo campo in un tipo di intervallo viene chiamato il *iniziali* campo, o il *significativo* campo. L'ultimo campo viene chiamato il *finali* campo.  
  
 In tutti gli intervalli, il campo iniziale non è vincolato dalle regole del calendario gregoriano. Ad esempio, in un intervallo ora-a-minuto, al campo dell'ora non è vincolato per essere compreso tra 0 e 23 (inclusi), perché in genere è. I campi finali dopo il campo iniziale seguono i vincoli normali del calendario gregoriano. Per altre informazioni, vedere [vincoli del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md), più avanti in questa appendice.  
  
 Sono disponibili tipi di dati SQL intervallo 13 e tipi di dati C intervallo 13. Ognuno dei tipi di dati di intervallo C Usa la stessa struttura, SQL_INTERVAL_STRUCT, per contenere i dati di intervallo. (Per altre informazioni, vedere la sezione successiva [struttura C Interval](../../../odbc/reference/appendixes/c-interval-structure.md).) Per altre informazioni sui tipi di dati SQL, vedere [tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md); per ulteriori informazioni sui tipi di dati C, vedere [tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md).  
  
|Identificatore del tipo|Classe|Descrizione|  
|---------------------|-----------|-----------------|  
|MONTH|Anno-mese|Numero di mesi tra due date.|  
|YEAR|Anno-mese|Numero di anni tra due date.|  
|YEAR_TO_MONTH|Anno-mese|Numero di anni e mesi che intercorrono tra due date.|  
|DAY|/ Ora|Numero di giorni tra due date.|  
|HOUR|/ Ora|Numero di ore tra due date/ore.|  
|MINUTE|/ Ora|Numero di minuti tra due date/ore.|  
|SECOND|/ Ora|Numero di secondi tra due date/ore.|  
|DAY_TO_HOUR|/ Ora|Numero di giorni/ore tra due date/ore.|  
|DAY_TO_MINUTE|/ Ora|Numero di giorni/ore/minuti tra due date/ore.|  
|DAY_TO_SECOND|/ Ora|Numero di giorni/ore/minuti/secondi tra due date/ore.|  
|HOUR_TO_MINUTE|/ Ora|Numero di ore o minuti tra due date/ore.|  
|HOUR_TO_SECOND|/ Ora|Numero di ore/minuti/secondi tra due date/ore.|  
|MINUTE_TO_SECOND|/ Ora|Numero di minuti/secondi tra due date/ore.|  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Struttura C Interval](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [Precisione del tipo di dati intervallo](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [Lunghezza del tipo di dati intervallo](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [Valori letterali intervallo](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [Override della precisione iniziale e in secondi predefinita per i tipi di dati intervallo](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
