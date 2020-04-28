---
title: Funzione CAST SQL-92 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 09d2a2de710dafd4e744166c4219f4c903fd3321
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305062"
---
# <a name="sql-92-cast-function"></a>Funzione SQL-92 CAST
La funzione **cast** definita in SQL-92 equivale alla funzione **Convert** definita in ODBC. La sintassi delle funzioni equivalenti è la seguente:  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 La funzione **cast** SQL-92 impone i tipi di dati che possono essere convertiti in altri tipi di dati. Per ulteriori informazioni, vedere la specifica di SQL-92. La funzione **cast** è supportata a livello di transizione FIPS.  
  
 Un'applicazione può determinare il supporto per la funzione **cast** , come indicato di seguito:  
  
1.  Chiamare **SQLGetInfo** con il tipo di informazioni SQL_SQL_CONFORMANCE. Se il valore restituito per il tipo di informazioni è SQL_SC_FIPS127_2_TRANSITIONAL, SQL_SC_SQL92_INTERMEDIATE o SQL_SC_SQL92_FULL, la funzione **cast** è supportata.  
  
2.  Se il valore restituito del tipo SQL_SQL_CONFORMANCE informazioni è SQL_SC_ENTRY_LEVEL o 0, chiamare **SQLGetInfo** con il tipo di informazioni SQL_SQL92_VALUE_EXPRESSIONS. Se viene impostato il bit SQL_SVE_CAST, la funzione **cast** è supportata.
