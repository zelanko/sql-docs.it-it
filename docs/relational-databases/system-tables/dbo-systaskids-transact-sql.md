---
title: dbo.sysTaskIDs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- systaskids_TSQL
- dbo.systaskids
- systaskids
- dbo.systaskids_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- systaskids system table
ms.assetid: 45c56d89-4160-4d84-80bf-a7a05488792d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2efb1920074ab0a15c14f1910cf8eb03ed3ef1f2
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890339"
---
# <a name="dbosystaskids-transact-sql"></a>dbo.systaskids (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene un mapping delle attività create in versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] su processi di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] nella versione corrente. Questa tabella è archiviata nel database **msdb** .  
  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**task_id**|**int**|ID dell'attività|  
|**job_id**|**uniqueidentifier**|ID del processo a cui si esegue il mapping dell'attività|  
  
  
