---
title: Installare Reporting Services modalità SharePoint per SharePoint 2013 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: b29d0f45-0068-4c84-bd7e-5b8a9cd1b538
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 8874d4c57e2fb7b94e4efac44c90e93865d2b40f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "72798341"
---
# <a name="install-reporting-services-sharepoint-mode-for-sharepoint-2013"></a>Installare la modalità SharePoint di Reporting Services per SharePoint 2013
  Nelle procedure contenute in questo argomento viene illustrata l'installazione di un unico server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint. Nei passaggi è inclusa l'esecuzione dell'Installazione guidata di SQL Server, nonché di attività di configurazione in cui viene utilizzata Amministrazione centrale SharePoint. L'argomento può inoltre essere utilizzato per singole procedure di aggiornamento di un'installazione esistente, ad esempio per creare una applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; **Nota:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] la modalità SharePoint **non** supporta il multi-tenant di SharePoint Server.|  
  
 Per informazioni sull'aggiunta di ulteriori server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a una farm esistente, vedere quanto riportato di seguito:  
  
-   [Aggiungere un ulteriore server di report a una farm &#40;la scalabilità orizzontale di SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
-   [Aggiungere un ulteriore front-end Web di Reporting Services a una farm](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 L'installazione a server singolo è utile per scenari di sviluppo e di test, ma non è consigliata per ambienti di produzione.  
  
 **In questo argomento**  
  
-   [Distribuzione a server singolo di esempio](#bkmk_singleserver)  
  
-   [Account di installazione](#bkmk_setupaccounts)  
  
-   [Passaggio 1: installare Reporting Services server di report in modalità SharePoint](#bkmk_install_SSRS)  
  
-   [Passaggio 2: registrare e avviare il servizio SharePoint di Reporting Services](#bkmk_install_SSRS_sharedservice)  
  
-   [Passaggio 3: creare un'applicazione di servizio Reporting Services](#bkmk_create_serrviceapplication)  
  
-   [Passaggio 4: attivare la funzionalità di raccolta siti Power View.](#bkmk_powerview)  
  
-   [Script di Windows PowerShell per i passaggi 1-4](#bkmk_full_script)  
  
-   [Configurazione aggiuntiva](#bkmk_additional_config) , incluso il provisioning per sottoscrizioni e avvisi, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] i tipi di contenuto e la configurazione di Excel Services per l'utilizzo di un server Analysis Services.  
  
-   [Verificare l'installazione](#bkmk_verify_installation)  
  
##  <a name="bkmk_singleserver"></a>Distribuzione a server singolo di esempio  
 L'installazione di un unico server è utile per scenari di sviluppo e di test ma l'utilizzo di un server singolo non è consigliato per un ambiente di produzione. Con il termine "ambiente a server singolo" ci si riferisce a un computer singolo con SharePoint e componenti [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installati nello stesso computer. In questo argomento non viene illustrata la scalabilità orizzontale con più server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Nel diagramma seguente sono illustrati i componenti che fanno parte di una distribuzione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a server singolo.  
  
|||  
|-|-|  
|**1**|Servizio SharePoint installato dal programma di installazione di SQL Server. È possibile creare una o più applicazioni di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|**2**|
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Il componente aggiuntivo per prodotti SharePoint fornisce i componenti dell'interfaccia utente nei server SharePoint.|  
|**(3)**|Applicazione Excel Services utilizzata da Power View e PowerPivot.|  
|**(4)**|Applicazione di servizio PowerPivot.|  
  
 ![Distribuzione a server singolo in modalità SharePoint per SSRS](../../../2014/sql-server/install/media/rs-sharepoint-1server-deployment.gif "Distribuzione a server singolo in modalità SharePoint per SSRS")  
  
> [!TIP]  
>  Per esempi di distribuzione più complessi, vedere [Installazione della modalità SharePoint di Reporting Services (SharePoint 2010 e SharePoint 2013)](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md).  
  
##  <a name="bkmk_setupaccounts"></a>Account di installazione  
 In questa sezione vengono descritti gli account e le autorizzazioni utilizzati per i passaggi relativi alla distribuzione principale di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint.  
  
 **Installazione e registrazione del [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servizio:**  
  
-   L'account corrente durante l'installazione (definito account di "configurazione") di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint deve disporre dei diritti amministrativi nel computer locale. Se si installa [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dopo l'installazione di SharePoint e l'account ' Setup ' è anche membro del gruppo di amministratori della farm di SharePoint, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] l'installazione registrerà [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] il servizio. Se si installa [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] prima dell'installazione di SharePoint o l'account di "configurazione" non è un membro del gruppo di amministratori farm, il servizio viene registrato manualmente. Vedere la sezione [Passaggio 2: Registrare e avviare il servizio SharePoint di Reporting Services](#bkmk_install_SSRS_sharedservice).  
  
 **Creazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] di applicazioni di servizio**  
  
-   Dopo l'installazione e la registrazione del servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , creare una o più applicazioni di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . L'account di servizio della farm di SharePoint deve essere temporaneamente membro del gruppo di amministratori locali affinché l'applicazione di servizio Reporting Services possa essere creata. Per ulteriori informazioni sulle autorizzazioni dell'account SharePoint 2013, vedere [autorizzazioni e impostazioni di sicurezza per l'account in sharepoint 2013](https://technet.microsoft.com/library/cc678863.aspx) (https://technet.microsoft.com/library/cc678863.aspx).  
  
     Per motivi di sicurezza è consigliabile che gli account amministratori di farm di SharePoint non siano anche account amministratori del sistema operativo locale. Se si aggiunge un account amministratore di farm al gruppo di amministratori locali durante il processo di installazione, è consigliabile rimuoverlo al termine dell'installazione.  
  
##  <a name="bkmk_install_SSRS"></a>Passaggio 1: installare Reporting Services server di report in modalità SharePoint  
 Tramite questo passaggio vengono installati un server di report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint e il componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per prodotti SharePoint. A seconda degli elementi già installati nel computer, alcune delle pagine di installazione descritte nei passaggi seguenti potrebbero non essere visualizzate.  
  
1.  Eseguire l'Installazione guidata di SQL Server (Setup.exe).  
  
2.  Fare clic su **Installazione** nella parte sinistra della procedura guidata, quindi scegliere **Nuova installazione autonoma di SQL Server o aggiunta di funzionalità a un'installazione esistente**.  
  
3.  Fare clic su **OK** nella pagina **Regole di supporto dell'installazione** , presupponendo che siano state soddisfatte tutte le regole.  
  
4.  Fare clic su **Installa** nella pagina **File di supporto per l'installazione** . A seconda degli elementi già installati nel computer, potrebbe essere visualizzato il messaggio seguente:  
  
    -   "Operazioni in sospeso in uno o più file interessati. Al termine del processo, è necessario riavviare il computer".  
  
    -   Fare clic su **OK**.  
  
5.  Al termine dell'installazione dei file di supporto fare clic su **Avanti** . Per le pagine **Regole di supporto** verrà visualizzato lo stato **Operazione riuscita**. esaminare eventuali avvisi o problemi che comportano blocchi.  
  
6.  Nella pagina **Tipo di installazione** fare clic sull'opzione **Aggiungi funzionalità a un'istanza esistente di SQL Server 2014**. Selezionare l'istanza corretta nell'elenco a discesa e scegliere **Avanti**.  
  
7.  Se viene visualizzata la pagina **Codice Product Key**, digitare il proprio codice o accettare l'impostazione predefinita dell'edizione "Enterprise Evaluation".  
  
     Fare clic su **Avanti**.  
  
8.  Se viene visualizzata la pagina relativa alle condizioni di licenza, rivederle e accettarle. Microsoft ringrazia gli utenti per la loro disponibilità a inviare dati di utilizzo delle funzionalità al fine di migliorare le funzionalità dei prodotti e il Servizio Supporto Tecnico Clienti.  
  
     Fare clic su **Avanti**.  
  
9. Se viene visualizzata la pagina **Impostazione ruolo** , selezionare **Installazione funzionalità SQL Server**  
  
     Fare clic su **Avanti**  
  
     ![Installazione funzionalità SQL Server per il ruolo di installazione](../../../2014/sql-server/install/media/rs-setuprole.gif "Installazione funzionalità SQL Server per il ruolo di installazione")  
  
10. Nella pagina **Selezione funzionalità** selezionare le opzioni seguenti:  
  
    -   **Reporting Services-SharePoint**  
  
    -   **Reporting Services componente aggiuntivo per prodotti SharePoint**.  
  
         ![Nota](../../../2014/reporting-services/media/rs-fyinote.png "note") L'opzione di installazione guidata per l'installazione del componente aggiuntivo è una novità [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] della versione.  
  
    -   Se non si dispone già di un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)]di SQL Server, è anche possibile selezionare **Servizi motore di database** e **Strumenti di gestione - Completa** per un ambiente completo.  
  
     Fare clic su **Avanti**.  
  
     ![Selezione della funzionalità SSRS per la modalità SharePoint](../../../2014/sql-server/install/media/rs-setupfeatureselection-sharepoint-with-circles.gif "Selezione della funzionalità SSRS per la modalità SharePoint")  
  
11. Se viene visualizzata la pagina **Regole di installazione** , esaminare eventuali avvisi o problemi che comportano blocchi. Quindi fare clic su **Avanti**  
  
12. Se si seleziona Servizi motore di database, accettare l'istanza predefinita di **MSSQLSERVER** nella pagina **Configurazione dell'istanza** e fare clic su **Avanti**.  
  
     ![Nota](../../../2014/reporting-services/media/rs-fyinote.png "note") L'architettura del servizio Reporting Services SharePoint non è basata su una SQL Server "istanza", come nell'architettura di Reporting Services precedente.  
  
13. Esaminare la pagina **Requisiti di spazio su disco** e fare clic su **Avanti**.  
  
14. Se viene visualizzata la pagina **Configurazione server** , digitare le credenziali appropriate. Se si desidera utilizzare le funzionalità di avvisi dati o sottoscrizioni di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , è necessario modificare il **Tipo di avvio** per SQL Server Agent in **Automatico**. La pagina **Configurazione server** potrebbe non essere visualizzata a seconda degli elementi già installati nel computer.  
  
     Fare clic su **Avanti**.  
  
15. Se si seleziona Servizi motore di database, verrà visualizzata la pagina **Configurazione del motore di database** ; aggiungere account appropriati all'elenco degli amministratori SQL e fare clic su **Avanti**.  
  
16. Nella pagina **Configurazione di Reporting Services** , l'opzione **Solo installazione** dovrebbe apparire come selezionata. Tramite questa opzione vengono installati i file del server di report e non viene configurato l'ambiente SharePoint per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
    > [!NOTE]  
    >  Una volta completata l'installazione di SQL Server, attenersi alle altre sezioni di questo argomento per configurare l'ambiente SharePoint. Questo include l'installazione del servizio Shared di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e la creazione delle applicazioni di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
     ![Installazione guidata di SQL Server- Pagina di configurazione di SSRS](../../../2014/sql-server/install/media/rs-2012sp1-setup-ssrs-configpage-with-circles.gif "Installazione guidata di SQL Server- Pagina di configurazione di SSRS")  
  
17. Supportare Microsoft nel migliorare le funzionalità e i servizi SQL Server facendo clic sulla casella di controllo per inviare segnalazioni di errori nella pagina **Segnalazione errori** .  
  
     Fare clic su **Avanti**.  
  
18. Esaminare eventuali avvisi, quindi fare clic su **Avanti** nella pagina **Regole di configurazione installazione** .  
  
19. Nella pagina **Inizio installazione** consultare il riepilogo sull'installazione, quindi fare clic su **Avanti**. Nel riepilogo verrà incluso un nodo figlio **Modalità SharePoint di Reporting Services** per cui verrà visualizzato un valore **SharePointFilesOnlyMode**. Fare clic su **Installa**.  
  
20. Per l'installazione saranno richiesti diversi minuti. Verrà visualizzata la pagina **Operazione completata** con le funzionalità elencate e il relativo stato. Potrebbe essere visualizzata una finestra di dialogo in cui viene indicata la necessità di riavviare il computer.  
  
##  <a name="bkmk_install_SSRS_sharedservice"></a>Passaggio 2: registrare e avviare il servizio SharePoint di Reporting Services  
 ![Contenuto correlato di PowerShell](../../../2014/reporting-services/media/rs-powershellicon.jpg "Contenuto correlato di PowerShell")  
  
> [!NOTE]  
>  Se si esegue l'installazione in una farm di SharePoint esistente, non è necessario completare i passaggi in questa sezione. Il servizio SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene installato e avviato durante l'esecuzione dell'Installazione guidata di SQL Server nella sezione precedente di questo documento.  
  
 Di seguito sono riportati i motivi comuni per cui è necessario registrare manualmente il servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   È stata installata la modalità SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] prima di SharePoint.  
  
-   L'account utilizzato per installare la modalità SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non era membro del gruppo di amministratori di farm di SharePoint. Per altre informazioni, vedere la sezione [Setup accounts](#bkmk_setupaccounts).  
  
 I file necessari sono stati installati come parte dell'Installazione guidata di SQL Server, ma i servizi devono essere registrati nella farm SharePoint. Nella versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] viene introdotto il supporto PowerShell per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint.  
  
 I passaggi seguenti illustrano l'apertura della shell di gestione SharePoint Management e l'esecuzione dei cmdlet:  
  
1.  Fare clic sul pulsante **Start**  
  
2.  Fare clic sul gruppo **Prodotti Microsoft SharePoint 2013** .  
  
3.  Fare clic con il pulsante destro del mouse su **Shell di gestione di SharePoint 2013** e scegliere **Esegui come amministratore**. NOTA: i comandi di SharePoint non sono riconosciuti nella finestra standard di Windows PowerShell. Utilizzare **Shell di gestione SharePoint 2013**.  
  
4.  Eseguire il comando PowerShell seguente per installare il servizio SharePoint. Se il comando viene correttamente eseguito, nella shell di gestione viene visualizzata una nuova riga. Quando il comando viene completato correttamente, **non viene restituito alcun messaggio** alla Management Shell:  
  
    ```powershell
    Install-SPRSService  
    ```  
  
    > [!IMPORTANT]  
    >  Se viene visualizzato un messaggio di errore simile al seguente,  
    >   
    >  Install-SPRSService: il termine ' install-SPRSService ' **non è riconosciuto** come  
    > nome di cmdlet, funzione, programma eseguibile o file script. Vedere  
    > l'ortografia del nome o verificare che il percorso sia incluso  
    > e corretto, quindi riprovare.  
  
5.  Eseguire il seguente comando PowerShell per installare il proxy del servizio. Se il comando viene correttamente eseguito, nella shell di gestione viene visualizzata una nuova riga. Quando il comando viene completato correttamente, **non viene restituito alcun messaggio** alla Management Shell:  
  
    ```powershell
    Install-SPRSServiceProxy  
    ```  
  
6.  Eseguire il seguente comando PowerShell per avviare il servizio o visualizzare le note seguenti per le istruzioni su come avviare il servizio da Amministrazione centrale SharePoint:  
  
    ```powershell
    Get-SPServiceInstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
    ```  
  
 Si è in Windows PowerShell anziché nella shell di gestione SharePoint oppure non è installata la modalità SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per altre informazioni su [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e PowerShell, vedere [PowerShell cmdlets for Reporting Services SharePoint Mode](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)(Cmdlet di PowerShell per la modalità SharePoint di Reporting Services).  
  
 È anche possibile avviare il servizio da Amministrazione centrale SharePoint anziché eseguire il terzo comando PowerShell. I passaggi seguenti sono anche utili per verificare che il servizio è in esecuzione.  
  
1.  Nel gruppo **Impostazioni sistema** di Amministrazione centrale SharePoint fare clic su **Gestisci servizi nel server** .  
  
2.  Individuare il **servizio SQL Server Reporting Services** e fare clic su **Avvio** nella colonna Azione.  
  
3.  Lo stato del servizio Reporting Services cambia da **Arrestato** in **Avviato**. Se il servizio Reporting Services non è presente nell'elenco, utilizzare PowerShell per installare il servizio.  
  
    > [!NOTE]  
    >  Se il servizio Reporting Services rimane nello stato **Avvio in corso** e non cambia in **Avviato**, verificare che il servizio "Amministrazione SharePoint 2013" venga avviato in Server Manager di Windows.  
  
##  <a name="bkmk_create_serrviceapplication"></a>Passaggio 3: creare un'applicazione di servizio Reporting Services  
 In questa sezione vengono presentati i passaggi per creare un'applicazione di servizio e una descrizione delle proprietà, se è in corso la revisione di un'applicazione di servizio esistente.  
  
1.  Nel gruppo **Gestione applicazioni** di amministrazione centrale SharePoint fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Nella barra multifunzione di SharePoint fare clic su **Nuovo** .  
  
3.  Nel menu Nuovo fare clic su **Applicazione di servizio SQL Server Reporting Services**.  
  
    > [!IMPORTANT]  
    >  Se l' [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] opzione non è presente nell'elenco, significa **che il [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servizio condiviso non è installato**. Rivedere la sezione precedente sull'utilizzo di cmdlts di PowerShell per installare il servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
4.  Nella pagina **Creazione di un'applicazione di servizio di SQL Server Reporting Services** immettere un nome per l'applicazione. Se si creano più applicazioni di servizio Reporting Services, tramite un nome descrittivo o una convenzione di denominazione sarà possibile organizzare le operazioni di amministrazione e gestione.  
  
5.  Nella sezione **Pool di applicazioni** creare un nuovo pool di applicazioni per l'applicazione (consigliato). Se si utilizza lo stesso nome sia per il pool di applicazioni sia per l'applicazione di servizio, l'amministrazione può risultare più semplice. Questa situazione può essere influenzata anche dal numero di applicazioni di servizio create e dall'eventuale necessità di utilizzarne diverse in un unico pool di applicazioni. Vedere la documentazione del server SharePoint relativa alle indicazioni e alle procedure consigliate per la gestione del pool di applicazioni.  
  
     Selezionare o creare un account di sicurezza per il pool di applicazioni. Assicurarsi di specificare un account utente di dominio. Un account utente di dominio permette di utilizzare la funzionalità dell'account gestito di SharePoint, che consente di aggiornare password e informazioni sull'account da un'unica posizione. Gli account di dominio sono inoltre obbligatori se si prevede di ridimensionare la distribuzione per includere istanze del servizio aggiuntive da eseguire con la stessa identità.  
  
6.  In **Server di database**è possibile utilizzare il server corrente o scegliere un SQL Server diverso.  
  
7.  In **Nome database** il valore predefinito è `ReportingService_<guid>`, ovvero un nome di database univoco. Se si immette un nuovo valore, accertarsi che sia univoco. Si tratta del nuovo database da creare in modo specifico per l'applicazione di servizio.  
  
8.  In **Autenticazione database**l'impostazione predefinita è Autenticazione di Windows. Se si sceglie **Autenticazione di SQL Server**, fare riferimento alla documentazione di SharePoint per le procedure consigliate sull'utilizzo di questo tipo di autenticazione in una distribuzione di SharePoint.  
  
9. Nella sezione **Associazione applicazione Web** , selezionare l'applicazione Web di cui effettuare il provisioning per l'accesso dall'applicazione di servizio Reporting Services corrente. È possibile associare un'applicazione di servizio Reporting Services a una sola applicazione Web. Se tutte le applicazioni Web correnti sono già associate con un'applicazione di servizio Reporting Services, viene visualizzato un messaggio di avviso.  
  
10. Fare clic su **OK**.  
  
11. Il completamento del processo di creazione dell'applicazione di servizio potrebbe richiedere diversi minuti. Al termine, verrà visualizzato un messaggio di conferma e un collegamento a una pagina di **provisioning di sottoscrizioni e avvisi** . Se si desidera utilizzare la funzionalità relativa a sottoscrizioni o avvisi dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , completare il passaggio di provisioning. Per altre informazioni, vedere [Eseguire il provisioning di sottoscrizioni e avvisi per le applicazioni di servizio SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md).  
  
 ![Contenuto correlato di PowerShell](../../../2014/reporting-services/media/rs-powershellicon.jpg "Contenuto correlato di PowerShell") Per informazioni sull'utilizzo di PowerShell per creare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] un'applicazione di servizio, vedere:  
  
-   Vedere la sezione seguente [Script di Windows PowerShell per i passaggi da 1 a 4](#bkmk_full_script).  
  
-   Argomento [Per creare un'applicazione di servizio Reporting Services con PowerShell](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md#bkmk_powershell_create_ssrs_serviceapp).  
  
##  <a name="bkmk_powerview"></a>Passaggio 4: attivare la funzionalità di raccolta siti Power View.  
 
  [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], una funzionalità del componente aggiuntivo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per i prodotti [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint, è una funzionalità di raccolta siti. La funzionalità viene attivata automaticamente per raccolte siti radice e raccolte siti create dopo che viene installato il componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Se si intende utilizzare [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], verificare che la funzionalità sia attivata.  
  
 Se si installa il componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per prodotti SharePoint dopo l'installazione del server SharePoint, le funzionalità di integrazione del server di report e di Power View saranno attivate solo per le raccolte siti radice. Per le altre raccolte siti, attivare manualmente le funzionalità.  
  
#### <a name="to-activate-or-verify-the-power-view-site-collection-feature"></a>Per attivare o verificare la funzionalità per la raccolta di siti di Power View  
  
1.  Nei passaggi seguenti si presuppone che il sito di SharePoint sia configurato per la versione 2013. ****  
  
     Aprire il browser al sito di SharePoint desiderato. Ad esempio http://\<nomeserver>/sites/bi  
  
2.  Fare clic su **Impostazioni**![impostazioni di SharePoint](https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "Impostazioni di SharePoint").  
  
3.  Fare clic su **Impostazioni sito**.  
  
4.  Nel gruppo **Amministrazione raccolta siti** fare clic su **Funzionalità raccolta siti**.  
  
5.  Individuare **Funzionalità di integrazione Power View** nell'elenco.  
  
6.  Fare clic su **Attiva**. Lo stato della funzionalità verrà impostato su **Attiva**.  
  
 Questa procedura viene completata per ogni raccolta siti. Per altre informazioni, vedere [Attivare le funzionalità di integrazione per Power View e server di report in SharePoint](../../../2014/reporting-services/activate-the-report-server-and-power-view-integration-features-in-sharepoint.md).  
  
##  <a name="bkmk_full_script"></a>Script di Windows PowerShell per i passaggi 1-4  
 Lo script di PowerShell in questa sezione è l'equivalente del completamento dei passaggi da 1 a 4 nelle sezioni precedenti. Lo script consente di completare quanto indicato di seguito:  
  
-   Viene installato il servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e il proxy del servizio e viene avviato il servizio.  
  
-   Viene creato un proxy del servizio denominato "Reporting Services".  
  
-   Crea un' [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] applicazione di servizio denominata "Reporting Services Application".  
  
-   Viene abilitata la funzionalità di [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] per una raccolta siti.  
  
 Parametri  
  
-   Aggiornare **-Account** per il proxy del servizio. È necessario che l'account sia un account del servizio gestito nella farm di SharePoint. Per ulteriori informazioni, vedere l'argomento di SharePoint [Pianificare gli account amministrativi e di servizio in SharePoint 2013](https://technet.microsoft.com/library/cc263445.aspx).  
  
-   Aggiornare il parametro **–DatabaseServer** per l'applicazione di servizio. Questo parametro è l'istanza del motore di database  
  
-   Aggiornare il parametro **–url** del sito per il quale si desidera abilitare la funzionalità [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)].  
  
 **Per usare lo script:**  
  
1.  Aprire Windows PowerShell con privilegi amministrativi.  
  
2.  Copiare il codice seguente nella finestra dello script.  
  
3.  Aggiornare i tre parametri descritti nella sezione precedente e quindi eseguire lo script.  
  
```powershell
#This script Configures SQL Server Reporting Services SharePoint mode  
  
$starttime = Get-Date  
Write-Host -foregroundcolor DarkGray StartTime>> $starttime   
  
Write-Host -ForegroundColor Green "Import the SharePoint PowerShell snappin"  
Add-PSSnapin Microsoft.Sharepoint.Powershell -EA 0  
  
Write-Host -ForegroundColor Green "Install SSRS Service and Service Proxy, and start the service"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
  
    Write-Host -ForegroundColor Green "Install the Reporting Services Shared Service"  
    Install-SPRSService  
  
    Write-Host -ForegroundColor Green " Install the Reporting Services Service Proxy"  
    Install-SPRSServiceProxy  
  
    # Get the ID of the RS Service Instance and start the service   
    Write-Host -ForegroundColor Green "Start the Reporting Services Service"  
    $RS = Get-SPServiceInstance | Where {$_.TypeName -eq "SQL Server Reporting Services Service"}  
    Start-SPServiceInstance -Identity $RS.Id.ToString()  
  
    # Wait for the Reporting Services Service to start...  
    $Status = Get-SPServiceInstance $RS.Id.ToString()  
    While ($Status.Status -ne "Online")  
    {  
        Write-Host -ForegroundColor Green "SSRS Service Not Online...Current Status = " $Status.Status  
        Start-Sleep -Seconds 2  
        $Status = Get-SPServiceInstance $RS.Id.ToString()  
    }  
  
$time = Get-Date  
Write-Host -foregroundcolor DarkGray StartTime>> $starttime   
Write-Host -foregroundcolor DarkGray $time  
  
Write-Host -ForegroundColor Green "Create a new application pool and Reporting Services service application"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Write-Host -ForegroundColor Green "Create a new application pool"  
#!!!! update "-Account" with an existing Managed Service Account  
New-SPServiceApplicationPool -Name "Reporting Services" -Account "<domain>\User name>"  
$appPool = Get-SPServiceApplicationPool "Reporting Services"  
  
Write-Host -ForegroundColor Green " Create the Reporting Services Service Application"  
#!!!! Update "-DatabaseServer", an instance of the SQL Server database engine   
$rsService = New-SPRSServiceApplication -Name "Reporting Services Application" -ApplicationPool $appPool -DatabaseName "Reporting_Services_Application" -DatabaseServer "<server name>"  
  
Write-Host -ForegroundColor Green "Create the Reporting Services Service Application Proxy"  
$rsServiceProxy = New-SPRSServiceApplicationProxy -Name "Reporting Services Application Proxy" -ServiceApplication $rsService  
  
Write-Host -ForegroundColor Green "Associate service application proxy to default web site and grant web applications rights to SSRS application pool"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"     
# Associate the Reporting Services Service Applicatoin Proxy to the default web site...  
Get-SPServiceApplicationProxyGroup -default | Add-SPServiceApplicationProxyGroupMember -Member $rsServiceProxy  
  
$time=Get-Date  
Write-Host -foregroundcolor DarkGray StartTime>> $starttime   
Write-Host -foregroundcolor DarkGray $time  
  
Write-Host -ForegroundColor Green "Enable the PowerView and reportserver site features"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
#!!!! update "-url"  of the site where you want the features enabled  
Enable-SPfeature -identity "powerview" -Url http://server/sites/bi  
Enable-SPfeature -identity "reportserver" -Url http://server/sites/bi  
  
####To Verify, you can run the following:  
#Get-SPRSServiceApplication  
#Get-SPServiceApplicationPool | where {$_.name -like "reporting*"}  
#Get-SPRSServiceApplicationProxy
```  
  
##  <a name="bkmk_additional_config"></a>Configurazione aggiuntiva  
 In questa sezione vengono descritti i passaggi di configurazione aggiuntivi che sono importanti nella maggior parte delle distribuzioni SharePoint.  
  
###  <a name="bkmk_configure_ECS"></a>Configurare Excel Services e PowerPivot  
 Se si desidera visualizzare i report [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] Power View in una cartella di lavoro di Excel 2013 in SharePoint, è necessario configurare un'applicazione di Excel Services nella farm per l'utilizzo di un server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità SharePoint. Inoltre, l'account di sicurezza del pool di applicazioni utilizzato dall'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] deve essere un amministratore del server Analysis Services. Per altre informazioni, vedere gli argomenti seguenti:  
  
-   La sezione "configurare Excel Services per l'integrazione di Analysis Services" nell' [installazione di PowerPivot per SharePoint 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode).  
  
-   [Gestire le impostazioni del modello di dati di Excel Services (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780.aspx).  
  
###  <a name="bkmk_provision_agent"></a>Provisioning di sottoscrizioni e avvisi  
 Le funzionalità di sottoscrizione e avviso dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] possono richiedere la configurazione di autorizzazioni di SQL Server Agent. Se viene visualizzato un messaggio di errore che indica che SQL Server Agent è richiesto sebbene sia in esecuzione, aggiornare le autorizzazioni. È possibile fare clic sul collegamento **Provisioning di sottoscrizioni e avvisi** nella pagina di creazione dell'applicazione di servizio per passare a un'altra pagina di provisioning di SQL Server Agent. Il passaggio di provisioning è necessario se la distribuzione attraversa i limiti della macchina, ad esempio quando l'istanza di database di SQL Server si trova su una macchina diversa. Per ulteriori informazioni, vedere [provisioning di sottoscrizioni e avvisi per le applicazioni di servizio SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  
### <a name="configure-e-mail-for-ssrs-service-applications"></a>Configurare la posta elettronica per le applicazioni di servizio SSRS  
 La funzionalità relativa agli avvisi dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] consente di inviare avvisi come messaggi di posta elettronica. Per inviare messaggi di posta elettronica potrebbe essere necessario configurare l'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , nonché modificare l'estensione per il recapito tramite posta elettronica per l'applicazione di servizio. Le impostazioni della posta elettronica sono richieste se si prevede di utilizzare l'estensione per il recapito tramite posta elettronica per la funzionalità di sottoscrizione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per altre informazioni, vedere [Configurare le impostazioni di posta elettronica per l'applicazione di servizio Reporting Services &#40;SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)  
  
### <a name="add-reporting-services-content-types-to-content-libraries"></a>Aggiungere i tipi di contenuto di Reporting Services alle raccolte contenuto  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornisce tipi di contenuto predefiniti usati per gestire file di origini dati condivise (con estensione rsds), modelli di report (con estensione smdl) e di definizione del report di Generatore report (con estensione rdl). Se si aggiungono i tipi di contenuto **Report di Generatore report**, **Modello di report**e **Origine dati report** a una raccolta, sarà possibile utilizzare il comando **Nuovo** per creare nuovi documenti del tipo desiderato. Per ulteriori informazioni, vedere [aggiungere tipi di contenuto del server di report a una raccolta &#40;Reporting Services in modalità integrata SharePoint&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
### <a name="activate-the-report-server-file-sync-feature"></a>Attivare la funzionalità di sincronizzazione del file server di report  
 La funzionalità a livello di sito **Sincronizzazione file server di report** è utile quando gli utenti caricano di frequente elementi di report pubblicati direttamente nelle raccolte documenti di SharePoint. La funzionalità di sincronizzazione file consente di sincronizzare il catalogo del server di report con gli elementi nelle raccolte documenti con maggiore frequenza. Per altre informazioni, vedere [Attivare la funzionalità Sincronizzazione file server di report in Amministrazione centrale SharePoint](../../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md).  
  
##  <a name="bkmk_verify_installation"></a>Verificare l'installazione  
 Di seguito sono riportati i passaggi e le procedure consigliati per verificare la distribuzione in modalità SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Vedere la sezione di SharePoint nell'argomento di verifica [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md).  
  
-   In una raccolta documenti di SharePoint creare un report semplice di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] contenente solo una casella di testo, ad esempio un titolo. Il report non contiene origini dati e set di dati. L'obiettivo consiste nel verificare che sia possibile aprire Generatore report, compilare un report semplice e visualizzare il report in anteprima.  
  
     Salvare il report nella raccolta documenti e quindi eseguire il report dalla raccolta. Per altre informazioni sulla creazione di report con Generatore report, vedere [Avviare Generatore report (Generatore report)](https://technet.microsoft.com/library/ms159221.aspx).  
  
## <a name="see-also"></a>Vedere anche  
 [Cmdlet di PowerShell per Reporting Services modalità SharePoint](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)   
 [Aggiornare ed eseguire la migrazione Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
 [Roadmap del contenuto: configurare e configurare SharePoint Server e SQL Server BI](https://technet.microsoft.com/library/dn205112.aspx)   
 [Funzionalità supportate dalle edizioni di SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473)   
 [Reporting Services servizio SharePoint e applicazioni di servizio](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md)
