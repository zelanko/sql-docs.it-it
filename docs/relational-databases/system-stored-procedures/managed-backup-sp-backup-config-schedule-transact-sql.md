---
title: managed_backup. sp_backup_config_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_backup_config_schedule_TSQL
- managed_backup.sp_backup_config_schedule
- managed_backup.sp_backup_config_schedule_TSQL
- sp_backup_config_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- managed_backup.sp_backup_config_schedule
- sp_backup_config_schedule
ms.assetid: 82541160-d1df-4061-91a5-6868dd85743a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 52df69439cecad5fddf3d38b8852a1ce86cc4dbd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67942077"
---
# <a name="managed_backupsp_backup_config_schedule-transact-sql"></a>managed_backup. sp_backup_config_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Configura le opzioni di pianificazione automatizzate o personalizzate [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]per.  
    
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
EXEC managed_backup.sp_backup_config_schedule   
    [@database_name = ] 'database_name'
    ,[@scheduling_option = ] {'Custom' | 'System'}  
    ,[@full_backup_freq_type = ] {'Daily' | 'Weekly'}  
    ,[@days_of_week = ] 'days_of_the_week'  
    ,[@backup_begin_time = ] 'begin time of the backup window'  
    ,[@backup_duration = ] 'backup window length'  
    ,[@log_backup_freq = ] 'frequency of log backup'  
```  
  
##  <a name="Arguments"></a> Argomenti  
 @database_name  
 Nome del database per l'abilitazione del backup gestito in un database specifico. Se è NULL o *, questo backup gestito si applica a tutti i database nel server.  
  
 @scheduling_option  
 Specificare "System" per la pianificazione dei backup controllata dal sistema. Specificare ' Custom ' per una pianificazione personalizzata definita dagli altri parametri dell'.  
  
 @full_backup_freq_type  
 Tipo di frequenza per l'operazione di backup gestito, che può essere impostata su' Daily ' o ' Weekly '.  
  
 @days_of_week  
 I giorni della settimana per i backup quando @full_backup_freq_type è impostato su settimanale. Specificare nomi di stringa completi, ad esempio ' Monday '.  È anche possibile specificare più di un nome di giorno, separati dalla pipe. Ad esempio N'Monday | Mercoledì | Venerdì.  
  
 @backup_begin_time  
 Ora di inizio della finestra di backup. I backup non verranno avviati al di fuori dell'intervallo di tempo, definito da una combinazione di @backup_begin_time e @backup_duration.  
  
 @backup_duration  
 Durata dell'intervallo di tempo di backup. Si noti che non esiste alcuna garanzia che i backup vengano completati durante l'intervallo di tempo @backup_begin_time definito @backup_durationda e. Le operazioni di backup avviate in questo intervallo di tempo ma che superano la durata della finestra non verranno annullate.  
  
 @log_backup_freq  
 Ciò determina la frequenza dei backup del log delle transazioni. Questi backup avvengono a intervalli regolari anziché alla pianificazione specificata per i backup del database. @log_backup_freqpuò essere in minuti o ore e 0 è valido, che indica nessun backup del log. La disabilitazione dei backup del log è appropriata solo per i database con un modello di recupero con registrazione minima.  
  
> [!NOTE]  
>  Se il modello di recupero viene modificato da semplice a completo, è necessario riconfigurare il log_backup_freq da 0 a un valore diverso da zero.  
  
## <a name="return-code-value"></a>Valore del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo **db_backupoperator** database, con autorizzazioni **ALTER ANY CREDENTIAL** e autorizzazioni **Execute** per **sp_delete_backuphistory** stored procedure.  
  
## <a name="see-also"></a>Vedere anche  
 [managed_backup. sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup. sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)  
  
  
