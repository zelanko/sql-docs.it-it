---
title: PowerPivot per SharePoint 2013 installazione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: d3310562-82c1-454f-9c48-33a241749238
author: minewiskan
ms.author: owend
ms.openlocfilehash: 82836ab9b7d4d191f48895e215ffb9293f4ffe97
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543943"
---
# <a name="powerpivot-for-sharepoint-2013-installation"></a>PowerPivot for SharePoint 2013 Installation
  Nelle procedure contenute in questo argomento viene illustrata l'installazione di un unico server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità di distribuzione SharePoint. Nei passaggi è inclusa l'esecuzione dell'Installazione guidata di SQL Server, nonché di attività di configurazione in cui viene utilizzata Amministrazione centrale SharePoint 2013.  
  
 **[!INCLUDE[applies](../../../includes/applies-md.md)]** SharePoint 2013 | SharePoint 201  
  
 **Contenuto dell'argomento:**  
  
 [Background](#bkmk_background)  
  
 [Prerequisiti](#bkmk_prereq)  
  
 [Passaggio 1: Installare PowerPivot per SharePoint](#InstallSQL)  
  
 [Passaggio 2: Configurare l'integrazione SharePoint per Analysis Services di base](#bkmk_config)  
  
 [Passaggio 3: Verificare l'integrazione](#bkmk_verify)  
  
 [Configurare Windows Firewall per consentire l'accesso ad Analysis Services](#bkmk_firewall)  
  
 [Aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato](#bkmk_upgrade_workbook)  
  
 [Oltre l'installazione a server singolo-PowerPivot per Microsoft SharePoint](#bkmk_multiple_servers)  
  
##  <a name="background"></a>Informazioni di background sul <a name="bkmk_background"></a>  
 PowerPivot per SharePoint è una raccolta di servizi di livello intermedio e di back-end che forniscono dati PowerPivot per accedere a una farm di SharePoint 2013.  
  
-   **Servizi back-end:** se si utilizza PowerPivot per Excel per creare cartelle di lavoro in cui sono contenuti dati analitici, è necessario disporre di PowerPivot per SharePoint per accedere a questi dati in un ambiente server. Il programma di installazione di SQL Server può essere eseguito in un computer in cui è installato SharePoint Server 2013 o in uno diverso in cui non è disponibile il software SharePoint. In Analysis Services non è presente alcuna dipendenza da SharePoint.  
  
     **Nota:** in questo argomento vengono descritti l'installazione del server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e i servizi back-end.  
  
-   **Livello intermedio:** sono stati apportati miglioramenti agli utilizzi di PowerPivot di SharePoint, tra cui la raccolta PowerPivot, la pianificazione dell'aggiornamento dati, il dashboard di gestione e i provider di dati. Per ulteriori informazioni sull'installazione e sulla configurazione del livello intermedio, vedere gli argomenti seguenti:  
  
    -   [Installare o disinstallare il componente aggiuntivo PowerPivot per SharePoint &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)  
  
    -   [Configurare PowerPivot e distribuire soluzioni &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013)  
  
##  <a name="prerequisites"></a><a name="bkmk_prereq"></a> Prerequisiti  
  
1.  Per eseguire il programma di installazione di SQL Server, è necessario essere un amministratore locale.  
  
2.  SharePoint Server 2013 Enterprise Edition è richiesto per PowerPivot per SharePoint. È anche possibile usare l'edizione Enterprise di valutazione.  
  
3.  Il computer deve essere unito a un dominio nella stessa foresta di Active Directory di Excel Services.  
  
4.  È necessario disporre del nome di istanza di PowerPivot. Nel computer in cui si sta installando Analysis Services in modalità SharePoint non deve essere presente un'istanza denominata di PowerPivot esistente.  
  
5.  Esaminare [i requisiti hardware e software per Analysis Services server in modalità SharePoint &#40;SQL Server 2014&#41;](../../../sql-server/install/hardware-software-requirements-analysis-services-server-sharepoint-mode.md).  
  
6.  Vedere le note sulla versione in [SQL Server 2012 Service Pack 1 Note sulla versione](https://go.microsoft.com/fwlink/?LinkID=248389) ( https://go.microsoft.com/fwlink/?LinkID=248389) .  
  
###  <a name="sql-server-edition-requirements"></a><a name="bkmk_sqleditions"></a> Requisiti relativi all'edizione di SQL Server  
 Non tutte le funzionalità di Business Intelligence sono disponibili in ogni edizione di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Per informazioni dettagliate, vedere [Features Supported by the Editions https://go.microsoft.com/fwlink/?linkid=232473) of SQL Server 2012 (](https://go.microsoft.com/fwlink/?linkid=232473) and [Editions and components of SQL Server 2014](../../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
 Le note sulla versione corrente sono disponibili nella pagina relativa alle [Note sulla versione di SQL Server 2012 SP1](https://go.microsoft.com/fwlink/?LinkID=248389) ( https://go.microsoft.com/fwlink/?LinkID=248389) .  
  
 [Note sulla versione di Microsoft SQL Server https://go.microsoft.com/fwlink/?LinkId=236893) 2012 (](https://go.microsoft.com/fwlink/?LinkId=236893).  
  
##  <a name="step-1-install-powerpivot-for-sharepoint"></a><a name="InstallSQL"></a>Passaggio 1: installare PowerPivot per SharePoint  
 In questo passaggio è possibile eseguire il programma di installazione di SQL Server per installare un server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità SharePoint. In un passaggio successivo è possibile configurare l'utilizzo da parte di Excel Services di questo server per i modelli di dati della cartella di lavoro.  
  
1.  Eseguire l'Installazione guidata di SQL Server (Setup.exe).  
  
2.  Fare clic su **Installazione** nel pannello di navigazione sinistro.  
  
3.  Fare clic su **Nuova installazione autonoma di SQL Server o aggiunta di funzionalità a un'installazione esistente**.  
  
4.  Se viene visualizzata la pagina **Codice Product Key** specificare la versione di valutazione o immettere un codice Product Key per una copia concessa in licenza dell'edizione Enterprise. Fare clic su **Avanti**. Per ulteriori informazioni sulle versioni, vedere [Editions and Components of SQL Server 2014](../../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
5.  Leggere e accettare le condizioni di licenza software Microsoft, quindi scegliere **Avanti**.  
  
6.  Se viene visualizzata la pagina **Regole globali** , esaminare eventuali informazioni relative alle regole visualizzate nell'installazione guidata.  
  
7.  Nella pagina **Microsoft Update** si consiglia di utilizzare Microsoft Update per verificare gli aggiornamenti, quindi scegliere **Avanti**.  
  
8.  La pagina **Installazione dei file di installazione** viene eseguita per diversi minuti. Esaminare eventuali avvisi sulle regole o regole con esito negativo, quindi fare clic su **Avanti**.  
  
9. Se **Regole di supporto dell'installazione**viene di nuovo visualizzato, verificare tutti gli avvisi e fare clic su **Avanti**.  
  
     **Nota:** poiché Windows Firewall è abilitato, viene visualizzato un avviso in cui è richiesto di aprire le porte per abilitare l'accesso remoto.  
  
10. Nella pagina **Impostazione ruolo** selezionare **SQL Server PowerPivot per SharePoint**. Tramite questa opzione viene installato Analysis Services in modalità SharePoint.  
  
     Facoltativamente, è possibile aggiungere un'istanza del Motore di database all'installazione. È possibile aggiungere il motore di database durante la configurazione di una nuova farm ed è necessario un server di database per eseguire la configurazione della farm e i database del contenuto. Tramite questa opzione viene inoltre installato [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
     Se si aggiunge il motore di database, viene installato come un'istanza denominata di **PowerPivot** . Ogni volta che si specifica una connessione a questa istanza, immettere il nome database nel formato: [`servername`]\PowerPivot.  
  
     Fare clic su **Avanti**.  
  
     ![Impostazione ruolo](../../../sql-server/install/media/gmni-setupui-featurerole-sql2012sp1.gif "Impostazione ruolo")  
  
11. In Selezione funzionalità viene visualizzato, a scopo informativo, un elenco in sola lettura delle funzionalità. Non è possibile aggiungere o rimuovere gli elementi preselezionati per questo ruolo. Fare clic su **Avanti**.  
  
12. Nella pagina **Configurazione dell'istanza** un nome dell'istanza in sola lettura di "PowerPivot" viene visualizzato a scopo informativo. Questo nome dell'istanza è obbligatorio e non può essere modificato. È tuttavia possibile immettere un ID istanza univoco per specificare un nome di directory descrittivo e chiavi del Registro di sistema. Fare clic su **Avanti**.  
  
13. Nella pagina **Configurazione server** configurare tutti i servizi per **Tipo di avvio**automatico. Specificare l'account di dominio e la password desiderati per **SQL Server Analysis Services**, **(1)** nel diagramma seguente.  
  
    -   Per [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]è possibile utilizzare un account **utente di dominio** o un account **NetworkService** . Non utilizzare gli account LocalService o LocalSystem.  
  
    -   Se si aggiungono il Motore di database di SQL Server e SQL Server Agent, è possibile configurare i servizi da eseguire in account utente di dominio o in account virtuali predefiniti.  
  
    -   Non eseguire mai il provisioning degli account di servizio con il proprio account utente di dominio. Con questa operazione si concedono al server le stesse autorizzazioni di cui l'utente dispone per le risorse disponibili nella rete. Se un utente malintenzionato compromette il server, l'utente in questione viene connesso con le proprie credenziali di dominio, pertanto, potrà scaricare o utilizzare gli stessi dati e le stesse applicazioni.  
  
     Fare clic su **Avanti**.  
  
     ![Configurazione di SSAS Server](../../../sql-server/install/media/ssas-powerpivotsetupsql2012sp1-serverconfiguration.gif "Configurazione di SSAS Server")  
  
14. Se si sta installando il [!INCLUDE[ssDE](../../../includes/ssde-md.md)], viene visualizzata la pagina **Configurazione del motore di database** . In Configurazione del [!INCLUDE[ssDE](../../../includes/ssde-md.md)] fare clic su **Aggiungi utente corrente** per concedere le autorizzazioni di amministratore dell'account utente per l'istanza del motore di database.  
  
     Fare clic su **Avanti**.  
  
15. Nella pagina **Configurazione di Analysis Services** fare clic su **Aggiungi utente corrente** per concedere le autorizzazioni amministrative dell'account utente. Saranno necessarie autorizzazioni amministrative per configurare il server dopo che è stata completata l'installazione.  
  
    -   Nella stessa pagina, aggiungere l'account utente di Windows di qualsiasi altra persona che richiede autorizzazioni amministrative. Ad esempio, qualsiasi utente che desidera connettersi all'istanza del [!INCLUDE[ssGeminiSrv](../../../includes/ssgeminisrv-md.md)] in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] per risolvere problemi di connessione al database deve disporre di autorizzazioni di amministratore di sistema. Aggiungere l'account utente di qualsiasi persona che potrebbe avere la necessità di risolvere problemi o amministrare il server.  
  
    -   > [!NOTE]  
        >  A tutte le applicazioni del servizio per cui è richiesto l'accesso all'istanza del server Analysis Services devono essere associate autorizzazioni amministrative di Analysis Services. Ad esempio, aggiungere gli account di servizio per Excel Services, Power View e Performance Point Services. Inoltre, aggiungere l'account della farm di SharePoint che viene utilizzato come identità dell'applicazione Web in cui è ospitata Amministrazione centrale.  
  
     Fare clic su **Avanti**.  
  
16. Nella pagina **Segnalazione errori** fare clic su **Avanti**.  
  
17. Nella pagina **Pronto per l'installazione**, fare clic su **Installa**.  
  
18. Se viene visualizzata la finestra di dialogo **Richiesto riavvio del computer**, fare clic su **OK**.  
  
19. Al termine dell'installazione fare clic su **Chiudi**.  
  
20. Riavviare il computer.  
  
21. Se nell'ambiente è disponibile un firewall, vedere l'argomento della documentazione online di SQL Server [Configure the Windows Firewall to Allow Analysis Services Access](../configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
### <a name="verify-the-sql-server-installation"></a>Verificare l'installazione di SQL Server  
 Verificare che il servizio Analysis Services sia in esecuzione.  
  
1.  In Microsoft Windows fare clic su **Start**, **Tutti i programmi**, quindi scegliere il gruppo **Microsoft SQL Server 2012** .  
  
2.  Fare clic su **SQL Server Management Studio**.  
  
3.  Connettersi all'istanza di Analysis Services, ad esempio **[nome server]\POWERPIVOT**. Se è possibile connettersi all'istanza, significa che il servizio è in esecuzione.  
  
##  <a name="step-2-configure-basic-analysis-services-sharepoint-integration"></a><a name="bkmk_config"></a>Passaggio 2: configurare l'integrazione di base Analysis Services SharePoint  
 Nei passaggi seguenti vengono descritte le modifiche di configurazione necessarie per interagire con i modelli di dati avanzati di Excel all'interno di una raccolta documenti di SharePoint. Completare questi passaggi dopo l'installazione di SharePoint Server 2013 e SQL Server Analysis Services.  
  
### <a name="grant-excel-services-server-administration-rights-on-analysis-services"></a>Garantire i diritti di amministrazione del server Excel Services per Analysis Services  
 Non è necessario completare questa sezione se durante l'installazione di Analysis Services è stato aggiunto l'account di servizio dell'applicazione Excel Services come amministratore di Analysis Services.  
  
1.  Nel server Analysis Services avviare SQL Server Management Studio e connettersi all'istanza di Analysis Services, ad esempio `[MyServer]\POWERPIVOT`.  
  
2.  In Esplora oggetti fare clic con il pulsante destro del mouse sul nome dell'istanza e scegliere **Proprietà**.  
  
     ![Visualizzazione delle proprietà di un server SSAS](../../../sql-server/install/media/as-ssms-proeprties.gif "Visualizzazione delle proprietà di un server SSAS")  
  
3.  Nel riquadro sinistro fare clic su **Sicurezza**. Aggiungere l'account di accesso del dominio configurato per l'applicazione Excel Services nel passaggio 1.  
  
     ![Impostazioni di sicurezza di un server SSAS](../../../sql-server/install/media/as-ssms-security.gif "Impostazioni di sicurezza di un server SSAS")  
  
### <a name="configure-excel-services-for-analysis-services-integration"></a>Configurare Excel Services per l'integrazione di Analysis Services  
  
1.  Nel gruppo Gestione applicazioni di Amministrazione centrale SharePoint fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Fare clic sul nome dell'applicazione di servizio. Il nome predefinito è **Applicazione Excel Services**.  
  
3.  Nella pagina **Gestione applicazione Excel Services**fare clic su **Impostazioni modello di dati**.  
  
4.  Fare clic su **Aggiungi server**.  
  
5.  In **Nome server**digitare il nome del server Analysis Services e il nome dell'istanza di PowerPivot. Ad esempio `MyServer\POWERPIVOT`. Il nome dell'istanza di PowerPivot è obbligatorio.  
  
     Digitare una descrizione.  
  
6.  Fare clic su **OK**.  
  
7.  Le modifiche verranno applicate in pochi minuti oppure è possibile scegliere le opzioni **Arresta** e **Avvia** il servizio **Servizi di calcolo Excel**. A  
  
     È anche possibile aprire un prompt dei comandi con privilegi amministrativi e digitare `iisreset /noforce`.  
  
     È possibile verificare se il server è riconosciuto da Excel Services controllando le voci nel log ULS. Saranno visualizzate voci simili alle seguenti:  
  
    ```  
    Excel Services Application            Data Model        27           Medium                Check Administrator Access ([ServerName]\POWERPIVOT): Pass.        f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Server Version ([ServerName]\POWERPIVOT): Pass (11.0.2809.24 >= 11.0.2800.0).         f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Deployment Mode ([ServerName]\POWERPIVOT): Pass.            f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
  
    ```  
  
##  <a name="step-3-verify-the-integration"></a><a name="bkmk_verify"></a>Passaggio 3: verificare l'integrazione  
 Nei passaggi seguenti vengono illustrati la creazione e il caricamento di una nuova cartella di lavoro per verificare l'integrazione di Analysis Services. È necessario disporre di un database di SQL Server per completare i passaggi.  
  
1.  **Nota:** se è già disponibile una cartella di lavoro avanzata con filtri dei dati o filtri, è possibile caricarla nella raccolta documenti di SharePoint e verificare l'eventuale possibilità di interagire con questi elementi dalla visualizzazione raccolta documenti.  
  
2.  Avviare una nuova cartella di lavoro in Excel  
  
3.  Nella scheda Dati fare clic su **Da altre origini** nella barra multifunzione in **Recupera dati esterni**.  
  
4.  Selezionare **Da SQL Server**.  
  
5.  In **Connessione guidata dati**immettere il nome dell'istanza di SQL Server in cui è presente il database che si desidera utilizzare.  
  
6.  In alternativa, in Credenziali di accesso verificare che **Usa autenticazione di Windows** sia selezionato, quindi fare clic su **Avanti**.  
  
7.  Selezionare il database che si desidera utilizzare.  
  
8.  Verificare che la casella di controllo **Connetti a una tabella specifica** sia selezionata.  
  
9. Fare clic sulla casella di controllo **Abilita selezione di più tabelle e aggiungi tabelle nel modello di dati di Excel** .  
  
10. Selezionare le tabelle che si desidera importare.  
  
11. Fare clic sulla casella di controllo **Importa relazioni tra le tabelle selezionate**, quindi fare clic su **Avanti**. Importando più tabelle da un database relazionale è possibile utilizzare tabelle già correlate. I passaggi vengono salvati poiché non è necessario compilare manualmente le relazioni.  
  
12. Nella pagina **Salva file di connessione dati e chiudi** della procedura guidata digitare un nome per la connessione e fare clic su **Fine**.  
  
13. Verrà visualizzata la finestra di dialogo **Importa dati** . Scegliere **Report di tabella pivot**, quindi fare clic su **OK**.  
  
14. Nella cartella di lavoro viene visualizzato un elenco dei campi della tabella pivot.   
    Nell'elenco dei campi fare clic sulla scheda **Tutti**  
  
15. Aggiungere campi nelle aree relative alle righe, alle colonne e ai valori nell'elenco dei campi.  
  
16. Aggiungere un filtro dei dati o un filtro nella tabella pivot. **Non ignorare questo passaggio**. Tramite il filtro dei dati o il filtro sarà possibile verificare l'installazione di Analysis Services.  
  
17. Salvare la cartella di lavoro in una raccolta documenti in un server SharePoint 2013 in cui è configurato Excel Services. La cartella di lavoro può anche essere salvata in una condivisione di file e, successivamente, caricata nella raccolta documenti del server SharePoint 2013.  
  
18. Fare clic sul nome della cartella di lavoro per visualizzarla in SharePoint, quindi fare clic sul filtro dei dati o modificare il filtro aggiunto in precedenza. Se si verifica un aggiornamento dei dati, significa che Analysis Services è installato e disponibile per Excel Services. Se si apre la cartella di lavoro in Excel, si utilizzerà una copia memorizzata nella cache e non il server Analysis Services.  
  
##  <a name="configure-the-windows-firewall-to-allow-analysis-services-access"></a><a name="bkmk_firewall"></a>Configurare la Windows Firewall per consentire l'accesso Analysis Services  
 Le informazioni fornite nell'argomento [Configure the Windows Firewall to Allow Analysis Services Access](../configure-the-windows-firewall-to-allow-analysis-services-access.md) consentono di stabilire se è necessario sbloccare le porte di un firewall per consentire l'accesso ad Analysis Services o PowerPivot per SharePoint. Le procedure descritte nell'argomento consentono di configurare le impostazioni delle porte e del firewall. Eseguire i passaggi indicati per consentire l'accesso al server Analysis Services.  
  
##  <a name="upgrade-workbooks-and-scheduled-data-refresh"></a><a name="bkmk_upgrade_workbook"></a>Aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato  
 I passaggi necessari per aggiornare le cartelle di lavoro create in versioni precedenti di PowerPivot dipendono dalla versione di PowerPivot tramite cui è stata creata la cartella di lavoro. Per altre informazioni, vedere [Aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013).  
  
##  <a name="beyond-the-single-server-installation--powerpivot-for-microsoft-sharepoint"></a><a name="bkmk_multiple_servers"></a>Oltre l'installazione a server singolo-PowerPivot per Microsoft SharePoint  
 **Front-end Web (WFE)** o **livello intermedio:**: per utilizzare un server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità SharePoint in una farm di SharePoint di grandi dimensioni e per installare le funzionalità aggiuntive di PowerPivot nella farm, eseguire il pacchetto di installazione **spPowerPivot.msi** in ogni server SharePoint. Tramite spPowerPivot.msi vengono installati i provider di dati necessari e lo strumento di configurazione di PowerPivot per SharePoint 2013.  
  
 Per ulteriori informazioni sull'installazione e sulla configurazione del livello intermedio, vedere gli argomenti seguenti:  
  
-   [Installare o disinstallare il componente aggiuntivo PowerPivot per SharePoint &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)  
  
-   Per scaricare il file con estensione msi, vedere [Microsoft SQL Server 2014 PowerPivot per Microsoft SharePoint 2013](https://go.microsoft.com/fwlink/?LinkID=324854).  
  
-   [Configurare PowerPivot e distribuire soluzioni &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013)  
  
 **Ridondanza e carico del server:** l'installazione di un secondo server o di più server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità SharePoint fornirà una ridondanza delle funzionalità del server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Tramite i server aggiuntivi, inoltre, verrà esteso il carico tra i server. Per altre informazioni, vedere gli argomenti seguenti:  
  
-   [Configurare Analysis Services per l'elaborazione di modelli di dati in Excel Services](https://technet.microsoft.com/library/jj614437\(v=office.15\)) ( https://technet.microsoft.com/library/jj614437(v=office.15)) .  
  
-   [Gestire le impostazioni del modello di dati di Excel Services (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780\(v=office.15\)) ( https://technet.microsoft.com/library/jj219780(v=office.15)) .  
  
 ![Le impostazioni di SharePoint](https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "Impostazioni di SharePoint") [inviano commenti e suggerimenti e informazioni di contatto tramite Microsoft SQL Server Connetti](https://connect.microsoft.com/SQLServer/Feedback) ( https://connect.microsoft.com/SQLServer/Feedback) .  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire la migrazione di PowerPivot a SharePoint 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013)   
 [Installare o disinstallare il componente aggiuntivo PowerPivot per SharePoint &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)   
 [Aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013)  
  
  
