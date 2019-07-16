---
title: Sys.sp_xtp_checkpoint_force_garbage_collection (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_checkpoint_force_garbage_collection_TSQL
- sys.sp_xtp_checkpoint_force_garbage_collection
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_checkpoint_force_garbage_collection
ms.assetid: 82b35b2b-edbd-44ac-9fc8-80695f2fd1df
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3b230fb659b41f16541fd841f1ff8b6f03d19cee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120042"
---
# <a name="sysspxtpcheckpointforcegarbagecollection-transact-sql"></a>sys.sp_xtp_checkpoint_force_garbage_collection (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Contrassegna i file di origine utilizzati durante l'operazione di merge con il numero di sequenza del file di log (LSN) che quindi diventano non necessari e possono essere sottoposti a Garbage Collection. Inoltre, sposta i file con un LSN associato inferiore al punto di troncamento del log nel Garbage Collection di FILESTREAM.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
 
## <a name="syntax"></a>Sintassi  
  
```  
sys.sp_xtp_checkpoint_force_garbage_collection [[ @dbname=database_name]  
```  
  
## <a name="arguments"></a>Argomenti  
 *database_name*  
 Il database in cui eseguire Garbage Collection. Il valore predefinito è il database attuale.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 per l'esito positivo. Diverso da zero per l'esito negativo.  
  
## <a name="result-set"></a>Set di risultati  
 Ogni riga restituita contiene le informazioni seguenti:  
  
|Colonna|Descrizione|  
|------------|-----------------|  
|num_collected_items|Indica il numero di file spostati nel Garbage Collection di FILESTREAM. Questi sono i file con un numero di sequenza del file di log (LSN) inferiore a quello del punto di troncamento del log|  
|num_marked_for_collection_items|Indica il numero dei file di dati o dei file differenziali con un LSN aggiornato con l'ID blocco dell'LSN di fine log.|  
|last_collected_xact_seqno|Restituisce l'ultimo LSN corrispondente fino al quale i file sono stati spostati nel Garbage Collection di FILESTREAM.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione di proprietario del database.  
  
## <a name="sample"></a>Esempio  
  
```  
exec [sys].[sp_xtp_checkpoint_force_garbage_collection] hkdb1  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [OLTP in memoria &#40;ottimizzazione per la memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
