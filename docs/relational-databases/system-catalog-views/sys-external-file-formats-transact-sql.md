---
title: sys. external_file_formats (Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 75e3f884e09d41c2ae7aa5c7610b0c7ac24691a7
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828515"
---
# <a name="sysexternal_file_formats-transact-sql"></a>sys. external_file_formats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contiene una riga per ogni formato di file esterno nel database corrente per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssSDS](../../includes/sssds-md.md)] e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] .  
  
 Contiene una riga per ogni formato di file esterno nel server per [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] .  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|file_format_id|**int**|ID oggetto per il formato di file esterno.||  
|name|**sysname**|Nome del formato di file. in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] è univoco per il database. In [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] è univoco per il server.||  
|format_type|**tinyint**|Tipo di formato di file.|DELIMITEDTEXT, RCFILE, ORC, PARQUET|  
|field_terminator|**nvarchar (10)**|Per format_type = DELIMITEDTEXT, questo è il carattere di terminazione del campo.||  
|string_delimiter|**nvarchar (10)**|Per format_type = DELIMITEDTEXT, questo è il delimitatore di stringa.||  
|date_format|**nvarchar(50)**|Per format_type = DELIMITEDTEXT, questo è il formato di data e ora definito dall'utente.||  
|use_type_default|**bit**|Per format_type = testo delimitato, specifica come gestire i valori mancanti durante l'importazione di dati da file di testo HDFS in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] .|0-archivia i valori mancanti come stringa ' NULL '.<br /><br /> 1-archivia i valori mancanti come valore predefinito della colonna.|  
|serde_method|**nvarchar(255)**|Per format_type = RCFILE, si tratta del metodo di serializzazione/deserializzazione.||  
|row_terminator|**nvarchar (10)**|Per format_type = DELIMITEDTEXT, si tratta della stringa di caratteri che termina ogni riga nel file Hadoop esterno.|Sempre "\n".|  
|codifica|**nvarchar (10)**|Per format_type = DELIMITEDTEXT, questo è il metodo di codifica per il file Hadoop esterno.|Sempre "UTF8".|  
|data_compression|**nvarchar(255)**|Metodo di compressione dati per i dati esterni.|Per format_type = DELIMITEDTEXT:<br /><br /> -' org. Apache. Hadoop. io. Compress. DefaultCodec '<br />-' org. Apache. Hadoop. io. Compress. GzipCodec '<br /><br /> Per format_type = RCFILE:<br /><br /> -' org. Apache. Hadoop. io. Compress. DefaultCodec '<br /><br /> Per format_type = ORC:<br /><br /> -' org. Apache. Hadoop. io. Compress. DefaultCodec '<br />-' org. Apache. Hadoop. io. Compress. SnappyCodec '<br /><br /> Per format_type = PARQUET:<br /><br /> -' org. Apache. Hadoop. io. Compress. GzipCodec '<br />-' org. Apache. Hadoop. io. Compress. SnappyCodec '|  
  
## <a name="permissions"></a>Autorizzazioni  
 La visibilità dei metadati nelle viste del catalogo è limitata alle entità a protezione diretta di cui l'utente è proprietario o per le quali dispone di autorizzazioni.  Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [sys. external_data_sources &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [sys. external_tables &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  
