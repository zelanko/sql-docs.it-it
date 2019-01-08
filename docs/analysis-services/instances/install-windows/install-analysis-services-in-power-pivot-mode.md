---
title: Installare Analysis Services in modalità Power Pivot | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e3e973c30ea178a544b9da3501d88f43cf9b1ddb
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52527746"
---
# <a name="install-analysis-services-in-power-pivot-mode"></a>Installazione di Analisi Services in modalità Power Pivot
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Nelle procedure contenute in questo argomento viene illustrata l'installazione di un unico server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per una distribuzione SharePoint. Nei passaggi è inclusa l'esecuzione dell'Installazione guidata di SQL Server, nonché di attività di configurazione in cui viene utilizzata Amministrazione centrale SharePoint.  
  
##  <a name="bkmk_background"></a> Background  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint è una raccolta di servizi di livello intermedio e di back-end che fornisce accesso ai dati [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in una farm di SharePoint 2016 o SharePoint 2013.  
  
-   **Servizi back-end:** Se si usa [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per Excel per creare cartelle di lavoro contenenti dati analitici, è necessario disporre [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint per accedere ai dati in un ambiente server. Il programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] può essere eseguito su un computer in cui è installato SharePoint Server oppure su un computer diverso in cui non è disponibile il software SharePoint. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] non è presente alcuna dipendenza da SharePoint.  
  
     **Nota:** in questo argomento vengono descritti l'installazione del server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e i servizi back-end.  
  
