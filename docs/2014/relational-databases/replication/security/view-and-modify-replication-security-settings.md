---
title: Visualizzare e modificare le impostazioni di sicurezza della replica | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- modifying replication security settings
- replication [SQL Server], security
- security [SQL Server replication], viewing settings
- viewing replication security settings
- security [SQL Server replication], modifying settings
ms.assetid: 67d79532-1482-4de1-ac9f-4a23d162c85e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 923d137b4b884300b2fb31cbacf2ee7dff1a6621
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "73912796"
---
# <a name="view-and-modify-replication-security-settings"></a>Visualizzazione e modifica delle impostazioni di sicurezza della replica
  In questo argomento viene descritto come visualizzare e modificare le impostazioni di sicurezza della replica in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o RMO (Replication Management Objects). È ad esempio possibile modificare la connessione dell'agente di lettura log al server di pubblicazione passando dall'autenticazione di SQL Server all'autenticazione integrata di Windows oppure potrebbe essere necessario modificare le credenziali utilizzate per eseguire un processo di agente al momento della modifica della password dell'account di Windows. Per informazioni sulle autorizzazioni richieste per ogni agente, vedere [Modello di sicurezza dell'agente di replica](replication-agent-security-model.md).  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per visualizzare e modificare le impostazioni di sicurezza della replica, utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Oggetti RMO (Replication Management Objects)](#RMOProcedure)  
  
-   **Completamento:**  [dopo avere modificato le impostazioni di sicurezza della replica](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Le stored procedure utilizzate dipenderanno dal tipo di agente e dal tipo di connessione al server.  
  
-   Le classi e le proprietà RMO utilizzate dipendono dal tipo di agente e dal tipo di connessione al server.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
 Per motivi di sicurezza, i valori effettivi delle password vengono mascherati nei set di risultati restituiti dalle stored procedure di replica.  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 Visualizzare e modificare le impostazioni di sicurezza nelle seguenti finestre di dialogo:  
  
1.  La finestra di dialogo **Aggiorna password di replica** , disponibile nella cartella **Replica** di [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Se si modifica la password di un account [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o Windows su un server di una topologia di replica, utilizzare questa finestra di dialogo anziché aggiornare la password per ogni agente che utilizza l'account. Se gli agenti di più server utilizzano lo stesso account, è necessario connettersi a ogni server e modificare la password. La password viene aggiornata in tutte le posizioni in cui viene utilizzata per la replica ma non viene aggiornata in altre posizioni, come i server collegati.  
  
2.  La pagina **Sicurezza agente** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** . Per ulteriori informazioni sull'accesso a questa finestra di dialogo, vedere [View and Modify Publication Properties](../publish/view-and-modify-publication-properties.md).  
  
3.  La finestra di dialogo **Proprietà sottoscrizione - \<Sottoscrizione>** . Per ulteriori informazioni sull'accesso a questa finestra di dialogo, vedere [View and Modify Push Subscription Properties](../view-and-modify-push-subscription-properties.md) e [View and Modify Pull Subscription Properties](../view-and-modify-pull-subscription-properties.md).  
  
4.  Le finestre di dialogo **Proprietà server di distribuzione - \<ServerDistribuzione>** e **Proprietà database di distribuzione - \<Database>** . Per ulteriori informazioni sull'accesso a queste finestre di dialogo, vedere [View and Modify Distributor and Publisher Properties](../view-and-modify-distributor-and-publisher-properties.md).  
  
5.  La finestra di dialogo **Proprietà server di pubblicazione - \<ServerPubblicazione>** . Per ulteriori informazioni sull'accesso a questa finestra di dialogo, [View and Modify Distributor and Publisher Properties](../view-and-modify-distributor-and-publisher-properties.md).  
  
#### <a name="to-change-the-password-for-an-account-used-by-one-or-more-agents"></a>Per modificare la password di un account utilizzato da uno o più agenti  
  
1.  Se l'account è di SQL Server, nella finestra di dialogo verrà modificata anche la password per tale account. Se l'account è di Windows, modificare innanzitutto la password in Windows. Per ulteriori informazioni, vedere la documentazione di Windows.  
  
    > [!NOTE]  
    >  Dopo aver modificato una password per la replica è necessario arrestare e riavviare ogni agente che utilizza la password prima che la modifica abbia effetto per tale agente.  
  
2.  Connettersi al server in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]e quindi espandere il nodo del server.  
  
3.  Fare clic con il pulsante destro del mouse sulla cartella **Replica** e quindi scegliere **Aggiorna password replica**.  
  
4.  Nella finestra di dialogo **Aggiorna password replica** specificare l'account e la nuova password.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-snapshot-agent"></a>Per modificare le impostazioni di sicurezza per l'agente snapshot  
  
1.  Nella pagina **Sicurezza agente** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** , fare clic sul pulsante **Impostazioni di sicurezza** accanto alla casella di testo **Agente snapshot**.  
  
2.  Nella finestra di dialogo **Sicurezza agente snapshot** specificare l'account con il quale eseguire l'agente:  
  
    -   Immettere un nuovo account di Windows nella casella di testo **Account processo** .  
  
    -   Immettere una nuova password complessa nelle caselle di testo **Password** e **Conferma password** .  
  
3.  Specificare il contesto in cui l'agente deve connettersi dal server di distribuzione al server di pubblicazione. Se si seleziona **Tramite l'account di accesso di SQL Server seguente**, è anche necessario specificare l'account di accesso:  
  
    -   Immettere un account di accesso nella casella di testo **Account di accesso**  
  
    -   Immettere una nuova password complessa nelle caselle di testo **Password** e **Conferma password** .  
  
    > [!NOTE]  
    >  Se il server di pubblicazione è Oracle, il contesto di connessione viene specificato nella finestra di dialogo **Proprietà server di distribuzione - \<ServerDistribuzione>** . Per la procedura di modifica del contesto, vedere di seguito.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-log-reader-agent"></a>Per modificare le impostazioni di sicurezza per l'agente di lettura log  
  
1.  Nella pagina **Sicurezza agente** della finestra di dialogo **Proprietà server di pubblicazione - \<Pubblicazione>** fare clic sul pulsante **Impostazioni sicurezza** accanto alla casella di testo **Agente di lettura log**.  
  
2.  Nella finestra di dialogo **Sicurezza agente di lettura log** specificare l'account con il quale eseguire l'agente:  
  
    -   Immettere un nuovo account di Windows nella casella di testo **Account processo**  
  
    -   Immettere una nuova password complessa nelle caselle di testo **Password** e **Conferma password** .  
  
3.  Specificare il contesto in cui l'agente deve connettersi dal server di distribuzione al server di pubblicazione. Se si seleziona **Tramite l'account di accesso di SQL Server seguente**, è anche necessario specificare l'account di accesso:  
  
    -   Immettere un account di accesso nella casella di testo **Account di accesso**  
  
    -   Immettere una nuova password complessa nelle caselle di testo **Password** e **Conferma password** .  
  
    > [!NOTE]  
    >  Se il server di pubblicazione è Oracle, il contesto di connessione viene specificato nella finestra di dialogo **Proprietà server di distribuzione - \<ServerDistribuzione>** . Modificare il contesto utilizzando la procedura descritta di seguito.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  A ogni database pubblicato è associato un agente di lettura log. La modifica delle impostazioni di sicurezza per l'agente di una pubblicazione influisce sulle impostazioni di tutte le pubblicazioni del database di pubblicazione.  
  
#### <a name="to-change-the-context-under-which-the-snapshot-agent-and-log-reader-agent-for-an-oracle-publication-make-connections-to-the-publisher"></a>Per modificare il contesto in cui l'agente snapshot e l'agente di lettura log di un'applicazione Oracle stabiliscono connessioni con il server di pubblicazione  
  
1.  Nella pagina **Server di pubblicazione** della finestra di dialogo **Proprietà server di distribuzione - \<ServerDistribuzione>** fare clic sul pulsante delle proprietà ( **...** ) accanto a un server di pubblicazione.  
  
2.  Nella sezione **Connessione agente al server di pubblicazione** specificare l'account di accesso e la password utilizzati con lo schema utente di amministrazione della replica configurato. Per altre informazioni, vedere [Configurare un server di pubblicazione Oracle](../non-sql/configure-an-oracle-publisher.md).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-push-subscription"></a>Per modificare le impostazioni di sicurezza dell'agente di distribuzione per una sottoscrizione push  
  
1.  Nella finestra di dialogo **Proprietà sottoscrizione - \<Sottoscrizione>** del server di pubblicazione è possibile apportare le modifiche seguenti:  
  
    -   Per modificare l'account utilizzato per eseguire l'agente di distribuzione e stabilire connessioni con il server di distribuzione, fare clic sulla riga **Account processo agente** e quindi sul pulsante delle proprietà ( **…** ) nella riga. Specificare un account e una password nella finestra di dialogo **Sicurezza agente di distribuzione** .  
  
    -   Per modificare il contesto nel quale l'agente di distribuzione esegue la connessione al Sottoscrittore, fare clic sulla riga **Connessione al Sottoscrittore** e quindi sul pulsante delle proprietà ( **…** ) nella riga. Specificare il contesto nella finestra di dialogo **Immissione delle informazioni per la connessione** .  
  
         Se si utilizzano sottoscrizioni ad aggiornamento in coda, anche l'agente di lettura coda utilizzerà il contesto specificato per le connessioni al Sottoscrittore.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-pull-subscription"></a>Per modificare le impostazioni di sicurezza dell'agente di distribuzione per una sottoscrizione pull  
  
1.  Nella finestra di dialogo **Proprietà sottoscrizione - \<Sottoscrizione>** del Sottoscrittore è possibile apportare le modifiche seguenti:  
  
    -   Per modificare l'account utilizzato per eseguire l'agente di distribuzione e stabilire connessioni con il Sottoscrittore, fare clic sulla riga **Account processo agente** e quindi sul pulsante delle proprietà ( **…** ) nella riga. Specificare un account e una password nella finestra di dialogo **Sicurezza agente di distribuzione** .  
  
         Se si utilizzano sottoscrizioni ad aggiornamento in coda, anche l'agente di lettura coda utilizzerà il contesto specificato per le connessioni al Sottoscrittore.  
  
    -   Per modificare il contesto nel quale l'agente di distribuzione esegue la connessione al server di distribuzione, fare clic sulla riga **Connessione server di distribuzione** e quindi sul pulsante delle proprietà ( **…** ) nella riga. Specificare il contesto nella finestra di dialogo **Immissione delle informazioni per la connessione** .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-push-subscription"></a>Per modificare le impostazioni di sicurezza dell'agente di merge per una sottoscrizione push  
  
1.  Nella finestra di dialogo **Proprietà sottoscrizione - \<Sottoscrizione>** del server di pubblicazione è possibile apportare le modifiche seguenti:  
  
    -   Per modificare l'account utilizzato per eseguire l'agente di merge e stabilire connessioni con il server di pubblicazione e il server di distribuzione, fare clic sulla riga **Account processo agente** e quindi sul pulsante delle proprietà ( **…** ) nella riga. Specificare un account e una password nella finestra di dialogo **Sicurezza agente di merge** .  
  
    -   Per modificare il contesto nel quale l'agente di merge esegue la connessione al Sottoscrittore, fare clic sulla riga **Connessione al Sottoscrittore** e quindi sul pulsante delle proprietà ( **…** ) nella riga. Specificare il contesto nella finestra di dialogo **Immissione delle informazioni per la connessione** .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-pull-subscription"></a>Per modificare le impostazioni di sicurezza dell'agente di merge per una sottoscrizione pull  
  
1.  Nella finestra di dialogo **Proprietà sottoscrizione - \<Sottoscrizione>** del Sottoscrittore è possibile apportare le modifiche seguenti:  
  
    -   Per modificare l'account utilizzato per eseguire l'agente di merge e stabilire connessioni con il Sottoscrittore, fare clic sulla riga **Account processo agente** e quindi sul pulsante delle proprietà ( **…** ) nella riga. Specificare un account e una password nella finestra di dialogo **Sicurezza agente di merge** .  
  
    -   Per modificare il contesto nel quale l'agente di merge esegue la connessione al server di pubblicazione e al server di distribuzione, fare clic sulla riga **Connessione server di pubblicazione** e quindi sul pulsante delle proprietà ( **…** ) nella riga. Specificare il contesto nella finestra di dialogo **Immissione delle informazioni per la connessione** .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-the-account-under-which-the-queue-reader-agent-runs"></a>Per modificare l'account per l'esecuzione dell'agente di lettura coda  
  
1.  Nella pagina **Generale** della finestra di dialogo **Proprietà server di distribuzione - \<ServerDistribuzione>** fare clic sul pulsante delle proprietà ( **…** ) accanto al database di distribuzione.  
  
2.  Nella finestra di dialogo **Proprietà database di distribuzione - \<Database>** fare clic sul pulsante **Impostazioni di sicurezza** accanto alla casella di testo **Account processo agente**.  
  
3.  Nella finestra di dialogo **Sicurezza agente di lettura coda** specificare l'account utilizzato per eseguire l'agente e stabilire connessioni con il server di distribuzione:  
  
    -   Immettere un nuovo account di Windows nella casella di testo **Account processo**  
  
    -   Immettere una nuova password complessa nelle caselle di testo **Password** e **Conferma password** .  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  A ogni database di distribuzione è associato un agente di lettura coda. La modifica delle impostazioni di sicurezza dell'agente influisce sulle impostazioni di tutte le pubblicazioni presenti in tutti i server di pubblicazione che utilizzano questo database di distribuzione.  
  
#### <a name="to-change-the-context-under-which-the-queue-reader-agent-makes-connections-to-the-publisher"></a>Per modificare il contesto in cui l'agente di lettura coda stabilisce connessioni con il server di pubblicazione  
  
1.  Nella pagina **Server di pubblicazione** della finestra di dialogo **Proprietà server di distribuzione - \<ServerDistribuzione>** fare clic sul pulsante delle proprietà ( **...** ) accanto al server di pubblicazione.  
  
2.  Nella sezione **Connessione agente al server di pubblicazione** specificare il valore **Rappresenta l'account del processo dell'agente** o **Autenticazione di SQL Server** per l'opzione **Modalità di connessione dell'agente** . Se si specifica **Autenticazione di SQL Server**, immettere anche i valori per **Account di accesso** e **Password**.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  A ogni database di distribuzione è associato un agente di lettura coda. La modifica delle impostazioni di sicurezza dell'agente influisce sulle impostazioni di tutte le pubblicazioni presenti in tutti i server di pubblicazione che utilizzano questo database di distribuzione.  
  
#### <a name="to-change-the-context-under-which-the-queue-reader-agent-makes-connections-to-the-subscriber"></a>Per modificare il contesto in cui l'agente di lettura coda stabilisce connessioni con il Sottoscrittore  
  
-   L'agente di lettura coda utilizza lo stesso contesto di connessione dell'agente di distribuzione per la sottoscrizione. Per ulteriori informazioni, vedere le procedure descritte prima per l'agente di distribuzione.  
  
#### <a name="to-change-security-settings-for-an-immediate-updating-pull-subscription"></a>Per modificare le impostazioni di sicurezza per una sottoscrizione pull ad aggiornamento immediato  
  
1.  Nella finestra di dialogo **Proprietà sottoscrizione - \<Sottoscrizione>** del Sottoscrittore fare clic sulla riga **Connessione server di pubblicazione** e quindi scegliere il pulsante delle proprietà (**…**) nella riga.  
  
2.  Nella finestra di dialogo **Immissione delle informazioni per la connessione** selezionare una delle seguenti opzioni:  
  
    -   **Usa account di accesso di un server collegato o remoto**. Selezionare questa opzione se è stato definito un server remoto o un server collegato tra il Sottoscrittore e il server di pubblicazione tramite [sp_addserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql), [sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql), [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o un altro metodo.  
  
    -   **Usa autenticazione di SQL Server con l'account e la password seguenti**. Selezionare questa opzione se non è stato definito un server remoto o un server collegato tra il Sottoscrittore e il server di pubblicazione. Durante il processo di replica verrà automaticamente creato un server collegato. È necessario che l'account specificato esista già nel server di pubblicazione.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  Questa procedura consente di modificare il metodo utilizzato con i trigger di replica per eseguire la connessione dal Sottoscrittore al server di pubblicazione quando vengono apportate modifiche nel Sottoscrittore. È anche possibile modificare le impostazioni associate all'agente di distribuzione per una sottoscrizione ad aggiornamento immediato. Per ulteriori informazioni, vedere le procedure descritte in precedenza in questo argomento.  
>   
>  Questa procedura è valida solo per le sottoscrizioni pull. Per le sottoscrizioni push, usare la stored procedure [sp_link_publication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql).  
  
#### <a name="to-change-the-password-for-the-administrative-connection-from-the-publisher-to-the-distributor"></a>Per modificare la password per la connessione amministrativa dal server di pubblicazione al database di distribuzione  
  
1.  Nella pagina **Server di pubblicazione** della finestra di dialogo **Proprietà server di distribuzione - \<ServerDistribuzione>** immettere una password complessa nelle caselle di testo **Password** e **Conferma password**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
3.  Nella pagina **Generale** della finestra di dialogo **Proprietà server di pubblicazione - \<ServerPubblicazione>** immettere una password complessa nelle caselle di testo **Password** **e Conferma password**.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
> [!IMPORTANT]  
>  In tutte le procedure descritte di seguito, quando possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se si archiviano le credenziali in un file di script, è necessario proteggere il file per impedire l'accesso non autorizzato.  
  
#### <a name="to-change-all-instances-of-a-stored-password-at-a-replication-server"></a>Per modificare tutte le istanze di una password archiviate in un server di replica  
  
1.  Nel database master in un server della topologia di replica eseguire [sp_changereplicationserverpasswords](/sql/relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql). Consente di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] specificare l'account [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di Windows o l' ** \@account di accesso**di cui si desidera modificare la password per ** \@** l'account di accesso e la nuova password per l'account o per l'accesso In questo modo viene modificata ogni istanza della password utilizzata da tutti gli agenti nel server quando si connettono ad altri server della topologia.  
  
    > [!NOTE]  
    >  Per modificare solo l'account di accesso e la password per una connessione a un particolare server della topologia, ad esempio il server di distribuzione o il Sottoscrittore ** \@**, specificare il nome del server per il server.  
  
2.  Ripetere il passaggio 1 in ogni server della topologia di replica in cui è necessario aggiornare la password.  
  
    > [!NOTE]  
    >  Dopo aver modificato una password per la replica è necessario arrestare e riavviare ogni agente che utilizza la password prima che la modifica abbia effetto per tale agente.  
  
#### <a name="to-change-security-settings-for-the-snapshot-agent"></a>Per modificare le impostazioni di sicurezza per l'agente snapshot  
  
1.  Nel server di pubblicazione eseguire [sp_helppublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql), specificando ** \@la pubblicazione**. Verranno restituite le impostazioni di sicurezza correnti per l'agente snapshot.  
  
2.  Nel server di pubblicazione eseguire [sp_changepublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql), specificando ** \@la pubblicazione** e una o più delle seguenti impostazioni di sicurezza da modificare:  
  
    -   Per modificare l'account di Windows con cui viene eseguito l'agente o solo la password per questo account, specificare ** \@job_login** e ** \@job_password**.  
  
    -   Per modificare la modalità di sicurezza utilizzata per la connessione al server di pubblicazione, specificare il valore **1** o **0** per ** \@publisher_security_mode**.  
  
    -   Quando si modifica la modalità di sicurezza utilizzata per la connessione al server di pubblicazione da **1** a **0** o quando si modifica un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] account di accesso utilizzato per questa connessione, specificare ** \@publisher_login** e ** \@publisher_password**.  
  
    > [!IMPORTANT]  
    >  Quando si configura un server di pubblicazione con un server di distribuzione remoto, i valori specificati per tutti i parametri, inclusi *job_login* e *job_password*, vengono inviati al server di distribuzione come testo normale. È consigliabile crittografare la connessione tra il server di pubblicazione e il server di distribuzione remoto prima di eseguire questa stored procedure. Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
#### <a name="to-change-security-settings-for-the-log-reader-agent"></a>Per modificare le impostazioni di sicurezza per l'agente di lettura log  
  
1.  Nel server di pubblicazione eseguire [sp_helplogreader_agent](/sql/relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql), specificando ** \@Publisher**. Verranno restituite le impostazioni di sicurezza correnti per l'agente di lettura log.  
  
2.  Nel server di pubblicazione eseguire [sp_changelogreader_agent](/sql/relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql), specificando ** \@la pubblicazione** e una o più delle seguenti impostazioni di sicurezza da modificare:  
  
    -   Per modificare l'account di Windows con cui viene eseguito l'agente o solo la password per questo account, specificare ** \@job_login** e ** \@job_password**.  
  
    -   Per modificare la modalità di sicurezza utilizzata per la connessione al server di pubblicazione, specificare il valore **1** o **0** per ** \@publisher_security_mode**.  
  
    -   Quando si modifica la modalità di sicurezza utilizzata per la connessione al server di pubblicazione da **1** a **0** o quando si modifica un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] account di accesso utilizzato per questa connessione, specificare ** \@publisher_login** e ** \@publisher_password**.  
  
    > [!NOTE]  
    >  Dopo la modifica dell'account di accesso o della password di un agente, è necessario arrestare e riavviare l'agente per rendere effettiva la modifica.  
  
    > [!IMPORTANT]  
    >  Quando si configura un server di pubblicazione con un server di distribuzione remoto, i valori specificati per tutti i parametri, inclusi *job_login* e *job_password*, vengono inviati al server di distribuzione come testo normale. È consigliabile crittografare la connessione tra il server di pubblicazione e il server di distribuzione remoto prima di eseguire questa stored procedure. Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-push-subscription"></a>Per modificare le impostazioni di sicurezza dell'agente di distribuzione per una sottoscrizione push  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql), specificando ** \@la pubblicazione** e ** \@il Sottoscrittore**. Verranno restituite le proprietà della sottoscrizione, incluse le impostazioni di sicurezza per l'agente di distribuzione eseguito nel server di distribuzione.  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_changesubscription](/sql/relational-databases/system-stored-procedures/sp-changesubscription-transact-sql), specificando ** \@la pubblicazione**, ** \@il Sottoscrittore** ** \@subscriber_db**, il valore **All** per ** \@article**, il nome della proprietà di sicurezza per ** \@Property**e il nuovo valore della proprietà per ** \@value**.  
  
3.  Ripetere il passaggio 2 per ognuna delle seguenti proprietà di sicurezza da modificare:  
  
    -   Per modificare l'account di Windows utilizzato per l'esecuzione dell'agente o solo la password per questo account, specificare il valore **distrib_job_password** per ** \@proprietà** e una nuova password per ** \@valore**. Quando si modifica l'account stesso, ripetere il passaggio 2 specificando il valore ** \@** **distrib_job_login** per la proprietà e il nuovo account di Windows per ** \@valore**.  
  
    -   Per modificare la modalità di sicurezza utilizzata per la connessione al Sottoscrittore, specificare il valore ** \@** **subscriber_security_mode** per la proprietà e il valore **1** (autenticazione integrata di Windows) o **0** (autenticazione SQL Server) per ** \@valore**.  
  
    -   Quando si modifica la modalità di sicurezza del Sottoscrittore in SQL Server autenticazione o se si modificano le informazioni di accesso per l'autenticazione SQL Server, specificare il valore **subscriber_password** per ** \@proprietà** e la nuova password per ** \@valore**. Ripetere il passaggio 2, specificando il valore **subscriber_login** per ** \@la proprietà** e il nuovo account di accesso per ** \@valore**.  
  
    > [!NOTE]  
    >  Dopo la modifica dell'account di accesso o della password di un agente, è necessario arrestare e riavviare l'agente per rendere effettiva la modifica.  
  
    > [!IMPORTANT]  
    >  Quando si configura un server di pubblicazione con un server di distribuzione remoto, i valori specificati per tutte le proprietà, inclusi **distrib_job_login** e **distrib_job_password**, vengono inviati al server di distribuzione come testo normale. È consigliabile crittografare la connessione tra il server di pubblicazione e il server di distribuzione remoto prima di eseguire questa stored procedure. Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-pull-subscription"></a>Per modificare le impostazioni di sicurezza dell'agente di distribuzione per una sottoscrizione pull  
  
1.  Nel Sottoscrittore eseguire [sp_helppullsubscription](/sql/relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql), specificando ** \@publication**. Verranno restituite le proprietà della sottoscrizione, incluse le impostazioni di sicurezza per l'agente di distribuzione eseguito nel Sottoscrittore.  
  
2.  Nel database di sottoscrizione del Sottoscrittore eseguire [sp_change_subscription_properties](/sql/relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql), specificando ** \@Publisher**, ** \@publisher_db**, ** \@publication**, il nome della proprietà di sicurezza per ** \@Property**e il nuovo valore della proprietà per ** \@value**.  
  
3.  Ripetere il passaggio 2 per ognuna delle seguenti proprietà di sicurezza da modificare:  
  
    -   Per modificare l'account di Windows utilizzato per l'esecuzione dell'agente o solo la password per questo account, specificare il valore **distrib_job_password** per ** \@proprietà** e una nuova password per ** \@valore**. Quando si modifica l'account stesso, ripetere il passaggio 2 specificando il valore ** \@** **distrib_job_login** per la proprietà e il nuovo account di Windows per ** \@valore**.  
  
    -   Per modificare la modalità di sicurezza utilizzata per la connessione al server di distribuzione, specificare il valore ** \@** **distributor_security_mode** per la proprietà e il valore **1** (autenticazione integrata di Windows) o **0** (autenticazione SQL Server) per ** \@valore**.  
  
    -   Quando si imposta la modalità di sicurezza del server di distribuzione su SQL Server autenticazione o se si modificano le informazioni di accesso per l'autenticazione SQL Server, specificare il valore **distributor_password** per ** \@proprietà** e la nuova password per ** \@valore**. Ripetere il passaggio 2, specificando il valore **distributor_login** per ** \@la proprietà** e il nuovo account di accesso per ** \@valore**.  
  
    > [!NOTE]  
    >  Dopo la modifica dell'account di accesso o della password di un agente, è necessario arrestare e riavviare l'agente per rendere effettiva la modifica.  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-push-subscription"></a>Per modificare le impostazioni di sicurezza dell'agente di merge per una sottoscrizione push  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_helpmergesubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql), specificando ** \@la pubblicazione**, ** \@il Sottoscrittore**e ** \@subscriber_db**. Verranno restituite le proprietà della sottoscrizione, incluse le impostazioni di sicurezza per l'agente di merge eseguito nel server di distribuzione.  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_changemergesubscription](/sql/relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql), specificando ** \@publication**, ** \@Subscriber**, ** \@subscriber_db**, il nome della proprietà di sicurezza per ** \@Property**e il nuovo valore della proprietà per ** \@value**.  
  
3.  Ripetere il passaggio 2 per ognuna delle seguenti proprietà di sicurezza da modificare:  
  
    -   Per modificare l'account di Windows utilizzato per l'esecuzione dell'agente o solo la password per questo account, specificare il valore **merge_job_password** per ** \@proprietà** e una nuova password per ** \@valore**. Quando si modifica l'account stesso, ripetere il passaggio 2 specificando il valore ** \@** **merge_job_login** per la proprietà e il nuovo account di Windows per ** \@valore**.  
  
    -   Per modificare la modalità di sicurezza utilizzata per la connessione al Sottoscrittore, specificare il valore ** \@** **subscriber_security_mode** per la proprietà e il valore **1** (autenticazione integrata di Windows) o **0** (autenticazione SQL Server) per ** \@valore**.  
  
    -   Quando si modifica la modalità di sicurezza del Sottoscrittore in SQL Server autenticazione o se si modificano le informazioni di accesso per l'autenticazione SQL Server, specificare il valore **subscriber_password** per ** \@proprietà** e la nuova password per ** \@valore**. Ripetere il passaggio 2, specificando il valore **subscriber_login** per ** \@la proprietà** e il nuovo account di accesso per ** \@valore**.  
  
    -   Per modificare la modalità di sicurezza utilizzata per la connessione al server di pubblicazione, specificare il valore ** \@** **publisher_security_mode** per la proprietà e il valore **1** (autenticazione integrata di Windows) o **0** (autenticazione SQL Server) per ** \@valore**.  
  
    -   Quando si modifica la modalità di sicurezza del server di pubblicazione per SQL Server autenticazione o se si modificano le informazioni di accesso per l'autenticazione SQL Server, specificare il valore **publisher_password** per ** \@proprietà** e la nuova password per ** \@valore**. Ripetere il passaggio 2, specificando il valore **publisher_login** per ** \@la proprietà** e il nuovo account di accesso per ** \@valore**.  
  
    > [!NOTE]  
    >  Dopo la modifica dell'account di accesso o della password di un agente, è necessario arrestare e riavviare l'agente per rendere effettiva la modifica.  
  
    > [!IMPORTANT]  
    >  Quando si configura un server di pubblicazione con un server di distribuzione remoto, i valori specificati per tutte le proprietà, inclusi **merge_job_login** e **distrib_job_password**, vengono inviati al server di distribuzione come testo normale. È consigliabile crittografare la connessione tra il server di pubblicazione e il server di distribuzione remoto prima di eseguire questa stored procedure. Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-pull-subscription"></a>Per modificare le impostazioni di sicurezza dell'agente di merge per una sottoscrizione pull  
  
1.  Nel Sottoscrittore eseguire [sp_helpmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql), specificando ** \@publication**. Verranno restituite le proprietà della sottoscrizione, incluse le impostazioni di sicurezza per l'agente di merge eseguito nel Sottoscrittore.  
  
2.  Nel database di sottoscrizione del Sottoscrittore eseguire [sp_change_subscription_properties](/sql/relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql), specificando ** \@Publisher**, ** \@publisher_db**, ** \@publication**, il nome della proprietà di sicurezza per ** \@Property**e il nuovo valore della proprietà per ** \@value**.  
  
3.  Ripetere il passaggio 2 per ognuna delle seguenti proprietà di sicurezza da modificare:  
  
    -   Per modificare l'account di Windows utilizzato per l'esecuzione dell'agente o solo la password per questo account, specificare il valore **merge_job_password** per ** \@la proprietà** e la nuova password per ** \@valore**. Quando si modifica l'account stesso, ripetere il passaggio 2 specificando il valore ** \@** **merge_job_login** per la proprietà e il nuovo account di Windows per ** \@valore**.  
  
    -   Per modificare la modalità di sicurezza utilizzata per la connessione al server di distribuzione, specificare il valore ** \@** **distributor_security_mode** per la proprietà e il valore **1** (autenticazione integrata di Windows) o **0** (autenticazione SQL Server) per ** \@valore**.  
  
    -   Quando si imposta la modalità di sicurezza del server di distribuzione su SQL Server autenticazione o se si modificano le informazioni di accesso per l'autenticazione SQL Server, specificare il valore **distributor_password** per ** \@proprietà** e la nuova password per ** \@valore**. Ripetere il passaggio 2, specificando il valore **distributor_login** per ** \@la proprietà** e il nuovo account di accesso per ** \@valore**.  
  
    -   Per modificare la modalità di sicurezza utilizzata per la connessione al server di pubblicazione, specificare il valore ** \@** **publisher_security_mode** per la proprietà e il valore **1** (autenticazione integrata di Windows) o **0** (autenticazione SQL Server) per ** \@valore**.  
  
    -   Quando si modifica la modalità di sicurezza del server di pubblicazione per SQL Server autenticazione o se si modificano le informazioni di accesso per l'autenticazione SQL Server, specificare il valore **publisher_password** per ** \@proprietà** e la nuova password per ** \@valore**. Ripetere il passaggio 2, specificando il valore **publisher_login** per ** \@la proprietà** e il nuovo account di accesso per ** \@valore**.  
  
    > [!NOTE]  
    >  Dopo la modifica dell'account di accesso o della password di un agente, è necessario arrestare e riavviare l'agente per rendere effettiva la modifica.  
  
#### <a name="to-change-security-settings-for-the-snapshot-agent-to-generate-a-filtered-snapshot-for-a-subscriber"></a>Per modificare impostazioni di sicurezza per l'agente snapshot e generare uno snapshot filtrato per un Sottoscrittore  
  
1.  Nel server di pubblicazione eseguire [sp_helpdynamicsnapshot_job](/sql/relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql), specificando ** \@la pubblicazione**. Nel set dei risultati Si noti il valore **job_name** per la partizione del Sottoscrittore da modificare.  
  
2.  Nel server di pubblicazione eseguire [sp_changedynamicsnapshot_job](/sql/relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql), specificando ** \@la pubblicazione**, il valore ottenuto nel passaggio 1 per ** \@dynamic_snapshot_jobname**e una nuova password per ** \@job_password** o account di accesso e password per l'account di Windows con cui viene eseguito l'agente per ** \@job_login** e ** \@job_password**.  
  
    > [!IMPORTANT]  
    >  Quando si configura un server di pubblicazione con un server di distribuzione remoto, i valori specificati per tutti i parametri, inclusi *job_login* e *job_password*, vengono inviati al server di distribuzione come testo normale. È consigliabile crittografare la connessione tra il server di pubblicazione e il server di distribuzione remoto prima di eseguire questa stored procedure. Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
#### <a name="to-change-security-settings-for-the-queue-reader-agent"></a>Per modificare le impostazioni di sicurezza per l'agente di lettura coda  
  
1.  Nel server di distribuzione eseguire [sp_helpqreader_agent](/sql/relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql). Verrà restituito l'account di Windows corrente utilizzato per eseguire l'agente di lettura coda.  
  
    -   Nel server di distribuzione eseguire [sp_changeqreader_agent](/sql/relational-databases/system-stored-procedures/sp-changeqreader-agent-transact-sql), specificando le impostazioni dell'account di Windows per ** \@job_login** e ** \@job_passwsord**.  
  
    > [!NOTE]  
    >  Dopo la modifica dell'account di accesso o della password di un agente, è necessario arrestare e riavviare l'agente per rendere effettiva la modifica. A ogni database di distribuzione è associato un agente di lettura coda. La modifica delle impostazioni di sicurezza dell'agente influisce sulle impostazioni di tutte le pubblicazioni presenti in tutti i server di pubblicazione che utilizzano questo database di distribuzione.  
  
2.  L'agente di lettura coda esegue le connessioni al Sottoscrittore utilizzando lo stesso contesto di connessione dell'agente di distribuzione per la sottoscrizione.  
  
#### <a name="to-change-security-mode-used-by-an-immediate-updating-subscriber-when-connecting-to-the-publisher"></a>Per modificare la modalità di sicurezza utilizzata da un Sottoscrittore ad aggiornamento immediato per la connessione al server di pubblicazione  
  
1.  Nel database di sottoscrizione del Sottoscrittore eseguire [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql). Specificare ** \@Publisher**, ** \@publication**, il nome del database di pubblicazione per ** \@publisher_db**e uno dei valori seguenti per ** \@security_mode**:  
  
    -   **0** per utilizzare l'autenticazione di SQL Server quando si eseguono aggiornamenti nel server di pubblicazione. Questa opzione richiede di specificare un account di accesso valido nel server di pubblicazione per l' ** \@account di accesso** e ** \@la password**.  
  
    -   **1** per utilizzare il contesto di sicurezza dell'utente che esegue le modifiche nel Sottoscrittore quando ci si connette al server di pubblicazione. Per informazioni sulle restrizioni correlate a questa modalità di sicurezza, vedere [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) .  
  
    -   **2** per usare un account di accesso esistente e definito dall'utente per il server collegato, creato con [sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql).  
  
#### <a name="to-change-the-password-for-a-remote-distributor"></a>Per modificare la password per un server di distribuzione remoto  
  
1.  Nel database di distribuzione del server di distribuzione eseguire [sp_changedistributor_password](/sql/relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql), specificando la nuova password per l'account ** \@** di accesso per la password.  
  
    > [!IMPORTANT]  
    >  Non modificare direttamente la password di **distributor_admin** .  
  
2.  In ogni server di pubblicazione che utilizza questo server di distribuzione remoto eseguire [sp_changedistributor_password](/sql/relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql), specificando la password del passaggio 1 per ** \@la password**.  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> Utilizzo di RMO (Replication Management Objects)  
  
> [!IMPORTANT]  
>  Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali, utilizzare i [servizi di crittografia](https://go.microsoft.com/fwlink/?LinkId=34733) offerti da [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows .NET Framework.  
  
#### <a name="to-change-all-instances-of-a-password-stored-on-a-replication-server"></a>Per modificare tutte le istanze di una password archiviate in un server di replica  
  
1.  Creare una connessione al server di replica tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.ReplicationServer> utilizzando la connessione creata nel passaggio 1.  
  
3.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeReplicationServerPasswords%2A> . Specificare i parametri seguenti:  
  
    -   *security_mode* : valore <xref:Microsoft.SqlServer.Replication.ReplicationSecurityMode> che specifica il tipo di autenticazione per cui vengono modificate tutte le istanze della password.  
  
    -   *login* : account di accesso per cui vengono modificate tutte le istanze della password.  
  
    -   *password* : nuovo valore della password.  
  
        > [!IMPORTANT]  
        >  Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali, utilizzare i [servizi di crittografia](https://go.microsoft.com/fwlink/?LinkId=34733) offerti da Windows .NET Framework.  
  
        > [!NOTE]  
        >  Solo un membro del ruolo predefinito del server `sysadmin` può chiamare questo metodo.  
  
4.  Ripetere i passaggi da 1 a 3 in ogni server della topologia di replica in cui è necessario aggiornare la password.  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-push-subscription-to-a-transactional-publication"></a>Per modificare le impostazioni di sicurezza dell'agente di distribuzione per una sottoscrizione push in una pubblicazione transazionale  
  
1.  Creare una connessione al server di pubblicazione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.TransSubscription>.  
  
3.  Impostare le proprietà <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>e <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> per la sottoscrizione, quindi impostare la connessione creata nel passaggio 1 per la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
4.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per recuperare le proprietà dell'oggetto. Se questo metodo restituisce `false`, le proprietà della sottoscrizione sono state definite in modo non corretto nel passaggio 3 oppure la sottoscrizione non esiste.  
  
5.  Impostare una o più delle seguenti proprietà di sicurezza sull'istanza di <xref:Microsoft.SqlServer.Replication.TransSubscription>:  
  
    -   Per modificare le credenziali per l'account di Windows utilizzato per eseguire l'agente, impostare i campi <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> di <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>.  
  
    -   Per specificare l'autenticazione integrata di Windows come tipo di autenticazione utilizzato dall'agente quando si connette al Sottoscrittore, impostare il campo <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> della proprietà <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> su `true`.  
  
    -   Per specificare SQL Server autenticazione come tipo di autenticazione utilizzato dall'agente quando si connette al <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> Sottoscrittore, impostare il campo della <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> proprietà su `false`e specificare le credenziali di accesso del Sottoscrittore per <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> i <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> campi e.  
  
        > [!NOTE]  
        >  La connessione dell'agente al server di distribuzione viene sempre eseguita utilizzando le credenziali di Windows specificate da <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>. Questo account viene utilizzato anche per stabilire connessioni remote tramite l'autenticazione di Windows.  
  
6.  (Facoltativo) Se si specifica un valore `true` per <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> per eseguire il commit delle modifiche nel server. Se si specifica un valore `false` per <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (impostazione predefinita), le modifiche vengono inviate immediatamente al server.  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-pull-subscription-to-a-transactional-publication"></a>Per modificare le impostazioni di sicurezza dell'agente di distribuzione per una sottoscrizione pull in una pubblicazione transazionale  
  
1.  Creare una connessione al Sottoscrittore tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.TransPullSubscription>.  
  
3.  Impostare le proprietà <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>e <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> per la sottoscrizione, quindi impostare la connessione creata nel passaggio 1 per la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
4.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per recuperare le proprietà dell'oggetto. Se questo metodo restituisce `false`, le proprietà della sottoscrizione sono state definite in modo non corretto nel passaggio 3 oppure la sottoscrizione non esiste.  
  
5.  Impostare una o più delle seguenti proprietà di sicurezza sull'istanza di <xref:Microsoft.SqlServer.Replication.TransPullSubscription>:  
  
    -   Per modificare le credenziali per l'account di Windows utilizzato per eseguire l'agente, impostare i campi <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> di <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>.  
  
    -   Per specificare l'autenticazione integrata di Windows come tipo di autenticazione utilizzato dall'agente quando si connette al server di distribuzione, impostare il campo <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> della proprietà <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> su `true`.  
  
    -   Per <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> specificare SQL Server autenticazione come tipo di autenticazione utilizzato dall'agente quando si connette al server di distribuzione, impostare il campo della <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> proprietà su `false`e specificare le credenziali di accesso al server di distribuzione per <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> i <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> campi e.  
  
        > [!NOTE]  
        >  La connessione dell'agente al Sottoscrittore viene sempre eseguita utilizzando le credenziali di Windows specificate da <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>. Questo account viene utilizzato anche per stabilire connessioni remote tramite l'autenticazione di Windows.  
  
6.  (Facoltativo) Se si specifica un valore `true` per <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> per eseguire il commit delle modifiche nel server. Se si specifica un valore `false` per <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (impostazione predefinita), le modifiche vengono inviate immediatamente al server.  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-pull-subscription-to-a-merge-publication"></a>Per modificare le impostazioni di sicurezza dell'agente di merge per una sottoscrizione pull in una pubblicazione di tipo merge  
  
1.  Creare una connessione al Sottoscrittore tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.MergePullSubscription>.  
  
3.  Impostare le proprietà <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>e <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> per la sottoscrizione, quindi impostare la connessione creata nel passaggio 1 per la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
4.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per recuperare le proprietà dell'oggetto. Se questo metodo restituisce `false`, le proprietà della sottoscrizione sono state definite in modo non corretto nel passaggio 3 oppure la sottoscrizione non esiste.  
  
5.  Impostare una o più delle seguenti proprietà di sicurezza sull'istanza di <xref:Microsoft.SqlServer.Replication.MergePullSubscription>:  
  
    -   Per modificare le credenziali per l'account di Windows utilizzato per eseguire l'agente, impostare i campi <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> di <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>.  
  
    -   Per specificare l'autenticazione integrata di Windows come tipo di autenticazione utilizzato dall'agente quando si connette al server di distribuzione, impostare il campo <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> della proprietà <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> su `true`.  
  
    -   Per <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> specificare SQL Server autenticazione come tipo di autenticazione utilizzato dall'agente quando si connette al server di distribuzione, impostare il campo della <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> proprietà su `false`e specificare le credenziali di accesso al server di distribuzione per <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> i <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> campi e.  
  
    -   Per specificare l'autenticazione integrata di Windows come tipo di autenticazione utilizzato dall'agente quando si connette al server di pubblicazione, impostare il campo <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> della proprietà <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> su `true`.  
  
    -   Per <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> specificare SQL Server autenticazione come tipo di autenticazione utilizzato dall'agente quando si connette al server di pubblicazione, impostare il campo della <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> proprietà su `false`e specificare le credenziali di accesso del server di pubblicazione per <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> i <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> campi e.  
  
        > [!NOTE]  
        >  La connessione dell'agente al Sottoscrittore viene sempre eseguita utilizzando le credenziali di Windows specificate da <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>. Questo account viene utilizzato anche per stabilire connessioni remote tramite l'autenticazione di Windows.  
  
6.  (Facoltativo) Se si specifica un valore `true` per <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> per eseguire il commit delle modifiche nel server. Se si specifica un valore `false` per <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (impostazione predefinita), le modifiche vengono inviate immediatamente al server.  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-push-subscription-to-a-merge-publication"></a>Per modificare le impostazioni di sicurezza dell'agente di merge per una sottoscrizione push in una pubblicazione di tipo merge  
  
1.  Creare una connessione al server di pubblicazione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.MergeSubscription>.  
  
3.  Impostare le proprietà <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>e <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> per la sottoscrizione, quindi impostare la connessione creata nel passaggio 1 per la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
4.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per recuperare le proprietà dell'oggetto. Se questo metodo restituisce `false`, le proprietà della sottoscrizione sono state definite in modo non corretto nel passaggio 3 oppure la sottoscrizione non esiste.  
  
5.  Impostare una o più delle seguenti proprietà di sicurezza sull'istanza di <xref:Microsoft.SqlServer.Replication.MergeSubscription>:  
  
    -   Per modificare le credenziali per l'account di Windows utilizzato per eseguire l'agente, impostare i campi <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> di <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>.  
  
    -   Per specificare l'autenticazione integrata di Windows come tipo di autenticazione utilizzato dall'agente quando si connette al Sottoscrittore, impostare il campo <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> della proprietà <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> su `true`.  
  
    -   Per specificare SQL Server autenticazione come tipo di autenticazione utilizzato dall'agente quando si connette al <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> Sottoscrittore, impostare il campo della <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> proprietà su `false`e specificare le credenziali di accesso del Sottoscrittore per <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> i <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> campi e.  
  
    -   Per specificare l'autenticazione integrata di Windows come tipo di autenticazione utilizzato dall'agente quando si connette al server di pubblicazione, impostare il campo <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> della proprietà <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> su `true`.  
  
    -   Per <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> specificare SQL Server autenticazione come tipo di autenticazione utilizzato dall'agente quando si connette al server di pubblicazione, impostare il campo della <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> proprietà su `false`e specificare le credenziali di accesso del server di pubblicazione per <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardLogin%2A> i <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardPassword%2A> campi e.  
  
        > [!NOTE]  
        >  La connessione dell'agente al server di distribuzione viene sempre eseguita utilizzando le credenziali di Windows specificate da <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>. Questo account viene utilizzato anche per stabilire connessioni remote tramite l'autenticazione di Windows.  
  
6.  (Facoltativo) Se si specifica un valore `true` per <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> per eseguire il commit delle modifiche nel server. Se si specifica un valore `false` per <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (impostazione predefinita), le modifiche vengono inviate immediatamente al server.  
  
#### <a name="to-change-the-login-information-used-by-an-immediate-updating-subscriber-when-it-connects-to-the-transactional-publisher"></a>Per modificare le informazioni di accesso utilizzate da un Sottoscrittore ad aggiornamento immediato quando si connette al server di pubblicazione transazionale  
  
1.  Creare una connessione al Sottoscrittore tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> per il database di sottoscrizione. Specificare <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.Name%2A> e <xref:Microsoft.SqlServer.Management.Common.ServerConnection> dal passaggio 1 per <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per recuperare le proprietà dell'oggetto. Se questo metodo restituisce `false`, le proprietà del database sono state definite in modo non corretto nel passaggio 2 oppure il database di sottoscrizione non esiste.  
  
4.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LinkPublicationForUpdateableSubscription%2A> , passando i parametri seguenti:  
  
    -   *Publisher* : nome del server di pubblicazione.  
  
    -   *PublisherDB* : nome del database di pubblicazione.  
  
    -   *Publication* : nome della pubblicazione sottoscritta dal Sottoscrittore ad aggiornamento immediato.  
  
    -   *Distributor* : nome del server di distribuzione.  
  
    -   *PublisherSecurity* - A <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext> che specifica il tipo di modalità di sicurezza utilizzato dal Sottoscrittore ad aggiornamento immediato quando si connette al server di pubblicazione e le credenziali di accesso per la connessione.  
  
###  <a name="example-rmo"></a><a name="PShellExample"></a> Esempio (RMO)  
 In questo esempio viene controllato il valore di accesso fornito e vengono modificate tutte le password per l'account di accesso di Windows o di SQL Server specificato archiviate dalla replica nel server.  
  
 [!code-csharp[HowTo#rmo_ChangeServerPasswords](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_changeserverpasswords)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeServerPasswords](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_changeserverpasswords)]  
  
##  <a name="follow-up-after-you-modify-replication-security-settings"></a><a name="FollowUp"></a> Completamento: dopo avere modificato le impostazioni di sicurezza della replica  
 Dopo la modifica dell'account di accesso o della password di un agente, è necessario arrestare e riavviare l'agente per rendere effettiva la modifica.  
  
## <a name="see-also"></a>Vedere anche  
 [Replication Management Objects Concepts](../concepts/replication-management-objects-concepts.md)   
 [Aggiornare gli script di replica &#40;programmazione Transact-SQL della replica&#41;](../administration/upgrade-replication-scripts-replication-transact-sql-programming.md)   
 [Gestire gli account di accesso e le password nella replica](identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)   
 [Modello di sicurezza dell'agente di replica](replication-agent-security-model.md)   
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [Sicurezza replica di SQL Server](view-and-modify-replication-security-settings.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)  
  
  
