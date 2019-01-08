---
title: Oggetti di configurazione di Posta elettronica database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqlimail.manageexistingaccount.f1
- sql12.swb.sqlimail.addaccounttoprofile.f1
- sql12.swb.sqlmailconfiguration.f1
- sql12.swb.sqlimail.profileandaccountmanagement.f1
- sql12.swb.sqlimail.manageprofilesecurity.principalview.f1
- sql12.swb.sqlimail.newsqlimailaccount.f1
- sql12.swb.sqlimail.configuresystem.f1
- sql12.swb.sqlimail.selectconfiguration.f1
- sql12.swb.sqlimail.newprofile.f1
- sql12.swb.sqlimail.manageexistingprofile.f1
- sql12.swb.sqlimail.welcome.f1
- sql12.swb.sqlimail.manageprofilesecurity.profileview.f1
- sql12.swb.sqlimail.completewizard.f1
- sql12.swb.sqlimail.newaccount.f1
helpviewer_keywords:
- Database Mail [SQL Server], configuration objects
- Database Mail [SQL Server], accounts
- configuration objects [Database Mail]
- Database Mail [SQL Server], profiles
- profiles [SQL Server], Database Mail
- accounts [Database Mail]
ms.assetid: 03f6e4c0-04ff-490a-bd91-637806215bd1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 71a2805eb935088f39c6b4a86714f263dc5ba643
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52772635"
---
# <a name="database-mail-configuration-objects"></a>Oggetti di configurazione di Posta elettronica database
  Posta elettronica database ha due oggetti di configurazione: Gli oggetti di configurazione database forniscono una modalità per configurare le impostazioni di tale Database di posta elettronica deve utilizzare quando si invia un messaggio di posta elettronica dall'applicazione di database o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dell'agente.  
  
-   Account di Posta elettronica database  
  
-   Profili di Posta elettronica database  
  
  
##  <a name="VisualElement"></a> Relazione tra oggetti di configurazione di Posta elettronica database  
 Nella figura seguente vengono illustrati due profili, tre account e tre utenti. User 1 può accedere a Profile 1, che usa Account 1 e Account 2. User 3 può accedere a Profile 2, che utilizza Account 2 e Account 3. User 2 può accedere sia a Profile 1 che a Profile 2.  
  
 ![Relazioni tra utenti, profili e account](../../database-engine/media/databasemailprofileaccount.gif "Relazioni tra utenti, profili e account")  
  
  
##  <a name="DBAccount"></a> Account di Posta elettronica database  
 Un account di Posta elettronica database contiene le informazioni utilizzate in Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'invio di messaggi di posta elettronica a un server SMTP. In ogni account sono incluse le informazioni per un singolo server di posta elettronica.  
  
 Posta elettronica database supporta tre metodi di autenticazione per la comunicazione con un server SMTP:  
  
-   Autenticazione di Windows: Posta elettronica database utilizza le credenziali del [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] Windows account del servizio per l'autenticazione nel server SMTP.  
  
-   Autenticazione di base:  Posta elettronica database utilizza il nome utente e la password specificati per l'autenticazione nel server SMTP.  
  
-   Autenticazione anonima:  Il server SMTP non richiede alcuna autenticazione.  Posta elettronica database non utilizzerà credenziali per l'autenticazione nel server SMTP.  
  
 Le informazioni sull'account vengono archiviate nel database **msdb** . Ciascun account include le informazioni seguenti:  
  
-   Nome dell'account.  
  
-   Descrizione dell'account.  
  
-   Indirizzo di posta elettronica dell'account.  
  
-   Nome visualizzato dell'account.  
  
-   Indirizzo di posta elettronica di risposta dell'account.  
  
-   Nome del server di posta elettronica.  
  
-   Tipo del server di posta elettronica. Per [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]corrisponde sempre a Simple Mail Transfer Protocol (SMTP).  
  
-   Numero di porta del server di posta elettronica.  
  
-   Colonna bit che indica se la connessione al server di posta elettronica SMTP viene eseguita utilizzando Secure Sockets Layer (SSL).  
  
-   Colonna bit che indica se la connessione al server SMTP viene eseguita tramite le credenziali configurate per [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)].  
  
-   Nome utente da utilizzare per l'autenticazione al server di posta elettronica, se tale server richiede l'autenticazione.  
  
