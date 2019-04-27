---
title: Conversioni di tipi di dati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], conversions
- SQL data types [ODBC], conversions
- converting data [ODBC]
- converting data types [ODBC]
- C data types [ODBC], conversions
ms.assetid: d311fe1c-d882-4136-9fa5-220a4121e04c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 84710ffd69ea377c979adf94af1394d8436ef10b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62640474"
---
# <a name="data-type-conversions"></a>Conversioni dei tipi di dati
I dati possono essere convertiti da un tipo a altro in uno dei quattro volte: quando i dati vengono trasferiti dalla variabile di un'applicazione a un altro (C per C), quando i dati in una variabile di applicazione viene inviati a un parametro dell'istruzione C a SQL, quando i dati in una colonna del set di risultati vengono restituiti una variabile di applicazione (da SQL a C) e quando i dati vengono trasferiti dall'origine una dati colonna a un altro (SQL per SQL).  
  
 Qualsiasi conversione che si verifica quando i dati vengono trasferiti dalla variabile di un'applicazione a un altro non rientra nell'ambito di questo documento.  
  
 Quando un'applicazione si associa una variabile a un parametro di colonna o l'istruzione set di risultati, l'applicazione specifica in modo implicito una conversione del tipo di dati di sua scelta del tipo di dati della variabile dell'applicazione. Si supponga, ad esempio, che una colonna contiene dati di tipo integer. Se l'applicazione associa una variabile integer per la colonna, specifica che non venga eseguita alcuna conversione; Se l'applicazione associa una variabile di caratteri nella colonna, specifica che i dati di essere convertita da integer in carattere.  
  
 ODBC definisce la modalità di conversione dei dati tra i diversi tipi di dati SQL e C. In sostanza, ODBC supporta tutte le conversioni ragionevole, ad esempio carattere da integer e integer in float e non supporta conversioni in modo non corretto, ad esempio float a oggi. I driver devono supportare tutte le conversioni per ogni tipo di dati SQL che supportano. Per un elenco completo delle conversioni tra tipi di dati SQL e C, vedere [conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) e [convertendo i dati da C a tipi di dati SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) nell'appendice d: Tipi di dati.  
  
 ODBC definisce anche una funzione scalare di convertire i dati da un tipo di dati SQL a un altro. Il **CONVERTIRE** viene eseguito il mapping di funzione scalare dal driver per la funzione scalare sottostante o le funzioni definite per eseguire conversioni nell'origine dati. Poiché questa funzione viene mappata a funzioni specifiche del sistema DBMS, ODBC non definisce come funzionano queste conversioni o quali le conversioni devono essere supportate. Un'applicazione consente di individuare quali conversioni vengono supportate da una determinata origine dati e driver tramite le opzioni SQL_CONVERT **SQLGetInfo**. Per altre informazioni sul **CONVERTIRE** funzione scalare, vedere [sequenze di Escape in ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) e [funzione di conversione tipo di dati esplicita](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md).
