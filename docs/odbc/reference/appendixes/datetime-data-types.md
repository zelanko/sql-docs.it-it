---
title: I tipi di dati DateTime | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- time data type [ODBC]
- datetime data types [ODBC]
- date data type [ODBC]
- data types [ODBC], date
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- data types [ODBC], timestamp
- data types [ODBC], backward compatibility
- compatibility [ODBC], datetime data types
- data types [ODBC], time
ms.assetid: 6b9363c9-04bf-4492-a210-7aa15dea4af8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 13cb433da64b78a8b5e70f28642fd576f6803ed5
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792590"
---
# <a name="datetime-data-types"></a>Tipi di dati datetime
In ODBC *3.x*, gli identificatori per data, ora e tipi di dati timestamp SQL sono stati modificati da SQL_DATE, SQL_TIME e SQL_TIMESTAMP (con istanze di **#define** nel file di intestazione di 9, 10 e 11) per SQL _ TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP (con istanze di **#define** nel file di intestazione di 91, 92 e 93), rispettivamente. Il tipo C corrispondente identificatori sono stati modificati da SQL_C_DATE SQL_C_TIME e SQL_C_TIMESTAMP SQL_C_TYPE_DATE, SQL_C_TYPE_TIME e SQL_C_TYPE_TIMESTAMP, rispettivamente e le istanze del **#define** sono stati modificati Secondo.  
  
 Le dimensioni e cifre decimali restituiscono per i tipi di dati datetime SQL in ODBC *3.x* quello utilizzato per la precisione e scala restituite dal in ODBC sono *2.x*. Questi valori sono diversi dai valori nei campi del descrittore SQL_DESC_PRECISION e SQL_DESC_SCALE. (Per altre informazioni, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) nell'appendice d: Tipi di dati.)  
  
 Queste modifiche interessano **SQLDescribeCol**, **SQLDescribeParam**, e **SQLColAttributes**; **SQLBindCol**, **SQLBindParameter**, e **SQLGetData**; e **SQLColumns**, **SQLGetTypeInfo** , **SQLProcedureColumns**, **SQLStatistics**, e **SQLSpecialColumns**.  
  
 Un database ODBC *3.x* driver elabora le chiamate di funzione elencate nel paragrafo precedente in base all'impostazione dell'attributo environment SQL_ATTR_ODBC_VERSION. Per la **SQLColumns**, **SQLGetTypeInfo**, **SQLProcedureColumns**, **SQLSpecialColumns**, e **SQLStatistics** , se SQL_ATTR_ODBC_VERSION è impostato su SQL_OV_ODBC3, le funzioni restituiscono SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP nel campo DATA_TYPE. La colonna COLUMN_SIZE (nel set di risultati restituito da **SQLColumns**, **SQLGetTypeInfo**, **SQLProcedureColumns**, e **SQLSpecialColumns**) contiene la precisione binaria per il tipo numerico approssimato. La colonna NUM_PREC_RADIX (nel set di risultati restituito da **SQLColumns**, **SQLGetTypeInfo**, e **SQLProcedureColumns**) contiene un valore pari a 2. Se SQL_ATTR_ODBC_VERSION è impostata su SQL_OV_ODBC2, le funzioni SQL_DATE, SQL_TIME e SQL_TIMESTAMP restituito nel campo DATA_TYPE, la colonna COLUMN_SIZE contiene la precisione decimale per il tipo numerico approssimato e la colonna NUM_PREC_RADIX contiene un valore pari a 10.  
  
 Quando vengono richiesti tutti i tipi di dati in una chiamata a **SQLGetTypeInfo**, il set di risultati restituito dalla funzione conterrà sia SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP come definito in ODBC *3.x*, e SQL_DATE, SQL_TIME e SQL_TIMESTAMP come definito in ODBC *2.x*.  
  
 A causa di come ODBC *3.x* Driver Manager esegue il mapping dei tipi di dati date, time e timestamp, ODBC *3.x* necessitano riconoscono solo i driver **#defines** di 91, 92, e 93 per la data, ora e tipi di dati timestamp C immesso nel *TargetType* argomenti del **SQLBindCol** e **SQLGetData** o  *ValueType* dell'argomento **SQLBindParameter**e necessario riconoscere solo **#defines** di 91, 92 e 93 per la data, ora e tipi di dati timestamp SQL immessa nel *ParameterType* argomento della **SQLBindParameter** o il *DataType* argomento del **SQLGetTypeInfo**. Per altre informazioni, vedere [modifiche ai tipi di dati Datetime](../../../odbc/reference/develop-app/datetime-data-type-changes.md).
