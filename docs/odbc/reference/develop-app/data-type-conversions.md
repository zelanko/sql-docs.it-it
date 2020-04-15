---
title: Conversioni dei tipi di dati Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd888fe32692494e2b0ceadc1ed872dd96e244a9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305213"
---
# <a name="data-type-conversions"></a>Conversioni dei tipi di dati
I dati possono essere convertiti da un tipo all'altro in una delle quattro volte: quando i dati vengono trasferiti da una variabile di applicazione a un'altra (da C a C), quando i dati in una variabile di applicazione vengono inviati a un parametro di istruzione (da C a SQL), quando i dati in una colonna del set di risultati vengono restituiti in una variabile di applicazione (da SQL a C) e quando i dati vengono trasferiti da una colonna di origine dati a un'altra (da SQL a SQL).  
  
 Qualsiasi conversione che si verifica quando i dati vengono trasferiti da una variabile di applicazione a un'altra non rientra nell'ambito di questo documento.  
  
 Quando un'applicazione associa una variabile a una colonna del set di risultati o a un parametro di istruzione, l'applicazione specifica in modo implicito una conversione del tipo di dati nella scelta del tipo di dati della variabile di applicazione. Si supponga, ad esempio, che una colonna contenga dati interi. Se l'applicazione associa una variabile integer alla colonna, specifica che non è eseguita alcuna conversione; se l'applicazione associa una variabile carattere alla colonna, specifica che i dati devono essere convertiti da integer a carattere.  
  
 ODBC definisce la modalità di conversione dei dati tra ogni tipo di dati SQL e C. Fondamentalmente, ODBC supporta tutte le conversioni ragionevoli, ad esempio da carattere a intero e da intero a float e non supporta le conversioni non definite, ad esempio da float a date aggiornate. I driver sono necessari per supportare tutte le conversioni per ogni tipo di dati SQL che supportano. Per un elenco completo delle conversioni tra i tipi di dati SQL e C, vedere [Conversione](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) di dati da tipi di dati SQL a C e [Conversione](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) di dati da C a tipi di dati SQL nell'appendice D: tipi di dati.  
  
 ODBC definisce inoltre una funzione scalare per la conversione dei dati da un tipo di dati SQL a un altro. La funzione scalare **CONVERT** viene mappata dal driver alla funzione scalare sottostante o alle funzioni definite per eseguire conversioni nell'origine dati. Poiché questa funzione è mappata a funzioni specifiche di DBMS, ODBC non definisce il funzionamento di queste conversioni o quali conversioni devono essere supportate. Un'applicazione individua le conversioni supportate da un driver e un'origine dati specifici tramite le opzioni SQL_CONVERT in **SQLGetInfo**. Per ulteriori informazioni sulla funzione scalare **CONVERT,** vedere [Sequenze di escape in ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) e Funzione di [conversione esplicita dei tipi](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)di dati .
