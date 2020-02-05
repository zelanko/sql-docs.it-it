---
title: Aggiornare gli script di replica (stored procedure di replica)
description: Informazioni su come usare le stored procedure di replica per aggiornare gli script usati per configurare una topologia di replica a livello di programmazione.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- scripts [SQL Server replication], upgrading
- upgrading SQL Server, replicated databases
- upgrading replication applications
- replication [SQL Server], scripting
- replication [SQL Server], upgrading
- upgrading replicated databases
ms.assetid: 0b8720bd-f339-4842-bc8f-b35a46f6d3ee
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: d5c50143bd5bb9e7891e92b6b539446e9df6b652
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "76288358"
---
# <a name="upgrade-replication-scripts-replication-transact-sql-programming"></a>Aggiornamento di script di replica (programmazione Transact-SQL della replica)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  È possibile utilizzare i file script[!INCLUDE[tsql](../../../includes/tsql-md.md)] per configurare a livello di programmazione una topologia di replica. Per altre informazioni, vedere [Concetti di base relativi alle stored procedure del sistema di replica](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md).  
  
> [!IMPORTANT]  
>  Sebbene non sia necessario aggiornare gli script eseguiti da membri del ruolo **sysadmin** , si consiglia di modificare gli script esistenti come descritto in questo argomento. Specificare un account con autorizzazioni minime per ogni agente di replica, come descritto nella sezione relativa alle autorizzazioni necessarie per gli agenti dell'argomento [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 Oltre a offrire un maggior controllo delle autorizzazioni, consentendo di specificare in modo esplicito gli account di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows in cui vengono eseguiti i processi dell'agente di replica, questi miglioramenti apportati alla sicurezza influiscono sulle seguenti stored procedure negli script esistenti:  
  
-   **sp_addpublication_snapshot**  
  
     È ora necessario specificare le credenziali di Windows come `@job_login` e `@job_password` durante l'esecuzione di [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) per creare il processo in cui viene eseguito l'agente snapshot nel server di distribuzione.  
  
-   **sp_addpushsubscription_agent**  
  
     È ora necessario eseguire [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) per aggiungere in modo esplicito un processo e specificare le credenziali di Windows (`@job_login` e `@job_password`) usate per l'esecuzione del processo dell'agente di distribuzione nel server di distribuzione. Nelle versioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]tale operazione viene eseguita automaticamente al momento della creazione di una sottoscrizione push.  
  
-   **sp_addmergepushsubscription_agent**  
  
     È ora necessario eseguire [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) per aggiungere in modo esplicito un processo e specificare le credenziali di Windows (`@job_login` e `@job_password`) usate per l'esecuzione del processo dell'agente di merge nel database di distribuzione. Nelle versioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]tale operazione viene eseguita automaticamente al momento della creazione di una sottoscrizione push.  
  
-   **sp_addpullsubscription_agent**  
  
     È ora necessario specificare le credenziali di Windows come `@job_login` e `@job_password` durante l'esecuzione di [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) per creare il processo in cui viene eseguito l'agente di distribuzione nel Sottoscrittore.  
  
-   **sp_addmergepullsubscription_agent**  
  
     È ora necessario specificare le credenziali di Windows come `@job_login` e `@job_password` durante l'esecuzione di [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) per creare il processo in cui viene eseguito l'agente di merge nel Sottoscrittore.  
  
-   **sp_addlogreader_agent**  
  
     È ora necessario eseguire [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) per aggiungere in modo manuale il processo e specificare le credenziali di Windows usate per l'esecuzione dell'agente di lettura log nel server di distribuzione. Nelle versioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]tale operazione viene eseguita automaticamente al momento della creazione di una pubblicazione transazionale.  
  