-   Password da utilizzare per l'autenticazione al server di posta elettronica, se tale server richiede l'autenticazione.  
  
 La Configurazione guidata posta elettronica database consente di creare e gestire account in modo rapido e semplice. Per la creazione e la gestione di account è anche possibile utilizzare le stored procedure di configurazione incluse in **msdb** .  
  
  
##  <a name="DBProfile"></a> Profilo di Posta elettronica database  
 Un profilo di Posta elettronica database è una raccolta ordinata di account di Posta elettronica database correlati. Le applicazioni che inviano messaggi di posta elettronica utilizzando Posta elettronica database specificano i profili, anziché utilizzare direttamente gli account. La separazione delle informazioni relative ai singoli server di posta elettronica dagli oggetti utilizzati dall'applicazione consente di migliorare la flessibilità e l'affidabilità. I profili offrono infatti il failover automatico e se un server è bloccato, Posta elettronica database invia automaticamente la posta a un altro server di posta elettronica. Gli amministratori di database possono aggiungere, rimuovere o riconfigurare gli account senza che sia necessario apportare modifiche al codice dell'applicazione o ai passaggi del processo.  
  
 I profili consentono inoltre di controllare l'accesso alla posta elettronica. L'appartenenza a **DatabaseMailUserRole** è necessaria per l'invio in Posta elettronica database. I profili consentono un'ulteriore flessibilità agli amministratori nel controllo di chi invia i messaggi e di quali account vengono utilizzati.  
  
 che possono essere pubblici o privati.  
  
 I**profili pubblici** sono disponibili per tutti i membri del ruolo del database **DatabaseMailUserRole** nel database **msdb** . Questi consentono a tutti i membri del ruolo **DatabaseMailUserRole** di inviare messaggi di posta elettronica tramite il profilo.  
  
 I**profili privati** vengono definiti per le entità di sicurezza nel database **msdb** . Solo gli utenti e i ruoli del database specificati e i membri del ruolo predefinito del server **sysadmin** possono inviare messaggi di posta elettronica tramite il profilo. Per impostazione predefinita, i profili sono privati e solo i membri del ruolo predefinito del server **sysadmin** possono accedervi. Per utilizzare un profilo privato, è necessario che **sysadmin** conceda agli utenti l'autorizzazione a utilizzare il profilo. L'autorizzazione EXECUTE sulla stored procedure **sp_send_dbmail** , poi, viene concessa solo ai membri di **DatabaseMailUserRole**. Perché l'utente possa inviare messaggi di posta elettronica, un amministratore di sistema deve aggiungere l'utente al ruolo del database **DatabaseMailUserRole** .  
  
 I profili migliorano l'affidabilità nei casi in cui un server di posta elettronica diventa irraggiungibile o non in grado di elaborare i messaggi. Ogni account del profilo è caratterizzato da un numero di sequenza. Il numero di sequenza determina l'ordine in cui Posta elettronica database utilizza gli account nel profilo. Per un nuovo messaggio di posta elettronica, Posta elettronica database utilizza l'ultimo account che ha inviato un messaggio di posta elettronica con esito positivo, o l'account che presenta il numero di sequenza più basso nel caso non siano stati ancora inviati messaggi. Se l'invio del messaggio con tale account ha esito negativo, Posta elettronica database prova con l'account con il numero di sequenza successivo e così via, finché il messaggio non viene inviato o finché anche l'invio con l'account con il numero di sequenza più alto non ha esito negativo. Se l'invio del messaggio con l'account con il numero di sequenza più alto non riesce, Posta elettronica database sospende i tentativi di invio del messaggio per il periodo di tempo specificato nel parametro **AccountRetryDelay** di **sysmail_configure_sp**. Trascorso questo periodo di tempo, Posta elettronica database prova di nuovo a inviare il messaggio, iniziando con l'account con il numero di sequenza più basso. Usare il parametro **AccountRetryAttempts** di **sysmail_configure_sp**per specificare quante volte il processo di posta elettronica esterno deve tentare di inviare il messaggio di posta elettronica usando ogni account indicato del profilo specificato.  
  
 Se esistono più account con lo stesso numero di sequenza, Posta elettronica database utilizza solo uno di questi account per un messaggio di posta specifico. In questo caso, non viene garantito quale account viene utilizzato per quel numero di sequenza né che venga utilizzato lo stesso account per ogni messaggio.  
  
  
##  <a name="RelatedTasks"></a> Attività di configurazione di Posta elettronica database  
 Nella tabella seguente vengono descritte le attività di configurazione di Posta elettronica database.  
  
