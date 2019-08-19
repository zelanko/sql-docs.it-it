---
title: Integrare un server di destinazione in un server master | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- enlisting target servers [SQL Server]
- SQL Server Agent jobs, target servers
- master servers [SQL Server], enlisting target servers
- SQL Server Agent jobs, master servers
- target servers [SQL Server], enlisting
ms.assetid: 7633adb5-d140-4e58-a8f2-5b4b50c2f95b
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 67971ce06b79d7a56af6ae9bfe6f5d153babbe80
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/16/2019
ms.locfileid: "69552909"
---
# <a name="enlist-a-target-server-to-a-master-server"></a>Integrare un server di destinazione in un server master
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In questo argomento viene illustrata la procedura per l'aggiunta di server di destinazione a una configurazione di amministrazione multiserver. Eseguire questa procedura dal server master. In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o SQL Server Management Objects (SMO).  
  
Per informazioni sugli effetti dell'uso dell'account di Windows per il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent su un ambiente multiserver, vedere [Creazione di un ambiente multiserver](../../ssms/agent/create-a-multiserver-environment.md).  
  
Per impostazione predefinita, per le connessioni tra server master e server di destinazione sono attive la crittografia SSL (Secure Sockets Layer) completa e la convalida del certificato. Per altre informazioni, vedere [Impostazione delle opzioni di crittografia nei server di destinazione](../../ssms/agent/set-encryption-options-on-target-servers.md).  
  
## <a name="SSMSProcedure"></a>Utilizzo di SQL Server Management Studio  
  
#### <a name="to-enlist-a-target-server"></a>Per integrare un server di destinazione  
  
1.  In **Esplora oggetti**espandere un server configurato come server master.  
  
2.  Fare clic con il pulsante destro del mouse su **SQL Server Agent**, scegliere **Amministrazione multiserver**e fare clic su **Aggiungi server di destinazione**.  
  
3.  In Configurazione guidata server di destinazione, eseguire i passaggi necessari per completare la procedura.  
  
## <a name="TsqlProcedure"></a>Utilizzo di Transact-SQL  
  
#### <a name="to-enlist-a-target-server"></a>Per integrare un server di destinazione  
  
1.  Usare la stored procedure **sp_msx_enlist** .  Per altre informazioni, vedere [sp_msx_enlist (Transact-SQL)](https://msdn.microsoft.com/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f)  
  
## <a name="see-also"></a>Vedere anche  
[Amministrazione automatizzata in un'organizzazione](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  
