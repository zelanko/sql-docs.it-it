---
title: 'Da C a SQL: Binary | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- binary data type [ODBC]
- data conversions from C to SQL types [ODBC], binary
- binary data transfers [ODBC]
- converting data from c to SQL types [ODBC], binary
ms.assetid: 3e9083f3-357b-41aa-833c-2c8aac2226cd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76c2e4673d9b561aeb5af3e61e1e4dc8532195d6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63201584"
---
# <a name="c-to-sql-binary"></a>Da C a SQL: Binario
L'identificatore per il tipo di dati C ODBC binario è:  
  
 SQL_C_BINARY  
  
 La tabella seguente illustra il codice SQL ODBC dei tipi di dati a cui possono essere convertiti i dati binari di C. Per una spiegazione delle colonne e le condizioni nella tabella, vedere [conversione di dati da C a tipi di dati SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificatore di tipo SQL|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Lunghezza in byte dei dati < = lunghezza di colonna in byte<br /><br /> Lunghezza in byte di dati > lunghezza di colonna in byte|n/d<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Lunghezza dei dati in caratteri < = lunghezza in caratteri colonna<br /><br /> Lunghezza dei dati in caratteri > lunghezza in caratteri colonna|n/d<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER<br /><br /> SQL_BIGINT<br /><br /> SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE<br /><br /> SQL_BIT SQL_TYPE_DATE<br /><br /> SQL_TYPE_TIME<br /><br /> SQL_TYPE_TIMESTAMP|Lunghezza in byte di dati = lunghezza dei dati SQL<br /><br /> Lunghezza in byte di lunghezza dei dati di data <> SQL|n/d<br /><br /> 22003|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|Lunghezza dei dati < = lunghezza della colonna<br /><br /> Lunghezza dei dati > lunghezza della colonna|n/d<br /><br /> 22001|
