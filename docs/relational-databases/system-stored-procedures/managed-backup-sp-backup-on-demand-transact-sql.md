---
title: managed_backup.sp_backup_on_demand (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- smart_admin.sp_backup_on_demand
- smart_admin.sp_backup_on_demand_TSQL
- sp_backup_on_demand_TSQL
- sp_backup_on_demand
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.sp_backup_on_demand
- sp_backup_on_demand
ms.assetid: 638f809f-27fa-4c44-a549-9cf37ecc920c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e34cf20585ea7dcd3690d80ee415fc274bf852ca
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155395"
---
# <a name="managed_backupsp_backup_on_demand-transact-sql"></a>managed_backup.sp_backup_on_demand (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Richiede al [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] di eseguire un backup del database specificato.  
  
 Utilizzare questa stored procedure per l'esecuzione dei backup ad hoc per un database configurato con il [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. In questo modo si impedisce che le interruzioni [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] della catena di backup e dei processi siano compatibili e che il backup venga archiviato nello stesso contenitore di archiviazione BLOB di Azure.  
  
 Al completamento del backup, viene restituito il percorso del file di backup completo che include il nome e la posizione del nuovo file di backup risultante dall'operazione di backup.  
  
 Viene restituito un errore se il [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] è in fase di esecuzione di un backup di un determinato tipo per il database specificato. In questo caso, il messaggio di errore restituito include il percorso del file di backup completo in cui il backup corrente viene caricato.  
   
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
EXEC managed_backup.sp_backup_on_demand   
[@database_name  =]  'database name',[@type = ] { 'Database' | 'Log' }  
  
```  
  
##  <a name="Arguments"></a> Argomenti  
 @database_name  
 Nome del database in cui deve essere eseguito il backup. È @database_name di **tipo sysname**.  
  
 @type  
 Tipo di backup da eseguire:  Database o log. Il @type parametro è di **tipo nvarchar (32)** .  
  
## <a name="return-code-value"></a>Valore del codice restituito  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo del database **db_backupoperator** , con autorizzazioni **ALTER ANY CREDENTIAL** e autorizzazioni **Execute** su **sp_delete_backuphistory**stored procedure.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eseguita una richiesta di backup del database per il database ' TestDB '. Per questo database è stato abilitato il [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
```  
Use MSDB  
Go  
EXEC managed_backup.sp_backup_on_demand  
 @database_name = 'TestDB'  
,@type = 'Database'  
  
```  
  
 Per ogni frammento di codice, selezionare 'tsql' nel campo dell'attributo di linguaggio.  
  
  
