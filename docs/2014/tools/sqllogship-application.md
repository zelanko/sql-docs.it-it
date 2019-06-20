---
title: Applicazione sqllogship | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- sqllogship
ms.assetid: 8ae70041-f3d9-46e4-8fa8-31088572a9f8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 14b9cda05bca998bd113a316692c4c2c2111d091
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63035067"
---
# <a name="sqllogship-application"></a>Applicazione sqllogship
  L'applicazione **sqllogship** esegue un'operazione di backup, copia o ripristino e le attività di pulizia associate per una configurazione per il log shipping. L'operazione viene eseguita su una specifica istanza di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per un database specifico.  
  
 ![Icona di collegamento un argomento](../../2014/database-engine/media/topic-link.gif "icona di collegamento argomento") per le convenzioni della sintassi, vedere [prompt dei comandi di riferimento all'utilità &#40;motore di Database&#41;](../tools/command-prompt-utility-reference-database-engine.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sqllogship  
-server  
instance_name { -backupprimary_id | -copysecondary_id | -restoresecondary_id } [ -verboselevellevel ] [ -logintimeouttimeout_value ] [ -querytimeouttimeout_value ]  
```  
  
## <a name="arguments"></a>Argomenti  
 **-server** _instance_name_  
 Specifica l'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in cui verrà eseguita l'operazione. L'istanza del server da specificare dipende dall'operazione di distribuzione dei log specificata. Nel caso dell'operazione **-backup**, *instance_name* deve essere il nome del server primario in una configurazione per il log shipping. Nel caso di un'operazione **-copy** o **-restore**, *instance_name* deve essere il nome del server secondario in una configurazione per il log shipping.  
  
 **-backup** _primary_id_  
 Esegue un'operazione di backup per il database primario corrispondente all'ID primario specificato tramite *primary_id*. Per ottenere questo ID, selezionarlo dalla tabella di sistema [log_shipping_primary_databases](/sql/relational-databases/system-tables/log-shipping-primary-databases-transact-sql) oppure usare la stored procedure [sp_help_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql) .  
  
 L'operazione di backup crea il backup del log nella directory di backup. L'applicazione **sqllogship** elimina quindi tutti i file di backup meno recenti in base al periodo di conservazione dei file. La cronologia per l'operazione di backup viene poi registrata dall'applicazione nel server primario e nel server di monitoraggio. L'applicazione esegue infine [sp_cleanup_log_shipping_history](/sql/relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql)che elimina le informazioni sulla cronologia meno recenti in base al periodo di conservazione.  
  
 **-copy** _secondary_id_  
 Esegue un'operazione di copia per copiare i backup dal server secondario specificato per il database o i database secondari, corrispondenti all'ID secondario specificato tramite *secondary_id*. Per ottenere questo ID, selezionarlo dalla tabella di sistema [log_shipping_secondary](/sql/relational-databases/system-tables/log-shipping-secondary-transact-sql) oppure usare la stored procedure [sp_help_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql) .  
  
 L'operazione copia i file di backup dalla directory di backup alla directory di destinazione. L'applicazione **sqllogship** registra quindi la cronologia per l'operazione di copia nel server secondario e nel server di monitoraggio.  
  
 **-restore** _secondary_id_  
 Esegue un'operazione di ripristino nel server secondario specificato per il database o i database secondari, corrispondenti all'ID secondario specificato tramite *secondary_id*. Per ottenere questo ID è possibile usare la stored procedure **sp_help_log_shipping_secondary_database** .  
  
 Tutti i file di backup nella directory di destinazione creati dopo il punto di ripristino più recente vengono ripristinati nel database o nei database secondari. L'applicazione **sqllogship** elimina quindi tutti i file di backup meno recenti in base al periodo di conservazione dei file. La cronologia per l'operazione di ripristino viene poi registrata dall'applicazione nel server secondario e nel server di monitoraggio. L'applicazione esegue infine **sp_cleanup_log_shipping_history**che elimina le informazioni sulla cronologia meno recenti in base al periodo di conservazione.  
  
 **-verboselevel** _level_  
 Specifica il livello di messaggi aggiunti alla cronologia di log shipping. *level* può essere uno dei valori interi seguenti:  
  
|level|Descrizione|  
|-----------|-----------------|  
|0|L'output non include messaggi di traccia e di debug.|  
|1|L'output include messaggi di gestione degli errori.|  
|2|L'output include messaggi di avviso e di gestione degli errori.|  
|**3**|L'output include messaggi informativi, di avviso e di gestione degli errori. Rappresenta il valore predefinito.|  
|4|L'output include tutti i messaggi di debug e di traccia.|  
  
 **-logintimeout** _timeout_value_  
 Specifica la quantità di tempo assegnata per un tentativo di accesso all'istanza del server prima del timeout. Il valore predefinito è 15 secondi. *timeout_value* is **int**_._  
  
 **-querytimeout** _timeout_value_  
 Specifica la quantità di tempo assegnata per l'avvio dell'operazione specificata prima del timeout del tentativo. Il valore predefinito non prevede un periodo di timeout. *timeout_value* is **int**_._  
  
## <a name="remarks"></a>Note  
 È consigliabile utilizzare i processi di backup, copia e ripristino per eseguire le operazioni corrispondenti, quando possibile. Per avviare questi processi da un'operazione batch o un'altra applicazione, chiamare la stored procedure [sp_start_job](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql) .  
  
 La cronologia di log shipping creata da **sqllogship** è intercalata dalla cronologia creata dai processi di backup, copia e ripristino del log shipping. Se si prevede di usare ripetutamente **sqllogship** per eseguire operazioni di backup, copia o ripristino per una configurazione per il log shipping, prendere in considerazione di disabilitare il processo o i processi per il log shipping corrispondenti. Per altre informazioni, vedere [Disable or Enable a Job](../ssms/agent/disable-or-enable-a-job.md).  
  
 Il **sqllogship** applicazione SqlLogShip.exe, viene installato nella directory Programmi\Microsoft SQL Server\120\Tools\Binn x:\Programmi\Microsoft.  
  
## <a name="permissions"></a>Permissions  
 **sqllogship** usa l'autenticazione di Windows. L'account con autenticazione di Windows utilizzato per l'esecuzione del comando deve disporre delle autorizzazioni di accesso alle directory di Windows e delle autorizzazioni per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Il requisito dipende dal fatto che il comando **sqllogship** specifichi l'opzione **-backup**, **-copy**oppure **-restore** .  
  
|Opzione|Accesso alla directory|Permissions|  
|------------|----------------------|-----------------|  
|**-backup**|È richiesto l'accesso in lettura/scrittura alla directory di backup.|Sono richieste le stesse autorizzazioni necessarie per l'istruzione BACKUP. Per altre informazioni, vedere [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).|  
|**-copy**|È richiesto l'accesso in lettura alla directory di backup e l'accesso in scrittura alla directory di copia.|Sono richieste le stesse autorizzazioni necessarie per la stored procedure [sp_help_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql) .|  
|**-restore**|È richiesto l'accesso in lettura/scrittura alla directory di copia.|Sono richieste le stesse autorizzazioni necessarie per l'istruzione RESTORE. Per altre informazioni, vedere [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).|  
  
> [!NOTE]  
>  Per trovare i percorsi delle directory di backup e di copia, è possibile eseguire la stored procedure **sp_help_log_shipping_secondary_database** o visualizzare la tabella **log_shipping_secondary** in **msdb**. I percorsi della directory di backup e della directory di destinazione sono indicati rispettivamente nelle colonne **backup_source_directory** e **backup_destination_directory** .  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sul log shipping &#40;SQL Server&#41;](../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [log_shipping_primary_databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/log-shipping-primary-databases-transact-sql)   
 [log_shipping_secondary &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/log-shipping-secondary-transact-sql)   
 [sp_cleanup_log_shipping_history &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql)   
 [sp_help_log_shipping_primary_database &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql)   
 [sp_help_log_shipping_secondary_database &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql)   
 [sp_start_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql)  
  
  