-   **Livello intermedio:** Miglioramenti per la [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] esperienze disponibili in SharePoint, tra cui [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Gallery, pianificazione dell'aggiornamento dati, dashboard di gestione e i provider di dati. Per ulteriori informazioni sull'installazione e sulla configurazione del livello intermedio, vedere gli argomenti seguenti:  
  
    -   [Installare o disinstallare il componente aggiuntivo PowerPivot per SharePoint (SharePoint 2016)](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016.md)  
  
    -   [Installare o disinstallare il componente aggiuntivo PowerPivot per SharePoint &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
    -   [Configurare PowerPivot e distribuire soluzioni &#40;SharePoint 2016&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2016.md)  
  
    -   [Configurare PowerPivot e distribuire soluzioni &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)  
  
##  <a name="bkmk_prereq"></a> Prerequisiti  
  
1.  Per eseguire il programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , è necessario essere un amministratore locale.  
  
2.  SharePoint Server edizione Enterprise è richiesto per [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint. È anche possibile usare l'edizione Enterprise di valutazione.  
  
3.  Il computer deve essere associato a un dominio nella stessa foresta di Active Directory di Office Online Server (SharePoint 2016) o Excel Services (SharePoint 2013).  
  
4.  È necessario disporre del nome di istanza di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Nel computer su cui si sta installando Analysis Services in modalità [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]non deve essere presente un'istanza denominata di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] esistente.  
  
     **Nota:** Il nome dell'istanza deve essere POWERPIVOT.  
  
5.  Esaminare [Requisiti hardware e software per il server Analysis Services in modalità SharePoint](http://msdn.microsoft.com/library/fb86ca0a-518c-4c61-ae78-7680c57fae1f).  
  
6.  Esaminare le note sulla versione alla pagina [SQL Server 2016 Release Notes](../../../sql-server/sql-server-2016-release-notes.md).  
  
###  <a name="bkmk_sqleditions"></a> Requisiti relativi all'edizione di SQL Server  
 Non tutte le funzionalità di Business Intelligence sono disponibili in ogni edizione di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Per informazioni dettagliate, vedere [funzionalità Analysis Services supportate dalle edizioni di SQL Server 2016](../../../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md) e [edizioni e componenti di SQL Server 2016](../../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
##  <a name="InstallSQL"></a> Passaggio 1: Installare Power Pivot per SharePoint  
 In questo passaggio è possibile eseguire il programma di installazione di SQL Server per installare un server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . In un passaggio successivo è possibile configurare l'utilizzo da parte di Excel Services di questo server per i modelli di dati della cartella di lavoro.  
  
1.  Eseguire l'Installazione guidata di SQL Server (Setup.exe).  
  
2.  Selezionare **Installazione** nel pannello di navigazione sinistro.  
  
3.  Selezionare **Nuova installazione autonoma di SQL Server o aggiunta di funzionalità a un'installazione esistente**.  
  
4.  Se viene visualizzata la pagina **Codice Product Key** specificare la versione di valutazione o immettere un codice Product Key per una copia concessa in licenza dell'edizione Enterprise. Fare clic su **Avanti**. Per ulteriori informazioni sulle versioni, vedere [Editions and Components of SQL Server 2016](../../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
5.  Leggere e accettare le condizioni di licenza software Microsoft, quindi fare clic su **Avanti**.  
  
6.  Se viene visualizzata la pagina **Regole globali** , esaminare eventuali informazioni relative alle regole visualizzate nell'installazione guidata.  
  
7.  Nella pagina **Microsoft Update** si consiglia di usare Microsoft Update per verificare la disponibilità degli aggiornamenti, quindi fare clic su **Avanti**.  
  
8.  La pagina **Installazione dei file di installazione** viene eseguita per diversi minuti. Esaminare eventuali avvisi sulle regole o regole con esito negativo, quindi fare clic su **Avanti**.  
  
9. Se viene nuovamente visualizzato **Regole di supporto per l'installazione**, verificare tutti gli avvisi e fare clic su **Avanti**.  
  
     **Nota:** poiché Windows Firewall è abilitato, viene visualizzato un avviso in cui è richiesto di aprire le porte per abilitare l'accesso remoto.  
  
10. Nella pagina **Impostazione ruolo** selezionare **Installazione funzionalità SQL Server**.  
  
     Selezionare **Avanti**.  
  
11. Nella pagina Selezione funzionalità scegliere **Analysis Services**. Questa opzione consente di installare una delle tre modalità [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Selezionare la modalità in un passaggio successivo. Selezionare **Avanti**.  
  
12. Nella pagina **Configurazione dell'istanza** selezionare **Istanza denominata** e digitare **POWERPIVOT** per il nome dell'istanza, quindi fare clic su **Avanti**.  
  
     ![Installazione di SQL - configurazione dell'istanza di pagina di destinazione](../../../analysis-services/instances/install-windows/media/sql2016-pp-instance-config-landing-page.png "installazione di SQL - configurazione dell'istanza di pagina di destinazione")  
  
13. Nella pagina **Configurazione server** configurare tutti i servizi per **Tipo di avvio**automatico. Specificare l'account di dominio e la password desiderati per **SQL Server Analysis Services**, **(1)** nel diagramma seguente.  
  
    -   Per [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]è possibile utilizzare un account **utente di dominio** o un account **NetworkService** . Non utilizzare gli account LocalService o LocalSystem.  
  
    -   Se si aggiungono il Motore di database di SQL Server e SQL Server Agent, è possibile configurare i servizi da eseguire in account utente di dominio o in account virtuali predefiniti.  
  
    -   Non eseguire mai il provisioning degli account di servizio con il proprio account utente di dominio. Con questa operazione si concedono al server le stesse autorizzazioni di cui l'utente dispone per le risorse disponibili nella rete. Se un utente malintenzionato compromette il server, l'utente in questione viene connesso con le proprie credenziali di dominio, pertanto, potrà scaricare o utilizzare gli stessi dati e le stesse applicazioni.  
  
     Selezionare **Avanti**.  
  
     ![Installazione di SQL - pagina di destinazione Server Configuration](../../../analysis-services/instances/install-windows/media/sql2016-pp-server-config-landing-page.png "SQL installazione - pagina di configurazione del Server")  
  
14. Se si sta installando il [!INCLUDE[ssDE](../../../includes/ssde-md.md)], viene visualizzata la pagina **Configurazione del motore di database** . In Configurazione del [!INCLUDE[ssDE](../../../includes/ssde-md.md)] selezionare **Aggiungi utente corrente** per concedere le autorizzazioni di amministratore dell'account utente per l'istanza del motore di database.  
  
     Selezionare **Avanti**.  
  
15. Nella pagina **Configurazione di Analysis Services** selezionare **Modalità PowerPivot** in **Modalità Server**.  
  
     ![Installazione di SQL - configurazione di Analysis Services Landing Page](../../../analysis-services/instances/install-windows/media/sql2016-pp-as-config-landing-page.png "SQL installazione - pagina di destinazione di configurazione di Analysis Services")  
  
16. Nella pagina **Configurazione di Analysis Services** selezionare **Aggiungi utente corrente** per concedere le autorizzazioni amministrative dell'account utente. Saranno necessarie autorizzazioni amministrative per configurare il server dopo che è stata completata l'installazione.  
  
    -   Nella stessa pagina, aggiungere l'account utente di Windows di qualsiasi altra persona che richiede autorizzazioni amministrative. Ad esempio, qualsiasi utente che desidera connettersi all'istanza del [!INCLUDE[ssGeminiSrv](../../../includes/ssgeminisrv-md.md)] in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] per risolvere problemi di connessione al database deve disporre di autorizzazioni di amministratore di sistema. Aggiungere l'account utente di qualsiasi persona che potrebbe avere la necessità di risolvere problemi o amministrare il server.  
  
    -   > [!NOTE]  
        >  A tutte le applicazioni del servizio per cui è richiesto l'accesso all'istanza del server Analysis Services devono essere associate autorizzazioni amministrative di Analysis Services. Ad esempio, aggiungere gli account di servizio per Excel Services, Power View e Performance Point Services. Inoltre, aggiungere l'account della farm di SharePoint che viene utilizzato come identità dell'applicazione Web in cui è ospitata Amministrazione centrale.  
  
     Selezionare **Avanti**.  
  
17. Nella pagina **Segnalazione errori** fare clic su **Avanti**.  
  
18. Nella pagina **Inizio installazione** fare clic su **Installa**.  
  
19. Se viene visualizzata la finestra di dialogo **Richiesto riavvio del computer**, selezionare **OK**.  
  
20. Al termine dell'installazione fare clic su **Chiudi**.  
  
21. Riavviare il computer.  
  
22. Se nell'ambiente è disponibile un firewall, vedere l'argomento della documentazione online di SQL Server [Configure the Windows Firewall to Allow Analysis Services Access](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
### <a name="verify-the-sql-server-installation"></a>Verificare l'installazione di SQL Server  
 Verificare che il servizio Analysis Services sia in esecuzione.  
  
1.  In Microsoft Windows fare clic su **Start**, **Tutti i programmi**, quindi selezionare il gruppo **Microsoft SQL Server 2016** .  
  
2.  Selezionare **SQL Server Management Studio**.  
  
3.  Connettersi all'istanza di Analysis Services, ad esempio **[nome server]\POWERPIVOT**. Se è possibile connettersi all'istanza, significa che il servizio è in esecuzione.  
  
##  <a name="bkmk_config"></a> Passaggio 2: Configurare l'integrazione SharePoint per Analysis Services di base  
 Nei passaggi seguenti vengono descritte le modifiche di configurazione necessarie per interagire con i modelli di dati avanzati di Excel all'interno di una raccolta documenti di SharePoint. Completare questi passaggi dopo l'installazione di SharePoint e SQL Server Analysis Services.  
  
### <a name="sharepoint-2016"></a>SharePoint 2016  
 Excel Services è stato rimosso da SharePoint 2016. Per l'hosting di Excel viene invece usato Office Online Server.  
  
#### <a name="grant-office-online-server-machine-account-administration-rights-on-analysis-services"></a>Concedere i diritti di amministrazione su Analysis Services all'account del computer Office Online Server  
 Non è necessario completare questa sezione se durante l'installazione di Analysis Services è stato aggiunto l'account del computer Office Online Server come amministratore di Analysis Services.  
  
1.  Nel server Analysis Services avviare SQL Server Management Studio e connettersi all'istanza di Analysis Services, ad esempio `[MyServer]\POWERPIVOT`.  
  
2.  In Esplora oggetti fare clic con il pulsante destro del mouse sul nome dell'istanza e selezionare **Proprietà**.  
  
     ![Visualizzare le proprietà di un server SSAS](../../../analysis-services/instances/install-windows/media/as-ssms-proeprties.gif "visualizzare le proprietà di un server SSAS")  
  
3.  Nel riquadro sinistro selezionare **Sicurezza**. Aggiungere l'account del computer su cui è installato Office Online Server.  
  
     ![Impostazioni di sicurezza di un Server SSAS](../../../analysis-services/instances/install-windows/media/as-ssms-security.gif "impostazioni di sicurezza di un Server SSAS")  
  
#### <a name="register-analysis-services-server-with-office-online-server"></a>Registrare il server Analysis Services all'Office Server Online  
 Sarà necessario eseguire questi passaggi sull'Office Online Server.  
  
-   Aprire una finestra di comando di PowerShell come amministratore.  
  
-   Caricare il modulo `OfficeWebApps` di PowerShell.  
  
     `Import-Module OfficeWebApps`  
  
-   Aggiungere il server Analysis Services, ad esempio `[MyServer]\POWERPIVOT`.  
  
     `New-OfficeWebAppsExcelBIServer -ServerId [MyServer]\POWERPIVOT]`  
  
### <a name="sharepoint-2013"></a>SharePoint 2013  
  
#### <a name="grant-excel-services-server-administration-rights-on-analysis-services"></a>Garantire i diritti di amministrazione del server Excel Services per Analysis Services  
 Non è necessario completare questa sezione se durante l'installazione di Analysis Services è stato aggiunto l'account di servizio dell'applicazione Excel Services come amministratore di Analysis Services.  
  
1.  Nel server Analysis Services avviare SQL Server Management Studio e connettersi all'istanza di Analysis Services, ad esempio `[MyServer]\POWERPIVOT`.  
  
2.  In Esplora oggetti fare clic con il pulsante destro del mouse sul nome dell'istanza e selezionare **Proprietà**.  
  
     ![Visualizzare le proprietà di un server SSAS](../../../analysis-services/instances/install-windows/media/as-ssms-proeprties.gif "visualizzare le proprietà di un server SSAS")  
  
3.  Nel riquadro sinistro selezionare **Sicurezza**. Aggiungere l'account di accesso del dominio configurato per l'applicazione Excel Services nel passaggio 1.  
  
     ![Impostazioni di sicurezza di un Server SSAS](../../../analysis-services/instances/install-windows/media/as-ssms-security.gif "impostazioni di sicurezza di un Server SSAS")  
  
#### <a name="configure-excel-services-for-analysis-services-integration"></a>Configurare Excel Services per l'integrazione di Analysis Services  
  
1.  Nel gruppo Gestione applicazioni di Amministrazione centrale SharePoint fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Fare clic sul nome dell'applicazione di servizio. Il nome predefinito è **Applicazione Excel Services**.  
  
3.  Nella pagina **Gestione applicazione Excel Services**fare clic su **Impostazioni modello di dati**.  
  
4.  Fare clic su **Aggiungi server**.  
  
5.  In **Nome del server**digitare il nome del server Analysis Services e il nome dell'istanza di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Ad esempio `MyServer\POWERPIVOT`. Il nome dell'istanza di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] è obbligatorio.  
  
     Digitare una descrizione.  
  
6.  Scegliere **OK**.  
  
7.  Le modifiche verranno applicate in pochi minuti oppure è possibile scegliere le opzioni **Arresta** e **Avvia** il servizio **Servizi di calcolo Excel**. Per  
  
     È anche possibile aprire un prompt dei comandi con privilegi amministrativi e digitare `iisreset /noforce`.  
  
     È possibile verificare se il server è riconosciuto da Excel Services controllando le voci nel log ULS. Saranno visualizzate voci simili alle seguenti:  
  
    ```  
    Excel Services Application            Data Model        27           Medium                Check Administrator Access ([ServerName]\POWERPIVOT): Pass.        f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Server Version ([ServerName]\POWERPIVOT): Pass (11.0.2809.24 >= 11.0.2800.0).         f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Deployment Mode ([ServerName]\POWERPIVOT): Pass.            f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
  
    ```  
  
##  <a name="bkmk_verify"></a> Passaggio 3: Verificare l'integrazione  
 Nei passaggi seguenti vengono illustrati la creazione e il caricamento di una nuova cartella di lavoro per verificare l'integrazione di Analysis Services. È necessario disporre di un database di SQL Server per completare i passaggi.  
  
1.  **Nota:** se è già disponibile una cartella di lavoro avanzata con filtri dei dati o filtri, è possibile caricarla nella raccolta documenti di SharePoint e verificare l'eventuale possibilità di interagire con questi elementi dalla visualizzazione raccolta documenti.  
  
2.  Avviare una nuova cartella di lavoro in Excel  
  
3.  Nella scheda Dati selezionare **Da altre origini** nella barra multifunzione in **Carica dati esterni**.  
  
4.  Selezionare **Da SQL Server**.  
  
5.  In **Connessione guidata dati**immettere il nome dell'istanza di SQL Server in cui è presente il database che si desidera utilizzare.  
  
6.  In alternativa, in Credenziali di accesso verificare che **Usa autenticazione di Windows** sia selezionata, quindi fare clic su **Avanti**.  
  
7.  Selezionare il database che si desidera utilizzare.  
  
8.  Verificare che la casella di controllo **Connetti a una tabella specifica** sia selezionata.  
  
9. Selezionare la casella di controllo **Abilita selezione di più tabelle e aggiungi tabelle nel modello di dati di Excel** .  
  
10. Selezionare le tabelle che si desidera importare.  
  
11. Selezionare la casella di controllo **Importa relazioni tra le tabelle selezionate**, quindi fare clic su **Avanti**. Importando più tabelle da un database relazionale è possibile utilizzare tabelle già correlate. I passaggi vengono salvati poiché non è necessario compilare manualmente le relazioni.  
  
12. Nella pagina **Salva file di connessione dati e chiudi** della procedura guidata digitare un nome per la connessione e selezionare **Fine**.  
  
13. Verrà visualizzata la finestra di dialogo **Importa dati** . Scegliere **Rapporto di tabella pivot**, quindi selezionare **OK**.  
  
14. Nella cartella di lavoro viene visualizzato un elenco dei campi della tabella pivot.   
    Nell'elenco dei campi selezionare la scheda **Tutti**  
  
15. Aggiungere campi nelle aree relative alle righe, alle colonne e ai valori nell'elenco dei campi.  
  
16. Aggiungere un filtro dei dati o un filtro nella tabella pivot. **Non ignorare questo passaggio**. Tramite il filtro dei dati o il filtro sarà possibile verificare l'installazione di Analysis Services.  
  
17. Salvare la cartella di lavoro in una raccolta documenti nella farm di SharePoint personale. La cartella di lavoro può anche essere salvata in una condivisione di file e, successivamente, caricata nella raccolta documenti di SharePoint.  
  
18. Selezionare il nome della cartella di lavoro per visualizzarla in Excel Online, quindi fare clic sul filtro dei dati o modificare il filtro aggiunto in precedenza. Se si verifica un aggiornamento dei dati, significa che Analysis Services è installato e disponibile per Excel. Se si apre la cartella di lavoro in Excel, si utilizzerà una copia memorizzata nella cache e non il server Analysis Services.  
  
##  <a name="bkmk_firewall"></a> Configurare Windows Firewall per consentire l'accesso ad Analysis Services  
 Le informazioni fornite nell'argomento [Configurare Windows Firewall per consentire l'accesso ad Analysis Services](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) consentono di stabilire se è necessario sbloccare le porte di un firewall per consentire l'accesso ad Analysis Services o a [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint. Le procedure descritte nell'argomento consentono di configurare le impostazioni delle porte e del firewall. Eseguire i passaggi indicati per consentire l'accesso al server Analysis Services.  
  
##  <a name="bkmk_upgrade_workbook"></a> Aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato  
 I passaggi necessari per aggiornare le cartelle di lavoro create in versioni precedenti di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] dipendono dalla versione di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] tramite cui è stata creata la cartella di lavoro. Per altre informazioni, vedere [Aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
##  <a name="bkmk_multiple_servers"></a> Oltre l'installazione a Server singolo - Power Pivot per Microsoft SharePoint  
 **Web front-end (WFE)** oppure **livello intermedio:**: Usare un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] server in modalità SharePoint in una farm di SharePoint di grandi dimensioni e per installare ulteriori [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] funzionalità nella farm, eseguire il pacchetto di installazione **spPowerPivot16.msi (SharePoint 2016), o sppowerpivot. msi (SharePoint 2013),** in ogni server SharePoint. Tramite spPowerPivot16.msi, o spPowerPivot.msi, vengono installati i provider di dati necessari e lo strumento di configurazione di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2016 o 2013.  
  
 Per ulteriori informazioni sull'installazione e sulla configurazione del livello intermedio, vedere gli argomenti seguenti:  
  
-   [Installare o disinstallare il componente aggiuntivo PowerPivot per SharePoint &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
-   [Installare o disinstallare il componente aggiuntivo PowerPivot per SharePoint &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
-   Per scaricare il file con estensione msi, vedere [Microsoft SQL Server 2016 Power Pivot per Microsoft SharePoint 2016](http://go.microsoft.com/fwlink/?LinkID=324854)  
  
-   [Configurare PowerPivot e distribuire soluzioni &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)  
  
 **Ridondanza e carico del server:** Installando un secondo o più [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] i server [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] modalità fornirà una ridondanza del [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] funzionalità del server. Tramite i server aggiuntivi, inoltre, verrà esteso il carico tra i server. Per ulteriori informazioni, vedere quanto segue:  
  
-   [Configurare Analysis Services per elaborare i modelli di dati in Excel Services (SharePoint 2013)](http://technet.microsoft.com/library/jj614437(v=office.15)).  
  
-   [Gestire impostazioni modello di dati di Excel Services (SharePoint 2013)](http://technet.microsoft.com/library/jj219780(v=office.15)).  
  
 ![Impostazioni di SharePoint](../../../analysis-services/media/as-sharepoint2013-settings-gear.gif "impostazioni SharePoint") [Invia commenti e suggerimenti e informazioni di contatto tramite SQL Server Feedback](https://feedback.azure.com/forums/908035-sql-server).  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire la migrazione di PowerPivot a SharePoint 2013](../../../analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013.md)   
 [Installare o disinstallare il componente aggiuntivo PowerPivot per SharePoint &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)   
 [Aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
  
