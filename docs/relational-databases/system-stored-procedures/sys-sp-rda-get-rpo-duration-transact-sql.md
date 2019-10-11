---
title: sys.sp_rda_get_rpo_duration (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_get_rpo_duration
- sys.sp_rda_get_rpo_duration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_get_rpo_duration stored procedure
ms.assetid: 35882067-3072-47ff-9024-ca453c0f49a7
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 715ceb531f2334f4cf9580c630d922f45faae74e
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252067"
---
# <a name="syssp_rda_get_rpo_duration-transact-sql"></a>sys.sp_rda_get_rpo_duration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Ottiene il numero di ore di dati migrati che SQL Server conserva in una tabella di staging per garantire un ripristino completo del database di Azure remoto, se è necessario un ripristino temporizzato. 
  
  Per altre informazioni, vedere [Stretch database riduce il rischio di perdita di dati per i dati di Azure mantenendo temporaneamente le righe migrate](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO).  
    
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>Sintassi    
    
```    
    
sp_rda_get_rpo_duration @durationinhours output    
    
```    
    
## <a name="output-parameter"></a>Parametro di output    
 *\@durationinhours*    
  Numero di ore (valore intero non null) dei dati migrati che SQL Server conserva per il database abilitato per l'estensione corrente.    
    
## <a name="permissions"></a>Permissions    
 Richiede autorizzazioni db_owner.    
    
## <a name="remarks"></a>Note    
 Modificare il valore eseguendo [sys. sp_rda_set_rpo_duration &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md).    
    
## <a name="see-also"></a>Vedere anche    
 [sys.sp_rda_set_rpo_duration &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md)     
 [Ripristinare i database abilitati per Stretch (stretch database)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)    
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)    
    
  
