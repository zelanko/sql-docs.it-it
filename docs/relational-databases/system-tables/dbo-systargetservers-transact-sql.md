---
title: dbo. systargetservers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.systargetservers_TSQL
- dbo.systargetservers
- systargetservers_TSQL
- systargetservers
dev_langs:
- TSQL
helpviewer_keywords:
- systargetservers system table
ms.assetid: 479d1314-be37-4d19-ac9c-419fc9110e53
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6193bdfaaac12d34ed4993b71fd6b5862046384c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82813800"
---
# <a name="dbosystargetservers-transact-sql"></a>dbo.systargetservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra i server di destinazione integrati nel dominio multiserver specificato.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|ID del server.|  
|**server_name**|**sysname**|Nome del server.|  
|**location**|**nvarchar(200)**|Posizione del server di destinazione specificato.|  
|**time_zone_adjustment**|**int**|Regolazione del fuso orario in ore rispetto all'ora di Greenwich (GMT).|  
|**enlist_date**|**datetime**|Data e ora in cui il server di destinazione specificato è stato integrato.|  
|**last_poll_date**|**datetime**|Data e ora dell'ultimo polling del server di destinazione specificato nella tabella di sistema **sysdownloadlist** multiserver per l'esecuzione dei processi.|  
|**Stato**|**int**|Stato del server di destinazione:<br /><br /> **1** = normale<br /><br /> **2** = risincronizzazione in sospeso<br /><br /> **4** = sospetto offline|  
|**local_time_at_last_poll**|**datetime**|Data e ora dell'ultimo polling del server di destinazione per operazioni di processo.|  
|**enlisted_by_nt_user**|**nvarchar (100)**|Nome utente della persona che esegue **sp_msx_enlist** nel server di destinazione.|  
|**poll_internal**|**int**|Numero di secondi che deve trascorrere prima che il server di destinazione esegua il polling del server master per individuare nuove istruzioni di download.|  
  
  
