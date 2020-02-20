---
title: Modifica dei server di destinazione di un processo
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- modifying target servers
- SQL Server Agent jobs, target servers
- target servers [SQL Server], modifying
ms.assetid: 9dbe24f2-acec-4aa2-920c-e8e96efa18e4
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a5300935cdbffc501996c7e68ba44b73b2964fa4
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75252382"
---
# <a name="modify-the-target-servers-for-a-job"></a>Modifica dei server di destinazione di un processo

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Questo argomento descrive come modificare i server di destinazione per i processi di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].

## <a name="BeforeYouBegin"></a>Prima di iniziare  
  
### <a name="Security"></a>Sicurezza  
  
#### <a name="Permissions"></a>Autorizzazioni  
Per impostazione predefinita, i membri del ruolo predefinito del server sysadmin possono eseguire questa stored procedure. Gli altri utenti devono appartenere a uno dei seguenti ruoli predefiniti del database di SQL Server Agent nel database msdb:  
  
1.  **SQLAgentUserRole**  
  
2.  **SQLAgentReaderRole**  
  
3.  SQLAgentOperatorRole  
  
## <a name="SSMSProcedure"></a>Utilizzo di SQL Server Management Studio  
  
#### <a name="to-modify-the-target-servers-for-a-job"></a>Per modificare i server di destinazione per un processo  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]ed espandere tale istanza.  
  
2.  Espandere **SQL Server Agent**e quindi **Processi**, fare clic con il pulsante destro del mouse sul processo e quindi scegliere **Proprietà**.  
  
3.  Nella finestra di dialogo **Proprietà processo** , fare clic sulla pagina **Server di destinazione**e quindi su **Server di destinazione locale**oppure **Più server di destinazione**.  
  
    Se si sceglie **Più server di destinazione**, specificare quali dovranno essere i server di destinazione del processo selezionando la casella a sinistra del nome di ogni server. Verificare che le caselle di controllo corrispondenti ai server che non saranno server di destinazione del processo siano deselezionate.  
  
## <a name="TsqlProcedure"></a>Utilizzo di Transact-SQL  
  
#### <a name="to-modify-the-target-servers-for-a-job"></a>Per modificare i server di destinazione per un processo  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio il processo multiserver Weekly Sales Backups viene assegnato al server SEATTLE2.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_jobserver  
    @job_name = N'Weekly Sales Backups',   
    @server_name = N'SEATTLE2' ;   
GO  
```  
  
Per altre informazioni, vedere [sp_add_jobserver (Transact-SQL)](https://msdn.microsoft.com/485252cc-0081-490a-9bd1-cbbd68eea286).  
  
## <a name="see-also"></a>Vedere anche  
[Amministrazione automatizzata in un'organizzazione](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  
