---
title: sys. server_assembly_modules (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_assembly_modules_TSQL
- sys.server_assembly_modules
- server_assembly_modules
- sys.server_assembly_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_assembly_modules catalog view
ms.assetid: af799e38-2d16-49b2-bcf5-6f9199af899e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a814539e3b04135a5d97ad4d4d7b31546c88e62d
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832739"
---
# <a name="sysserver_assembly_modules-transact-sql"></a>sys.server_assembly_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni modulo in assembly per i trigger a livello di server di tipo TA. Questa vista esegue il mapping tra trigger di assembly e l'implementazione CLR sottostante. È possibile unire in join questa relazione a **sys. server_triggers**. L'assembly deve essere caricato nel database **Master** . La tuple (object_id) è la chiave della relazione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Riferimento FOREIGN KEY all'oggetto in base a cui è stato definito questo modulo in assembly.|  
|**assembly_id**|**int**|ID dell'assembly da cui è stato creato questo modulo. L'assembly deve essere caricato nel database master.|  
|**assembly_class**|**sysname**|Nome della classe all'interno dell'assembly che definisce questo modulo.|  
|**assembly_method**|**sysname**|Nome del metodo all'interno della classe che definisce questo modulo. Questo valore è NULL per le funzioni di aggregazione.|  
|**execute_as_principal_id**|**int**|ID dell'entità server EXECUTE AS.<br /><br /> Questo valore è NULL per impostazione predefinita e se viene utilizzato EXECUTE AS CALLER.<br /><br /> ID dell'entità specificata se EXECUTE AS SELF EXECUTE AS \< principal>.<br /><br /> -2 = EXECUTE AS OWNER.|  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Viste del catalogo dell'oggetto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
