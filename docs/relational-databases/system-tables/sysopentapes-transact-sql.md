---
description: sysopentapes (Transact-SQL)
title: sysopentapes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysopentapes
- sysopentapes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], sysopentapes system table
- sysopentapes system table
ms.assetid: c066ca9b-9cfd-46b1-90a3-5c8dc9e7b6ae
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5a64ea925775daacdbd44a71a945e86fe0f2c9aa
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537906"
---
# <a name="sysopentapes-transact-sql"></a>sysopentapes (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene una riga per ogni dispositivo nastro attualmente aperto. Questa vista è archiviata nel database **Master** .  
  
> [!IMPORTANT]  
>  Questa tabella di sistema è disponibile come vista per la compatibilità con le versioni precedenti. Utilizzare invece la vista [a gestione dinamica&#41;Transact-SQL &#40;sys. dm_io_backup_tapes ](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md) .  
  
> [!NOTE]  
>  Non è possibile eliminare la visualizzazione **sysopentapes** .  

  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**openTape**|**nvarchar (64)**|Nome di file fisico del dispositivo nastro aperto. Per ulteriori informazioni sull'apertura e il rilascio di dispositivi nastro, vedere [BACKUP &#40;Transact-sql&#41;](../../t-sql/statements/backup-transact-sql.md) e [Restore &#40;transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).|  
  
## <a name="permissions"></a>Autorizzazioni  
 L'utente deve disporre dell'autorizzazione VIEW SERVER STATE nel server.  
  
  
