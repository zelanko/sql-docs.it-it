---
description: sys.parameter_xml_schema_collection_usages (Transact-SQL)
title: sys.parameter_xml_schema_collection_usages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.parameter_xml_schema_collection_usages
- parameter_xml_schema_collection_usages
- parameter_xml_schema_collection_usages_TSQL
- sys.parameter_xml_schema_collection_usages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.parameter_xml_schema_collection_usages catalog view
ms.assetid: bffb91a3-492c-4375-bd2a-db8fc1a3ace4
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0c309fa0c801787c464d294b12f5bc5a8e9cd6af
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461622"
---
# <a name="sysparameter_xml_schema_collection_usages-transact-sql"></a>sys.parameter_xml_schema_collection_usages (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Restituisce una riga per ogni parametro convalidato da uno XML Schema.  
  
 |Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID dell'oggetto a cui appartiene il parametro.|  
|**parameter_id**|**int**|ID del parametro.  Valore univoco all'interno dell'oggetto.|  
|**xml_collection_id**|**int**|ID della raccolta di XML Schema contenente lo spazio dei nomi di XML Schema di convalida per il parametro.|  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML Schema &#40;viste del catalogo&#41; di sistema di tipo XML &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
