---
title: Sys. sp_xtp_merge_checkpoint_files (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_merge_checkpoint_files_TSQL
- sys.sp_xtp_merge_checkpoint_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_merge_checkpoint_files
ms.assetid: da04df2a-f7a1-41e7-a1ef-2d5d68919892
author: stevestein
ms.author: sstein
ms.openlocfilehash: 73638d41c7a24a37c068d365771b4d0469a174d5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041020"
---
# <a name="sysspxtpmergecheckpointfiles-transact-sql"></a>sys.sp_xtp_merge_checkpoint_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  **Sys. sp_xtp_merge_checkpoint_files** unisce tutti i file di dati e differenziali nell'intervallo di transazione specificato.  
  
 Per altre informazioni, vedere [creazione e la gestione dell'archiviazione per gli oggetti ottimizzati per la memoria](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
||  
|-|  
|**Nota**: Questa stored procedure è deprecata in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Non è più necessario e non può essere usata, a partire dal [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].|  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.sp_xtp_merge_checkpoint_files database_name, @transaction_lower_bound, @transaction_upper_bound  
[;]  
```  
  
## <a name="arguments"></a>Argomenti  
 *database_name*  
 Nome del database in cui richiamare l'unione. Se il database non include tabelle in memoria, questa stored procedure restituisce un errore utente. Se il database è offline, restituisce un errore.  
  
 *lower_bound_Tid*  
 Il limite inferiore (bigint) delle transazioni per un file di dati, come illustrato nella [DM db_xtp_checkpoint_files &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md) corrispondente al file di checkpoint di inizio dell'unione. Viene generato un errore per un valore transactionId non valido.  
  
 *upper_bound_Tid*  
 Il limite superiore (bigint) delle transazioni per un file di dati, come illustrato nella [DM db_xtp_checkpoint_files &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md). Viene generato un errore per un valore transactionId non valido.  
  
## <a name="return-code-values"></a>Valori restituiti  
 Nessuna  
  
## <a name="cursors-returned"></a>Cursori restituiti  
 Nessuna  
  
## <a name="permissions"></a>Permissions  
 È richiesto il ruolo predefinito del server sysadmin e il ruolo predefinito del database db_owner.  
  
## <a name="remarks"></a>Note  
 Unisce tutti i dati e i file differenziali nell'intervallo valido per produrre un singolo dato e un file differenziale. Questa stored procedure non rispetta i criteri di unione.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [OLTP in memoria &#40;ottimizzazione per la memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
