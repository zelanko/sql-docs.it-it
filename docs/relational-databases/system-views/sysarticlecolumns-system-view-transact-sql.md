---
title: sysarticlecolumns (vista di sistema) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticlecolumns
- sysarticlecolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticlecolumns view
ms.assetid: a8dd8d13-c827-45c4-87ba-802725301382
author: stevestein
ms.author: sstein
ms.openlocfilehash: 10467dfa991efbed27941ba31424057b721527d1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750129"
---
# <a name="sysarticlecolumns-system-view-transact-sql"></a>sysarticlecolumns (vista di sistema) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  La vista **sysarticlecolumns** espone informazioni aggiuntive sulle colonne negli articoli pubblicati. Questa vista è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Identifica un articolo.|  
|**colid**|**int**|Identifica una colonna di un articolo.|  
|**is_udt**|**int**|Indica se il tipo di dati della colonna è un tipo definito dall'utente (UDT). Il valore **1** indica una colonna con tipo definito dall'utente.|  
|**is_xml**|**int**|Indica se la colonna è una colonna **XML** . Il valore **1** indica una colonna **XML** .|  
|**is_max**|**int**|Indica se la colonna è una colonna con tipo di dati con valori di grandi dimensioni (**varchar (max)**, **nvarchar (max)** o **varbinary (max)**). Il valore **1** indica una colonna con valori di grandi dimensioni.|  
  
## <a name="see-also"></a>Vedere anche  
 [sp_articlecolumn &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;&#41;Transact-SQL](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
