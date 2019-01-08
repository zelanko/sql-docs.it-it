---
title: MSrepl_version (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_version
- MSrepl_version_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_version system table
ms.assetid: c1330f03-940b-4564-ac42-6030c6e21173
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 94cb0913e8122997652786cd4bf09ddccf7fa433
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52775438"
---
# <a name="msreplversion-transact-sql"></a>MSrepl_version (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSrepl_version** tabella contiene una riga con la versione corrente della replica installata. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**versione_principale**|**int**|Numero di versione principale del database di distribuzione.|  
|**versione_secondaria**|**int**|Numero di versione secondario del database di distribuzione.|  
|**revisione**|**int**|Numero di revisione.|  
|**db_existed**|**bit**|Indica se il database di distribuzione esiste prima **sp_adddistributiondb** viene chiamato.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
