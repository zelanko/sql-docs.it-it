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
ms.openlocfilehash: 590bd488ae87e8e871837c3055a3225794850d00
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077012"
---
# <a name="data-type-conversions"></a>Conversioni dei tipi di dati
I dati possono essere convertiti da un tipo a un altro per quattro volte: quando i dati vengono trasferiti da una variabile dell'applicazione a un'altra (da C a C), quando i dati di una variabile di applicazione vengono inviati a un parametro di istruzione (da C a SQL), quando i dati in una colonna del set di risultati vengono restituiti in una variabile di applicazione (da SQL a C) e quando i dati vengono trasferiti da una colonna di origine dati a un'altra (da SQL a SQL).  
  
 Qualsiasi conversione che si verifica quando i dati vengono trasferiti da una variabile dell'applicazione a un'altra esula dall'ambito di questo documento.  
  
 Quando un'applicazione associa una variabile a una colonna del set di risultati o a un parametro di istruzione, l'applicazione specifica in modo implicito una conversione del tipo di dati nella scelta del tipo di dati della variabile dell'applicazione. Si supponga, ad esempio, che una colonna contenga dati Integer. Se l'applicazione associa una variabile integer alla colonna, specifica che non viene eseguita alcuna conversione. Se l'applicazione associa una variabile di tipo carattere alla colonna, specifica che i dati devono essere convertiti da Integer a carattere.  
  
 ODBC definisce la modalità di conversione dei dati tra ogni tipo di dati SQL e C. In pratica, ODBC supporta tutte le conversioni ragionevoli, ad esempio da carattere a Integer e da Integer a float, e non supporta le conversioni non definite in modo corretto, ad esempio float to date. I driver sono necessari per supportare tutte le conversioni per ogni tipo di dati SQL supportati. Per un elenco completo delle conversioni tra i tipi di dati SQL e C, vedere Conversione di dati [da SQL a tipi di dati c](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) e [conversione di dati da C a tipi](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) di dati SQL in Appendice D: tipi di dati.  
  
 ODBC definisce inoltre una funzione scalare per la conversione di dati da un tipo di dati SQL a un altro. La funzione **Convert** Scalar viene mappata dal driver alla funzione scalare sottostante o alle funzioni definite per eseguire le conversioni nell'origine dati. Poiché questa funzione è mappata a funzioni specifiche del sistema DBMS, ODBC non definisce la modalità di funzionamento di queste conversioni o le conversioni che devono essere supportate. Un'applicazione individua le conversioni supportate da un particolare driver e da un'origine dati tramite le opzioni SQL_CONVERT in **SQLGetInfo**. Per ulteriori informazioni sulla funzione **Convert** Scalar, vedere [sequenze di escape in ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) e [funzione di conversione del tipo di dati esplicita](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md).
