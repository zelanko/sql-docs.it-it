---
description: MSreplication_objects (Transact-SQL)
title: MSreplication_objects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_objects
- MSreplication_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_objects system table
ms.assetid: 08f9710d-976d-448e-bead-ac9835e87bc5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d3c582b495702a46c51519f56dee1e977980840f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538268"
---
# <a name="msreplication_objects-transact-sql"></a>MSreplication_objects (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabella **MSreplication_objects** contiene una riga per ogni oggetto associato alla replica nel database del Sottoscrittore. Questa tabella è archiviata nel database di sottoscrizione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**pubblicazione**|**sysname**|Nome del server di pubblicazione.|  
|**publisher_db**|**sysname**|Nome del database del server di pubblicazione.|  
|**pubblicazione**|**sysname**|Nome della pubblicazione.|  
|**object_name**|**sysname**|Nome dell'oggetto.|  
|**object_type**|**char(2)**|Tipo di oggetto:<br /><br /> **u** = tabella.<br /><br /> **t** = trigger.<br /><br /> **p** = stored procedure.|  
|**articolo**|**sysname**|Nome dell'articolo a cui è associato l'oggetto.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
