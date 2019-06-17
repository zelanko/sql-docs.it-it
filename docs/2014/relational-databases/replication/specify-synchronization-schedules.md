---
title: Specificare le pianificazioni della sincronizzazione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], synchronizing
- scheduling synchronization [SQL Server replication]
- synchronization [SQL Server replication], schedules
- replication [SQL Server], synchronization
ms.assetid: 97f2535b-ec19-4973-823d-bcf3d5aa0216
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9bfbb62c58efea29df26cb9fc6e632bc4e2b3642
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62630801"
---
# <a name="specify-synchronization-schedules"></a>Impostazione di pianificazioni della sincronizzazione
  In questo argomento viene descritto come specificare le pianificazioni di sincronizzazione in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o RMO (Replication Management Objects). Quando si crea una sottoscrizione, è possibile definire una pianificazione della sincronizzazione per controllare l'esecuzione dell'agente di replica per la sottoscrizione. Se non si specificano parametri di pianificazione, per la sottoscrizione verrà utilizzata la pianificazione predefinita.  
  
 Le sottoscrizioni vengono sincronizzate dall'agente di distribuzione, per la replica snapshot e transazionale, o dall'agente di merge, per la replica di tipo merge. Gli agenti possono essere in esecuzione continuamente, essere in esecuzione su richiesta o essere in esecuzione su una pianificazione.  
  
 **Contenuto dell'argomento**  
  
-   **Per impostare le pianificazioni della sincronizzazione, utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Oggetti RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 Impostare le pianificazioni della sincronizzazione nella pagina **Pianificazione della sincronizzazione** della Creazione guidata nuova sottoscrizione. Per ulteriori informazioni sull'accesso a questa procedura guidata, vedere [Create a Push Subscription](create-a-push-subscription.md) e [Create a Pull Subscription](create-a-pull-subscription.md).  
  
 Modificare le pianificazioni della sincronizzazione nella finestra di dialogo **Proprietà pianificazione processo** , alla quale è possibile accedere dalla cartella **Processi** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e dalle finestre relative ai dettagli dell'agente in Monitoraggio replica. Per informazioni sull'avvio di Monitoraggio replica, vedere [Avviare Monitoraggio replica](monitor/start-the-replication-monitor.md).  
  
 Se si specificano le pianificazioni dalla cartella **Processi** , utilizzare la tabella seguente per determinare il nome del processo dell'agente.  
  
|Agent|Nome processo|  
|-----------|--------------|  
|Agente di merge per le sottoscrizioni pull|**\<ServerPubblicazione>-\<DatabasePubblicazione>-\<Pubblicazione>-\<Sottoscrittore>-\<DatabaseSottoscrizione>-\<intero>**|  
|Agente di merge per le sottoscrizioni push|**\<ServerPubblicazione>-\<DatabasePubblicazione>-\<Pubblicazione>-\<Sottoscrittore>-\<intero>**|  
|Agente di distribuzione per le sottoscrizioni push|**\<ServerPubblicazione>-\<DatabasePubblicazione>-\<Pubblicazione>-\<Sottoscrittore>-\<intero>** <sup>1</sup>|  
|Agente di distribuzione per le sottoscrizioni pull|**\<ServerPubblicazione>-\<DatabasePubblicazione>-\<Pubblicazione>-\<Sottoscrittore>-\<DatabaseSottoscrizione>-\<GUID>** <sup>2</sup>|  
|Agente di distribuzione per le sottoscrizioni push di Sottoscrittori non SQL Server|**\<ServerPubblicazione>-\<DatabasePubblicazione>-\<Pubblicazione>-\<Sottoscrittore>-\<intero>**|  
  
 <sup>1</sup> Per le sottoscrizioni push di pubblicazioni Oracle, è **\<ServerPubblicazione>-\<ServerPubblicazione**> invece di **\<ServerPubblicazione>-\<DatabasePubblicazione>**  
  
 <sup>2</sup> Per le sottoscrizioni pull di pubblicazioni Oracle, è **\<ServerPubblicazione>-\<DatabaseDistribuzione**> invece di **\<ServerPubblicazione>-\<DatabasePubblicazione>**  
  
#### <a name="to-specify-synchronization-schedules"></a>Per impostare le pianificazioni della sincronizzazione  
  
