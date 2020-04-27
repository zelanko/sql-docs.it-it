---
title: Aggiornare Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9c3543f3-3eb9-455d-a9bf-f17e9506ad21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: da78f21c6346281dc23332f40e8e6f46ff07aa06
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62774656"
---
# <a name="upgrade-master-data-services"></a>Aggiornare Master Data Services
  Esistono quattro scenari di aggiornamento a Microsoft [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2. Scegliere lo scenario più appropriato alla propria situazione.  
  
-   [Aggiornare senza aggiornamento del motore di database](#noengine)  
  
-   [Aggiornamento con motore di database aggiornamento](#engine)  
  
-   [Eseguire l'aggiornamento in uno scenario con due computer](#twocomputer)  
  
-   [Eseguire l'aggiornamento con il ripristino di un database da un backup](#restore)  
  
> [!IMPORTANT]
>  -   L'aggiornamento dalla versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP1 alla versione CTP2 non è supportato.  
> -   Eseguire il backup del database prima di effettuare qualsiasi aggiornamento.  
> -   Con il processo di aggiornamento vengono ricreate le stored procedure e le tabelle aggiornate utilizzate da [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Le personalizzazioni apportate a questi componenti potrebbero andare perse.  
> -   I pacchetti di distribuzione di modelli possono essere utilizzati solo nell'edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzata per crearli. Non è possibile distribuire pacchetti di distribuzione di [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] / [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] modelli [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]creati in a.  
> -   È possibile continuare a usare la versione [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 del componente aggiuntivo Master Data Services per Excel dopo l'aggiornamento di Master Data Services e di Data Quality Services a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2. Tuttavia, una versione precedente del componente aggiuntivo Master Data Services per Excel non funzionerà dopo l'aggiornamento a SQL Server 2014 CTP2. È possibile scaricare la versione [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 del componente aggiuntivo Master Data Services per Excel da [qui](https://go.microsoft.com/fwlink/?LinkId=328664).  
  
##  <a name="upgrade-without-database-engine-upgrade"></a><a name="noengine"></a>Aggiornamento senza motore di database aggiornamento  
 Questo scenario può essere considerato un'installazione side-by-Side, perché sia [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] / [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] che [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] sono installati in parallelo, nello stesso computer o in computer separati.  
  
 In questo scenario si continua a utilizzare [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] per ospitare il database MDS. Tuttavia, è necessario aggiornare lo schema del database MDS e, successivamente, creare un'applicazione Web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per accedere al database MDS. L'accesso al database MDS non può essere eseguito più dall'applicazione Web [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
 Se si sceglie di installare [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e una versione precedente di SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]/[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) nello stesso computer, è possibile farlo perché i file vengono installati in un percorso diverso.  
  
-   Per impostazione predefinita, in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]i file sono installati in *unità*:\Programmi\Microsoft SQL Server\120\Master Data Services.  
  
-   Per impostazione predefinita, in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]i file sono installati in *unità*:\Programmi\Microsoft SQL Server\110\Master Data Services.  
  
-   Per impostazione predefinita, in [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]i file sono installati in *unità*:\Programmi\Microsoft SQL Server\Master Data Services.  
  
 Per eseguire questa attività, effettuare le operazioni indicate di seguito.  
  
1.  Installare [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e qualsiasi altra funzionalità desiderata.  
  
    1.  Aprire l'Installazione guidata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    2.  Fare clic su **Installazione**nel riquadro sinistro.  
  
    3.  Nel riquadro destro, fare clic su **Nuova installazione autonoma di SQL Server o aggiunta di funzionalità a un'installazione esistente**.  
  
    4.  Nella pagina **Selezione funzionalità** , selezionare **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** e qualsiasi altra funzionalità si voglia installare.  
  
    5.  Completare la procedura guidata.  
  
2.  Una volta completata l'installazione, aggiornare lo schema del database MDS.  
  
    1.  Aprire la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
        > [!IMPORTANT]  
        >  Per aggiornare lo schema del database MDS, è necessario avere effettuato l'accesso con l'account Administrator specificato quando è stato creato il database MDS. Nel database MDS, in mdm.tblUser, a questo utente è assegnato il valore **ID****1**. Per informazioni sulla modifica di questo utente, vedere [modificare l'account amministratore di sistema &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
    2.  Nel riquadro sinistro fare clic su **Configurazione database**.  
  
    3.  Nel riquadro destro fare clic su **Seleziona database** e specificare le informazioni per l' [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] istanza [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] del database o.  
  
    4.  Fare clic su **Aggiorna database** per avviare l' **Aggiornamento guidato database**. Per altre informazioni, vedere [Aggiornamento guidato database &#40;Gestione configurazione Master Data Services&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md).  
  
3.  Quando l'aggiornamento è completato, creare un'applicazione Web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    1.  Aprire la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
    2.  Nel riquadro sinistro fare clic su **Configurazione Web**.  
  
    3.  Nel riquadro destro, selezionare nell'elenco **Sito Web** una delle seguenti opzioni:  
  
        -   **Sito Web predefinito**, quindi scegliere **Crea applicazione**.  
  
        -   **Crea nuovo sito**. Quando si crea il sito Web, viene creata automaticamente una nuova applicazione Web.  
  
        > [!IMPORTANT]  
        >  L'applicazione Web MDS esistente di una versione precedente di SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) è disponibile per la selezione nella versione SQL Server 2014 di Gestione configurazione Master Data Services. Non è necessario selezionare l'applicazione Web esistente, è invece necessario creare un'applicazione Web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per MDS. In caso contrario, verrà visualizzato un errore quando si tenta di associare l'applicazione Web al database MDS aggiornato, indicante che non è possibile accedere alla pagina richiesta perché i dati di configurazione correlati per la pagina non sono validi.  
        >   
        >  Se si desidera utilizzare lo stesso nome (alias) per l'applicazione Web MDS dell'applicazione Web ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) esistente, è necessario innanzitutto eliminare l'applicazione Web e il pool di applicazioni associato da IIS e, successivamente, creare un'applicazione Web con lo stesso nome utilizzando la versione SQL Server 2014 di Gestione configurazione Master Data Services. Per informazioni sulla rimozione di un'applicazione Web e di pool di applicazioni da IIS, vedere [Rimuovere un'applicazione (IIS)](https://go.microsoft.com/fwlink/?LinkId=323537) e [Rimuovere un pool di applicazioni (IIS)](https://go.microsoft.com/fwlink/?LinkId=323538).  
  
4.  A questo punto, associare la nuova applicazione Web al database MDS aggiornato.  
  
    1.  Nella sezione **Associare un'applicazione a un database** fare clic su **Seleziona**.  
  
    2.  Selezionare il database MDS.  
  
    3.  Fare clic su **Apply**.  
  
##  <a name="upgrade-with-database-engine-upgrade"></a><a name="engine"></a> Aggiornare con l'aggiornamento del motore di database  
 In questo scenario il motore di database e l'applicazione [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] verranno aggiornati da [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o SQL Server 2012 a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Per eseguire questa attività, effettuare le operazioni indicate di seguito.  
  
1.  **Solo per [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** : aprire **Pannello di controllo** > **Programmi e funzionalità** e disinstallare Microsoft [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
2.  Aggiornare il motore di database a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    1.  Aprire l'Installazione guidata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    2.  Fare clic su **Installazione**nel riquadro sinistro.  
  
    3.  Nel riquadro di destra fare clic su **Aggiorna da SQL Server 2005, SQL Server 2008, SQL Server 2008 R2 o SQL Server 2012**.  
  
    4.  Completare la procedura guidata.  
  
3.  **Solo [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] per**: al termine dell'aggiornamento, aggiungere la **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** funzionalità.  
  
    1.  Aprire l'Installazione guidata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    2.  Fare clic su **Installazione**nel riquadro sinistro.  
  
    3.  Nel riquadro destro, fare clic su **Nuova installazione autonoma di SQL Server o aggiunta di funzionalità a un'installazione esistente**.  
  
    4.  Nella pagina **tipo di installazione** della procedura guidata selezionare l'opzione **Aggiungi funzionalità a un'istanza esistente** e scegliere l'istanza in cui è installato il database MDS.  
  
    5.  Nella pagina **Selezione funzionalità** , in **funzionalità condivise**, selezionare **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]**.  
  
    6.  Completare la procedura guidata.  
  
4.  Aggiornare lo schema del database MDS.  
  
    1.  Aprire la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
        > [!IMPORTANT]  
        >  Per aggiornare lo schema del database MDS, è necessario avere effettuato l'accesso con l'account Administrator specificato quando è stato creato il database MDS. Nel database MDS, in mdm.tblUser, a questo utente è assegnato il valore **ID****1**. Per informazioni sulla modifica di questo utente, vedere [modificare l'account amministratore di sistema &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
    2.  Nel riquadro sinistro fare clic su **Configurazione database**.  
  
    3.  Nel riquadro destro fare clic su **Seleziona database** e specificare le informazioni per l'istanza del database.  
  
    4.  Fare clic su **Aggiorna database** per avviare l' **Aggiornamento guidato database**. Per altre informazioni, vedere [Aggiornamento guidato database &#40;Gestione configurazione Master Data Services&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md).  
  
    5.  Fare clic su **Applica**.  
  
5.  Quando l'aggiornamento è completato, creare un'applicazione Web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    1.  Aprire la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
    2.  Nel riquadro sinistro fare clic su **Configurazione Web**.  
  
    3.  Nel riquadro destro, selezionare nell'elenco **Sito Web** una delle seguenti opzioni:  
  
        -   **Sito Web predefinito**, quindi scegliere **Crea applicazione**.  
  
        -   **Crea nuovo sito**. Quando si crea il sito Web, viene creata automaticamente una nuova applicazione Web.  
  
        > [!IMPORTANT]  
        >  L'applicazione Web MDS esistente di una versione precedente di SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) è disponibile per la selezione nella versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di Gestione configurazione Master Data Services. Non è necessario selezionare l'applicazione Web esistente, è invece necessario creare un'applicazione Web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per MDS. In caso contrario, verrà visualizzato un errore quando si tenta di associare l'applicazione Web al database MDS aggiornato, indicante che non è possibile accedere alla pagina richiesta perché i dati di configurazione correlati per la pagina non sono validi.  
        >   
        >  Se si desidera utilizzare lo stesso nome (alias) per l'applicazione Web MDS dell'applicazione Web ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) esistente, è necessario innanzitutto eliminare l'applicazione Web e il pool di applicazioni associato da IIS e, successivamente, creare un'applicazione Web con lo stesso nome utilizzando la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di Gestione configurazione Master Data Services. Per informazioni sulla rimozione di un'applicazione Web e di pool di applicazioni da IIS, vedere [Rimuovere un'applicazione (IIS)](https://go.microsoft.com/fwlink/?LinkId=323537) e [Rimuovere un pool di applicazioni (IIS)](https://go.microsoft.com/fwlink/?LinkId=323538).  
  
6.  A questo punto, associare la nuova applicazione Web al database MDS aggiornato.  
  
    1.  Nella sezione **Associare un'applicazione a un database** fare clic su **Seleziona**.  
  
    2.  Selezionare il database MDS.  
  
    3.  Fare clic su **Applica**.  
  
##  <a name="upgrade-in-two-computer-scenario"></a><a name="twocomputer"></a> Aggiornare in uno scenario con due computer  
 Questo scenario comporta l'aggiornamento di un sistema nel quale SQL Server viene installato in due computer: uno con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e l'altro con SQL Server 2008 R2 o SQL Server 2012.  
  
 Se è installato [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], si continua a utilizzare rispettivamente [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] per ospitare il database MDS in un computer. Tuttavia, è necessario aggiornare lo schema del database MDS e quindi utilizzare l'applicazione Web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per accedere al database MDS. L'accesso al database MDS non può essere eseguito più dall'applicazione Web [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
-   Per impostazione predefinita, in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]i file sono installati in *unità*:\Programmi\Microsoft SQL Server\120\Master Data Services.  
  
-   Per impostazione predefinita, in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]i file sono installati in *unità*:\Programmi\Microsoft SQL Server\110\Master Data Services.  
  
-   Per impostazione predefinita, in [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]i file sono installati in *unità*:\Programmi\Microsoft SQL Server\Master Data Services.  
  
 Per eseguire questa attività, effettuare le operazioni indicate di seguito.  
  
1.  Installare [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e qualsiasi altra funzionalità desiderata.  
  
    1.  Aprire l'Installazione guidata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    2.  Fare clic su **Installazione**nel riquadro sinistro.  
  
    3.  Nel riquadro destro, fare clic su **Nuova installazione autonoma di SQL Server o aggiunta di funzionalità a un'installazione esistente**.  
  
    4.  Nella pagina **Selezione funzionalità** , selezionare **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** e qualsiasi altra funzionalità si voglia installare.  
  
    5.  Completare la procedura guidata.  
  
2.  Una volta completata l'installazione, aggiornare lo schema del database MDS.  
  
    1.  Aprire la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
        > [!IMPORTANT]  
        >  Per aggiornare lo schema del database MDS, è necessario avere effettuato l'accesso con l'account Administrator specificato quando è stato creato il database MDS. Nel database MDS, in mdm.tblUser, a questo utente è assegnato il valore **ID****1**. Per informazioni sulla modifica di questo utente, vedere [modificare l'account amministratore di sistema &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
    2.  Nel riquadro sinistro fare clic su **Configurazione database**.  
  
    3.  Nel riquadro destro fare clic su **Seleziona database** e specificare le informazioni per l' [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] istanza [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] del database o nell'altro computer, se [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] è installato nell'altro computer.  
  
    4.  Fare clic su **Aggiorna database** per avviare l' **Aggiornamento guidato database**. Per altre informazioni, vedere [Aggiornamento guidato database &#40;Gestione configurazione Master Data Services&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md).  
  
3.  Quando l'aggiornamento è completato, creare un'applicazione Web SQL Server 2014.  
  
    1.  Aprire la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
    2.  Nel riquadro sinistro fare clic su **Configurazione Web**.  
  
    3.  Nel riquadro destro, selezionare nell'elenco **Sito Web** una delle seguenti opzioni:  
  
        -   **Sito Web predefinito**, quindi scegliere **Crea applicazione**.  
  
        -   **Crea nuovo sito**. Quando si crea il sito Web, viene creata automaticamente una nuova applicazione Web.  
  
        > [!IMPORTANT]  
        >  L'applicazione Web MDS esistente di una versione precedente di SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) è disponibile per la selezione nella versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di Gestione configurazione Master Data Services. Non è necessario selezionare l'applicazione Web esistente, è invece necessario creare un'applicazione Web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per MDS. In caso contrario, verrà visualizzato un errore quando si tenta di associare l'applicazione Web al database MDS aggiornato, indicante che non è possibile accedere alla pagina richiesta perché i dati di configurazione correlati per la pagina non sono validi.  
        >   
        >  Se si desidera utilizzare lo stesso nome (alias) per l'applicazione Web MDS dell'applicazione Web ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) esistente, è necessario innanzitutto eliminare l'applicazione Web e il pool di applicazioni associato da IIS e, successivamente, creare un'applicazione Web con lo stesso nome utilizzando la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di Gestione configurazione Master Data Services. Per informazioni sulla rimozione di un'applicazione Web e di pool di applicazioni da IIS, vedere [Rimuovere un'applicazione (IIS)](https://go.microsoft.com/fwlink/?LinkId=323537) e [Rimuovere un pool di applicazioni (IIS)](https://go.microsoft.com/fwlink/?LinkId=323538).  
  
4.  A questo punto, associare l'applicazione Web al database MDS aggiornato.  
  
    1.  Nella sezione **Associare un'applicazione a un database** fare clic su **Seleziona**.  
  
    2.  Selezionare il database MDS.  
  
    3.  Fare clic su **Applica**.  
  
##  <a name="upgrade-with-restoring-a-database-from-backup"></a><a name="restore"></a> Aggiornare con il ripristino di un database da un backup  
 In questo scenario, [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] è installato insieme a SQL Server 2008 R2 o SQL Server 2012 nello stesso computer o in due computer differenti. Inoltre, è stato eseguito il backup di un database in una versione precedente a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2, prima dell'aggiornamento, e il database deve essere ripristinato.  
  
-   Per impostazione predefinita, in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]i file sono installati in *unità*:\Programmi\Microsoft SQL Server\120\Master Data Services.  
  
-   Per impostazione predefinita, in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]i file sono installati in *unità*:\Programmi\Microsoft SQL Server\110\Master Data Services.  
  
-   Per impostazione predefinita, in [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]i file sono installati in *unità*:\Programmi\Microsoft SQL Server\Master Data Services.  
  
 Per eseguire questa attività, effettuare le operazioni indicate di seguito.  
  
1.  Installare [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e qualsiasi altra funzionalità desiderata.  
  
    1.  Aprire l'Installazione guidata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    2.  Fare clic su **Installazione**nel riquadro sinistro.  
  
    3.  Nel riquadro destro, fare clic su **Nuova installazione autonoma di SQL Server o aggiunta di funzionalità a un'installazione esistente**.  
  
    4.  Nella pagina **Selezione funzionalità** , selezionare **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** e qualsiasi altra funzionalità si voglia installare.  
  
    5.  Completare la procedura guidata.  
  
2.  Ripristinare il database di cui è stato eseguito il backup.  
  
3.  Una volta completata l'installazione, aggiornare lo schema del database MDS.  
  
    1.  Aprire la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
        > [!IMPORTANT]  
        >  Per aggiornare lo schema del database MDS, è necessario avere effettuato l'accesso con l'account Administrator specificato quando è stato creato il database MDS. Nel database MDS, in mdm.tblUser, a questo utente è assegnato il valore **ID****1**. Per informazioni sulla modifica di questo utente, vedere [modificare l'account amministratore di sistema &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
    2.  Nel riquadro sinistro fare clic su **Configurazione database**.  
  
    3.  Nel riquadro destro fare clic su **Seleziona database** e specificare le informazioni per l' [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] istanza [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] del database o.  
  
    4.  Fare clic su **Aggiorna database** per avviare l' **Aggiornamento guidato database**. Per altre informazioni, vedere [Aggiornamento guidato database &#40;Gestione configurazione Master Data Services&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md).  
  
4.  Quando l'aggiornamento è completato, creare un'applicazione Web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    1.  Aprire la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
    2.  Nel riquadro sinistro fare clic su **Configurazione Web**.  
  
    3.  Nel riquadro destro, selezionare nell'elenco **Sito Web** una delle seguenti opzioni:  
  
        -   **Sito Web predefinito**, quindi scegliere **Crea applicazione**.  
  
        -   **Crea nuovo sito**. Quando si crea il sito Web, viene creata automaticamente una nuova applicazione Web.  
  
        > [!IMPORTANT]  
        >  L'applicazione Web MDS esistente di una versione precedente di SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) è disponibile per la selezione nella versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di Gestione configurazione Master Data Services. Non è necessario selezionare l'applicazione Web esistente, è invece necessario creare un'applicazione Web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per MDS. In caso contrario, verrà visualizzato un errore quando si tenta di associare l'applicazione Web al database MDS aggiornato, indicante che non è possibile accedere alla pagina richiesta perché i dati di configurazione correlati per la pagina non sono validi.  
        >   
        >  Se si desidera utilizzare lo stesso nome (alias) per l'applicazione Web MDS dell'applicazione Web ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) esistente, è necessario innanzitutto eliminare l'applicazione Web e il pool di applicazioni associato da IIS e, successivamente, creare un'applicazione Web con lo stesso nome utilizzando la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di Gestione configurazione Master Data Services. Per informazioni sulla rimozione di un'applicazione Web e di pool di applicazioni da IIS, vedere [Rimuovere un'applicazione (IIS)](https://go.microsoft.com/fwlink/?LinkId=323537) e [Rimuovere un pool di applicazioni (IIS)](https://go.microsoft.com/fwlink/?LinkId=323538).  
  
5.  A questo punto, associare la nuova applicazione Web al database MDS aggiornato.  
  
    1.  Nella sezione **Associare un'applicazione a un database** fare clic su **Seleziona**.  
  
    2.  Selezionare il database MDS.  
  
    3.  Fare clic su **Applica**.  
  
## <a name="troubleshooting"></a>Risoluzione dei problemi  
 **Problema:** Quando si apre l' [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] applicazione [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web o, viene visualizzato il messaggio di errore "versione client non compatibile con la versione del database".  
  
 **Soluzione:** Questo problema si verifica quando [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] un' [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] applicazione Web o gestione dati master tenta di accedere a un database che è stato [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] aggiornato a Master Data Services. È necessario quindi utilizzare un'applicazione Web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
 Questo problema si può verificare anche qualora non si arresti e riavvii il **pool di applicazioni MDS** in IIS in caso di aggiornamento dello schema del database MDS. Riavviare il **pool di applicazioni MDS** per correggere il problema.  
  
## <a name="see-also"></a>Vedi anche  
 [Installazione di Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
