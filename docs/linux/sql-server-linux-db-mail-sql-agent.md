---
title: Posta elettronica database e gli avvisi di posta elettronica con SQL Agent in Linux
description: Questo articolo descrive come usare posta elettronica database e gli avvisi di posta elettronica con SQL Server in Linux
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: tbd
ms.openlocfilehash: 031fdff258e6dba4976fec4e0b1c5ed10aa48f47
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833838"
---
# <a name="db-mail-and-email-alerts-with-sql-agent-on-linux"></a>Posta elettronica database e gli avvisi di posta elettronica con SQL Agent in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

I passaggi seguenti mostrano come configurare posta elettronica database e usarlo con SQL Server Agent (**mssql-server-agent**) in Linux. 

## <a name="1-enable-db-mail"></a>1. Abilitare posta elettronica database

```sql
USE master 
GO 
sp_configure 'show advanced options',1 
GO 
RECONFIGURE WITH OVERRIDE 
GO 
sp_configure 'Database Mail XPs', 1 
GO 
RECONFIGURE  
GO  
```

## <a name="2-create-a-new-account"></a>2. Crea nuovo account
```sql
EXECUTE msdb.dbo.sysmail_add_account_sp 
@account_name = 'SQLAlerts', 
@description = 'Account for Automated DBA Notifications', 
@email_address = 'sqlagenttest@gmail.com', 
@replyto_address = 'sqlagenttest@gmail.com', 
@display_name = 'SQL Agent', 
@mailserver_name = 'smtp.gmail.com', 
@port = 587, 
@enable_ssl = 1, 
@username = 'sqlagenttest@gmail.com', 
@password = '<password>' 
GO
```

## <a name="3-create-a-default-profile"></a>3. Creare un profilo predefinito

```sql
EXECUTE msdb.dbo.sysmail_add_profile_sp 
@profile_name = 'default', 
@description = 'Profile for sending Automated DBA Notifications' 
GO
```

## <a name="4-add-the-database-mail-account-to-a-database-mail-profile"></a>4. Aggiungere l'account di posta elettronica Database a un profilo di posta elettronica Database
```sql
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp 
@profile_name = 'default', 
@principal_name = 'public', 
@is_default = 1 ; 
 ```
 
## <a name="5-add-account-to-profile"></a>5. Aggiungere account al profilo 
```sql
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp   
@profile_name = 'default',   
@account_name = 'SQLAlerts',   
@sequence_number = 1;  
 ```
 
## <a name="6-send-test-email"></a>6. Invio di posta elettronica di test
> [!NOTE]
> Potrebbe essere necessario passare al client di posta elettronica e abilitare il "client meno sicuri inviare posta elettronica Consenti". Non tutti i client riconoscono posta elettronica database come un daemon di posta elettronica.

```
EXECUTE msdb.dbo.sp_send_dbmail 
@profile_name = 'default', 
@recipients = 'recipient-email@gmail.com', 
@Subject = 'Testing DBMail', 
@Body = 'This message is a test for DBMail' 
GO
```

## <a name="7-set-db-mail-profile-using-mssql-conf-or-environment-variable"></a>7. Impostare il profilo di posta elettronica database utilizzando mssql-conf o variabile di ambiente
È possibile utilizzare l'utilità mssql-conf o variabili di ambiente per registrare il profilo di posta elettronica database. In questo caso, è possibile chiamare predefinito del profilo.

```bash
# via mssql-conf
sudo /opt/mssql/bin/mssql-conf set sqlagent.databasemailprofile default
# via environment variable
MSSQL_AGENT_EMAIL_PROFILE=default
```

## <a name="8-set-up-an-operator-for-sqlagent-job-notifications"></a>8. Configurare un operatore per le notifiche dei processi SQLAgent 

```sql
EXEC msdb.dbo.sp_add_operator 
@name=N'JobAdmins',  
@enabled=1, 
@email_address=N'recipient-email@gmail.com',  
@category_name=N'[Uncategorized]' 
GO 
```

## <a name="9-send-email-when-agent-test-job-succeeds"></a>9. Invia messaggio di posta elettronica quando ha esito positivo 'Agente processo di Test' 

```
EXEC msdb.dbo.sp_update_job 
@job_name='Agent Test Job', 
@notify_level_email=1, 
@notify_email_operator_name=N'JobAdmins' 
GO
```

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni su come usare SQL Server Agent per creare, pianificare ed eseguire i processi, vedere [eseguire un processo di SQL Server Agent in Linux](sql-server-linux-run-sql-server-agent-job.md).
