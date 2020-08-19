---
description: dbo.syscategories (Transact-SQL)
title: Categorie di dbo.sys(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.syscategories_TSQL
- syscategories
- syscategories_TSQL
- dbo.syscategories
dev_langs:
- TSQL
helpviewer_keywords:
- syscategories system table
ms.assetid: eb2cb75c-dc58-4a5b-b329-664e9fe20ce0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1c4a0fd7272a859672b70742a8c79eb1ac6690a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446704"
---
# <a name="dbosyscategories-transact-sql"></a>dbo.syscategories (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene le categorie utilizzate da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per organizzare processi, avvisi e operatori. Questa tabella è archiviata nel database **msdb** .  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|ID della categoria.|  
|**category_class**|**int**|Tipo di elemento della categoria:<br /><br /> **1** = processo<br /><br /> **2** = avviso<br /><br /> **3** = (operatore)|  
|**category_type**|**tinyint**|Tipo di categoria:<br /><br /> **1** = locale<br /><br /> **2** = multiserver<br /><br /> **3** = nessuna|  
|**nome**|**sysname**|Nome della categoria.|  
  
  
