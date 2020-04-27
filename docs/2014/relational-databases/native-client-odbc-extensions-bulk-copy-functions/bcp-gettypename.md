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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
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
|`SQLDECIMAL`|Prima o dopo|**decimal**|  
|`SQLNUMERIC`|Prima o dopo|**numeric**|  
|`SQLINT1`|Prima o dopo|**tinyint**|  
|`SQLINT2`|Prima o dopo|**smallint**|  
|`SQLINT4`|Prima o dopo|**int**|  
|`SQLMONEY`|Prima o dopo|**money**|  
|`SQLFLT8`|Prima o dopo|**float**|  
|`SQLDATETIME`|Prima o dopo|**datetime**|  
|`SQLBITN`|Prima o dopo|**bit-null**|  
|`SQLBIT`|Prima o dopo|**bit**|  
|`SQLBIGCHAR`|No|**char**|  
|`SQLCHARACTER`|No|**char**|  
|`SQLBIGVARCHAR`|No|**varchar**|  
|`SQLVARCHAR`|No|**varchar**|  
|`SQLTEXT`|Prima o dopo|**text**|  
|`SQLBIGBINARY`|No|**binary**|  
|`SQLBINARY`|No|**Binario**|  
|`SQLBIGVARBINARY`|No|**Varbinary**|  
|`SQLVARBINARY`|No|**Varbinary**|  
|`SQLIMAGE`|Prima o dopo|**Immagine**|  
|`SQLINTN`|Prima o dopo|**int-null**|  
|`SQLDATETIMN`|Prima o dopo|**datetime-null**|  
|`SQLMONEYN`|Prima o dopo|**money-null**|  
|`SQLFLTN`|Prima o dopo|**float-null**|  
|`SQLAOPSUM`|Prima o dopo|**Somma**|  
|`SQLAOPAVG`|Prima o dopo|**AVG**|  
|`SQLAOPCNT`|Prima o dopo|**Numero**|  
|`SQLAOPMIN`|Prima o dopo|**Min**|  
|`SQLAOPMAX`|Prima o dopo|**Max**|  
|`SQLDATETIM4`|Prima o dopo|**smalldatetime**|  
|`SQLMONEY4`|Prima o dopo|**Smallmoney**|  
|`SQLFLT4`|Prima o dopo|**Reale**|  
|`SQLUNIQUEID`|Prima o dopo|**uniqueidentifier**|  
|`SQLNCHAR`|No|**Nchar**|  
|`SQLNVARCHAR`|No|**Nvarchar**|  
|`SQLNTEXT`|Prima o dopo|**Ntext**|  
|`SQLVARIANT`|Prima o dopo|**sql_variant**|  
|`SQLINT8`|Prima o dopo|**Bigint**|  
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
|`SQLUDT`|Prima o dopo|**UDT**|  
  
## <a name="bcp_gettypename-support-for-enhanced-date-and-time-features"></a>Supporto di bcp_gettypename per le caratteristiche avanzate di data e ora  
 I valori dei parametri del token per i tipi data/ora vengono descritti nella colonna "tipo in sqlncli. h" della tabella nelle [modifiche della copia bulk per i tipi di data e ora avanzati &#40;OLE DB e ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md). Il valore restituito si trova nella riga corrispondente della colonna "Tipo di archiviazione di file".  
  
 Per ulteriori informazioni, vedere [miglioramenti di data e ora &#40;&#41;ODBC ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Funzioni di copia bulk](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