-   **sp_addqreader_agent**  
  
     È ora necessario eseguire [sp_addqreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md) per aggiungere in modo manuale il processo e specificare le credenziali di Windows usate per l'esecuzione dell'agente di lettura coda nel server di distribuzione. Nelle versioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]tale operazione viene eseguita automaticamente al momento della creazione di una pubblicazione transazionale con supporto dell'aggiornamento in coda.  
  
 Nel modello di sicurezza introdotto in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] gli agenti di replica stabiliscono sempre le connessioni all'istanza locale di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con l'autenticazione di Windows, usando le credenziali specificate in `@job_name` e `@job_password`. Per informazioni sui requisiti degli account di Windows utilizzati quando si eseguono processi dell'agente di replica, vedere [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
> [!IMPORTANT]  
>  Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se si archiviano le credenziali in un file script, assicurarsi che quest'ultimo sia protetto.  
  
### <a name="to-upgrade-scripts-that-configure-a-snapshot-or-transactional-publication"></a>Per aggiornare gli script di configurazione di una pubblicazione snapshot o transazionale  
  
1.  Nello script esistente, prima di [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), eseguire [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) nel server di pubblicazione nel database di pubblicazione. Specificare le credenziali di Windows usate per l'esecuzione dell'agente di lettura log per `@job_name` e `@job_password`. Se l'agente usa l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per la connessione al server di pubblicazione, è inoltre necessario specificare il valore **0** per `@publisher_security_mode` e le credenziali di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per `@publisher_login` e `@publisher_password`. Verrà creato un processo dell'agente di lettura log per il database di pubblicazione.  
  
    > [!NOTE]  
    >  Questo passaggio è necessario solo per le pubblicazioni transazionali, non per le pubblicazioni snapshot.  
  
2.  (Facoltativo) Prima di [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), eseguire [sp_addqreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md) nel server di distribuzione nel database di distribuzione. Specificare le credenziali di Windows usate per l'esecuzione dell'agente di lettura coda per `@job_name` e `@job_password`. Verrà creato un processo dell'agente di lettura coda per il server di distribuzione.  
  
    > [!NOTE]  
    >  Questo passaggio è necessario solo per le pubblicazioni transazionali che supportano Sottoscrittori ad aggiornamento in coda.  
  
3.  (Facoltativo) Aggiornare l'esecuzione di [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) per impostare eventuali valori non predefiniti per i parametri che implementano nuove funzionalità di replica.  
  
4.  Dopo [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), eseguire [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) nel server di pubblicazione nel database di pubblicazione. Specificare `@publication` e le credenziali di Windows usate per l'esecuzione dell'agente snapshot per `@job_name` e `@job_password`. Se l'agente usa l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per la connessione al server di pubblicazione, è inoltre necessario specificare il valore **0** per `@publisher_security_mode` e le credenziali di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per `@publisher_login` e `@publisher_password`. Verrà creato un processo dell'agente snapshot per la pubblicazione.  
  
5.  (Facoltativo) Aggiornare l'esecuzione di [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) per impostare eventuali valori non predefiniti per i parametri che implementano nuove funzionalità di replica.  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-snapshot-or-transactional-publication"></a>Per aggiornare gli script per l'aggiunta di sottoscrizioni di una pubblicazione snapshot o transazionale  
  