1.  Nella pagina **Pianificazione della sincronizzazione** della Creazione guidata nuova sottoscrizione selezionare uno dei valori seguenti nell'elenco a discesa **Pianificazione agente** per ogni sottoscrizione creata:  
  
    -   **Esecuzione continua**  
  
    -   **Esecuzione solo su richiesta**  
  
    -   **\<Definisci pianificazione...>**  
  
2.  Se si seleziona **\<Definisci pianificazione...>** , specificare una pianificazione nella finestra di dialogo **Proprietà pianificazione processo** e quindi fare clic su **OK**.  
  
3.  Completare la procedura guidata.  
  
#### <a name="to-modify-a-synchronization-schedule-for-a-push-subscription-in-replication-monitor"></a>Per modificare una pianificazione della sincronizzazione per una sottoscrizione push in Monitoraggio replica  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro a sinistra di Monitoraggio replica, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.  
  
2.  Fare clic sulla scheda **Tutte le sottoscrizioni** .  
  
3.  Fare clic con il pulsante destro del mouse su una sottoscrizione e quindi scegliere **Visualizza dettagli**.  
  
4.  Nel **sottoscrizione \< Nomesottoscrizione >** finestra, fare clic su **azione**e quindi fare clic su  **\<AgentName > Proprietà processo**.  
  
5.  Nella pagina **Pianificazioni** della finestra di dialogo **Proprietà processo - \<NomeProcesso>** fare clic su **Modifica**.  
  
6.  Nella finestra di dialogo **Proprietà pianificazione processo** selezionare un valore nell'elenco a discesa **Tipo pianificazione** :  
  
    -   Per specificare che l'agente deve essere eseguito in modo continuo, selezionare **Avvia automaticamente all'avvio di SQL Server Agent**.  
  
    -   Per specificare che l'agente deve essere eseguito in base a una pianificazione, selezionare **Periodica**.  
  
    -   Per specificare che l'agente deve essere eseguito su richiesta, selezionare **Singola occorrenza**.  
  
7.  Se si seleziona **Periodica**, specificare una pianificazione per l'agente.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### <a name="to-modify-a-synchronization-schedule-for-a-push-subscription-in-management-studio"></a>Per modificare una pianificazione della sincronizzazione per una sottoscrizione push in Management Studio  
  
1.  Connettersi al server di distribuzione in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **SQL Server Agent** e quindi la cartella **Processi** .  
  
3.  Fare clic con il pulsante destro del mouse sull'agente di distribuzione o sull'agente di merge associato alla sottoscrizione e quindi scegliere **Proprietà**.  
  
4.  Nella pagina **Pianificazioni** della finestra di dialogo **Proprietà processo - \<NomeProcesso>** fare clic su **Modifica**.  
  
5.  Nella finestra di dialogo **Proprietà pianificazione processo** selezionare un valore nell'elenco a discesa **Tipo pianificazione** :  
  
    -   Per specificare che l'agente deve essere eseguito in modo continuo, selezionare **Avvia automaticamente all'avvio di SQL Server Agent**.  
  
    -   Per specificare che l'agente deve essere eseguito in base a una pianificazione, selezionare **Periodica**.  
  
    -   Per specificare che l'agente deve essere eseguito su richiesta, selezionare **Singola occorrenza**.  
  
6.  Se si seleziona **Periodica**, specificare una pianificazione per l'agente.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### <a name="to-modify-a-synchronization-schedule-for-a-pull-subscription-in-management-studio"></a>Per modificare una pianificazione della sincronizzazione per una sottoscrizione pull in Management Studio  
  
1.  Connettersi al Sottoscrittore in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **SQL Server Agent** e quindi la cartella **Processi** .  
  
3.  Fare clic con il pulsante destro del mouse sull'agente di distribuzione o sull'agente di merge associato alla sottoscrizione e quindi scegliere **Proprietà**.  
  
4.  Nella pagina **Pianificazioni** della finestra di dialogo **Proprietà processo - \<NomeProcesso>** fare clic su **Modifica**.  
  
5.  Nella finestra di dialogo **Proprietà pianificazione processo** selezionare un valore nell'elenco a discesa **Tipo pianificazione** :  
  
    -   Per specificare che l'agente deve essere eseguito in modo continuo, selezionare **Avvia automaticamente all'avvio di SQL Server Agent**.  
  
    -   Per specificare che l'agente deve essere eseguito in base a una pianificazione, selezionare **Periodica**.  
  
    -   Per specificare che l'agente deve essere eseguito su richiesta, selezionare **Singola occorrenza**.  
  
