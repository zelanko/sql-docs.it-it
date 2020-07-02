---
title: BackupMediaSet (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backupmediaset
- backupmediaset_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], backupmediaset system table
- backupmediaset system table
ms.assetid: d9c18a93-cab9-4db8-ae09-c6bd8145ab8f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 86f1b7fcc8e801f70bf070911feadb059108dff5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750364"
---
# <a name="backupmediaset-transact-sql"></a>backupmediaset (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Contiene una riga per ogni set di supporti di backup. Questa tabella è archiviata nel database **msdb** .  
 
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|Numero di identificazione univoco del set di supporti. Identità, chiave primaria.|  
|**media_uuid**|**uniqueidentifier**|UUID del set di supporti. Tutti i [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] set di supporti hanno un UUID.<br /><br /> Per le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , tuttavia, se un set di supporti contiene un solo gruppo di supporti, la colonna **media_uuid** potrebbe essere null (**media_family_count** è 1).|  
|**media_family_count**|**tinyint**|Numero di gruppi di supporti nel set di supporti. Può essere NULL.|  
|**nome**|**nvarchar(128)**|Nome del set di supporti. Può essere NULL.<br /><br /> Per ulteriori informazioni, vedere MEDIAname e MEDIADESCRIPTION in [BACKUP &#40;&#41;Transact-SQL ](../../t-sql/statements/backup-transact-sql.md).|  
|**Descrizione**|**nvarchar(255)**|Descrizione in formato testo del set di supporti. Può essere NULL.<br /><br /> Per ulteriori informazioni, vedere MEDIAname e MEDIADESCRIPTION in [BACKUP &#40;&#41;Transact-SQL ](../../t-sql/statements/backup-transact-sql.md).|  
|**software_name**|**nvarchar(128)**|Nome del software di backup con cui è stata scritta l'etichetta del supporto. Può essere NULL.|  
|**software_vendor_id**|**int**|Numero di identificazione del produttore del software con cui è stata scritta l'etichetta del supporto di backup. Può essere NULL.<br /><br /> Il valore per [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è esadecimale 0x1200.|  
|**MTF_major_version**|**tinyint**|Numero principale della versione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Tape Format utilizzata per generare il set di supporti. Può essere NULL.|  
|**mirror_count**|**tinyint**|Numero di mirroring nel set di supporti.|  
|**is_password_protected**|**bit**|Set di supporti protetto da password:<br /><br /> 0 = non protetto<br /><br /> 1 = protetto|  
|**is_compressed**|**bit**|Specifica se il backup è compresso:<br /><br /> 0 = non compresso<br /><br /> 1 = compresso<br /><br /> Durante un aggiornamento di **msdb** , questo valore è impostato su null. che indica un backup non compresso.|  
|**is_encrypted**|**Po'**|Specifica se il backup è crittografato:<br /><br /> 0 = Non crittografato<br /><br /> 1 = Crittografato|  
  
## <a name="remarks"></a>Osservazioni  
 RESTOre VERIFYONLY FROM *backup_device* with LOADHISTORY popola le colonne della tabella **BackupMediaSet** con i valori appropriati dell'intestazione del set di supporti.  
  
 Per ridurre il numero di righe in questa tabella e in altre tabelle di backup e di cronologia, eseguire la [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) stored procedure.  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di backup e ripristino &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Tabelle di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
