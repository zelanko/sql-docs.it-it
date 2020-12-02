---
description: Attività Backup database
title: Attività Backup database | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.backupdatabasetask.f1
helpviewer_keywords:
- database backups [Integration Services]
- Back Up Database task [Integration Services]
- backing up databases [Integration Services]
- transaction log backups [Integration Services]
- backing up transaction logs [Integration Services]
ms.assetid: b8839d71-13b7-41f2-a434-cb95020e79d7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 63e02be4fe2c7fdd1c0293cd5e76dcb9e0adca22
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123612"
---
# <a name="back-up-database-task"></a>Attività Backup database

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  L'attività Backup database consente di eseguire diversi tipi di backup dei database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Backup e ripristino di database SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
 Tramite l'attività Backup database un pacchetto può eseguire il backup di uno o più database. Se si utilizza l'attività per eseguire il backup di un singolo database, sarà possibile scegliere il componente di cui eseguire il backup, ovvero il database o i relativi file e filegroup.  
  
## <a name="supported-recover-models-and-backup-types"></a>Modelli di recupero e tipi di backup supportati  
 Nella tabella seguente sono elencati i modelli di recupero e i tipi di backup supportati dall'attività Backup database.  
  
|modello di recupero|Database|Differenziale del database|Log delle transazioni|File o differenziale del file|  
|--------------------|--------------|---------------------------|---------------------|-------------------------------|  
|Semplice|Obbligatoria|Facoltativo|Non supportate|Non supportate|  
|Full|Obbligatoria|Facoltativo|Obbligatoria|Facoltativo|  
|Registrazione minima delle operazioni bulk|Obbligatoria|Facoltativo|Obbligatoria|Facoltativo|  
  
 L'attività Backup database incapsula l'istruzione Transact-SQL BACKUP. Per altre informazioni, vedere [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).  
  
## <a name="configuration-of-the-back-up-database-task"></a>Configurazione dell'attività Backup database  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Questa attività è disponibile nella sezione **Attività di manutenzione** della **casella degli strumenti** di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)].  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Attività Backup database &#40;Piano di manutenzione&#41;](../../relational-databases/maintenance-plans/options-in-the-back-up-database-task-for-maintenance-plan.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