6.  Se si seleziona **Periodica**, specificare una pianificazione per l'agente.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
 È possibile definire pianificazioni della sincronizzazione a livello di programmazione tramite stored procedure di replica. Le stored procedure utilizzate dipendono dal tipo di replica e dal tipo di sottoscrizione (pull o push).  
  
 Una pianificazione è definita dai parametri di programmazione seguenti, i cui comportamenti vengono ereditati da [sp_add_schedule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-schedule-transact-sql):  
  
-   **@frequency_type** : tipo di frequenza utilizzata per la pianificazione dell'agente.  
  
-   **@frequency_interval** : giorno della settimana in cui viene eseguito un agente.  
  
-   **@frequency_relative_interval** : settimana di un determinato mese in cui è pianificata l'esecuzione mensile dell'agente.  
  
-   **@frequency_recurrence_factor** : numero di unità relative al tipo di frequenza tra sincronizzazioni.  
  
-   **@frequency_subday** : unità della frequenza quando l'agente viene eseguito più di una volta al giorno.  
  
-   **@frequency_subday_interval** : numero di unità della frequenza tra un'esecuzione e l'altra quando l'agente viene eseguito più di una volta al giorno.  
  
-   **@active_start_time_of_day** : ora di un determinato giorno in cui un agente viene avviato per la prima volta.  
  
-   **@active_end_time_of_day** : ora di un determinato giorno in cui un agente viene avviato per l'ultima volta.  
  
-   **@active_start_date** : primo giorno di applicazione della pianificazione dell'agente.  
  
-   **@active_end_date** : ultimo giorno di applicazione della pianificazione dell'agente.  
  
#### <a name="to-define-the-synchronization-schedule-for-a-pull-subscription-to-a-transactional-publication"></a>Per definire la pianificazione della sincronizzazione per una sottoscrizione pull di una pubblicazione transazionale  
  
1.  Creare una nuova sottoscrizione pull di una pubblicazione transazionale. Per altre informazioni, vedere [Creazione di una sottoscrizione pull](create-a-pull-subscription.md).  
  
2.  Nel Sottoscrittore eseguire [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql). Specificare **@publisher** , **@publisher_db** , **@publication** e le credenziali di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows utilizzate per eseguire l'agente di distribuzione nel Sottoscrittore per **@job_name** e **@password** . Specificare i parametri di sincronizzazione, descritti in dettaglio in precedenza, con cui definire la pianificazione per il processo dell'agente di distribuzione che sincronizza la sottoscrizione.  
  
#### <a name="to-define-the-synchronization-schedule-for-a-push-subscription-to-a-transactional-publication"></a>Per definire la pianificazione della sincronizzazione per una sottoscrizione push di una pubblicazione transazionale  
  
1.  Creare una nuova sottoscrizione push di una pubblicazione transazionale. Per altre informazioni, vedere [Creazione di una sottoscrizione push](create-a-push-subscription.md).  
  
2.  Nel Sottoscrittore eseguire [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql). Specificare **@subscriber** , **@subscriber_db** , **@publication** e le credenziali di Windows utilizzate per eseguire l'agente di distribuzione nel Sottoscrittore per **@job_name** e **@password** . Specificare i parametri di sincronizzazione, descritti in dettaglio in precedenza, con cui definire la pianificazione per il processo dell'agente di distribuzione che sincronizza la sottoscrizione.  
  
#### <a name="to-define-the-synchronization-schedule-for-a-pull-subscription-to-a-merge-publication"></a>Per definire la pianificazione della sincronizzazione per una sottoscrizione pull di una pubblicazione di tipo merge  
  
1.  Creare una nuova sottoscrizione pull di una pubblicazione di tipo merge. Per altre informazioni, vedere [Creazione di una sottoscrizione pull](create-a-pull-subscription.md).  
  
2.  Nel Sottoscrittore eseguire [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql). Specificare **@publisher** , **@publisher_db** , **@publication** e le credenziali di Windows utilizzate per eseguire l'agente di merge nel Sottoscrittore per **@job_name** e **@password** . Specificare i parametri di sincronizzazione, descritti in dettaglio in precedenza, con cui definire la pianificazione per il processo dell'agente di merge che sincronizza la sottoscrizione.  
  
