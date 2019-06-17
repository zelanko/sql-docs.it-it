---
title: Funzione SQL-92 CAST | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], SQL-92 functions
- SQL-92 functions [ODBC]
- CAST function [ODBC]
ms.assetid: 982f09e5-8205-41b9-98b3-8f898e24743f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db5077b9df2673593b6eaec9622aafd1d2c77234
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270625"
---
# <a name="sql-92-cast-function"></a>Funzione SQL-92 CAST
Il **CAST** definito in SQL-92 è equivalente alle **CONVERTIRE** funzione definita in ODBC. La sintassi di funzioni equivalenti è come segue:  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 SQL-92 **CAST** funzione impone i tipi di dati possono essere convertiti in quali altri tipi di dati. (Per altre informazioni, vedere la specifica di SQL-92.) Il **CAST** funzione è supportata a livello di FIPS transitorio.  
  
 Un'applicazione può determinare il supporto per la **CAST** funzionare nel modo seguente:  
  
1.  Chiamare **SQLGetInfo** con il tipo di informazioni SQL_SQL_CONFORMANCE. Se il valore restituito per il tipo di informazioni è SQL_SC_FIPS127_2_TRANSITIONAL, SQL_SC_SQL92_INTERMEDIATE o SQL_SC_SQL92_FULL, il **CAST** funzione è supportata.  
  
2.  Se il valore restituito del tipo di informazioni SQL_SQL_CONFORMANCE SQL_SC_ENTRY_LEVEL o 0, chiamare **SQLGetInfo** con il tipo di informazioni SQL_SQL92_VALUE_EXPRESSIONS. Se è impostato il bit SQL_SVE_CAST, il **CAST** funzione è supportata.
