---
title: Sys. filetables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- filetables
- filetables_TSQL
- sys.filetables
- sys.filetables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.filetables catalog view
ms.assetid: a740be59-cd52-4707-9ad2-5203669a63ac
author: stevestein
ms.author: sstein
ms.openlocfilehash: 791bba2f5ec1830e343acff24fd55628a3f13d2e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133995"
---
# <a name="sysfiletables-transact-sql"></a>sys.filetables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Viene restituita una riga per ogni oggetto FileTable in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Per altre informazioni sugli oggetti FileTable, vedere [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md).    
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**object_id**||Numero di identificazione dell'oggetto. Valore univoco all'interno di un database.<br /><br /> Per altre informazioni, [Sys. Objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**is_enabled**|**bit**|1 = Lo stato dell'oggetto FileTable è "abilitato".|  
|**directory_name**|**varchar(255)**|Nome della directory radice per un oggetto FileTable.|  
|**filename_collation_id**||Identificatore delle regole di confronto definito per l'oggetto FileTable.|  
|**filename_collation_name**||Nome delle regole di confronto definito per l'oggetto FileTable.|  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire tabelle Filetable](../../relational-databases/blob/manage-filetables.md)   
 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  
  
  
