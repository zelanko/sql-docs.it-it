---
title: sp_add_log_shipping_primary_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_primary_database
- sp_add_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_primary_database
ms.assetid: 69531611-113f-46b5-81a6-7bf496d0353c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5af11c14c7b0bf3b8e32d503c4b77e59623ce9ff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140452"
---
# <a name="spaddlogshippingprimarydatabase-transact-sql"></a>sp_add_log_shipping_primary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Imposta il database primario per una configurazione di log shipping, inclusi il processo di backup, il record di monitoraggio locale e il record di monitoraggio remoto.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_add_log_shipping_primary_database [ @database = ] 'database',   
[ @backup_directory = ] 'backup_directory',   
[ @backup_share = ] 'backup_share',   
[ @backup_job_name = ] 'backup_job_name',   
[, [ @backup_retention_period = ] backup_retention_period]  
[, [ @monitor_server = ] 'monitor_server']  
[, [ @monitor_server_security_mode = ] monitor_server_security_mode]  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @backup_threshold = ] backup_threshold ]   
[, [ @threshold_alert = ] threshold_alert ]   
[, [ @threshold_alert_enabled = ] threshold_alert_enabled ]   
[, [ @history_retention_period = ] history_retention_period ]  
[, [ @backup_job_id = ] backup_job_id OUTPUT ]  
[, [ @primary_id = ] primary_id OUTPUT]  
[, [ @backup_compression = ] backup_compression_option ]  
  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @database = ] 'database'` È il nome del database primario di log shipping. *database* viene **sysname**, non prevede alcun valore predefinito e non può essere NULL.  
  
`[ @backup_directory = ] 'backup_directory'` È il percorso della cartella di backup nel server primario. *backup_directory* viene **nvarchar(500)** , non prevede alcun valore predefinito e non può essere NULL.  
  
`[ @backup_share = ] 'backup_share'` È il percorso di rete per la directory di backup nel server primario. *backup_share* viene **nvarchar(500)** , non prevede alcun valore predefinito e non può essere NULL.  
  
`[ @backup_job_name = ] 'backup_job_name'` È il nome del processo di SQL Server Agent nel server primario che copia il backup nella cartella di backup. *backup_job_name* viene **sysname** e non può essere NULL.  
  
`[ @backup_retention_period = ] backup_retention_period` È il periodo di tempo, espresso in minuti, per mantenere il file di backup di log nella directory di backup nel server primario. *backup_retention_period* viene **int**, non prevede alcun valore predefinito e non può essere NULL.  
  
`[ @monitor_server = ] 'monitor_server'` È il nome del server di monitoraggio. *Monitor_server* viene **sysname**, non prevede alcun valore predefinito e non può essere NULL.  
  
`[ @monitor_server_security_mode = ] monitor_server_security_mode` La modalità di sicurezza utilizzata per la connessione al server di monitoraggio.  
  
 1 = Autenticazione di Windows.  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione. *monitor_server_security_mode* viene **bit** e non può essere NULL.  
  
`[ @monitor_server_login = ] 'monitor_server_login'` È il nome utente dell'account usato per accedere al server di monitoraggio.  
  
`[ @monitor_server_password = ] 'monitor_server_password'` È la password dell'account usato per accedere al server di monitoraggio.  
  
`[ @backup_threshold = ] backup_threshold` Periodo di tempo, espresso in minuti, trascorso dall'ultimo backup prima di un *threshold_alert* viene generato un errore. *backup_threshold* viene **int**, con un valore predefinito è 60 minuti.  
  
`[ @threshold_alert = ] threshold_alert` È l'avviso da generare quando viene superata la soglia per il backup. *threshold_alert* viene **int**, con un valore predefinito è 14,420.  
  
`[ @threshold_alert_enabled = ] threshold_alert_enabled` Specifica se un avviso verrà generato quando *backup_threshold* viene superato. Il valore predefinito 0 indica che l'avviso è disabilitato e non verrà generato. *threshold_alert_enabled* viene **bit**.  
  
`[ @history_retention_period = ] history_retention_period` È il periodo di tempo in minuti in cui verrà mantenuta la cronologia. *history_retention_period* viene **int**, con un valore predefinito è NULL. Se non si specifica un valore, verrà utilizzato il valore 14420.  
  
`[ @backup_job_id = ] backup_job_id OUTPUT` Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ID processo dell'agente associato con il processo di backup nel server primario. *backup_job_id* viene **uniqueidentifier** e non può essere NULL.  
  
`[ @primary_id = ] primary_id OUTPUT` L'ID del database primario per la configurazione di log shipping. *primary_id* viene **uniqueidentifier** e non può essere NULL.  
  
`[ @backup_compression = ] backup_compression_option` Specifica se Usa una configurazione di log shipping [compressione dei backup](../../relational-databases/backup-restore/backup-compression-sql-server.md). Questo parametro è supportato solo in [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] o versione successiva.  
  
 0 = disabilitati. I backup del log non vengono mai compressi.  
  
 1 = abilitati. I backup del log vengono sempre compressi.  
  
 2 = utilizzare l'impostazione delle [visualizzare o configurare l'opzione di configurazione del Server backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md). Rappresenta il valore predefinito.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Nessuna  
  
## <a name="remarks"></a>Note  
 **sp_add_log_shipping_primary_database** deve essere eseguita la **master** database nel server primario. Questa stored procedure esegue le funzioni seguenti:  
  
1.  Genera un ID primario e aggiunge una voce per il database primario nella tabella **log_shipping_primary_databases** utilizzando gli argomenti specificati.  
  
2.  Crea un processo di backup per il database primario disabilitato.  
  
3.  Imposta l'ID di processo di backup di **log_shipping_primary_databases** voce per l'ID del processo del processo di backup.  
  
4.  Aggiunge un record di monitoraggio locale nella tabella **log_shipping_monitor_primary** nel server primario utilizzando gli argomenti specificati.  
  
5.  Se il server di monitoraggio è diverso dal server primario, aggiunge un record di monitoraggio **log_shipping_monitor_primary** sul monitor server utilizzando gli argomenti specificati.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server può eseguire questa procedura.  
  
## <a name="examples"></a>Esempi  
 In questo esempio il database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] viene aggiunto come database primario in una configurazione per il log shipping.  
  
```  
DECLARE @LS_BackupJobId AS uniqueidentifier ;  
DECLARE @LS_PrimaryId AS uniqueidentifier ;  
  
EXEC master.dbo.sp_add_log_shipping_primary_database   
@database = N'AdventureWorks'   
,@backup_directory = N'c:\lsbackup'   
,@backup_share = N'\\tribeca\lsbackup'   
,@backup_job_name = N'LSBackup_AdventureWorks'   
,@backup_retention_period = 1440  
,@monitor_server = N'rockaway'   
,@monitor_server_security_mode = 1   
,@backup_threshold = 60   
,@threshold_alert = 0   
,@threshold_alert_enabled = 0   
,@history_retention_period = 1440   
,@backup_job_id = @LS_BackupJobId OUTPUT   
,@primary_id = @LS_PrimaryId OUTPUT   
,@overwrite = 1   
,@backup_compression = 0;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sul log shipping &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
