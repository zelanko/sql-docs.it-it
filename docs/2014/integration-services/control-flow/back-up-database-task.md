---
title: Attività Backup database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.backupdatabasetask.f1
helpviewer_keywords:
- database backups [Integration Services]
- Back Up Database task [Integration Services]
- backing up databases [Integration Services]
- transaction log backups [Integration Services]
- backing up transaction logs [Integration Services]
ms.assetid: b8839d71-13b7-41f2-a434-cb95020e79d7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d4b6aabb1f44c2a25704b7079074a5600c4d52d4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62833129"
---
# <a name="back-up-database-task"></a>Attività Backup database
  L'attività Backup database consente di eseguire diversi tipi di backup dei database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Backup e ripristino di database SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
 Tramite l'attività Backup database un pacchetto può eseguire il backup di uno o più database. Se si utilizza l'attività per eseguire il backup di un singolo database, sarà possibile scegliere il componente di cui eseguire il backup, ovvero il database o i relativi file e filegroup.  
  
## <a name="supported-recover-models-and-backup-types"></a>Modelli di recupero e tipi di backup supportati  
 Nella tabella seguente sono elencati i modelli di recupero e i tipi di backup supportati dall'attività Backup database.  
  
|modello di recupero|Database|Differenziale del database|Log delle transazioni|File o differenziale del file|  
|--------------------|--------------|---------------------------|---------------------|-------------------------------|  
|Semplice|Obbligatoria|Facoltativo|Non supportate|Non supportate|  
|Full|Obbligatoria|Facoltativo|Obbligatoria|Facoltativo|  
|Registrazione minima delle operazioni bulk|Obbligatoria|Facoltativo|Obbligatoria|Facoltativo|  
  
 L'attività Backup database incapsula l'istruzione Transact-SQL BACKUP. Per altre informazioni, vedere [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
## <a name="configuration-of-the-back-up-database-task"></a>Configurazione dell'attività Backup database  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] . Questa attività è disponibile nella sezione **Attività di manutenzione** della **casella degli strumenti** di Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Attività Backup database &#40;Piano di manutenzione&#41;](../../relational-databases/maintenance-plans/options-in-the-back-up-database-task-for-maintenance-plan.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
  
