---
title: sys. backup_devices (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backup_devices_TSQL
- backup_devices
- sys.backup_devices
- sys.backup_devices_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup devices [SQL Server], viewing information
- sys.backup_devices catalog view
ms.assetid: 457edaa4-aca1-4bd3-bf8d-734490b80fcd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b5f70fa8b486688a6c83133781b63d188742e345
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82816169"
---
# <a name="sysbackup_devices-transact-sql"></a>sys.backup_devices (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni dispositivo di backup registrato utilizzando **sp_addumpdevice** o creato in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**nome**|**sysname**|Nome del dispositivo di backup, univoco nel set.|  
|**type**|**tinyint**|Tipo di dispositivo di backup:<br /><br /> 2 = Disco<br /><br /> 3 = Disco floppy (obsoleto)<br /><br /> 5 = Nastro<br /><br /> 6 = Pipe (obsoleto)<br /><br /> 7 = Dispositivo virtuale (per l'utilizzo facoltativo da fornitori di terze parti)<br /><br /> In genere, vengono utilizzati solo disco (2) e nastro (5).|  
|**type_desc**|**nvarchar(60)**|Descrizione del tipo di dispositivo di backup:<br /><br /> DISK<br /><br /> DISKETTE (obsoleto)<br /><br /> TAPE<br /><br /> PIPE (obsoleto)<br /><br /> VIRTUAL_DEVICE (per l'utilizzo facoltativo da fornitori di terze parti)<br /><br /> In genere, vengono utilizzati solo DISK e TAPE.|  
|**physical_name**|**nvarchar(260)**|Nome o percorso del file fisico del dispositivo di backup.|  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Dispositivi di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [Viste del catalogo di database e file &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [Domande frequenti sull'esecuzione di query sul catalogo di sistema di SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