1.  Dopo avere eseguito la stored procedure di creazione della sottoscrizione, assicurarsi di eseguire la stored procedure di creazione di un processo dell'agente di distribuzione per sincronizzare la sottoscrizione. La stored procedure utilizzata varia in base al tipo di sottoscrizione.  
  
    -   Nel caso di una sottoscrizione pull, aggiornare l'esecuzione di [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) in modo da specificare le credenziali di Windows usate per l'esecuzione dell'agente di distribuzione nel Sottoscrittore per `@job_name` e `@job_password`. Tale operazione viene effettuata dopo l'esecuzione di [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md). Per altre informazioni, vedere [Creazione di una sottoscrizione pull](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
    -   Per una sottoscrizione push, eseguire [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) nel server di pubblicazione. Specificare `@subscriber`, `@subscriber_db`, `@publication`, le credenziali di Windows usate per l'esecuzione dell'agente di distribuzione nel server di distribuzione per `@job_name` e `@job_password`, oltre a una pianificazione per il processo dell'agente. Per altre informazioni, vedere [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md). Tale operazione viene effettuata dopo l'esecuzione di [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Per altre informazioni, vedere [Creazione di una sottoscrizione push](../../../relational-databases/replication/create-a-push-subscription.md).  
  
### <a name="to-upgrade-scripts-that-configure-a-merge-publication"></a>Per aggiornare gli script di configurazione di una pubblicazione di tipo merge  
  
1.  (Facoltativo) Nello script esistente aggiornare l'esecuzione di [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) per impostare eventuali valori non predefiniti per i parametri che implementano nuove funzionalità di replica.  
  
2.  Dopo [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), eseguire [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) nel server di pubblicazione nel database di pubblicazione. Specificare `@publication` e le credenziali di Windows usate per l'esecuzione dell'agente snapshot per `@job_name` e `@job_password`. Se l'agente usa l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per la connessione al server di pubblicazione, è inoltre necessario specificare il valore **0** per `@publisher_security_mode` e le credenziali di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per `@publisher_login` e `@publisher_password`. Verrà creato un processo dell'agente snapshot per la pubblicazione.  
  
3.  (Facoltativo) Aggiornare l'esecuzione di [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) per impostare eventuali valori non predefiniti per i parametri che implementano nuove funzionalità di replica.  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-merge-publication"></a>Per aggiornare gli script per l'aggiunta di sottoscrizioni di una pubblicazione di tipo merge  
  
1.  Dopo avere eseguito la stored procedure di creazione della sottoscrizione, assicurarsi di eseguire la stored procedure di creazione di un processo dell'agente di merge per sincronizzare la sottoscrizione. La stored procedure utilizzata varia in base al tipo di sottoscrizione.  
  
    -   Nel caso di una sottoscrizione pull, aggiornare l'esecuzione di [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) in modo da specificare le credenziali di Windows usate per l'esecuzione dell'agente di merge nel Sottoscrittore per `@job_name` e `@job_password`. Tale operazione viene effettuata dopo l'esecuzione di [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Per altre informazioni, vedere [Creazione di una sottoscrizione pull](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
    -   Per una sottoscrizione push, eseguire [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) nel server di pubblicazione. Specificare `@subscriber`, `@subscriber_db`, `@publication`, le credenziali di Windows usate per l'esecuzione dell'agente di merge nel server di distribuzione per `@job_name` e `@job_password`, oltre a una pianificazione per il processo dell'agente. Per altre informazioni, vedere [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md). Tale operazione viene effettuata dopo l'esecuzione di [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md). Per altre informazioni, vedere [Creazione di una sottoscrizione push](../../../relational-databases/replication/create-a-push-subscription.md).  
  
## <a name="example"></a>Esempio  
 Di seguito è riportato un esempio di uno script [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] per la creazione di una pubblicazione transazionale per la tabella Product. Questa pubblicazione supporta l'aggiornamento immediato sostituito dall'aggiornamento in coda come soluzione di failover. I parametri predefiniti sono stati rimossi per una maggiore leggibilità.  
  
 [!code-sql[HowTo#sp_createtranpub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_1.sql)]  
  
## <a name="example"></a>Esempio  
 Di seguito è riportato un esempio dello script precedente per la creazione di una pubblicazione transazionale, aggiornato in modo da essere eseguito correttamente in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versioni successive. Questa pubblicazione supporta l'aggiornamento immediato sostituito dall'aggiornamento in coda come soluzione di failover. I valori predefiniti dei nuovi parametri sono stati dichiarati in modo esplicito.  
  
> [!NOTE]  
>  Le credenziali di Windows vengono specificate in fase di esecuzione mediante variabili di scripting **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createtranpub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_2.sql)]  
  
## <a name="example"></a>Esempio  
 Di seguito è riportato un esempio di uno script [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] per la creazione di una pubblicazione di tipo merge per la tabella Customers. I parametri predefiniti sono stati rimossi per una maggiore leggibilità.  
  
 [!code-sql[HowTo#sp_createmergepub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_3.sql)]  
  
## <a name="example"></a>Esempio  
 Di seguito è riportato un esempio dello script precedente per la creazione di una pubblicazione di tipo merge, aggiornato in modo da essere eseguito correttamente in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versioni successive. I valori predefiniti dei nuovi parametri sono stati dichiarati in modo esplicito.  
  
> [!NOTE]  
>  Le credenziali di Windows vengono specificate in fase di esecuzione mediante variabili di scripting **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createmergepub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_4.sql)]  
  
## <a name="example"></a>Esempio  
 Di seguito è riportato un esempio di uno script [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] per la creazione di una sottoscrizione push di una pubblicazione transazionale. I parametri predefiniti sono stati rimossi per una maggiore leggibilità.  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_5.sql)]  
  
## <a name="example"></a>Esempio  
 Di seguito è riportato un esempio dello script precedente per la creazione di una sottoscrizione push di una pubblicazione transazionale, aggiornato in modo da essere eseguito correttamente in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versioni successive. I valori predefiniti dei nuovi parametri sono stati dichiarati in modo esplicito.  
  
> [!NOTE]  
>  Le credenziali di Windows vengono specificate in fase di esecuzione mediante variabili di scripting **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_6.sql)]  
  
