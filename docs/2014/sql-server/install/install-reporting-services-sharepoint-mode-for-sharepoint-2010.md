---
title: Installare Reporting Services in modalità SharePoint per SharePoint 2010 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 47efa72e-1735-4387-8485-f8994fb08c8c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: cc0fe3bef02ebd50558c298ef8d9b3d8565744ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298680"
---
# <a name="install-reporting-services-sharepoint-mode-for-sharepoint-2010"></a>Installare la modalità SharePoint di Reporting Services per SharePoint 2010
  Nelle procedure contenute in questo argomento viene illustrata l'installazione di un server unico di un server di report di Reporting Services in modalità SharePoint. Nei passaggi è inclusa l'esecuzione dell'Installazione guidata di SQL Server, nonché di attività di configurazione aggiuntive in cui viene utilizzata Amministrazione centrale SharePoint 2010. L'argomento può inoltre essere utilizzato per singole procedure, ad esempio per creare una applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Per informazioni sull'aggiunta di ulteriori [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] server a una farm esistente, vedere [aggiungere un ulteriore Server di Report a una Farm di &#40;scalabilità orizzontale SSRS&#41; ](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md) e [Aggiungi un Web aggiuntivi Reporting Services Front-end a una Farm](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md).  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010|  
  
 L'installazione di un unico server è utile per scenari di sviluppo e di test ma non è consigliata per ambienti di produzione.  
  
> [!NOTE]  
>  Per informazioni sull'aggiornamento ed esistente [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installazione in modalità SharePoint a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], vedere [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  

  
##  <a name="bkmk_prereq"></a> Prerequisiti  
  
