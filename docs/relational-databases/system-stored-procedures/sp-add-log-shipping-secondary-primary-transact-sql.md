---
title: sp_add_log_shipping_secondary_primary (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_secondary_primary_TSQL
- sp_add_log_shipping_secondary_primary
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_secondary_primary
ms.assetid: bfbbbee2-c255-4a59-a963-47d6e980a8e2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 155f59426e8167d5d888f3890089dd4b2ea3bf7c
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909690"
---
# <a name="sp_add_log_shipping_secondary_primary-transact-sql"></a>sp_add_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Imposta le informazioni primarie, aggiunge collegamenti di monitoraggio locale e remoto e crea processi di copia e di ripristino nel server secondario per il database primario specificato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_add_log_shipping_secondary_primary  
 [ @primary_server = ] 'primary_server',   
[ @primary_database = ] 'primary_database',  
[ @backup_source_directory = ] 'backup_source_directory' ,   
[ @backup_destination_directory = ] 'backup_destination_directory'  
[ @copy_job_name = ] 'copy_job_name'  
[ @restore_job_name = ] 'restore_job_name'  
[, [ @file_retention_period = ] 'file_retention_period']  
[, [ @monitor_server = ] 'monitor_server']  
[, [ @monitor_server_security_mode = ] 'monitor_server_security_mode']  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @copy_job_id = ] 'copy_job_id' OUTPUT ]  
[, [ @restore_job_id = ] 'restore_job_id' OUTPUT ]  
[, [ @secondary_id = ] 'secondary_id' OUTPUT]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @primary_server = ] 'primary_server'` il nome dell'istanza primaria del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] nella configurazione log shipping. *primary_server* è di **tipo sysname** e non può essere null.  
  
`[ @primary_database = ] 'primary_database'` è il nome del database nel server primario. *primary_database* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @backup_source_directory = ] 'backup_source_directory'` directory in cui vengono archiviati i file di backup del log delle transazioni dal server primario. *backup_source_directory* è di **tipo nvarchar (500)** e non può essere null.  
  
`[ @backup_destination_directory = ] 'backup_destination_directory'` la directory nel server secondario in cui vengono copiati i file di backup. *backup_destination_directory* è di **tipo nvarchar (500)** e non può essere null.  
  
`[ @copy_job_name = ] 'copy_job_name'` il nome da utilizzare per il processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent creato per copiare i backup del log delle transazioni nel server secondario. *copy_job_name* è di **tipo sysname** e non può essere null.  
  
`[ @restore_job_name = ] 'restore_job_name'` è il nome del processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent nel server secondario che ripristina i backup nel database secondario. *restore_job_name* è di **tipo sysname** e non può essere null.  
  
`[ @file_retention_period = ] 'file_retention_period'` periodo di tempo, in minuti, durante il quale un file di backup viene mantenuto nel server secondario nel percorso specificato dal parametro @backup_destination_directory prima di essere eliminato. *history_retention_period* è di **tipo int**e il valore predefinito è null. Se non si specifica un valore, verrà utilizzato il valore 14420.  
  
`[ @monitor_server = ] 'monitor_server'` è il nome del server di monitoraggio. *Monitor_server* è di **tipo sysname**e non prevede alcun valore predefinito e non può essere null.  
  
`[ @monitor_server_security_mode = ] 'monitor_server_security_mode'` la modalità di sicurezza utilizzata per la connessione al server di monitoraggio.  
  
 1 = Autenticazione di Windows.  
  
 0 = Autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *monitor_server_security_mode* è di **bit** e non può essere null.  
  
`[ @monitor_server_login = ] 'monitor_server_login'` è il nome utente dell'account utilizzato per accedere al server di monitoraggio.  
  
`[ @monitor_server_password = ] 'monitor_server_password'` è la password dell'account utilizzato per accedere al server di monitoraggio.  
  
`[ @copy_job_id = ] 'copy_job_id' OUTPUT` l'ID associato al processo di copia nel server secondario. *copy_job_id* è di tipo **uniqueidentifier** e non può essere null.  
  
`[ @restore_job_id = ] 'restore_job_id' OUTPUT` l'ID associato al processo di ripristino nel server secondario. *restore_job_id* è di tipo **uniqueidentifier** e non può essere null.  
  
`[ @secondary_id = ] 'secondary_id' OUTPUT` l'ID del server secondario nella configurazione del log shipping. *secondary_id* è di tipo **uniqueidentifier** e non può essere null.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Nessuno  
  
## <a name="remarks"></a>Osservazioni  
 **sp_add_log_shipping_secondary_primary** deve essere eseguito dal database **Master** nel server secondario. Questa stored procedure esegue le operazioni seguenti:  
  
1.  Genera un ID secondario per il server e il database primari specificati.  
  
2.  Esegue le operazioni seguenti:  

    1.  Aggiunge una voce per l'ID secondario in **log_shipping_secondary** usando gli argomenti forniti.  
  
    2.  Crea un processo di copia per l'ID secondario disabilitato.  
  
    3.  Imposta l'ID del processo di copia nella voce **log_shipping_secondary** sull'ID processo del processo di copia.  
  
    4.  Crea un processo di ripristino per l'ID secondario disabilitato.  
  
    5.  Impostare l'ID del processo di ripristino nella voce **log_shipping_secondary** sull'ID processo del processo di ripristino.  
  
## <a name="permissions"></a>Autorizzazioni  
 Questa procedura può essere eseguita solo dai membri del ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
 Questo esempio illustra l'uso della stored procedure **sp_add_log_shipping_secondary_primary** per configurare le informazioni per il database primario [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] nel server secondario.  
  
```  
EXEC master.dbo.sp_add_log_shipping_secondary_primary   
@primary_server = N'TRIBECA'   
,@primary_database = N'AdventureWorks'   
,@backup_source_directory = N'\\tribeca\LogShipping'   
,@backup_destination_directory = N''   
,@copy_job_name = N''   
,@restore_job_name = N''   
,@file_retention_period = 1440   
,@monitor_server = N'ROCKAWAY'   
,@monitor_server_security_mode = 1   
,@copy_job_id = @LS_Secondary__CopyJobId OUTPUT   
,@restore_job_id = @LS_Secondary__RestoreJobId OUTPUT   
,@secondary_id = @LS_Secondary__SecondaryId OUTPUT ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sul log shipping &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
