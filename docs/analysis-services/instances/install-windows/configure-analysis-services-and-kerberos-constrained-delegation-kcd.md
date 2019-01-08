---
title: Configurare Analysis Services la delega vincolata Kerberos (KCD) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cc8c2ee84c8210adc3a52d81deff5edf6d3f542f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52811153"
---
# <a name="configure-analysis-services-and-kerberos-constrained-delegation-kcd"></a>Configurare Analysis Services per la delega vincolata Kerberos
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  La delega vincolata Kerberos è un protocollo di autenticazione che è possibile configurare con l'autenticazione di Windows per delegare le credenziali client da servizio a servizio in tutto l'ambiente. La delega vincolata Kerberos richiede un'infrastruttura aggiuntiva, ad esempio un controller di dominio, e un'ulteriore configurazione dell'ambiente. La delega vincolata Kerberos è un requisito in alcuni scenari che coinvolgono dati di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in SharePoint 2016. In SharePoint 2016 Excel Services si trova all'esterno della farm di SharePoint, in un nuovo server separato, **Office Online Server**. Visto che Office Online Server è un server separato, è ancora più importante trovare una soluzione per delegare le credenziali client negli scenari tipici a due hop.  
  
## <a name="overview"></a>Panoramica  
 La delega vincolata Kerberos consente a un account di rappresentare un altro account allo scopo di fornire accesso alle risorse. L'account rappresentante sarebbe un account di servizio assegnato a un'applicazione Web o l'account computer di un server Web, mentre l'account che viene rappresentato sarebbe un account utente che richiede l'accesso alle risorse. La delega vincolata Kerberos opera a livello di servizio, affinché l'account rappresentante possa consentire l'accesso a determinati servizi in un server, negandolo ad altri servizi nello stesso server o in altri server.  
  
 Le sezioni in questo argomento illustrano scenari comuni in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in cui è richiesta la delega vincolata Kerberos. È anche illustrata una distribuzione server di esempio con un riepilogo generale di ciò che è necessario installare e configurare. Nella sezione [Altre informazioni e contenuto della community](#bkmk_moreinfo) sono disponibili collegamenti a informazioni più dettagliate sulle tecnologie coinvolte, ad esempio i controller di dominio e la delega vincolata Kerberos.  
  
## <a name="scenario-1-workbook-as-data-source-wds"></a>Scenario 1: Cartella di lavoro come origine dati (WDS).  
 ![vedere 1](../../../analysis-services/instances/install-windows/media/ssas-callout1.png "vedere 1") Office Online Server apre una cartella di lavoro di Excel e ![vedere 2](../../../analysis-services/instances/install-windows/media/ssas-callout2.png "vedere 2") rileva una connessione dati a un'altra cartella di lavoro. Office Online Server invia una richiesta per il [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] servizio Redirector ![vedere 3](../../../analysis-services/instances/install-windows/media/ssas-callout3.png "vedere 3") per aprire la seconda cartella di lavoro e i dati ![vedere 4](../../../analysis-services/instances/install-windows/media/ssas-callout4.png "vedere 4 ").  
  
 In questo scenario le credenziali utente devono essere delegate da Office Online Server al servizio Redirector di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in SharePoint.  
  
 ![cartella di lavoro come origine dati](../../../analysis-services/instances/install-windows/media/ssas-kcd-wtih-wds.png "della cartella di lavoro come origine dati")  
  
## <a name="scenario-2-an-analysis-services-tabular-model-links-to-an-excel-workbook"></a>Scenario 2: Un modello tabulare di Analysis Services è collegato a una cartella di lavoro di Excel  
 Un modello tabulare di Analysis Services ![vedere 1](../../../analysis-services/instances/install-windows/media/ssas-callout1.png "vedere 1") collegamenti a una cartella di lavoro di Excel che contiene un modello Power Pivot. In questo scenario, quando [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] carica il modello tabulare, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] rileva il collegamento alla cartella di lavoro. Durante l'elaborazione del modello, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] invia una richiesta di query a SharePoint per caricare la cartella di lavoro. In questo scenario **non** è necessaria la delega delle credenziali client da Analysis Services a SharePoint, ma un'applicazione client può sovrascrivere le informazioni dell'origine dati in un'associazione out-of-line. Se la richiesta di associazione out-of-line specifica la rappresentazione dell'utente corrente, è necessario delegare le credenziali utente. A questo scopo deve essere configurata la delega vincolata Kerberos tra [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e SharePoint.  
  
 ![office online server](../../../analysis-services/instances/install-windows/media/ssas-kcd-wtih-oos.png "office online server")  
  
