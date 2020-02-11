---
title: bcp_gettypename | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_gettypename
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_gettypename function
ms.assetid: 65f036d1-f60e-4b8a-97b3-76fccf0dfed4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5bc7caa063d14967e576fd009a23110b9647836b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62689025"
---
# <a name="bcp_gettypename"></a>bcp_gettypename
  Restituisce il nome del tipo SQL per il nome di un tipo di token specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RETCODE bcp_gettypename (  
INT   
token  
,  
DBBOOL   
fIsMaxType  
);  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *token*  
 Valore che indica un token di tipo BCP.  
  
 *campo*  
 Indica se il token richiesto è un tipo max.  
  
## <a name="returns"></a>Valori di codice restituiti  
 Una stringa che contiene il nome del tipo SQL che corrisponde al tipo BCP. Se viene specificato un tipo BCP non valido, viene restituita una stringa vuota.  
  
## <a name="remarks"></a>Osservazioni  
 I token del tipo BCP vengono definiti nel file di intestazione sqlncli.h e nella libreria sqlncli11.lib.  
  
 Nella tabella seguente viene specificato quali sono i possibili tipi BCP, se si tratta di tipi max e l'output previsto.  
  
|Nome del tipo BCP|MaxType|Output|  
|-------------------|-------------|------------|  
|`SQLDECIMAL`|È possibile usare il|**decimal**|  
|`SQLNUMERIC`|È possibile usare il|**numerico**|  
|`SQLINT1`|È possibile usare il|**tinyint**|  
|`SQLINT2`|È possibile usare il|**smallint**|  
|`SQLINT4`|È possibile usare il|**int**|  
|`SQLMONEY`|È possibile usare il|**money**|  
|`SQLFLT8`|È possibile usare il|**float**|  
|`SQLDATETIME`|È possibile usare il|**datetime**|  
|`SQLBITN`|È possibile usare il|**bit-null**|  
|`SQLBIT`|È possibile usare il|**bit**|  
|`SQLBIGCHAR`|No|**char**|  
|`SQLCHARACTER`|No|**char**|  
|`SQLBIGVARCHAR`|No|**varchar**|  
|`SQLVARCHAR`|No|**varchar**|  
|`SQLTEXT`|È possibile usare il|**text**|  
|`SQLBIGBINARY`|No|**BINARY**|  
|`SQLBINARY`|No|**Binario**|  
|`SQLBIGVARBINARY`|No|**Varbinary**|  
|`SQLVARBINARY`|No|**Varbinary**|  
|`SQLIMAGE`|È possibile usare il|**Immagine**|  
|`SQLINTN`|È possibile usare il|**int-null**|  
|`SQLDATETIMN`|È possibile usare il|**datetime-null**|  
|`SQLMONEYN`|È possibile usare il|**money-null**|  
|`SQLFLTN`|È possibile usare il|**float-null**|  
|`SQLAOPSUM`|È possibile usare il|**Somma**|  
|`SQLAOPAVG`|È possibile usare il|**AVG**|  
|`SQLAOPCNT`|È possibile usare il|**Conteggio**|  
|`SQLAOPMIN`|È possibile usare il|**Min**|  
|`SQLAOPMAX`|È possibile usare il|**Max**|  
|`SQLDATETIM4`|È possibile usare il|**smalldatetime**|  
|`SQLMONEY4`|È possibile usare il|**Smallmoney**|  
|`SQLFLT4`|È possibile usare il|**Real**|  
|`SQLUNIQUEID`|È possibile usare il|**uniqueidentifier**|  
|`SQLNCHAR`|No|**Nchar**|  
|`SQLNVARCHAR`|No|**Nvarchar**|  
|`SQLNTEXT`|È possibile usare il|**Ntext**|  
|`SQLVARIANT`|È possibile usare il|**sql_variant**|  
|`SQLINT8`|È possibile usare il|**Bigint**|  
|`SQLCHARACTER`|Sì|**ntext**|  
|`SQLBIGCHAR`|Sì|**ntext**|  
|`SQLBIGVARCHAR`|Sì|**ntext**|  
|`SQLVARCHAR`|Sì|**ntext**|  
|`SQLBINARY`|Sì|**varbinary(max)**|  
|`SQLBIGBINARY`|Sì|**varbinary(max)**|  
|`SQLBIGVARBINARY`|Sì|**varbinary(max)**|  
|`SQLVARBINARY`|Sì|**varbinary(max)**|  
|`SQLNCHAR`|Sì|**nvarchar(max)**|  
|`SQLNVARCHAR`|Sì|**nvarchar(max)**|  
|`SQLXML`|Sì|**XML**|  
|`SQLUDT`|È possibile usare il|**UDT**|  
  
## <a name="bcp_gettypename-support-for-enhanced-date-and-time-features"></a>Supporto di bcp_gettypename per le caratteristiche avanzate di data e ora  
 I valori dei parametri del token per i tipi data/ora vengono descritti nella colonna "tipo in sqlncli. h" della tabella nelle [modifiche della copia bulk per i tipi di data e ora avanzati &#40;OLE DB e ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md). Il valore restituito si trova nella riga corrispondente della colonna "Tipo di archiviazione di file".  
  
 Per ulteriori informazioni, vedere [miglioramenti di data e ora &#40;&#41;ODBC ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
