---
title: sys.database_recovery_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_recovery_status_TSQL
- database_recovery_status
- sys.database_recovery_status
- sys.database_recovery_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_recovery_status catalog view
ms.assetid: 46fab234-1542-49be-8edf-aa101e728acf
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0e78b5a8640918291fc68e5b4882448b94a1b9d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079517"
---
# <a name="sysdatabaserecoverystatus-transact-sql"></a>sys.database_recovery_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Include una riga per database. Se il database non è aperto, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] tenta di avviarlo.  
  
 Per visualizzare la riga per un database diverso da **master** oppure **tempdb**, è necessario applicare uno dei seguenti:  
  
-   Essere proprietario del database.  
  
-   Disporre delle autorizzazioni ALTER ANY DATABASE o VIEW ANY DATABASE a livello di server.  
  
-   Disporre dell'autorizzazione CREATE DATABASE nel **master** database.    
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID del database, univoco all'interno di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**database_guid**|**uniqueidentifier**|Utilizzato per mettere il relazione tra loro tutti i file di un database. È necessario che tutti i file includano questo GUID nella pagina di intestazione per essere avviati come previsto. Solo un database dovrebbe includere questo GUID, ma è possibile creare duplicati copiando o collegando i database. RESTORE genera sempre un nuovo GUID quando si ripristina un database non ancora esistente.<br /><br /> NULL= Il database è offline o non può essere avviato.|  
|**family_guid**|**uniqueidentifier**|Identificatore del "gruppo di backup" del database per l'individuazione di stati di ripristino corrispondenti.<br /><br /> NULL= Il database è offline o non può essere avviato.|  
|**last_log_backup_lsn**|**numeric(25,0)**|Il numero di sequenza del log iniziale del backup del log successivo.<br /><br /> Se NULL, nuovamente un log delle transazioni fino non può essere eseguito perché il database è di recupero con registrazione minima o non vi è alcun backup del database corrente.|  
|**recovery_fork_guid**|**uniqueidentifier**|Identifica il fork di recupero corrente nel quale il database è attualmente attivo.<br /><br /> NULL= Il database è offline o non può essere avviato.|  
|**first_recovery_fork_guid**|**uniqueidentifier**|Identificatore del fork di recupero di inizio.<br /><br /> NULL= Il database è offline o non può essere avviato.|  
|**fork_point_lsn**|**numeric(25,0)**|Se **first_recovery_fork_guid** non è uguale (! =) per **recovery_fork_guid**, **fork_point_lsn** è il numero di sequenza del log del punto di fork corrente. Negli altri casi il valore è NULL.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Viste del catalogo di database e file &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [Domande frequenti sull'esecuzione di query nel catalogo di sistema di SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
