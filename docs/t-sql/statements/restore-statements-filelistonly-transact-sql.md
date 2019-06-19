---
title: RESTORE FILELISTONLY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RESTORE FILELISTONLY
- RESTORE_FILELISTONLY_TSQL
- FILELISTONLY
- FILELISTONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backups [SQL Server], file lists
- RESTORE FILELISTONLY statement
- listing backed up files
ms.assetid: 0b4b4d11-eb9d-4f3e-9629-6c79cec7a81a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: b9480fc29339d0cd33d063c24f19c083804d1ae0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65948369"
---
# <a name="restore-statements---filelistonly-transact-sql"></a>Istruzioni RESTORE - FILELISTONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md )]


  Restituisce un set di risultati contenente un elenco dei file di database e di log contenuti nel set di backup in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

> [!NOTE]  
>  Per le descrizioni degli argomenti, vedere [Argomenti RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RESTORE FILELISTONLY   
FROM <backup_device>   
[ WITH   
 {  
--Backup Set Options  
   FILE = { backup_set_file_number | @backup_set_file_number }   
 | PASSWORD = { password | @password_variable }   
  
--Media Set Options  
 | MEDIANAME = { media_name | @media_name_variable }   
 | MEDIAPASSWORD = { mediapassword | @mediapassword_variable }  
  
--Error Management Options  
 | { CHECKSUM | NO_CHECKSUM }   
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }  
  
--Tape Options  
 | { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }    
 } [ ,...n ]  
]  
[;]  
  
<backup_device> ::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
   | { DISK | TAPE } = { 'physical_backup_device_name' |  
       @physical_backup_device_name_var }   
}  
  
```  
  
## <a name="arguments"></a>Argomenti  
 Per le descrizioni degli argomenti RESTORE FILELISTONLY, vedere [Argomenti RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
## <a name="result-sets"></a>Set di risultati  
 Un client può utilizzare RESTORE FILELISTONLY per ottenere un elenco dei file contenuti in un set di backup. Queste informazioni vengono restituite come set di risultati contenente una riga per ogni file.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-|-|-|  
|LogicalName|**nvarchar(128)**|Nome logico del file.|  
|PhysicalName|**nvarchar(260)**|Nome fisico o del sistema operativo del file.|  
|Tipo|**char(1)**|Tipo di file. I tipi possibili sono:<br /><br /> **L** = File di log di Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> **D** =  file di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> **F** = catalogo full text<br /><br /> **S** = contenitore FileStream, FileTable o [!INCLUDE[hek_2](../../includes/hek-2-md.md)]|  
|FileGroupName|**nvarchar(128)** NULL|Nome del filegroup che contiene il file.|  
|Dimensione|**numeric(20,0)**|Dimensioni correnti in byte.|  
|MaxSize|**numeric(20,0)**|Dimensioni massime consentite in byte.|  
|FileID|**bigint**|Identificatore del file, univoco all'interno del database.|  
|CreateLSN|**numeric(25,0)**|Numero di sequenza del file di log in corrispondenza del quale il file è stato creato.|  
|DropLSN|**numeric(25,0)** NULL|Numero di sequenza del log in corrispondenza del quale è stato eliminato il file. Se il file non è stato eliminato, questo valore è NULL.|  
|UniqueID|**uniqueidentifier**|Identificatore univoco globale del file.|  
|ReadOnlyLSN|**numeric(25,0) NULL**|Numero di sequenza del file di log in corrispondenza del quale la modalità del filegroup contenente il file è passata da lettura/scrittura a sola lettura (la modifica più recente).|  
|ReadWriteLSN|**numeric(25,0)** NULL|Numero di sequenza del file di log in corrispondenza del quale la modalità del filegroup contenente il file è passata da sola lettura a lettura/scrittura (la modifica più recente).|  
|BackupSizeInBytes|**bigint**|Dimensioni in byte del backup di questo file.|  
|SourceBlockSize|**int**|Dimensioni in byte del blocco del dispositivo fisico contenente il file, non del dispositivo di backup.|  
|FileGroupID|**int**|ID del filegroup.|  
|LogGroupGUID|**uniqueidentifier** Null|NULL|  
|DifferentialBaseLSN|**numeric(25,0)** NULL|Per i backup differenziali le modifiche con numeri di sequenza del file di log maggiori o uguali a **DifferentialBaseLSN** sono incluse nel backup differenziale.<br /><br /> Per gli altri tipi di backup il valore è NULL.|  
|DifferentialBaseGUID|**uniqueidentifier** Null|Per i backup differenziali, identificatore univoco della base differenziale.<br /><br /> Per gli altri tipi di backup il valore è NULL.|  
|IsReadOnly|**bit**|**1** = Il campo è di sola lettura.|  
|IsPresent|**bit**|**1** = Il file è incluso nel backup.|  
|TDEThumbprint|**varbinary(32)** NULL|Indica l'identificazione digitale della chiave di crittografia del database. L'identificazione digitale del componente di crittografia è un hash SHA-1 del certificato con cui viene crittografata la chiave. Per altre informazioni sulla crittografia trasparente del database, vedere [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).|  
|SnapshotURL|**nvarchar(360)** NULL|URL dello snapshot Azure del file di database contenuto nel backup FILE_SNAPSHOT. Restituisce NULL se non è presente un backup FILE_SNAPSHOT.|  
  
## <a name="security"></a>Security  
 Per un'operazione di backup è possibile specificare password per un set di supporti o un set di backup oppure per entrambi. Se è stata impostata una password per un set di supporti o un set di backup, la password o le password corrette devono essere specificate nell'istruzione RESTORE. Queste password impediscono operazioni di ripristino non autorizzate e l'aggiunta non autorizzata di set di backup ai supporti tramite gli strumenti di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Tuttavia, la password non impedisce la sovrascrittura dei supporti tramite l'opzione FORMAT dell'istruzione BACKUP.  
  
> [!IMPORTANT]  
>  Il livello di protezione garantito da questa password è vulnerabile. Lo scopo è impedire un ripristino non corretto da parte di utenti autorizzati o non autorizzati mediante gli strumenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Non impedisce la lettura dei dati di backup eseguita con altri mezzi o la sostituzione della password. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Per ottenere un livello di protezione adeguato dei backup è consigliabile archiviare i nastri di backup in un luogo sicuro oppure eseguire il backup su file su disco protetti da elenchi di controllo di accesso (ACL) appropriati. Gli elenchi di controllo di accesso devono essere impostati a livello della directory radice in cui vengono creati i backup.  
  
### <a name="permissions"></a>Autorizzazioni  
 A partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], per ottenere informazioni su un set o dispositivo di backup è necessario disporre dell'autorizzazione CREATE DATABASE. Per altre informazioni, vedere [GRANT - autorizzazioni per database &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite le informazioni contenute in un dispositivo di backup denominato `AdventureWorksBackups`. Nell'esempio viene utilizzata l'opzione `FILE` per specificare il secondo set di backup nel dispositivo.  
  
```  
RESTORE FILELISTONLY FROM AdventureWorksBackups   
   WITH FILE=2;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Informazioni sulla cronologia e sull'intestazione del backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
