---
title: Supporto sql_variant per i tipi Date e Time | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sql_variant data type
ms.assetid: 12ff1ea6-e2cc-40e6-910c-3126974a90b3
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 718fc8b9a323ca6b1575021d748afde527dfb872
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68062428"
---
# <a name="sqlvariant-support-for-date-and-time-types"></a>Supporto sql_variant per i tipi di data e ora
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Questo argomento viene descritto come la **sql_variant** tipo di dati supporta funzionalità avanzate di data e ora.  
  
 L'attributo della colonna SQL_CA_SS_VARIANT_TYPE è utilizzato per restituire il tipo C di una colonna dei risultati variant. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] introduce un attributo aggiuntivo, SQL_CA_SS_VARIANT_SQL_TYPE, che imposta il tipo SQL di una colonna di risultati variant nel descrittore della riga di implementazione (IRD). SQL_CA_SS_VARIANT_SQL_TYPE è anche utilizzabile nel descrittore di parametri di implementazione (IPD) per specificare il tipo SQL di un SQL_SS_TIME2 o SQL_SS_TIMESTAMPOFFSET parametro che ha un tipo SQL_C_BINARY C associato al tipo SQL_SS_VARIANT.  
  
 I nuovi tipi SQL_SS_TIME2 e SQL_SS_TIMESTAMPOFFSET possono essere impostati da SQLColAttribute. SQL_CA_SS_VARIANT_SQL_TYPE può essere restituito da SQLGetDescField.  
  
 Per le colonne dei risultati, il driver convertirà i tipi da variant a date/time. Per altre informazioni, vedere [le conversioni da SQL a C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md). Quando l'associazione SQL_C_BINARY, la lunghezza del buffer deve essere sufficientemente grande per la ricezione della struttura che corrisponde al tipo SQL.  
  
 Per i parametri SQL_SS_TIME2 e SQL_SS_TIMESTAMPOFFSET, il driver convertirà i valori C **sql_variant** valori, come descritto nella tabella seguente. Se un parametro viene associato come SQL_C_BINARY e il tipo di server è SQL_SS_VARIANT, verrà trattato come valore binario, a meno che l'applicazione non abbia impostato SQL_CA_SS_VARIANT_SQL_TYPE su un tipo SQL diverso. In questo caso SQL_CA_SS_VARIANT_SQL_TYPE ha la precedenza, ovvero se è impostato SQL_CA_SS_VARIANT_SQL_TYPE, viene ignorato il comportamento predefinito che consiste nel dedurre il tipo SQL variant dal tipo C.  
  
|Tipo C|Tipo server|Commenti|  
|------------|-----------------|--------------|  
|SQL_C_CHAR|varchar|SQL_CA_SS_VARIANT_SQL_TYPE viene ignorato.|  
|SQL_C_WCHAR|nvarcar|SQL_CA_SS_VARIANT_SQL_TYPE viene ignorato.|  
|SQL_C_TINYINT|smallint|SQL_CA_SS_VARIANT_SQL_TYPE viene ignorato.|  
|SQL_C_STINYINT|smallint|SQL_CA_SS_VARIANT_SQL_TYPE viene ignorato.|  
|SQL_C_SHORT|smallint|SQL_CA_SS_VARIANT_SQL_TYPE viene ignorato.|  
|SQL_C_SSHORT|smallint|SQL_CA_SS_VARIANT_SQL_TYPE viene ignorato.|  
|SQL_C_USHORT|int|SQL_CA_SS_VARIANT_SQL_TYPE viene ignorato.|  
|SQL_C_LONG|int|SQL_CA_SS_VARIANT_SQL_TYPE viene ignorato.|  
|SQL_C_SLONG|int|SQL_CA_SS_VARIANT_SQL_TYPE viene ignorato.|  
|SQL_C_ULONG|bigint|SQL_CA_SS_VARIANT_SQL_TYPE viene ignorato.|  
|SQL_C_SBIGINT|bigint|SQL_CA_SS_VARIANT_SQL_TYPE viene ignorato.|  
|SQL_C_FLOAT|real|SQL_CA_SS_VARIANT_SQL_TYPE viene ignorato.|  
|SQL_C_DOUBLE|float|SQL_CA_SS_VARIANT_SQL_TYPE viene ignorato.|  
|SQL_C_BIT|bit|SQL_CA_SS_VARIANT_SQL_TYPE viene ignorato.|  
|SQL_C_UTINYINT|tinyint|SQL_CA_SS_VARIANT_SQL_TYPE viene ignorato.|  
|SQL_C_BINARY|varbinary|SQL_CA_SS_VARIANT_SQL_TYPE non è impostato.|  
|SQL_C_BINARY|time|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIME2<br /><br /> La scala è impostata su SQL_DESC_PRECISION (il *DecimalDigits* del parametro **SQLBindParameter**).|  
|SQL_C_BINARY|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIMESTAMPOFFSET<br /><br /> La scala è impostata su SQL_DESC_PRECISION (il *DecimalDigits* del parametro **SQLBindParameter**).|  
|SQL_C_TYPE_DATE|date|SQL_CA_SS_VARIANT_SQL_TYPE viene ignorato.|  
|SQL_C_TYPE_TIME|time(0)|SQL_CA_SS_VARIANT_SQL_TYPE viene ignorato.|  
|SQL_C_TYPE_TIMESTAMP|datetime2|La scala è impostata su SQL_DESC_PRECISION (il *DecimalDigits* del parametro **SQLBindParameter**).|  
|SQL_C_NUMERIC|decimal|La precisione è impostata su SQL_DESC_PRECISION (il *ColumnSize* del parametro **SQLBindParameter**).<br /><br /> Scala impostata su SQL_DESC_SCALE (il *DecimalDigits* parametro di SQLBindParameter).|  
|SQL_C_SS_TIME2|time|SQL_CA_SS_VARIANT_SQL_TYPE viene ignorato|  
|SQL_C_SS_TIMESTAMPOFFSET|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE viene ignorato|  
  
## <a name="see-also"></a>Vedere anche  
 [Data e miglioramenti per la fase &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
