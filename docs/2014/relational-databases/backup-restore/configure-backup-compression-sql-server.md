---
title: Configurare la compressione dei backup (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 430905eb-d218-458c-bd48-aeee6fbb7446
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bcfc0dea167b972f4e463333ab6851b038a284ed
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62922252"
---
# <a name="configure-backup-compression-sql-server"></a>Configura compressione backup (SQL Server)
  In fase di installazione, la compressione dei backup è disattivata per impostazione predefinita. Il comportamento predefinito della compressione dei backup è determinato dall'opzione di configurazione a livello di server **backup compression default** . È possibile tuttavia eseguire l'override dell'impostazione predefinita a livello del server durante la creazione di un singolo backup o la pianificazione di una serie di backup di routine. Per modificare il valore predefinito a livello di server, vedere [Visualizzare o configurare l'opzione di configurazione del server backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).  
  
## <a name="override-the-backup-compression-default"></a>Eseguire l'override dell'impostazione predefinita della compressione dei backup  
 È possibile modificare il comportamento della compressione dei backup per un singolo backup, processo di backup o configurazione per il log shipping.  
  
-   **[!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
     Per eseguire l'override del valore predefinito di compressione dei backup del server durante la creazione di un backup, usare WITH NO_COMPRESSION o WITH COMPRESSION nell'istruzione [BACKUP](/sql/t-sql/statements/backup-transact-sql).  
  
     Per una configurazione per il log shipping, è possibile determinare il comportamento della compressione dei backup dei log usando [sp_add_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql)[sp_change_log_shipping_primary_database &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql).  
  
-   **[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
     Per informazioni su come visualizzare o configurare l'opzione di configurazione del server backup compression default per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Visualizzare o configurare l'opzione di configurazione del server backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).  
  
     È possibile eseguire l'override dell'opzione backup compression default del server durante la creazione di un backup specificando **Comprimi backup** o **Non comprimere il backup** in una delle finestre di dialogo seguenti:  
  
    -   [Backup database (pagina Opzioni)](back-up-database-backup-options-page.md)  
  
         Quando si esegue il backup di un database, è possibile determinare la compressione dei backup per il backup di un singolo database, file o log.  
  
    -   [Utilizzare la Creazione guidata piano di manutenzione](../maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
         La Creazione guidata piano di manutenzione consente di controllare la compressione dei backup per ciascun set di backup completo o differenziale del database o backup del log pianificati.  
  
    -   Integration Services (SSIS) [Attività backup database](../../integration-services/control-flow/back-up-database-task.md)  
  
         È possibile controllare il comportamento della compressione dei backup durante la creazione di un pacchetto per l'esecuzione del backup di un singolo database o di più database.  
  
    -   [Log shipping - Impostazioni backup log delle transazioni](../databases/log-shipping-transaction-log-backup-settings.md)  
  
         È possibile determinare il comportamento della compressione dei backup dei log.  
  
  
## <a name="see-also"></a>Vedere anche  
 [Compressione backup &#40;SQL Server&#41;](backup-compression-sql-server.md)  
  
  