#### <a name="to-define-the-synchronization-schedule-for-a-push-subscription-to-a-merge-publication"></a>Per definire la pianificazione della sincronizzazione per una sottoscrizione push di una pubblicazione di tipo merge  
  
1.  Creare una nuova sottoscrizione push di una pubblicazione di tipo merge. Per altre informazioni, vedere [Creazione di una sottoscrizione push](create-a-push-subscription.md).  
  
2.  Nel Sottoscrittore eseguire [sp_addmergepushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql). Specificare **@subscriber** , **@subscriber_db** , **@publication** e le credenziali di Windows utilizzate per eseguire l'agente di merge nel Sottoscrittore per **@job_name** e **@password** . Specificare i parametri di sincronizzazione, descritti in dettaglio in precedenza, con cui definire la pianificazione per il processo dell'agente di merge che sincronizza la sottoscrizione.  
  
##  <a name="RMOProcedure"></a> Utilizzo di RMO (Replication Management Objects)  
 La replica utilizza SQL Server Agent per pianificare i processi per attività che vengono svolte periodicamente, ad esempio la generazione di snapshot e la sincronizzazione delle sottoscrizioni. È possibile utilizzare gli oggetti RMO (Replication Management Objects) a livello di programmazione per specificare le pianificazioni per i processi dell'agente di replica.  
  
> [!NOTE]  
>  Quando si crea una sottoscrizione e si specifica un valore `false` per `CreateSyncAgentByDefault` (comportamento predefinito per le sottoscrizioni pull), il processo dell'agente non viene creato e le proprietà di pianificazione vengono ignorate. In questo caso, la pianificazione della sincronizzazione deve essere determinata dall'applicazione. Per ulteriori informazioni, vedere [Create a Pull Subscription](create-a-pull-subscription.md) e [Create a Push Subscription](create-a-push-subscription.md).  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-push-subscription-to-a-transactional-publication"></a>Per definire una pianificazione dell'agente di replica quando si crea una sottoscrizione push di una pubblicazione transazionale  
  
1.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.TransSubscription> per la sottoscrizione da creare. Per altre informazioni, vedere [Create a Push Subscription](create-a-push-subscription.md).  
  
2.  Prima di chiamare <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>, impostare uno o più dei seguenti campi della proprietà <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A> :  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> : tipo di frequenza (ad esempio giornaliera o settimanale) utilizzata per la pianificazione dell'agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> : giorno della settimana in cui viene eseguito un agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> : settimana di un determinato mese in cui è pianificata l'esecuzione mensile dell'agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> : numero di unità relative al tipo di frequenza tra sincronizzazioni.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> : unità della frequenza quando l'agente viene eseguito più di una volta al giorno.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> : numero di unità della frequenza tra un'esecuzione e l'altra quando l'agente viene eseguito più di una volta al giorno.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> : ora di un determinato giorno in cui un agente viene avviato per la prima volta.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> : ora di un determinato giorno in cui un agente viene avviato per l'ultima volta.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> : primo giorno di applicazione della pianificazione dell'agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> : ultimo giorno di applicazione della pianificazione dell'agente.  
  
    > [!NOTE]  
    >  Se una di queste proprietà viene omessa, viene impostato un valore predefinito.  
  
3.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> per creare la sottoscrizione.  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-pull-subscription-to-a-transactional-publication"></a>Per definire una pianificazione dell'agente di replica quando si crea una sottoscrizione pull di una pubblicazione transazionale  
  
1.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.TransPullSubscription> per la sottoscrizione da creare. Per altre informazioni, vedere [Creazione di una sottoscrizione pull](create-a-pull-subscription.md).  
  
