---
title: Configurare la compressione dei backup (SQL Server) | Microsoft Docs
description: Questo articolo descrive come eseguire l'override dell'impostazione predefinita a livello di server durante la creazione di un singolo backup o la pianificazione di una serie di backup di routine in SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 430905eb-d218-458c-bd48-aeee6fbb7446
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d9ba9a26022c194316089bf13eb4c1d6811b76c4
ms.sourcegitcommit: 9afb612c5303d24b514cb8dba941d05c88f0ca90
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2020
ms.locfileid: "82220466"
---
# <a name="configure-backup-compression-sql-server"></a>Configura compressione backup (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In fase di installazione, la compressione dei backup è disattivata per impostazione predefinita. Il comportamento predefinito della compressione dei backup è determinato dall'opzione di configurazione a livello di server **backup compression default** . È possibile tuttavia eseguire l'override dell'impostazione predefinita a livello del server durante la creazione di un singolo backup o la pianificazione di una serie di backup di routine. Per modificare il valore predefinito a livello di server, vedere [Visualizzare o configurare l'opzione di configurazione del server backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).  
  
## <a name="override-the-backup-compression-default"></a>Eseguire l'override dell'impostazione predefinita della compressione dei backup  
 È possibile modificare il comportamento della compressione dei backup per un singolo backup, processo di backup o configurazione per il log shipping.  
  
-   **[!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
     Per eseguire l'override del valore predefinito di compressione dei backup del server durante la creazione di un backup, usare WITH NO_COMPRESSION o WITH COMPRESSION nell'istruzione [BACKUP](../../t-sql/statements/backup-transact-sql.md).  
  
     Per una configurazione per il log shipping, è possibile determinare il comportamento della compressione dei backup dei log usando [sp_add_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)[sp_change_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql.md).  
  
-   **[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
     Per informazioni su come visualizzare o configurare l'opzione di configurazione del server backup compression default per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Visualizzare o configurare l'opzione di configurazione del server backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).  
  
     È possibile eseguire l'override dell'opzione backup compression default del server durante la creazione di un backup specificando **Comprimi backup** o **Non comprimere il backup** in una delle finestre di dialogo seguenti:  
  
    -   [Backup database (pagina Opzioni)](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)  
  
         Quando si esegue il backup di un database, è possibile determinare la compressione dei backup per il backup di un singolo database, file o log.  
  
    -   [Utilizzare la Creazione guidata piano di manutenzione](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
         La Creazione guidata piano di manutenzione consente di controllare la compressione dei backup per ciascun set di backup completo o differenziale del database o backup del log pianificati.  
  
    -   Integration Services (SSIS) [Attività backup database](../../integration-services/control-flow/back-up-database-task.md)  
  
         È possibile controllare il comportamento della compressione dei backup durante la creazione di un pacchetto per l'esecuzione del backup di un singolo database o di più database.  
  
    -   [Log shipping - Impostazioni backup log delle transazioni](../../relational-databases/databases/log-shipping-transaction-log-backup-settings.md)  
  
         È possibile determinare il comportamento della compressione dei backup dei log.  
  
  
## <a name="see-also"></a>Vedere anche  
 [Compressione backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md)  
  
  
