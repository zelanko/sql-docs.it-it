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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c6682ae98f2da64f6936049bee96fe2fff2a84db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057065"
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