## <a name="example"></a>Esempio  
 Di seguito è riportato un esempio di uno script [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] per la creazione di una sottoscrizione push di una pubblicazione di tipo merge. I parametri predefiniti sono stati rimossi per una maggiore leggibilità.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_7.sql)]  
  
## <a name="example"></a>Esempio  
 Di seguito è riportato un esempio dello script precedente per la creazione di una sottoscrizione push di una pubblicazione di tipo merge, aggiornato in modo da essere eseguito correttamente in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versioni successive. I valori predefiniti dei nuovi parametri sono stati dichiarati in modo esplicito.  
  
> [!NOTE]  
>  Le credenziali di Windows vengono specificate in fase di esecuzione mediante variabili di scripting **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_8.sql)]  
  
## <a name="example"></a>Esempio  
 Di seguito è riportato un esempio di uno script [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] per la creazione di una sottoscrizione pull di una pubblicazione transazionale. I parametri predefiniti sono stati rimossi per una maggiore leggibilità.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_7.sql)]  
  
## <a name="example"></a>Esempio  
 Di seguito è riportato un esempio dello script precedente per la creazione di una sottoscrizione pull di una pubblicazione transazionale, aggiornato in modo da essere eseguito correttamente in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versioni successive. I valori predefiniti dei nuovi parametri sono stati dichiarati in modo esplicito.  
  
> [!NOTE]  
>  Le credenziali di Windows vengono specificate in fase di esecuzione mediante variabili di scripting **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createtranpullsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_9.sql)]  
  
## <a name="example"></a>Esempio  
 Di seguito è riportato un esempio di uno script [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] per la creazione di una sottoscrizione pull di una pubblicazione di tipo merge. I parametri predefiniti sono stati rimossi per una maggiore leggibilità.  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_10.sql)]  
  
## <a name="example"></a>Esempio  
 Di seguito è riportato un esempio dello script precedente per la creazione di una sottoscrizione pull di una pubblicazione di tipo merge, aggiornato in modo da essere eseguito correttamente in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versioni successive. I valori predefiniti dei nuovi parametri sono stati dichiarati in modo esplicito.  
  
> [!NOTE]  
>  Le credenziali di Windows vengono specificate in fase di esecuzione mediante variabili di scripting **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_11.sql)]  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)   
 [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md)   
 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)   
 [Visualizzare e modificare le impostazioni di sicurezza della replica](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [MSSQL_ENG021797](../../../relational-databases/replication/mssql-eng021797.md)   
 [MSSQL_ENG021798](../../../relational-databases/replication/mssql-eng021798.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Aggiornare database replicati](../../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
  
