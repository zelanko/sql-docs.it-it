---
title: Prefissi e suffissi letterali Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], literal prefixes and suffixes
- literals [ODBC], prefixes and suffixes
ms.assetid: 29f468f2-f557-4a92-b31d-569c63cc6272
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d52ca54c329353e3d9dc67ca35d89b2d28cedf74
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287983"
---
# <a name="literal-prefixes-and-suffixes"></a>Prefissi e suffissi per valori letterali
In un'istruzione SQL, un *valore letterale* è una rappresentazione di caratteri di un valore di dati effettivo. Ad esempio, nell'istruzione seguente, ABC, FFFF e 10 sono valori letterali:For example, in the following statement, ABC, FFFF, and 10 are literals:  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 I valori letterali per alcuni tipi di dati richiedono prefissi e suffissi speciali. Nell'esempio precedente, il valore letterale carattere (ABC) richiede una virgoletta singola (') sia come prefisso che come suffisso, il valore letterale binario (FFFF) richiede i caratteri 0x come prefisso e il valore letterale integer (10) non richiede un prefisso o un suffisso.  
  
 Per tutti i tipi di dati, ad eccezione di data, ora e timestamp, le applicazioni interoperabili devono utilizzare i valori restituiti nelle colonne LITERAL_PREFIX e LITERAL_SUFFIX nel set di risultati creato da **SQLGetTypeInfo**. Per i valori letterali di intervallo date, ora, timestamp e datetime, le applicazioni interoperabili devono utilizzare le sequenze di escape descritte nella sezione precedente.
