---
title: sys. sp_rda_get_rpo_duration (Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d1e89e4901cf8e0bb5674038bfd8fe74bc637511
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82814763"
---
# <a name="syssp_rda_get_rpo_duration-transact-sql"></a>sys. sp_rda_get_rpo_duration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Ottiene il numero di ore di dati migrati che SQL Server conserva in una tabella di staging per garantire un ripristino completo del database di Azure remoto, se è necessario un ripristino temporizzato. 
  
  Per altre informazioni, vedere [Stretch database riduce il rischio di perdita di dati per i dati di Azure mantenendo temporaneamente le righe migrate](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO).  
    
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>Sintassi    
    
```    
    
sp_rda_get_rpo_duration @durationinhours output    
    
```    
    
## <a name="output-parameter"></a>Parametro di output    
 *\@durationinhours*    
  Numero di ore (valore intero non null) dei dati migrati che SQL Server conserva per il database abilitato per l'estensione corrente.    
    
## <a name="permissions"></a>Autorizzazioni    
 Richiede autorizzazioni db_owner.    
    
## <a name="remarks"></a>Commenti    
 Modificare il valore eseguendo [sys. sp_rda_set_rpo_duration &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md).    
    
## <a name="see-also"></a>Vedere anche    
 [sys. sp_rda_set_rpo_duration &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md)     
 [Ripristinare i database abilitati per Stretch (Stretch Database)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)    
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)    
    
  
