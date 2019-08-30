---
title: Configurare il backup gestito (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.managedbackup.configure.f1
ms.assetid: 79397cf6-0611-450a-b0d8-e784a76e3091
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 021db5a2283eb6ec68ea80302e938f08e7ba1a5c
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154346"
---
# <a name="configure-managed-backup-sql-server-management-studio"></a>Configurare il backup gestito (SQL Server Management Studio)
  La finestra di dialogo **backup gestito** consente di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] configurare le impostazioni predefinite per l'istanza. In questo argomento viene descritto come usare questa finestra di dialogo per configurare le impostazioni predefinite di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per l'istanza e le opzioni che è necessario considerare quando si esegue questa operazione. Quando [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] è configurato per l'istanza, le impostazioni vengono applicate a qualsiasi nuovo database creato successivamente.  
  
 Se si vuole configurare [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per un database specifico, vedere [abilitare e configurare SQL Server backup gestito in Azure per un database](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md#DatabaseConfigure).  
 
> [!NOTE] 
> Il backup gestito di SQL Server non è supportato con i server proxy. 
  
## <a name="task-list"></a>Elenco attività  
  
## <a name="includess_smartbackupincludesss-smartbackup-mdmd-functions-using-managed-backup-interface-in-sql-server-management-studio"></a>Funzioni di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] mediante l'interfaccia di backup gestita in SQL Server Management Studio  
 In questa versione è possibile configurare solo le impostazioni predefinite a livello di istanza usando l'interfaccia di **backup di gestione** . Non è possibile configurare [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per un database, sospendere o riprendere operazioni [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] o impostare notifiche email. Per informazioni su come eseguire operazioni attualmente non supportate tramite l'interfaccia di **backup gestita** , vedere [SQL Server backup gestito in Azure-impostazioni di conservazione e archiviazione](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md).  
  
## <a name="permissions"></a>Permissions  
 **Il nodo Visualizza backup gestito è SQL Server Management Studio:** Per visualizzare il nodo **backup gestito** in **Esplora oggetti**, è necessario essere un amministratore di sistema o disporre delle seguenti autorizzazioni concesse in modo specifico al proprio account utente:  
  
-   `db_backupoperator`  
  
-   `VIEW SERVER STATE`  
  
-   `ALTER ANY CREDENTIAL`  
  
-   `VIEW ANY DEFINITION`  
  
-   `EXECUTE`il `smart_admin.fn_is_master_switch_on`.  
  
-   `SELECT`il `smart_admin.fn_backup_instance_config`.  
  
 **Per configurare il backup gestito:** per [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] configurare in SQL Server Management Studio, è necessario essere un amministratore di sistema o disporre delle autorizzazioni seguenti:  
  
 L'appartenenza al ruolo del database `db_backupoperator`, con le autorizzazioni `ALTER ANY CREDENTIAL` e `EXECUTE` sulla stored procedure `sp_delete_backuphistory`.  
  
 `SELECT`autorizzazioni sulla `smart_admin.fn_get_current_xevent_settings` funzione.  
  
 `EXECUTE`autorizzazioni per l' `smart_admin.sp_get_backup_diagnostics` stored procedure. È inoltre richiesta l'autorizzazione `VIEW SERVER STATE` poiché vengono chiamati internamente altri oggetti di sistema che richiedono tale autorizzazione.  
  
 Le autorizzazioni `EXECUTE` per `smart_admin.sp_set_instance_backup` e `smart_admin.sp_backup_master_switch`.  
  
## <a name="configure-includess_smartbackupincludesss-smartbackup-mdmd-using-sql-server-management-studio"></a>Configurare [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] tramite SQL Server Management Studio  
 In **Esplora oggetti**espandere il nodo **gestione** e fare clic con il pulsante destro del mouse su **backup gestito**. Selezionare **Configura**. Viene aperta la finestra di dialogo **Backup gestito** .  
  
 Selezionare l'opzione **Abilita backup gestito** e specificare i valori di configurazione:  
  
 Il periodo di **memorizzazione dei file** è specificato in giorni e deve essere compreso tra 1 e 30.  
  
 Le **credenziali SQL** selezionate devono corrispondere all'account di archiviazione. Se al momento non si dispone di credenziali SQL che archiviano le informazioni di autenticazione, è possibile crearne una facendo clic su **Crea**. È anche possibile creare le credenziali usando l'istruzione Transact-SQL CREATE CREDENTIAL e fornire il nome account di archiviazione per l'identità e la chiave di accesso per i parametri chiave privati. Per altre informazioni, vedere [creare una credenziale](../relational-databases/backup-restore/sql-server-backup-to-url.md#credential).  
  
 Specificare l' **URL di archiviazione** per l'account di archiviazione di Azure, le credenziali SQL che archiviano le informazioni di autenticazione per l'account di archiviazione e il periodo di memorizzazione per i file di backup.  
  
 Il formato dell'URL di archiviazione è\<: https://StorageAccount >. blob. Core. Windows. NET/  
  
 Per impostare le impostazioni di crittografia a livello di istanza, selezionare l'opzione **Crittografa backup** e specificare l'algoritmo e un certificato o una chiave asimmetrica da utilizzare per la crittografia.  Questa proprietà è impostata a livello di istanza e viene usata per tutti i nuovi database creati dopo l'applicazione di questa configurazione.  
  
> [!WARNING]  
>  Non è possibile usare questa finestra di dialogo per specificare le opzioni di crittografia senza configurare [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Queste opzioni di crittografia si applicano solo a operazioni [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Per usare la crittografia per altre procedure di backup, vedere [crittografia dei backup](../relational-databases/backup-restore/backup-encryption.md).  
  
### <a name="considerations"></a>Considerazioni  
 Se si configura [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] a livello di istanza, le impostazioni vengono applicate a qualsiasi nuovo database creato successivamente.  Tuttavia, i database esistenti non ereditano automaticamente queste impostazioni. Per configurare [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] su database già esistenti, è necessario configurare ogni database in modo specifico. Per altre informazioni, vedere [abilitare e configurare SQL Server backup gestito in Azure per un database](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md#DatabaseConfigure).  
  
 Se [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] è stato sospeso `smart_admin.sp_backup_master_switch`utilizzando, verrà visualizzato un messaggio di avviso che indica che il backup gestito è disabilitato e che le configurazioni correnti non diverranno effettive. Quando si tenta di completare la configurazione. Usare l' `smart_admin.sp_backup_master_switch` oggetto archiviato e @new_stateimpostare = 1. Questa attività riprenderà i servizi [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] e le impostazioni di configurazione diventeranno attive. Per ulteriori informazioni sulla stored procedure, vedere [smart_admin. sp_ backup_master_switch &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql).  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server backup gestito in Azure: Interoperabilità e coesistenza](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
  
