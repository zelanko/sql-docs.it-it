---
title: sys.syscharsets (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.syscharsets
- syscharsets
- sys.syscharsets_TSQL
- syscharsets_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syscharsets system table
- sys.syscharsets compatibility view
ms.assetid: f16d987c-bd19-4668-9ef7-785b8fb9ff5b
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 141a57db220be9d415febc5722eb34e313d6830f
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009964"
---
# <a name="syssyscharsets-transact-sql"></a>sys.syscharsets (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Contiene una riga per ogni set di caratteri e tipo di ordinamento definito per l'utilizzo in [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Uno degli ordinamenti è contrassegnato in **sysconfigures** come ordinamento predefinito. ed è l'unico effettivamente utilizzato.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**type**|**smallint**|Tipo di entità rappresentata dalla riga:<br /><br /> 1001 = Set di caratteri.<br /><br /> 2001 = Tipo di ordinamento.|  
|**id**|**tinyint**|ID univoco del set di caratteri o del tipo di ordinamento. I tipi di ordinamento e i set di caratteri non possono condividere lo stesso numero ID. L'intervallo di ID compreso tra 1 e 240 è riservato per l'utilizzo in [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|**csid**|**tinyint**|Se la riga rappresenta un set di caratteri, questo campo non viene utilizzato. Se la riga rappresenta un tipo di ordinamento, questo campo contiene l'ID del set di caratteri in base al quale viene compilato il tipo di ordinamento. Si suppone che nella tabella esista una riga di set di caratteri a cui è associato questo ID.|  
|**Stato**|**smallint**|Bit interni di informazioni sullo stato del sistema.|  
|**nome**|**sysname**|Nome univoco del set di caratteri o del tipo di ordinamento. Questo campo può contenere solo lettere dalla A alla Z (maiuscole e minuscole), numeri da 0 a 9 e caratteri di sottolineatura (_) e deve iniziare con una lettera.|  
|**Descrizione**|**nvarchar(255)**|Descrizione facoltativa delle funzionalità del set di caratteri o del tipo di ordinamento.|  
|**binarydefinition**|**varbinary(6000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**definizione**|**image**|Definizione interna del set di caratteri o del tipo di ordinamento. La struttura dei dati in questo campo dipende dal tipo.|  
  
## <a name="see-also"></a>Vedere anche  
 [Mapping di tabelle di sistema a viste di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Viste della compatibilità &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
