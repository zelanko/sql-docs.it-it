---
title: MSmerge_settingshistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_settingshistory
- MSmerge_settingshistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_settingshistory system table
ms.assetid: 0bdf2d5f-5502-44cd-aa9d-2d5006ad20ce
author: stevestein
ms.author: sstein
ms.openlocfilehash: d8cb78229ea20d5b4c1b01b17c9fef1d85ca83b9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68106325"
---
# <a name="msmerge_settingshistory-transact-sql"></a>MSmerge_settingshistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabella **MSmerge_settingshistory** viene utilizzata per mantenere una cronologia delle modifiche apportate alle proprietà degli articoli e delle pubblicazioni per la replica di tipo merge, con una riga per ogni modifica apportata a una topologia di replica di tipo merge. Nella tabella sono inoltre archiviate informazioni sulle impostazioni iniziali delle proprietà. Questa tabella è archiviata nei database di pubblicazione e di sottoscrizione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**EventTime**|**datetime**|Data e ora in cui è stato generato l'evento.|  
|**pubid**|**uniqueidentifier**|Identificatore univoco per la pubblicazione specificata.|  
|**artid**|**uniqueidentifier**|Identificatore univoco per l'articolo specificato.|  
|**EventType**|**tinyint**|Specifica il tipo di evento registrato. I possibili valori sono i seguenti:<br /><br /> **1** : impostazione della proprietà del livello di pubblicazione iniziale.<br /><br /> **2** -modifica di una proprietà di pubblicazione.<br /><br /> **101** -impostazione iniziale della proprietà dell'articolo.<br /><br /> **102** -modifica in una proprietà di articolo.|  
|**propertyname**|**sysname**|Nome della proprietà impostata o modificata.|  
|**previousvalue**|**sysname**|Valore precedente di una proprietà modificata.|  
|**NewValue**|**sysname**|Valore con cui viene modificata o creata la proprietà.|  
|**eventtext**|**nvarchar (2000)**|Stringa di caratteri che descrive l'evento.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