2.  Prima di chiamare <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>, impostare uno o più dei seguenti campi della proprietà <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A> :  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> : tipo di frequenza (ad esempio giornaliera o settimanale) utilizzata per la pianificazione dell'agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> : giorno della settimana in cui viene eseguito un agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> : settimana di un determinato mese in cui è pianificata l'esecuzione mensile dell'agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> : numero di unità relative al tipo di frequenza tra sincronizzazioni.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> : unità della frequenza quando l'agente viene eseguito più di una volta al giorno.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> : numero di unità della frequenza tra un'esecuzione e l'altra quando l'agente viene eseguito più di una volta al giorno.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> : ora di un determinato giorno in cui un agente viene avviato per la prima volta.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> : ora di un determinato giorno in cui un agente viene avviato per l'ultima volta.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> : primo giorno di applicazione della pianificazione dell'agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> : ultimo giorno di applicazione della pianificazione dell'agente.  
  
    > [!NOTE]  
    >  Se una di queste proprietà viene omessa, viene impostato un valore predefinito.  
  
3.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> per creare la sottoscrizione.  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-pull-subscription-to-a-merge-publication"></a>Per definire una pianificazione dell'agente di replica quando si crea una sottoscrizione pull di una pubblicazione di tipo merge  
  
1.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.MergePullSubscription> per la sottoscrizione da creare. Per altre informazioni, vedere [Creazione di una sottoscrizione pull](create-a-pull-subscription.md).  
  
2.  Prima di chiamare <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>, impostare uno o più dei seguenti campi della proprietà <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A> :  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> : tipo di frequenza (ad esempio giornaliera o settimanale) utilizzata per la pianificazione dell'agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> : giorno della settimana in cui viene eseguito un agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> : settimana di un determinato mese in cui è pianificata l'esecuzione mensile dell'agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> : numero di unità relative al tipo di frequenza tra sincronizzazioni.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> : unità della frequenza quando l'agente viene eseguito più di una volta al giorno.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> : numero di unità della frequenza tra un'esecuzione e l'altra quando l'agente viene eseguito più di una volta al giorno.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> : ora di un determinato giorno in cui un agente viene avviato per la prima volta.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> : ora di un determinato giorno in cui un agente viene avviato per l'ultima volta.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> : primo giorno di applicazione della pianificazione dell'agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> : ultimo giorno di applicazione della pianificazione dell'agente.  
  
    > [!NOTE]  
    >  Se una di queste proprietà viene omessa, viene impostato un valore predefinito.  
  
3.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> per creare la sottoscrizione.  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-push-subscription-to-a-merge-publication"></a>Per definire una pianificazione dell'agente di replica quando si crea una sottoscrizione push di una pubblicazione di tipo merge  
  
1.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.MergeSubscription> per la sottoscrizione da creare. Per altre informazioni, vedere [Create a Push Subscription](create-a-push-subscription.md).  
  
2.  Prima di chiamare <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>, impostare uno o più dei seguenti campi della proprietà <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A> :  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> : tipo di frequenza (ad esempio giornaliera o settimanale) utilizzata per la pianificazione dell'agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> : giorno della settimana in cui viene eseguito un agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> : settimana di un determinato mese in cui è pianificata l'esecuzione mensile dell'agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> : numero di unità relative al tipo di frequenza tra sincronizzazioni.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> : unità della frequenza quando l'agente viene eseguito più di una volta al giorno.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> : numero di unità della frequenza tra un'esecuzione e l'altra quando l'agente viene eseguito più di una volta al giorno.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> : ora di un determinato giorno in cui un agente viene avviato per la prima volta.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> : ora di un determinato giorno in cui un agente viene avviato per l'ultima volta.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> : primo giorno di applicazione della pianificazione dell'agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> : ultimo giorno di applicazione della pianificazione dell'agente.  
  
    > [!NOTE]  
    >  Se una di queste proprietà viene omessa, viene impostato un valore predefinito.  
  
3.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> per creare la sottoscrizione.  
  
###  <a name="PShellExample"></a> Esempio (RMO)  
 In questo esempio viene creata una sottoscrizione push di una pubblicazione di tipo merge e viene specificata la pianificazione per la sincronizzazione di tale sottoscrizione.  
  
 [!code-csharp[HowTo#rmo_CreateMergePushSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## <a name="see-also"></a>Vedere anche  
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [Sottoscrivere le pubblicazioni](subscribe-to-publications.md)   
 [Sincronizzare una sottoscrizione push](synchronize-a-push-subscription.md)   
 [Sincronizzare una sottoscrizione pull](synchronize-a-pull-subscription.md)   
 [Sincronizzare i dati](synchronize-data.md)  
  
  
