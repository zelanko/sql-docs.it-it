---
title: Valore letterale prefissi e suffissi | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f4eabc3e0c354e02ad8df790d896dc43ae49c9bd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313005"
---
# <a name="literal-prefixes-and-suffixes"></a>Prefissi e suffissi per valori letterali
In un'istruzione SQL, un *letterale* è una rappresentazione di caratteri di un valore effettivo dei dati. Nell'istruzione seguente, ad esempio, ABC, FFFF e 10 sono valori letterali:  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 Valori letterali per alcuni tipi di dati richiedono speciali prefissi e suffissi. Nell'esempio precedente, il valore letterale carattere (ABC) richiede una virgoletta singola (') come un prefisso e suffisso, il valore letterale binario (FFFF) richiede i caratteri 0x come un prefisso e il valore letterale integer (10) non richiede un prefisso o suffisso.  
  
 Per tutti i tipi di dati, ad eccezione di date, time e timestamp applicazioni interoperative devono usare i valori restituiti nelle colonne del set di risultati creati da:: SQLGetTypeInfo e SQL_VARCHAR **SQLGetTypeInfo**. Per data, ora, timestamp e i valori letterali intervallo datetime, applicazioni interoperative devono usare le sequenze di escape illustrate nella sezione precedente.