-   > [!IMPORTANT]  
    >  Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non è più richiesto o supportato per configurare e amministrare la modalità SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Utilizzare Amministrazione centrale SharePoint per configurare un server di report in modalità SharePoint. Per altre informazioni, vedere [gestire un'applicazione di servizio Reporting Services SharePoint](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md).  
  
-   Rivedere gli argomenti seguenti per i requisiti, inclusi i prodotti SharePoint 2010:  
  
    -   [Note sulla versione online](https://msdn.microsoft.com/library/dn169381.aspx)
  
    -   [Guida per l'utilizzo delle funzionalità di Business Intelligence di SQL Server in una farm di SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
-   In questo argomento non viene descritta l'installazione di prodotti SharePoint 2010. Per altre informazioni, vedere [materiale sussidiario per usando le funzionalità di Business Intelligence di SQL Server in una Farm di SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md).  
  
-   Queste procedure possono essere utilizzate per la configurazione di un server di report [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e non funzioneranno per le versioni precedenti del server di report. Nelle versioni precedenti del server di report non veniva utilizzata l'architettura del servizio SharePoint Shared. Ad esempio, i server di report SQL Server 2008 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e i server di report SQL Server 2008 R2 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Verificare i **SharePoint 2010 Administration** viene avviato in Server Manager di Windows.  
  
 ![Componenti di SSRS in un'installazione 1 server](../../../2014/sql-server/install/media/rs-deployment-1-server.gif "componenti di SSRS in un'installazione 1 server")  
  
### <a name="database-considerations-for-a-single-server-configuration"></a>Considerazioni sui database per una configurazione a server unico  
  
-   In Reporting Services e nei prodotti e nelle tecnologie SharePoint vengono utilizzati database relazionali di SQL Server per archiviare i dati dell'applicazione.  
  
-   Per [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] è richiesta un'istanza del motore SQL di un'edizione di valutazione di SQL Server compatibile.  
  
-   Nei prodotti SharePoint può essere utilizzata un'istanza del database esistente. Se un'istanza del motore di Database non è installata, il programma di installazione dei prodotti SharePoint consente di installare SQL Server Express Edition per i database dell'applicazione SharePoint.  
  
-   L'istanza del server di report non può utilizzare SQL Server Express Edition per il proprio database. Tuttavia, l'istanza di SQL Server Express Edition installata mediante il prodotto SharePoint può esistere in modalità side-by-side con altre eventuali edizioni del motore di database.  
  

  
##  <a name="bkmk_install_SSRS"></a> Installazione del Server di Report di Reporting Services in modalità SharePoint  
  
1.  Eseguire l'Installazione guidata di SQL Server.  
  
2.  Fare clic su **Installazione** nella parte sinistra della procedura guidata, quindi scegliere **Nuova installazione autonoma di SQL Server o aggiunta di funzionalità a un'installazione esistente**.  
  
3.  Fare clic su **OK** nella pagina **Regole di supporto dell'installazione** , presupponendo che siano state soddisfatte tutte le regole.  
  
4.  Fare clic su **Installa** nella pagina **File di supporto per l'installazione** .  
  
5.  Fare clic su **successivo** dopo avranno completato l'installazione i file di supporto e le regole di supporto per lo stato di un **passato**. esaminare eventuali avvisi o problemi che comportano blocchi.  
  
6.  Nel **codice Product Key** pagina, digitare il proprio codice o accettare quello predefinito dell'edizione "Enterprise Evaluation".  
  
     Scegliere **Avanti**.  
  
7.  Leggere e accettare le condizioni di licenza. Microsoft ringrazia gli utenti per la loro disponibilità a inviare dati di utilizzo delle funzionalità al fine di migliorare le funzionalità dei prodotti e il Servizio Supporto Tecnico Clienti.  
  
     Scegliere **Avanti**.  
  
8.  Selezionare **installazione funzionalità SQL Server** nel **impostazione ruolo** pagina.  
  
     Scegliere **Avanti**  
  
     ![Installazione di funzionalità di SQL Server per impostazione ruolo](../../../2014/sql-server/install/media/rs-setuprole.gif "Installazione di funzionalità di SQL Server per impostazione ruolo")  
  
9. Nella pagina **Selezione funzionalità** selezionare le opzioni seguenti:  
  
    -   **Reporting Services – SharePoint**  
  
    -   **Reporting Services aggiuntivo per prodotti SharePoint 2010**. ![Nota](../../../2014/reporting-services/media/rs-fyinote.png "nota")l'opzione dell'installazione guidata per installare il componente aggiuntivo è una novità di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] release.  
  
    -   Se non si dispone già di un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)]di SQL Server, è anche possibile selezionare **Servizi motore di database** e **Strumenti di gestione - Completa** per un ambiente completo.  
  
     Scegliere **Avanti**.  
  
     ![Selezione della funzionalità SSRS per la modalità SharePoint](../../../2014/sql-server/install/media/rs-setupfeatureselection-sharepoint-with-circles.gif "selezione della funzionalità SSRS per la modalità SharePoint")  
  
10. Fare clic su **successivo** nel **regole di installazione** pagina. esaminare eventuali avvisi o problemi che comportano blocchi.  
  
11. Se si seleziona Servizi motore di database, accettare l'istanza predefinita di **MSSQLSERVER** nella pagina **Configurazione dell'istanza** e fare clic su **Avanti**. L'architettura del servizio Shared di Reporting Services non è basata su un'istanza SQL Server come l'architettura di Reporting Services precedente.  
  
12. Esaminare la pagina **Requisiti di spazio su disco** e fare clic su **Avanti**.  
  
13. Nel **configurazione Server** pagina digitare le credenziali appropriate. Se si desidera utilizzare le funzionalità di avvisi dati o sottoscrizioni di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , è necessario modificare il **Tipo di avvio** per SQL Server Agent in **Automatico**.  
  
     Scegliere **Avanti**.  
  
14. Se si seleziona Servizi motore di database, verrà visualizzata la pagina **Configurazione del motore di database** ; aggiungere account appropriati all'elenco degli amministratori SQL e fare clic su **Avanti**.  
  
15. Nella pagina **Configurazione di Reporting Services** , l'opzione **Solo installazione** dovrebbe apparire come selezionata. Questa opzione consente di installare i file del server di report, ma non di configurare l'ambiente SharePoint per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Al termine dell'installazione di SQL Server, seguire le altre sezioni di questo argomento per configurare l'ambiente SharePoint. Questo include l'installazione del servizio Shared di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e la creazione delle applicazioni di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
     ![rs_SQL11_SETUP_SSRS_configpage_withcircles](../../../2014/sql-server/install/media/rs-kj-setup-ssrs-configpage-withcircles.gif "rs_SQL11_SETUP_SSRS_configpage_withcircles")  
  
16. Supportare Microsoft nel migliorare le funzionalità e i servizi SQL Server facendo clic sulla casella di controllo per inviare segnalazioni di errori nella pagina **Segnalazione errori** .  
  
     Scegliere **Avanti**.  
  
17. Esaminare eventuali avvisi, quindi fare clic su **Avanti** nella pagina **Regole di configurazione installazione** .  
  
18. Nella pagina **Inizio installazione** consultare il riepilogo sull'installazione, quindi fare clic su **Avanti**. Nel riepilogo verrà incluso un **Reporting Services** nodo che includerà il valore di modalità di installazione di **SharePointFilesOnlyMode** , nonché le informazioni sull'account.  
  

  
##  <a name="bkmk_install_SSRS_sharedservice"></a> Installare e avviare il servizio SharePoint di Reporting Services  
 ![Contenuto correlato di PowerShell](../../../2014/reporting-services/media/rs-powershellicon.jpg "Contenuto correlato di PowerShell")  
  
> [!NOTE]  
>  Se in una farm di SharePoint esistente, si sta installando **non è necessario a** completare i passaggi descritti in questa sezione. Il servizio SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è stato installato e avviato durante l'esecuzione dell'Installazione guidata di SQL Server nella sezione precedente.  
  
 I file necessari sono stati installati come parte dell'Installazione guidata di SQL Server, ma i servizi devono essere registrati nella farm SharePoint. Nella versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] viene introdotto il supporto PowerShell per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint. I passaggi seguenti illustrano l'apertura della shell di gestione SharePoint Management e l'esecuzione dei cmdlet:  
  
1.  Fare clic sul menu **Start** .  
  
2.  Scegliere il **prodotti Microsoft SharePoint 2010** gruppo.  
  
3.  Fare doppio clic su **Shell di gestione SharePoint 2010** fare clic su **Esegui come amministratore**.  
  
4.  Eseguire il comando PowerShell seguente per installare il servizio SharePoint. Se il comando viene correttamente eseguito, nella shell di gestione viene visualizzata una nuova riga. In questo caso, non viene restituito alcun messaggio:  
  
    ```  
    Install-SPRSService  
    ```  
  
5.  Eseguire il comando PowerShell seguente per installare il proxy del servizio:  
  
    ```  
    Install-SPRSServiceProxy  
    ```  
  
6.  Eseguire il comando PowerShell seguente per avviare il servizio o visualizzare le note seguenti per le istruzioni su come avviare il servizio da Amministrazione centrale SharePoint:  
  
    ```  
    get-spserviceinstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
    ```  
  
 È anche possibile avviare il servizio da Amministrazione centrale SharePoint anziché eseguire il terzo comando PowerShell. I passaggi seguenti sono anche utili per verificare che il servizio è in esecuzione.  
  
1.  Nel gruppo **Impostazioni sistema** di Amministrazione centrale SharePoint fare clic su **Gestisci servizi nel server** .  
  
2.  Individuare il **servizio SQL Server Reporting Services** e fare clic su **Avvio** nella colonna Azione.  
  
3.  Lo stato del servizio Reporting Services cambia da **Arrestato** in **Avviato**. Se il servizio Reporting Services non è presente nell'elenco, utilizzare PowerShell per installare il servizio.  
  
    > [!NOTE]  
    >  Se il servizio Reporting Services rimane nel **Starting** lo stato e non cambia in **avviato**, verificare che il servizio 'SharePoint 2010 Administration' viene avviato in Server Manager di Windows.  
  

  
##  <a name="bkmk_create_serrviceapplication"></a> Creare un'applicazione di servizio Reporting Services  
 In questa sezione vengono presentati i passaggi per creare un'applicazione di servizio e una descrizione delle proprietà, se è in corso la revisione di un'applicazione di servizio esistente.  
  
1.  Nel gruppo **Gestione applicazioni** di Amministrazione centrale SharePoint fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Nella barra multifunzione di SharePoint fare clic su **Nuovo** .  
  
3.  Nel menu Nuovo fare clic su **Applicazione di servizio SQL Server Reporting Services**.  
  
    > [!WARNING]  
    >  Se il [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] opzione non viene visualizzata nell'elenco, si tratta di un' **indicazione che la [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servizi condivisi non sono installato**. Rivedere la sezione precedente sull'utilizzo di cmdlts di PowerShell per installare il servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
4.  Nella pagina **Creazione di un'applicazione di servizio di SQL Server Reporting Services** immettere un nome per l'applicazione. Se si creano più applicazioni di servizio Reporting Services, tramite un nome descrittivo o una convenzione di denominazione sarà possibile organizzare l'amministrazione e la gestione delle operazioni.  
  
5.  Nella sezione **Pool di applicazioni** creare un nuovo pool di applicazioni per l'applicazione (consigliato). Se per il nuovo pool di applicazioni si utilizza lo stesso nome dell'applicazione di servizio, l'amministrazione può risultare più semplice.  
  
     Selezionare o creare un account gestito di sicurezza per il pool di applicazioni. Assicurarsi di specificare un account utente di dominio. Un account utente di dominio permette di utilizzare la funzionalità dell'account gestito di SharePoint, che consente di aggiornare password e informazioni sull'account da un'unica posizione. Gli account di dominio sono inoltre obbligatori se si prevede di ridimensionare la distribuzione per includere istanze del servizio aggiuntive da eseguire con la stessa identità.  
  
6.  In **Server di database**è possibile utilizzare il server corrente o scegliere un SQL Server diverso.  
  
7.  In **Nome database** il valore predefinito è `ReportingService_<guid>`, ovvero un nome di database univoco. Se si immette un nuovo valore, accertarsi che sia univoco.  
  
8.  In **Autenticazione database**l'impostazione predefinita è Autenticazione di Windows. Se si sceglie **Autenticazione di SQL Server**, fare riferimento alla guida dell'amministratore di SharePoint per le procedure consigliate sull'utilizzo di questo tipo di autenticazione in una distribuzione di SharePoint.  
  
9. Nella sezione **Associazione applicazione Web** , selezionare l'applicazione Web di cui effettuare il provisioning per l'accesso dall'applicazione di servizio Reporting Services corrente. È possibile associare un'applicazione di servizio Reporting Services a una sola applicazione Web. Se tutte le applicazioni Web correnti sono già associate con un'applicazione di servizio Reporting Services, viene visualizzato un messaggio di avviso.  
  
10. Fare clic su **OK**.  
  
11. Il completamento del processo di creazione dell'applicazione di servizio potrebbe richiedere diversi minuti. Al termine, verrà visualizzato un messaggio di conferma e un collegamento a una pagina di **provisioning di sottoscrizioni e avvisi** . Se si desidera utilizzare le funzionalità relative a sottoscrizioni e avvisi di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], completare il passaggio di provisioning. Per altre informazioni, vedere [Eseguire il provisioning di sottoscrizioni e avvisi per le applicazioni di servizio SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md).  
  
 ![Contenuto correlato di PowerShell](../../../2014/reporting-services/media/rs-powershellicon.jpg "contenuto correlato di PowerShell") per informazioni su come usare PowerShell per creare una [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] applicazione del servizio, vedere [per creare un'applicazione di servizio Reporting Services uso di PowerShell](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md#bkmk_powershell_create_ssrs_serviceapp).  
  

  
##  <a name="bkmk_powerview"></a> Attivare la funzionalità raccolta siti di Power View.  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], una funzionalità del [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aggiuntivo per [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition, è una funzionalità di raccolta siti. La funzionalità viene attivata automaticamente per raccolte siti radice e raccolte siti create dopo che viene installato il componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Se si intende utilizzare [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], verificare che la funzionalità sia attivata.  
  
 Se si installa il componente aggiuntivo di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per Prodotti SharePoint 2010 dopo l'installazione del prodotto SharePoint 2010, la funzionalità di integrazione del server di report e la funzionalità di integrazione di Power View saranno attivate solo per le raccolte siti radice. Per le altre raccolte siti, attivare manualmente le funzionalità.  
  
#### <a name="to-activate-the-power-view-feature"></a>Per attivare la funzionalità di Power View  
  
1.  Aprire il browser al sito di SharePoint desiderato.  
  
2.  Fare clic su **Azioni sito**.  
  
3.  Fare clic su **Impostazioni sito**.  
  
4.  Fare clic su **Funzionalità raccolta siti** nel gruppo Amministrazione raccolta siti  
  
5.  Individuare **Funzionalità di integrazione Power View** nell'elenco.  
  
6.  Fare clic su **Attiva**.  
  
 Questa procedura viene completata per ogni raccolta siti. Per altre informazioni, vedere [attivare le funzionalità di integrazione Power View in SharePoint e il Server di Report](../../reporting-services/activate-the-report-server-and-power-view-integration-features-in-sharepoint.md) .  
  
##  <a name="bkmk_additional_config"></a> Configurazione aggiuntiva  
 In questa sezione vengono descritti i passaggi di configurazione aggiuntivi che sono importanti nella maggior parte delle distribuzioni SharePoint.  
  
###  <a name="bkmk_provision_agent"></a> Avvisi e sottoscrizioni provisioning  
 Le funzionalità di sottoscrizione e avviso dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] possono richiedere la configurazione di autorizzazioni di SQL Server Agent. Se viene visualizzato un messaggio di errore che indica che SQL Server Agent è richiesto sebbene sia in esecuzione, aggiornare le autorizzazioni. È possibile fare clic sul collegamento **Provisioning di sottoscrizioni e avvisi** nella pagina di creazione dell'applicazione di servizio per passare a un'altra pagina di provisioning di SQL Server Agent. Il passaggio di provisioning è necessario se la distribuzione attraversa i limiti della macchina, ad esempio quando l'istanza di database di SQL Server si trova su una macchina diversa. Per altre informazioni, vedere [Eseguire il provisioning di sottoscrizioni e avvisi per le applicazioni di servizio SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md).  
  

  
### <a name="configure-e-mail-for-a-service-application"></a>Configurazione delle impostazioni di posta elettronica per un'applicazione di servizio  
 La funzionalità relativa agli avvisi dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] consente di inviare avvisi come messaggi di posta elettronica. Per inviare messaggi di posta elettronica potrebbe essere necessario configurare l'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , nonché modificare l'estensione per il recapito tramite posta elettronica per l'applicazione di servizio. Le impostazioni della posta elettronica sono richieste se si prevede di utilizzare l'estensione per il recapito tramite posta elettronica per la funzionalità di sottoscrizione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per altre informazioni, vedere [Configurare le impostazioni di posta elettronica per l'applicazione di servizio Reporting Services &#40;SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)  
  

  
### <a name="add-reporting-services-content-types"></a>Aggiunta di tipi di contenuto di Reporting Services  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornisce tipi di contenuto predefiniti usati per gestire file di origini dati condivise (con estensione rsds), modelli di report (con estensione smdl) e di definizione del report di Generatore report (con estensione rdl). Se si aggiungono i tipi di contenuto **Report di Generatore report**, **Modello di report**e **Origine dati report** a una raccolta, sarà possibile utilizzare il comando **Nuovo** per creare nuovi documenti del tipo desiderato. Per altre informazioni, vedere [aggiungere tipi di contenuto in una raccolta di &#40;Reporting Services in modalità integrata SharePoint&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  

  
### <a name="activate-the-file-sync-feature"></a>Attivazione della funzionalità Sincronizzazione file  
 La funzionalità Sincronizzazione file server di report è utile quando gli utenti caricano di frequente elementi di report pubblicati direttamente nelle raccolte documenti di SharePoint. La funzionalità di sincronizzazione file consente di sincronizzare il catalogo del server di report con gli elementi nelle raccolte documenti con maggiore frequenza. Per altre informazioni, vedere [Attivare la funzionalità Sincronizzazione file server di report in Amministrazione centrale SharePoint](../../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [PowerShell cmdlets for Reporting Services SharePoint Mode](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)   
 [Funzionalità supportate dalle edizioni di SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473)   
 [Servizio SharePoint di Reporting Services e applicazioni di servizio](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md)  
  
  
