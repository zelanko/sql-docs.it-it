---
title: sys.external_file_formats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a89efb2c-0a3a-4b64-9284-6e93263e29ac
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b16deb7ed2bd43cc45966d27b79729897e76405c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52532363"
---
# <a name="sysexternalfileformats-transact-sql"></a>sys.external_file_formats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contiene una riga per ogni formato di file esterno nel database corrente per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)], e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
 Contiene una riga per ogni formato di file esterno nel server per [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|file_format_id|**int**|ID oggetto per il formato di file esterno.||  
|NAME|**sysname**|Nome del formato di file. nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], questo valore è univoco per il database. In [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], questo valore è univoco per il server.||  
|format_type|**tinyint**|Il tipo di formato di file.|DELIMITEDTEXT, RCFILE, ORC, PARQUET|  
|carattere_terminazione_campo|**nvarchar(10)**|Per format_type = DELIMITEDTEXT, questo è il carattere di terminazione del campo.||  
|string_delimiter|**nvarchar(10)**|Per format_type = DELIMITEDTEXT, questo è il delimitatore di stringa.||  
|date_format|**nvarchar(50)**|Per format_type = DELIMITEDTEXT, si tratta della data definito dall'utente e il formato dell'ora.||  
|use_type_default|**bit**|Per format_type = delimitato da testo: specifica come gestire valori mancanti quando PolyBase sta importando dati da file di testo HDFS in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].|0 - archiviare i valori mancanti come stringa 'NULL'.<br /><br /> 1: archiviare i valori mancanti come il valore predefinito della colonna.|  
|serde_method|**nvarchar(255)**|Per format_type = RCFILE, si tratta del metodo di serializzazione/deserializzazione.||  
|carattere_terminazione_riga|**nvarchar(10)**|Per format_type = DELIMITEDTEXT, questa è la stringa di carattere che interrompe ogni riga nel file Hadoop esterno.|Sempre '\n'.|  
|codifica|**nvarchar(10)**|Per format_type = DELIMITEDTEXT, si tratta del metodo di codifica per il file Hadoop esterno.|Sempre 'UTF8'.|  
|data_compression|**nvarchar(255)**|Il metodo di compressione dei dati per i dati esterni.|Per format_type = DELIMITEDTEXT:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br />-   'org.apache.hadoop.io.compress.GzipCodec'<br /><br /> Per format_type = RCFILE:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br /><br /> Per format_type = ORC:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br />-   'org.apache.hadoop.io.compress.SnappyCodec'<br /><br /> Per format_type = PARQUET:<br /><br /> -   'org.apache.hadoop.io.compress.GzipCodec'<br />-   'org.apache.hadoop.io.compress.SnappyCodec'|  
  
## <a name="permissions"></a>Permissions  
 La visibilità dei metadati nelle viste del catalogo è limitata alle entità a protezione diretta di cui l'utente è proprietario o per le quali dispone di autorizzazioni. Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [sys.external_data_sources &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [sys.external_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  
