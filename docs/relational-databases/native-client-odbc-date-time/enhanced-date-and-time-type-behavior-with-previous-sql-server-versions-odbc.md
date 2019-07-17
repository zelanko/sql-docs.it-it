---
title: Avanzate di data e ora il comportamento dei tipi con precedenti versioni di SQL Server (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- date/time [ODBC], enhanced behavior with earlier SQL Server versions
ms.assetid: cd4e137f-dc5e-4df7-bc95-51fe18c587e0
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: daa906f14711976587661640fba30130de1a01c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030380"
---
# <a name="enhanced-date-and-time-type-behavior-with-previous-sql-server-versions-odbc"></a>Comportamento dei tipi di data e ora migliorati con le versioni di SQL Server precedenti (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  In questo argomento viene descritto il comportamento previsto quando un'applicazione client che utilizza caratteristiche avanzate di data e ora comunica con una versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedente a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e quando un'applicazione client che utilizza Microsoft Data Access Components, Windows Data Access Components o una versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client precedente a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] invia comandi a un server che supporta le caratteristiche avanzate di data e ora.  
  
## <a name="down-level-client-behavior"></a>Comportamento dei client legacy  
 Nelle applicazioni client compilate utilizzando una versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client precedente a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] i nuovi tipi di data/ora vengono visualizzati come colonne nvarchar. Il contenuto delle colonne è costituito da rappresentazioni letterali, come descritto in "formati di dati: Sezione stringhe e valori letterali"di [supporto dei tipi di dati per ODBC Date e miglioramenti per la fase](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md). Le dimensioni di colonna corrispondono alla lunghezza massima in valori letterali per la precisione frazionaria dei secondi specificata per la colonna.  
  
 Le API di catalogo restituiranno metadati consistenti con il codice del tipo di dati legacy restituito al client, ad esempio nvarchar, e la rappresentazione legacy associata, ad esempio il formato letterale appropriato. Il nome del tipo di dati restituito, tuttavia, coinciderà con il nome effettivo del tipo di dati di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
 Metadati di istruzione restituiti da SQLDescribeCol, SQLDescribeParam, SQGetDescField e SQLColAttribute restituiranno metadati che sono coerenti con il tipo di livello inferiore in tutti gli aspetti, tra cui il nome del tipo. È un esempio di tale tipo di livello inferiore **nvarchar**.  
  
 Quando un'applicazione client legacy viene eseguita in un [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (o versione successiva) in cui le modifiche dello schema di data/ora sono stato apportati tipi di server, il comportamento previsto è come segue:  
  
|Tipo di SQL Server 2005|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (o versioni successive) Tipo|Tipo del client ODBC|Conversione risultati (da SQL a C)|Conversione parametri (da C a SQL)|  
|--------------------------|----------------------------------------------|----------------------|------------------------------------|---------------------------------------|  
|Datetime|Date|SQL_C_TYPE_DATE|OK|OK (1)|  
|||SQL_C_TYPE_TIMESTAMP|Campi dell'ora impostati su zero.|OK (2)<br /><br /> Esito negativo se il campo dell'ora è diverso da zero. Compatibile con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||Time(0)|SQL_C_TYPE_TIME|OK|OK (1)|  
|||SQL_C_TYPE_TIMESTAMP|Campi della data impostati sulla data corrente.|OK (2)<br /><br /> La data viene ignorata. Esito negativo se i secondi frazionari sono diversi da zero. Compatibile con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||Time(7)|SQL_C_TIME|Si verifica un errore: valore letterale di ora non valida.|OK (1)|  
|||SQL_C_TYPE_TIMESTAMP|Si verifica un errore: valore letterale di ora non valida.|OK (1)|  
||Datetime2 (3)|SQL_C_TYPE_TIMESTAMP|OK|OK (1)|  
||datetime2(7)|SQL_C_TYPE_TIMESTAMP|OK|Il valore viene arrotondato a 1/300 di secondo dalla conversione client.|  
|Smalldatetime|Date|SQL_C_TYPE_DATE|OK|OK|  
|||SQL_C_TYPE_TIMESTAMP|Campi dell'ora impostati su zero.|OK (2)<br /><br /> Esito negativo se il campo dell'ora è diverso da zero. Compatibile con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||Time(0)|SQL_C_TYPE_TIME|OK|OK|  
|||SQL_C_TYPE_TIMESTAMP|Campi della data impostati sulla data corrente.|OK (2)<br /><br /> La data viene ignorata. Esito negativo se i secondi frazionari sono diversi da zero.<br /><br /> Compatibile con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||datetime2(0)|SQL_C_TYPE_TIMESTAMP|OK|OK|  
  