## <a name="example-deployment-of-kcd-with-office-online-server-and-analysis-services"></a>Esempio di distribuzione della delega vincolata Kerberos con Office Online Server e Analysis Services  
 Questa sezione descrive un esempio di distribuzione che usa quattro computer. Nelle sezioni seguenti sono riepilogati i passaggi di installazione e configurazione principali per ogni computer. Prima di iniziare le distribuzioni, è consigliabile che nei computer siano state applicate le patch più recenti per il sistema operativo ed è opportuno conoscere i nomi dei computer perché sono necessari in alcuni passaggi di configurazione.  
  
-   Controller di dominio  
  
-   Motore di database di SQL Server e Analysis Services in modalità Power Pivot. L'istanza del motore di database verrà usata per i database del contenuto di SharePoint.  
  
-   SharePoint server 2016  
  
-   Office Online Server  
  
 ![domain controller](../../../analysis-services/instances/install-windows/media/ssas-kcd-domainserver-icon.png "domain controller")  
  
### <a name="domain-controller"></a>Controller di dominio  
 Di seguito è riportato un riepilogo di ciò che occorre installare per il controller di dominio.  
  
-   **Ruolo:** Servizi di dominio Active Directory. Per una panoramica, vedere [Configuring Active Directory (AD DS) in Windows Server 2012](http://sharepointgeorge.com/2012/configuring-active-directory-ad-ds-in-windows-server-2012/)(Configurazione di Active Directory (AD DS) in Windows Server 2012).  
  
-   **Ruolo:** Server DNS  
  
-   **Funzionalità:** funzionalità di .NET Framework 3.5/.NET Framework 3.5  
  
-   **Funzionalità:** Strumenti di amministrazione remota del Server / strumenti di amministrazione ruoli  
  
-   Configurare Active Directory per creare una nuova foresta e aggiungere i computer al dominio. Prima di tentare di aggiungere altri computer al dominio privato, è necessario configurare i DNS dei computer client sull'indirizzo IP del controller di dominio. Nel computer controller di dominio eseguire `ipconfig /all` per ottenere gli indirizzi IPv4 e IPv6 per il passaggio successivo.  
  
-   È consigliabile configurare indirizzi sia IPv4 che IPv6. A questo scopo si può usare il Pannello di controllo di Windows:  
  
    1.  Fare clic su **Centro connessioni di rete e condivisione**  
  
    2.  Fare clic sulla connessione Ethernet  
  
    3.  Fare clic su **Proprietà**  
  
    4.  Fare clic su **Protocollo Internet versione 6 (TCP/IPv6)**  
  
    5.  Fare clic su **Proprietà**  
  
    6.  Fare clic su **Utilizza i seguenti indirizzi server DNS**  
  
    7.  Digitare l'indirizzo IP dal comando ipconfig.  
  
    8.  Fare clic sul pulsante **Avanzate** , selezionare la scheda **DNS** e verificare che i suffissi DNS siano corretti.  
  
    9. Fare clic su **Aggiungi questi suffissi DNS**.  
  
    10. Ripetere la procedura per IPv4.  
  
-   **Nota:** è possibile aggiungere computer al dominio dal Pannello di controllo di Windows, in Impostazioni di sistema. Per altre informazioni, vedere [How To Join Windows Server 2012 to a Domain](http://social.technet.microsoft.com/wiki/contents/articles/20260.how-to-join-windows-server-2012-to-a-domain.aspx)(Come aggiungere Windows Server 2012 a un dominio).  
  
 ![server in modalità powerpivot di SSAS](../../../analysis-services/instances/install-windows/media/ssas-kcd-powerpivotserver-icon.png "server ssas in modalità powerpivot")  
  
### <a name="2016-sql-server-database-engine-and-analysis-services-in-power-pivot-mode"></a>Motore di database di SQL Server 2016 e Analysis Services in modalità Power Pivot.  
 Di seguito è riportato un riepilogo di ciò che occorre installare nel computer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 ![Nota](../../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "nota") nel [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Nell'Installazione guidata [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in Power Pivot modalità viene installata come parte del flusso di lavoro selezione funzionalità.  
  
1.  Eseguire l'Installazione guidata di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] e quindi nella pagina Selezione funzionalità fare clic sul motore di database, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]e sugli strumenti di gestione. In una configurazione successiva dell'Installazione guidata è possibile specificare la modalità [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
2.  Per la configurazione dell'istanza, configurare un'istanza denominata di "POWERPIVOT".  
  
3.  Nella pagina Configurazione di Analysis Services configurare il server Analysis Services per la modalità **PowerPivot** e aggiungere il **nome computer** di Office Online Server all'elenco di amministratori del server Analysis Services. Per altre informazioni, vedere [Install Analysis Services in Power Pivot Mode](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
4.  Si noti che, per impostazione predefinita il tipo di oggetto "Computer" non sono incluso nella ricerca. Fare clic su ![fare clic su oggetti per aggiungere account computer](../../../analysis-services/instances/install-windows/media/ss-objects-button.png "fare clic su oggetti per aggiungere account computer") per aggiungere l'oggetto computer.  
  
     ![aggiungere account computer come amministratori ssas](../../../analysis-services/instances/media/ssas-in-ssms-computerobjects.png "aggiungere account computer come amministratori ssas")  
  
5.  Creare i nomi dell'entità servizio (SPN) per l'istanza di Analysis Services.  
  
     Ecco alcuni comandi SPN utili:  
  
    -   Elencare il nome SPN per un nome account specifico che esegue il servizio di interesse: `SetSPN -l <account-name>`  
  
    -   Impostare un nome SPN per un nome account che esegue il servizio di interesse: `SetSPN -a <SPN> <account-name>`  
  
    -   Eliminare un nome SPN da un nome account specifico che esegue il servizio di interesse: `SetSPN -D <SPN> <account-name>`  
  
    -   Cercare nomi SPN duplicati: `SetSPN -X`  
  
     Il nome SPN per l'istanza di PowerPivot sarà nel formato:  
  
    ```  
    MSSQLSvc.3/\<Fully Qualified Domain Name (FQDN)>:POWERPIVOT  
    MSSQLSvc.3/<NetBIOS Name>:POWERPIVOT  
    ```  
  
     Dove il nome di dominio completo e i nomi NetBIOS corrispondono al nome del computer in cui risiede l'istanza. Questi nomi SPN verranno posizionati nell'account di dominio usato per l'account del servizio.  Se si usa Servizio di rete, Sistema locale o ID servizio, è opportuno inserire il nome SPN nell'account computer di dominio.  Se si usa un account utente di dominio, inserire il nome SPN in tale account.  
  
6.  Creare il nome SPN per il servizio SQL Browser nel computer di Analysis Services.  
  
     [Scopri di più](https://support.microsoft.com/en-us/kb/950599)  
  
7.  **Configurare le impostazioni della delega vincolata** nell'account del servizio Analysis Services per qualsiasi origine esterna da cui si eseguirà l'aggiornamento, ad esempio SQL Server o file di Excel. Nell'account del servizio Analysis Services, è necessario assicurarsi che sia impostato quanto segue.  
  
     **Nota:** Se non è possibile visualizzare la scheda delega per l'account, all'interno di Active Directory Users and Computers, è che non esiste alcun nome SPN nell'account.  È possibile aggiungere un nome SPN fittizio per far sì che venga visualizzato come `my/spn`.  
  
     **Utente attendibile per la delega solo ai servizi specificati** e **Utilizza un qualsiasi protocollo di autenticazione**.  
  
     Questa operazione è detta delega vincolata ed è necessaria perché il token di Windows avrà origine da Attestazioni per il servizio token Windows (C2WTS) che richiede la delega vincolata con transizione di protocollo.  
  
     ![Analysis Services - la delega vincolata](../../../analysis-services/instances/install-windows/media/analysis-services-constrained-delegation.png "Analysis Services - la delega vincolata")  
  
     Occorrerà anche aggiungere i servizi a cui si delegherà. Questo aspetto varia in base all'ambiente.  
  
### <a name="office-online-server"></a>Office Online Server  
  
1.  Installare Office Online Server  
  
2.  **Configurare Office Online Server** per la connessione al server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Si noti che l'account computer di Office Online Server deve essere un amministratore del server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Questa operazione è stata completata in una sezione precedente di questo argomento, con l'installazione del server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
    1.  In Office Online Server aprire una finestra di PowerShell con privilegi amministrativi ed eseguire il comando seguente  
  
    2.  `New-OfficeWebAppsExcelBIServer -ServerId <AS instance name>`  
  
    3.  Esempio: `New-OfficeWebAppsExcelBIServer -ServerId "MTGQLSERVER-13\POWERPIVOT"`  
  
3.  **Configurare Active Directory** per consentire all'account computer di Office Online Server di rappresentare gli utenti nell'account del servizio SharePoint. Quindi, impostare la proprietà di delega in dell'entità che esegue il Pool di applicazioni per i servizi Web SharePoint in Office Online Server: I comandi di PowerShell in questa sezione richiedono gli oggetti PowerShell di Active Directory (AD).  
  
    1.  Ottenere l'identità Active Directory di Office Online Server  
  
        ```  
        $computer1 = Get-ADComputer -Identity [ComputerName]  
        ```  
  
         il nome di questa entità si trova in Gestione attività/Dettagli/nome utente di w3wp.exe. Ad esempio "svcSharePoint"  
  
        ```  
        Set-ADUser svcSharePoint -PrincipalsAllowedToDelegateToAccount $computer1  
  
        ```  
  
    2.  Per verificare che la proprietà sia stata impostata correttamente  
  
    3.  ```  
        Get-ADUser svcSharePoint -Properties PrincipalsAllowedToDelegateToAccount  
        ```  
  
4.  **Configurare le impostazioni della delega vincolata** dell'account di Office Online Server sull'istanza di Analysis Services Power Pivot. Deve essere l'account del computer con cui viene eseguito Office Online Server. Nell'account di Office Online Server, è necessario assicurarsi che sia impostato quanto segue.  
  
     **Nota:** Se non è possibile visualizzare la scheda delega per l'account, all'interno di Active Directory Users and Computers, è che non esiste alcun nome SPN nell'account.  È possibile aggiungere un nome SPN fittizio per far sì che venga visualizzato come `my/spn`.  
  
     **Utente attendibile per la delega solo ai servizi specificati** e **Utilizza un qualsiasi protocollo di autenticazione**.  
  
     Questa operazione è detta delega vincolata ed è necessaria perché il token di Windows avrà origine da Attestazioni per il servizio token Windows (C2WTS) che richiede la delega vincolata con transizione di protocollo.  Sarà quindi necessario consentire la delega ai nomi SPN MSOLAPSvc.3 e MSOLAPDisco.3 creati in precedenza.  
  
5.  Configurare Attestazioni per il servizio token Windows (C2WTS) **Necessario per lo scenario 1**. Per altre informazioni, vedere [Cenni preliminari su Claims to Windows Token Service (c2WTS)](https://msdn.microsoft.com/library/ee517278.aspx).  
  
6.  **Configurare le impostazioni della delega vincolata** nell'account del servizio C2WTS.  Le impostazioni devono corrispondere a quanto configurato nel passaggio 4.  
  
 ![server di SharePoint](../../../analysis-services/instances/install-windows/media/ssas-kcd-sharepointserver-icon.png "sharepoint server")  
  
### <a name="sharepoint-server-2016"></a>SharePoint Server 2016  
 Di seguito è riportato un riepilogo dell'installazione di SharePoint Server.  
  
1.  Installare il programma di installazione dei prerequisiti di SharePoint  
  
2.  Eseguire l'installazione di SharePoint e selezionare l'impostazione ruolo **Single Server Farm** (Server farm singola).  
  
3.  Eseguire il componente aggiuntivo PowerPivot per SharePoint (spPowerPivot16.msi). Per altre informazioni, vedere [installare o disinstallare Power Pivot per SharePoint Add-in (SharePoint 2016)](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016.md)  
  
4.  Eseguire la Configurazione guidata PowerPivot. Vedere [Strumenti di configurazione di Power Pivot](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
5. Connettere SharePoint a Office Online Server. (Configure_xlwac_on_SPO.ps1)
  
6.  Configurare i provider di autenticazione SharePoint per Kerberos. **Necessario per lo scenario 1**. Per altre informazioni, vedere [Pianificare l'autenticazione Kerberos in SharePoint 2013](https://technet.microsoft.com/library/ee806870.aspx).  
  
##  <a name="bkmk_moreinfo"></a> Altre informazioni e contenuto della community  
 [Kerberos per amministratori impegnati](http://blogs.technet.com/b/askds/archive/2008/03/06/kerberos-for-the-busy-admin.aspx)  
  
 [Informazioni su Kerberos con doppio hop](http://blogs.technet.com/b/askds/archive/2008/06/13/understanding-kerberos-double-hop.aspx)  
  
 [Tutto su .NET e SharePoint](http://sbrickey.com/Tech/Blog/Post/Kerberos_Primer)  
  
 [Delega vincolata Kerberos basata su risorse](http://blog.kloud.com.au/2013/07/11/kerberos-constrained-delegation/)  
  
 [Nozioni di base su Kerberos: video](http://blog.martinlund.it/kerberos-primer/)  
  
 [Microsoft® Kerberos Configuration Manager per Microsoft SQL Server®](http://www.microsoft.com/en-us/download/details.aspx?id=39046)  
  
  
