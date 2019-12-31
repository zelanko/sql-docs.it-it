---
title: Usare la Creazione guidata Gruppo di disponibilità (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.newagwizard.f1
- sql12.swb.newavgroupwiz.f1
helpviewer_keywords:
- New Availability Group Wizard, availability replicas
- Availability Groups [SQL Server], wizards
- Availability Groups [SQL Server], creating
ms.assetid: e1f1dccc-9e65-471d-8fd1-b45085c9484a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 70227f556ae268144549616dab0895e70ff39de8
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228736"
---
# <a name="use-the-availability-group-wizard-sql-server-management-studio"></a>Utilizzare la Creazione guidata Gruppo di disponibilità (SQL Server Management Studio)
  In questo argomento viene descritto come usare la Creazione guidata Gruppo di disponibilità (in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]) per creare e configurare un gruppo di disponibilità AlwaysOn in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Tramite un *gruppo di disponibilità* vengono definiti un set di database utente di cui verrà eseguito il failover come unità singola e un set di partner di failover, noti come *repliche di disponibilità*, che supportano il failover.  
  
> [!NOTE]  
>  Per un'introduzione ai gruppi di disponibilità, vedere [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md).  
  
-   **Prima di iniziare:**  
  
     [Prerequisiti, restrizioni e raccomandazioni](#PrerequisitesRestrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per creare e configurare un gruppo di disponibilità utilizzando:**  [creazione guidata gruppo di disponibilità (SQL Server Management Studio)](#RunAGwiz)  
  
> [!NOTE]  
>  In alternativa all'utilizzo della Creazione guidata Gruppo di disponibilità, è possibile usare [!INCLUDE[tsql](../../../includes/tsql-md.md)] o i cmdlet di PowerShell per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Creare un gruppo di disponibilità &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md) o i cmdlet di PowerShell per [Creare un gruppo di disponibilità &#40; PowerShell SQL Server&#41;](../../../powershell/sql-server-powershell.md).  
  
##  <a name="BeforeYouBegin"></a>Prima di iniziare  
 Prima di iniziare a creare il primo gruppo di disponibilità, è consigliabile leggere questa sezione.  
  
###  <a name="PrerequisitesRestrictions"></a>Prerequisiti, restrizioni e raccomandazioni  
 Nella maggior parte dei casi, è possibile usare la Creazione guidata Gruppo di disponibilità per completare tutte le attività necessarie per la creazione e la configurazione di un gruppo di disponibilità. Potrebbe tuttavia essere necessario completare manualmente alcune attività.  
  
-   Prima di creare un gruppo di disponibilità, verificare che le istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che ospitano repliche di disponibilità si trovino in un nodo del Clustering di failover di Windows Server (Windows Server Failover Clustering, WSFC) diverso all'interno dello stesso cluster di failover WSFC. Inoltre, verificare che ciascuna delle istanze del server soddisfi tutti gli altri prerequisiti [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] . Per altre informazioni è consigliabile leggere [Prerequisiti, restrizioni e consigli per i gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
-   Se un'istanza del server selezionata come host per una replica di disponibilità è in esecuzione in un account utente di dominio e non dispone ancora di un endpoint del mirroring del database, tramite la procedura guidata è possibile creare l'endpoint e concedere l'autorizzazione CONNECT all'account del servizio dell'istanza del server. Se, tuttavia, il servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene eseguito come account predefinito, ad esempio Sistema locale, Servizio locale o Servizio di rete, oppure come account non di dominio, è necessario usare certificati per l'autenticazione dell'endpoint e non sarà possibile creare un endpoint del mirroring del database nell'istanza del server tramite la procedura guidata. In tal caso, è consigliabile creare gli endpoint del mirroring del database manualmente prima di avviare la Creazione guidata Gruppo di disponibilità.  
  
     `To use certificates for a database mirroring endpoint:`  
  
     [CREAZIONE di ENDPOINT &#40;&#41;Transact-SQL](/sql/t-sql/statements/create-endpoint-transact-sql)  
  
     [Utilizzare certificati per un endpoint del mirroring del database &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   Le istanze del cluster di failover di SQL Server non supportano il failover automatico da gruppi di disponibilità, pertanto le replica di disponibilità ospitate da un'istanza del cluster di failover possono essere configurate solo per il failover manuale.  
  
-   Se un database viene crittografato o contiene una chiave di crittografia del database (DEK), non è possibile usare [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] o [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] per aggiungere il database a un gruppo di disponibilità. Anche se è stato decrittografato un database crittografato, i backup del log potrebbero contenere dati crittografati. In questo caso, la sincronizzazione dei dati iniziale completa potrebbe non riuscire sul database. Questo avviene perché l'operazione di ripristino del log potrebbe richiedere il certificato usato dalle chiavi di crittografia del database e tale certificato potrebbe non essere disponibile.  
  
     Affinché un database decrittografato sia idoneo a essere aggiunto a un gruppo di disponibilità usando la procedura guidata:  
  
    1.  Creare un backup del log del database primario.  
  
    2.  Creare un backup del log completo del database primario.  
  
    3.  Ripristinare il backup del database nell'istanza del server in cui è ospitata la replica secondaria.  
  
    4.  Creare un nuovo backup del log dal database primario.  
  
    5.  Ripristinare questo backup del log sul database secondario.  
  
-   **Prerequisiti per la procedura guidata per eseguire la sincronizzazione dati iniziale completa**  
  
    -   Tutti i percorsi di file dei database devono essere identici in ogni istanza del server in cui è ospitata una replica per il gruppo di disponibilità.  
  
    -   In un'istanza del server in cui è ospitata una replica secondaria non può essere presente alcun nome di database primario. Ciò significa che non può essere ancora presente alcun nuovo database secondario.  
  
    -   Sarà necessario specificare una condivisione di rete affinché la procedura guidata sia in grado di creare e accedere ai backup. Per la replica primaria, all'account usato per avviare il [!INCLUDE[ssDE](../../../includes/ssde-md.md)] devono essere associate le autorizzazioni del file system in lettura e scrittura per una condivisione di rete. Per le repliche secondarie, all'account deve essere associata l'autorizzazione di lettura per la condivisione di rete.  
  
        > [!IMPORTANT]  
        >  I backup del log faranno parte della catena di backup del log. Archiviare i file di backup del log in modo appropriato.  
  
     Se non è possibile usare la procedura guidata per eseguire la sincronizzazione dei dati iniziale completa, sarà necessario preparare i database secondari manualmente. Tale operazione può essere eseguita prima o dopo l'esecuzione della procedura guidata. Per altre informazioni, vedere [Preparare manualmente un database secondario per un gruppo di disponibilità &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
###  <a name="Security"></a>Sicurezza  
  
####  <a name="Permissions"></a>Autorizzazioni  
 Sono necessarie l'appartenenza al ruolo predefinito del server **sysadmin** e l'autorizzazione server CREATE AVAILABILITY GROUP oppure l'autorizzazione ALTER ANY AVAILABILITY GROUP o CONTROL SERVER.  
  
 È inoltre necessaria l'autorizzazione CONTROL ON ENDPOINT se si desidera gestire l'endpoint del mirroring del database tramite la Creazione guidata Gruppo di disponibilità.  
  
##  <a name="RunAGwiz"></a>Utilizzo della creazione guidata gruppo di disponibilità  
  
1.  In Esplora oggetti connettersi all'istanza del server che ospita la replica primaria.  
  
2.  Espandere il nodo **Disponibilità elevata AlwaysOn** e il nodo **Gruppi di disponibilità** .  
  
3.  Per avviare la Creazione guidata Gruppo di disponibilità, selezionare il comando **Creazione guidata Gruppo di disponibilità** .  
  
4.  Quando si esegue la procedura guidata per la prima volta, viene visualizzata una pagina **Introduzione** . Per ignorare questa pagina in futuro, è possibile fare clic su **Non visualizzare più questa pagina**. Dopo avere letto questa pagina, fare clic su **Avanti**.  
  
5.  Nella pagina **Specifica nome del gruppo di disponibilità** immettere il nome del nuovo gruppo di disponibilità nel campo **Nome gruppo di disponibilità** . Questo nome deve essere un identificatore di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] valido e univoco nel cluster di failover WSFC e nell'intero dominio. La lunghezza massima consentita per il nome del gruppo di disponibilità è 128 caratteri.  
  
6.  Nella griglia della pagina **Seleziona database** sono elencati i database utente sull'istanza del server connessa idonei per diventare i *database di disponibilità*. Selezionare uno o più dei database elencati per usarli nel nuovo gruppo di disponibilità. Questi database diventeranno inizialmente i *database primari*iniziali.  
  
     Per ogni database elencato, nella colonna **Dimensioni** viene visualizzata la dimensione del database, se nota. La colonna **Stato** indica se un determinato database soddisfa i [prerequisiti](prereqs-restrictions-recommendations-always-on-availability.md)per i database di disponibilità. Se i prerequisiti non vengono soddisfatti, una breve descrizione dello stato indica il motivo per il database non è idoneo; ad esempio, se non usano il modello di recupero con registrazione completa. Per altre informazioni, fare clic sulla descrizione relativa allo stato.  
  
     Se si modifica un database per renderlo idoneo, fare clic su **Aggiorna** per aggiornare la griglia dei database.  
  
7.  Nella pagina **Specifica repliche** specificare e configurare una o più repliche per il nuovo gruppo di disponibilità. In questa pagina sono incluse quattro schede. Queste schede vengono presentate nella tabella seguente. Per altre informazioni, vedere l'argomento [Pagina Specifica repliche &#40;Creazione guidata Gruppo di disponibilità: Aggiungi replica&#41;](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md).  
  
    |TAB|Breve descrizione|  
    |---------|-----------------------|  
    |**Repliche**|Usare questa scheda per specificare ogni istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che ospiterà una replica secondaria. Si noti che la replica primaria sarà ospitata nell'istanza del server a cui si è attualmente connessi.|  
    |**Endpoint**|Usare questa scheda per verificare eventuali endpoint del mirroring di database esistenti e, inoltre, se tale endpoint risulta mancante in un'istanza del server i cui account del servizio usano l'autenticazione di Windows, per creare l'endpoint automaticamente. **Nota:**  Se un'istanza del server è in esecuzione con un account utente non di dominio, è necessario apportare una modifica manuale all'istanza del server prima di poter continuare con la procedura guidata. Per altre informazioni, vedere la sessione [Prerequisiti](#PrerequisitesRestrictions)più indietro in questo argomento.|  
    |**Preferenze di backup**|Usare questa scheda per specificare le preferenze di backup per il gruppo di disponibilità nel suo complesso e le priorità di backup per le singole repliche di disponibilità.|  
    |**Listener**|Usare questa scheda per creare un listener del gruppo di disponibilità. Per impostazione predefinita, la procedura guidata non crea un listener.|  
  
8.  Nella pagina **Seleziona sincronizzazione dei dati iniziale** specificare come creare e aggiungere i nuovi database secondari al gruppo di disponibilità. Scegliere una delle opzioni seguenti:  
  
    -   **Completo**  
  
         Selezionare questa opzione se l'ambiente soddisfa i requisiti per l'avvio automatico della sincronizzazione dei dati iniziale. Per altre informazioni, vedere [Prerequisiti, restrizioni e raccomandazioni](#PrerequisitesRestrictions), più indietro in questo argomento.  
  
         Se si seleziona **Completo**, dopo avere creato il gruppo di disponibilità verrà eseguito il backup di ogni database primario e del relativo log delle transazioni su una condivisione di rete e verranno ripristinati i backup su ogni istanza del server in cui è ospitata una replica secondaria. Ogni database secondario verrà quindi aggiunto al gruppo di disponibilità.  
  
         Nel campo **Specificare un percorso di rete condiviso accessibile da tutte le repliche:** specificare una condivisione di backup a cui possano accedere in lettura e scrittura tutte le istanze del server che ospitano repliche. Per altre informazioni, vedere la sessione [Prerequisiti](#PrerequisitesRestrictions)più indietro in questo argomento.  
  
    -   **Solo join**  
  
         Se sono stati preparati manualmente database secondari sulle istanze del server che ospiteranno le repliche secondarie, è possibile selezionare questa opzione. I database secondari esistenti verranno uniti al gruppo di disponibilità tramite la procedura guidata.  
  
    -   **Ignora sincronizzazione dati iniziale**  
  
         Selezionare questa opzione se si desidera usare i backup dei database e del log dei database primari. Per altre informazioni, vedere [Avviare lo spostamento dati su un database secondario AlwaysOn &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
9. Nella pagina **Convalida** viene verificato se i valori specificati in questa procedura guidata soddisfano i requisiti della Creazione guidata Gruppo di disponibilità. Per apportare una modifica, fare clic su **Precedente** per tornare a una pagina precedente della procedura guidata per modificare uno o più valori. Scegliere **Avanti** per tornare alla pagina **Convalida**, quindi fare clic su **Ripeti convalida**.  
  
10. Nella pagina **Riepilogo** rivedere le scelte effettuate per il nuovo gruppo di disponibilità. Per apportare una modifica, fare clic su **Indietro** per tornare alla pagina pertinente. Dopo avere apportato la modifica, fare clic su **Avanti** per tornare alla pagina **Riepilogo** .  
  
    > [!IMPORTANT]  
    >  Se l'account del servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di un'istanza del server che ospiterà una nuova replica di disponibilità non esiste già come account di accesso, ne verrà creato uno tramite la Creazione guidata Gruppo di disponibilità. Nella pagina **Riepilogo** vengono visualizzate le informazioni relative all'account di accesso da creare. Se si fa clic su **Fine**, viene creato questo account di accesso per l'account del servizio SQL Server e viene concessa l'autorizzazione CONNECT.  
  
     Se si è soddisfatti delle selezioni, è possibile fare clic su **Script** per creare uno script dei passaggi eseguiti nel corso della procedura guidata. Per creare e configurare il nuovo gruppo di disponibilità, fare quindi clic su **Fine**.  
  
11. La pagina **Stato** visualizza lo stato di avanzamento dei passaggi per la creazione del gruppo di disponibilità, ovvero configurazione di endpoint, creazione del gruppo di disponibilità e creazione di un join della replica secondaria al gruppo.  
  
12. Al termine di questi passaggi, nella pagina **Risultati** vengono visualizzati i relativi risultati. Se tutti questi passaggi sono stati eseguiti correttamente, il nuovo gruppo di disponibilità è completamente configurato. Se si verifica un errore durante uno dei passaggi, potrebbe essere necessario completare manualmente la configurazione o usare una procedura dettagliata per il passaggio errato. Per informazioni sulla causa di un determinato errore, fare clic sul collegamento "Errore" nella colonna **Risultato** .  
  
     Al termine della procedura guidata, fare clic su **Chiudi** per uscire.  
  
##  <a name="RelatedTasks"></a>Attività correlate  
 **Per completare la configurazione del gruppo di disponibilità**  
  
-   [Aggiungere una replica secondaria a un gruppo di disponibilità &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Preparare manualmente un database secondario per un gruppo di disponibilità &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Aggiungere un database secondario a un gruppo di disponibilità &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Creare o configurare un listener del gruppo di disponibilità &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **Modalità alternative di creazione di un gruppo di disponibilità**  
  
-   [Utilizzare la finestra di dialogo nuovo gruppo di disponibilità &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Creare un gruppo di disponibilità &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md)  
  
-   [Creare un gruppo di disponibilità &#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md)  
  
 **Per abilitare Gruppi di disponibilità AlwaysOn**  
  
-   [Abilitare e disabilitare Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **Per configurare un endpoint del mirroring del database**  
  
-   [Creazione di un endpoint del mirroring del database per Gruppi di disponibilità AlwaysOn &#40;SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Creazione di un endpoint del mirroring del database per l'autenticazione di Windows &#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Utilizzare certificati per un endpoint del mirroring del database &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   [Specificare l'URL dell'endpoint quando si aggiunge o si modifica una replica di disponibilità &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **Per risolvere i problemi relativi alla configurazione di Gruppi di disponibilità AlwaysOn**  
  
-   [Risolvere i problemi di Gruppi di disponibilità AlwaysOn &#40;di configurazione SQL Server eliminati&#41;](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [Risolvere i problemi relativi a un'operazione di aggiunta file non riuscita &#40;Gruppi di disponibilità AlwaysOn&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a>Contenuto correlato  
  
-   **Blog**  
  
     [Pagina relativa alla serie di informazioni su HADRON riguardanti l'utilizzo del pool di lavoro per database abilitati HADRON in AlwaysOn](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [Blog del team di SQL Server AlwaysOn: Blog ufficiale del team di SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Blog sui tecnici SQL Server CSS](https://blogs.msdn.com/b/psssql/)  
  
-   **Video**  
  
     [Pagina relativa alla prima parte riguardante l'introduzione della soluzione a disponibilità elevata di prossima generazione della serie AlwaysOn di Microsoft SQL Server nome in codice "Denali"](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Pagina relativa alla seconda parte riguardante la compilazione di una soluzione a disponibilità elevata critica tramite AlwasyOn della serie AlwaysOn di Microsoft SQL Server nome in codice "Denali"](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **White paper**  
  
     [Pagina relativa alla guida alle soluzioni AlwaysOn di Microsoft SQL Server per la disponibilità elevata e il ripristino di emergenza](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [White paper Microsoft per SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [White paper del team di consulenza clienti di SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Vedere anche  
 [&#40;SQL Server dell'endpoint del mirroring del database&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Prerequisiti, restrizioni e consigli per Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
  
