---
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 813592ffa5b67a4926dff611c2ba0e0faf36d273
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029804"
---
# <a name="sysopentapes-transact-sql"></a>sysopentapes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni dispositivo nastro attualmente aperto. Questa vista è archiviata nel **master** database.  
  
> [!IMPORTANT]  
>  Questa tabella di sistema è disponibile come vista per la compatibilità con le versioni precedenti. Usare invece i [DM io_backup_tapes &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md) vista a gestione dinamica.  
  
> [!NOTE]  
>  Non è possibile eliminare il **sysopentapes** visualizzazione.  

  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**openTape**|**nvarchar(64)**|Nome di file fisico del dispositivo nastro aperto. Per altre informazioni sull'apertura e il rilascio di dispositivi nastro, vedere [BACKUP &#40;Transact-SQL&#41; ](../../t-sql/statements/backup-transact-sql.md) e [ripristinare &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).|  
  
## <a name="permissions"></a>Permissions  
 L'utente deve disporre dell'autorizzazione VIEW SERVER STATE nel server.  
  
  
