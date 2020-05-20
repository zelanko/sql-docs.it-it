---
title: sys. sp_rda_reconcile_batch (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_reconcile_batch
- sys.sp_rda_reconcile_batch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_batch stored procedure
ms.assetid: 6d21eac3-7b6c-4fe0-8bc4-bf503f3948a6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 40fb2b497f799bc03551ff113c3b779510d1dee1
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827400"
---
# <a name="syssp_rda_reconcile_batch-transact-sql"></a>sys. sp_rda_reconcile_batch (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Risolve l'ID batch archiviato nella tabella SQL Server abilitata per l'estensione con l'ID batch archiviato nella tabella remota di Azure.  
  
 In genere è necessario eseguire **sp_rda_reconcile_batch** solo se sono stati eliminati manualmente i dati migrati più di recente dalla tabella remota. Quando si eliminano manualmente i dati remoti che includono il batch più recente, gli ID batch non sono sincronizzati e la migrazione viene arrestata.  
 
 Per eliminare i dati di cui è già stata eseguita la migrazione in Azure, vedere la sezione Osservazioni in questa pagina.
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_rda_reconcile_batch @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>Argomenti  
 \@objname ='* \@ ObjName*'  
 Nome della tabella SQL Server abilitata per l'estensione.  
  
## <a name="permissions"></a>Autorizzazioni  
 Richiede autorizzazioni db_owner.  
  
## <a name="remarks"></a>Commenti  
 Se si desidera eliminare i dati di cui è già stata eseguita la migrazione in Azure, eseguire le operazioni seguenti.  
  
1.  Sospendere la migrazione dei dati. Per altre informazioni, vedere [Sospendere e riprendere la migrazione dei dati &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
2.  Eliminare i dati dalla tabella di staging SQL Server eseguendo un comando DELETE con l'hint STAGE_ONLY. Per altre informazioni, vedere [eseguire aggiornamenti amministrativi ed eliminazioni](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md#adminHints).
  
3.  Eliminare gli stessi dati dalla tabella remota di Azure eseguendo un comando DELETE con l'hint REMOTE_ONLY.  
  
4.  Eseguire **sp_rda_reconcile_batch**.  
  
5.  Riprendere la migrazione dei dati. Per altre informazioni, vedere [Sospendere e riprendere la migrazione dei dati &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
## <a name="example"></a>Esempio  
 Per riconciliare gli ID batch, eseguire l'istruzione seguente.  
  
```sql  
EXEC sp_rda_reconcile_batch @objname = N'StretchEnabledTableName';  
```  
  
  
