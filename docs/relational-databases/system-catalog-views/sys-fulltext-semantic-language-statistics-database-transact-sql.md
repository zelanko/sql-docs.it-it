---
title: sys. fulltext_semantic_language_statistics_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_semantic_language_statistics_database_TSQL
- fulltext_semantic_language_statistics_database_TSQL
- fulltext_semantic_language_statistics_database
- sys.fulltext_semantic_language_statistics_database
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_semantic_language_statistics_database catalog view
ms.assetid: 32e95614-ed88-4068-8c37-1e21544717bc
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 993715676a6abd5d6687b7b1adbbeb3ab121d39f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85764686"
---
# <a name="sysfulltext_semantic_language_statistics_database-transact-sql"></a>sys.fulltext_semantic_language_statistics_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Restituisce una riga sul database di statistiche lingua semantica installato nell'istanza corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 È possibile eseguire una query su questa vista per individuare il componente delle statistiche sulla lingua per l'indicizzazione semantica necessario per l'elaborazione semantica.  
   
  
||||  
|-|-|-|  
|**Nome colonna**|**Tipo**|**Descrizione**|  
|**database_id**|**int**|ID del database, univoco all'interno di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**register_date**|**datetime**|Data in cui il database è stato registrato per l'elaborazione semantica.|  
|**registered_by**|**int**|ID dell'entità server che ha registrato il database per l'elaborazione semantica.|  
|**version**|**nvarchar(128)**|Informazioni sulla versione più recente specifiche per il database di statistiche lingua semantica.|  
  
## <a name="general-remarks"></a>Osservazioni generali  
 Per altre informazioni, vedere [Installazione e configurazione della ricerca semantica](../../relational-databases/search/install-and-configure-semantic-search.md).  
  
## <a name="metadata"></a>Metadati  
 Per informazioni sulle lingue supportate per l'indicizzazione semantica, eseguire una query sulla vista del catalogo [sys. fulltext_semantic_languages &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md).  
  
## <a name="security"></a>Sicurezza  
  
### <a name="permissions"></a>Autorizzazioni  
 La visibilità dei metadati nelle viste del catalogo è limitata alle entità a protezione diretta di cui l'utente è proprietario o per le quali dispone di autorizzazioni.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato come eseguire una query su **sys. fulltext_semantic_language_statistics_database** per ottenere informazioni sul database di statistiche lingua semantica registrato nell'istanza corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
```  
SELECT * FROM sys.fulltext_semantic_language_statistics_database;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Installazione e configurazione della ricerca semantica](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