## <a name="key-to-symbols"></a>Descrizione dei simboli  
  
|Simbolo|Significato|  
|------------|-------------|  
|1|Un funzionamento corretto in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] corrisponde a un corretto funzionamento in una versione più recente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|2|Un'applicazione che funziona correttamente in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] potrebbe non essere eseguita correttamente in una versione più recente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
 Si noti che sono state prese in considerazione solo le modifiche dello schema comuni, elencate di seguito:  
  
-   Utilizzo di un nuovo tipo nei casi in cui logicamente un'applicazione richiede solo un valore di data o di ora. Nelle versioni precedenti viene imposto l'utilizzo di datetime o smalldatetime all'applicazione in quanto non sono disponibili tipi di data e ora distinti.  
  
-   Utilizzo di un nuovo tipo per ottenere precisione o accuratezza maggiore nei secondi frazionari.  
  
-   Passaggio a datetime2 in quanto tipo di dati preferito per la data e l'ora.  
  
### <a name="column-metadata-returned-by-sqlcolumns-sqlprocedurecolumns-and-sqlspecialcolumns"></a>Metadati di colonna restituiti da SQLColumns, SQLProcedureColumns e SQLSpecialColumns  
 Per i tipi di data/ora vengono restituiti i valori di colonna seguenti:  
  
|Tipo di colonna|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|-----------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_WVARCHAR|SQL_WVARCHAR|  
|TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|COLUMN_SIZE|10|8,10..16|16|23|19, 21..27|26, 28..34|  
|BUFFER_LENGTH|20|16, 20..32|16|16|38, 42..54|52, 56..68|  
|DECIMAL_DIGITS|NULL|NULL|0|3|NULL|NULL|  
|SQL_DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_DATETIME|SQL_DATETIME|SQL_WVARCHAR|SQL_WVARCHAR|  
|SQL_DATETIME_SUB|NULL|NULL|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|NULL|NULL|  
|CHAR_OCTET_LENGTH|NULL|NULL|NULL|NULL|NULL|NULL|  
|SS_DATA_TYPE|0|0|111|111|0|0|  
  
 SQLSpecialColumns non restituisce SQL_DATA_TYPE, SQL_DATETIME_SUB, CHAR_OCTET_LENGTH o SS_DATA_TYPE.  
  
### <a name="data-type-metadata-returned-by-sqlgettypeinfo"></a>Metadati del tipo di dati restituiti da SQLGetTypeInfo  
 Per i tipi di data/ora vengono restituiti i valori di colonna seguenti:  
  
|Tipo di colonna|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|-----------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_WVARCHAR|SQL_WVARCHAR|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|'|'|'|'|'|'|  
|LITERAL_SUFFIX|'|'|'|'|'|'|  
|CREATE_PARAMS|NULL|NULL|NULL|NULL|NULL|NULL|  
|NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|  
|CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|AUTO_UNIQUE_VALUE|NULL|NULL|NULL|NULL|NULL|NULL|  
|LOCAL_TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|NULL|0|3|NULL|NULL|  
|MAXIMUM_SCALE|NULL|NULL|0|3|NULL|NULL|  
|SQL_DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_DATETIME|SQL_DATETIME|SQL_WVARCHAR|SQL_WVARCHAR|  
|SQL_DATETIME_SUB|NULL|NULL|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|NULL|NULL|  
|NUM_PREC_RADIX|NULL|NULL|NULL|NULL|NULL|NULL|  
|INTERVAL_PRECISION|NULL|NULL|NULL|NULL|NULL|NULL|  
|USERTYPE|0|0|12|22|0|0|  
  
## <a name="down-level-server-behavior"></a>Comportamento dei server legacy  
 In caso di connessione a un'istanza del server di una versione precedente a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], qualsiasi tentativo di utilizzo di nuovi tipi di server o codici di metadati e campi di descrizione associati provocherà la restituzione di SQL_ERROR. Verrà generato un record di diagnostica con SQLSTATE HY004 e il messaggio "Tipo di dati non valido per la versione del server in connessione" o con 07006 e il messaggio "Violazione dell'attributo del tipo di dati".  
  
## <a name="see-also"></a>Vedere anche  
 [Data e miglioramenti per la fase &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