|Attività di configurazione|Collegamento all'argomento|  
|------------------------|----------------|  
|Viene illustrata la creazione di account di Posta elettronica database|[Creare un account di Posta elettronica database.](create-a-database-mail-account.md)|  
|Viene illustrata la creazione di profili di Posta elettronica database|[Creare un profilo di Posta elettronica database](create-a-database-mail-profile.md)|  
|Viene illustrata la configurazione di Posta elettronica database|[Configurare Posta elettronica database](configure-database-mail.md)|  
|Viene illustrata la creazione di uno script di configurazione per Posta elettronica database utilizzando i modelli||  
  
  
##  <a name="Add_Tasks"></a> Attività aggiuntive di configurazione di Posta elettronica database (Stored procedure di sistema)  
 Le stored procedure per la configurazione di Posta elettronica database sono disponibili nel database **msdb** .  
  
 Nelle tabelle seguenti vengono elencate le stored procedure utilizzate per la configurazione e la gestione di Posta elettronica database.  
  
### <a name="database-mail-settings"></a>Impostazioni di Posta elettronica database  
  
|nome|Descrizione|  
|----------|-----------------|  
|[sysmail_configure_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql)|Modifica le impostazioni di configurazione per Posta elettronica database.|  
|[sysmail_help_configure_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-help-configure-sp-transact-sql)|Visualizza le impostazioni di configurazione per Posta elettronica database.|  
  
### <a name="accounts-and-profiles"></a>Account e profili  
  
|nome|Descrizione|  
|----------|-----------------|  
|[sysmail_add_profileaccount_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql)|Aggiunge un account di posta a un profilo di Posta elettronica database.|  
|[sysmail_delete_account_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-delete-account-sp-transact-sql)|Elimina un account di Posta elettronica database.|  
|[sysmail_delete_profile_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-delete-profile-sp-transact-sql)|Elimina un profilo di Posta elettronica database.|  
|[sysmail_delete_profileaccount_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-delete-profileaccount-sp-transact-sql)|Rimuove un account da un profilo di Posta elettronica database.|  
|[sysmail_help_account_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-help-account-sp-transact-sql)|Elenca informazioni relative agli account di Posta elettronica database.|  
|[sysmail_help_profile_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-help-profile-sp-transact-sql)|Elenca informazioni relative a uno o più profili di Posta elettronica database.|  
|[sysmail_help_profileaccount_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-help-profileaccount-sp-transact-sql)|Elenca gli account associati a uno o più profili di Posta elettronica database.|  
|[sysmail_update_account_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-update-account-sp-transact-sql)|Aggiorna le informazioni in un account di Posta elettronica database esistente.|  
|[sysmail_update_profile_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-update-profile-sp-transact-sql)|Modifica la descrizione o il nome di un profilo di Posta elettronica database.|  
|[sysmail_update_profileaccount_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-update-profileaccount-sp-transact-sql)|Aggiorna il numero di sequenza di un account in un profilo di Posta elettronica database.|  
  
### <a name="security"></a>Sicurezza  
  
|nome|Descrizione|  
|----------|-----------------|  
|[sysmail_add_principalprofile_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql)|Concede le autorizzazioni necessarie a una entità database per utilizzare un profilo di Posta elettronica database.|  
|[sysmail_delete_principalprofile_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-delete-principalprofile-sp-transact-sql)|Rimuove le autorizzazioni che consentono a un utente di database di utilizzare un profilo pubblico o privato di Posta elettronica database.|  
|[sysmail_help_principalprofile_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-help-principalprofile-sp-transact-sql)|Elenca le informazioni relative al profilo di Posta elettronica database per un determinato utente di database.|  
|[sysmail_update_principalprofile_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-update-principalprofile-sp-transact-sql)|Aggiorna le informazioni relative alle autorizzazioni per un determinato utente di database.|  
  
### <a name="system-state"></a>Stato del sistema  
  
|nome|Descrizione|  
|----------|-----------------|  
|[sysmail_start_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql)|Avvia il programma esterno Posta elettronica database e la coda associata di SQL Service Broker.|  
|[sysmail_stop_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql)|Arresta il programma esterno Posta elettronica database e la coda associata di SQL Service Broker.|  
|[sysmail_help_status_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-help-status-sp-transact-sql)|Indica se Posta elettronica database è stato avviato.|  
  
##  <a name="RelatedContent"></a> Riferimenti aggiuntivi  
  
-   [Controlli e registrazione di Posta elettronica database](database-mail-log-and-audits.md)  
  
  
  
