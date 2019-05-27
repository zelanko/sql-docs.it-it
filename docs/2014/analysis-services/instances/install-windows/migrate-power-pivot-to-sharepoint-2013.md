---
title: Eseguire la migrazione di PowerPivot per SharePoint 2013 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: f698ceb1-d53e-4717-a3a0-225b346760d0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6cbbe9f2ba24773ef2b55444e65ce946b0763a41
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079851"
---
# <a name="migrate-powerpivot-to-sharepoint-2013"></a>Eseguire la migrazione di PowerPivot a SharePoint 2013
  
  
 SharePoint 2013 non supporta l'aggiornamento sul posto. Tuttavia, la procedura di **aggiornamento del collegamento di un database è supportata**. Il comportamento è diverso dall'aggiornamento a SharePoint 2010, in cui un cliente può scegliere tra i due approcci di aggiornamento di base: l'aggiornamento sul posto e l'aggiornamento del collegamento di un database.  
  
 Se si dispone di un'installazione di [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] integrata con SharePoint 2010, non è possibile eseguire l'aggiornamento sul posto del server SharePoint. È tuttavia possibile eseguire la migrazione dei database del contenuto e di quelli dell'applicazione di servizio dalla farm di SharePoint 2010 a una di SharePoint 2013. In questo argomento viene fornita una panoramica dei passaggi necessari per completare un aggiornamento del collegamento di un database e una migrazione correlata a PowerPivot:  
  
 **[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2013  
  
### <a name="migration-overview"></a>Panoramica della migrazione  
  
|1|2|3|4|  
|-------|-------|-------|-------|  
|Preparare la farm di SharePoint 2013|Eseguire il backup, la copia e il ripristino dei database|Montare i database del contenuto|Eseguire la migrazione delle pianificazioni di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]|  
||[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|Amministrazione centrale SharePoint<br /><br /> Windows PowerShell|Pagine dell'applicazione SharePoint<br /><br /> Windows PowerShell|  
  
 **Contenuto dell'argomento:**  
  
-   [1) Preparare la farm di SharePoint 2013](#bkmk_prepare_sharepoint2013)  
  
-   [2) Eseguire il backup, la copia e il ripristino dei database](#bkmk_backup_restore)  
  
-   [3) Preparare le applicazioni Web e montare i database del contenuto](#bkmk_prepare_mount_databases)  
  
-   [4) aggiornare le pianificazioni di PowerPivot](#bkmk_upgrade_powerpivot_schedules)  
  
-   [Risorse aggiuntive](#bkmk_additional_resources)  
  
##  <a name="bkmk_prepare_sharepoint2013"></a> 1) Preparare la farm di SharePoint 2013  
  
1.  > [!TIP]  
    >  Controllare il metodo di autenticazione per cui sono configurate le applicazioni Web esistenti. Le applicazioni Web SharePoint 2013 sono impostate in modo predefinito sull'autenticazione basata sulle attestazioni. Per le applicazioni Web SharePoint 2010 configurate per l'autenticazione in modalità classica sono richiesti passaggi aggiuntivi per eseguire la migrazione dei database da SharePoint 2010 a SharePoint 2013. Se le applicazioni Web sono configurate per l'autenticazione in modalità classica, controllare la documentazione di SharePoint 2013.  
  
2.  Installare una nuova farm di SharePoint Server 2013.  
  
3.  Installare un'istanza di un server [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità SharePoint. Per ulteriori informazioni, vedere [PowerPivot for SharePoint 2013 Installation](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
4.  Eseguire il pacchetto di installazione di [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] **spPowerPivot.msi** in ogni server nella farm SharePoint. Per altre informazioni, vedere [installare o disinstallare PowerPivot per SharePoint Add-in &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).  
  
5.  In Amministrazione centrale SharePoint 2013 configurare l'applicazione di servizio per Excel Services per l'utilizzo del server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità SharePoint creato nel passaggio precedente. Per altre informazioni, vedere la sezione "Configurare Analysis Services SharePoint integrazione di base" del [PowerPivot per SharePoint 2013 Installation](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
##  <a name="bkmk_backup_restore"></a> 2) Eseguire il backup, la copia e il ripristino dei database  
 Il processo "SharePoint database aggiornamento del collegamento" è una sequenza di passaggi per eseguire il backup, copia e ripristino PowerPivot contenuto correlato e database dell'applicazione di servizio per SharePoint 2013 farm.  
  
1.  **Impostare il Database in sola lettura:** Nelle [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], fare doppio clic il nome del database e fare clic su **proprietà**. Nella pagina **Opzioni** impostare la proprietà **Database di sola lettura** su **True**.  
  
2.  **Eseguire il backup:** Eseguire il backup di ogni database del contenuto e database dell'applicazione di servizio che si desidera eseguire la migrazione alla farm di SharePoint 2013. In [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]fare clic con il pulsante destro del mouse sul nome del database, fare clic su **Attività**e scegliere **Backup**.  
  
3.  Copiare i file di backup del database (con estensione bak) nel server di destinazione desiderato.  
  
4.  **Ripristino:** Ripristinare i database nella destinazione [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]. Questo passaggio può essere completato utilizzando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
5.  **Impostare il Database in lettura / scrittura:** Impostare il **Database di sola lettura** al **False**.  
  
##  <a name="bkmk_prepare_mount_databases"></a> 3) Preparare le applicazioni Web e montare i database del contenuto  
 Per una spiegazione più dettagliata delle procedure seguenti, vedere [aggiornare i database da SharePoint 2010 a SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256690) (https://go.microsoft.com/fwlink/p/?LinkId=256690).  
  
1.  **Portare i database offline:**  
  
     Portare offline ogni database del contenuto di SharePoint 2013 utilizzando Amministrazione centrale SharePoint. I database del contenuto vengono sostituiti da quelli copiati. Si tenga in considerazione la migliore sequenza per l'ambiente. Valutare l'opportunità di portare offline ogni database e montare il relativo database di sostituzione prima di portare offline il successivo database del contenuto. Un'altra opzione consiste nel portare offline tutti i database del contenuto come gruppo.  
  
    1.  In Amministrazione centrale SharePoint fare clic su **Gestione applicazioni**.  
  
    2.  Fare clic su **Gestisci database del contenuto**.  
  
    3.  Fare clic sul nome del database.  
  
    4.  In **Gestisci impostazioni database del contenuto**impostare **Stato del database** su **Offline**.  
  
    5.  Selezionare **Rimuovi database del contenuto**. Si noti l'avviso indicante che i siti archiviati nel database del contenuto non saranno più accessibili.  
  
-   **Montare i database del contenuto:**  
  
     Utilizzare i cmdlet PowerShell nella shell di gestione di SharePoint 2013 per montare il database del contenuto migrato. È necessario montare solo i database di contenuto, non il database dell'applicazione di servizio: ![Contenuto correlato di PowerShell](../../../reporting-services/media/rs-powershellicon.jpg "Contenuto correlato di PowerShell")  
  
    ```  
    Mount-SPContentDatabase "SharePoint_Content_O14-KJSP1" -DatabaseServer "[server name]\powerpivot" -WebApplication [web application URL]  
    ```  
  
     Per altre informazioni, vedere [collegamento o scollegamento di database del contenuto (SharePoint Server 2010)](https://technet.microsoft.com/library/ff628582.aspx) (https://technet.microsoft.com/library/ff628582.aspx).  
  
     **Stato al completamento del passaggio:**  Una volta completata l'operazione di montaggio, gli utenti possono visualizzare i file disponibili nel database del contenuto precedente. Di conseguenza, essi possono visualizzare e aprire le cartelle di lavoro nella raccolta documenti.  
  
    > [!TIP]  
    >  È possibile creare, a questo punto del processo di migrazione, nuove pianificazioni per le cartelle di lavoro migrate. Tuttavia, le pianificazioni vengono create nel nuovo database dell'applicazione di servizio [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e non nel database copiato dalla farm SharePoint precedente. Pertanto, in esso non sarà contenuta alcuna pianificazione precedente. Dopo aver completato i passaggi seguenti per utilizzare il database precedente ed eseguire la migrazione delle pianificazioni precedenti, le nuove pianificazioni non saranno disponibili.  
  
### <a name="troubleshoot-issues-when-you-attempt-to-mount-databases"></a>Risolvere eventuali problemi durante il tentativo di montaggio di database  
 In questa sezione vengono riepilogati i possibili problemi riscontrati durante il montaggio del database.  
  
1.  **Errori di autenticazione:** Se vengono visualizzati errori relativi all'autenticazione, controllare le modalità di autenticazione utilizzano nelle applicazioni web di origine. L'errore potrebbe essere causato da una mancata corrispondenza dell'autenticazione tra l'applicazione Web SharePoint 2013 e l'applicazione Web SharePoint 2010. Per ulteriori informazioni, vedere [1) Preparare la farm di SharePoint 2013](#bkmk_prepare_sharepoint2013) .  
  
2.  **File mancante:** Se vengono visualizzati errori relativi alla mancanza di DLL di PowerPivot, il **sppowerpivot. msi** non è stato installato o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] dello strumento di configurazione non è stato usato per configurare PowerPivot.  
  
##  <a name="bkmk_upgrade_powerpivot_schedules"></a> 4) aggiornare le pianificazioni di PowerPivot  
 In questa sezione vengono illustrati i dettagli e le opzioni per eseguire la migrazione delle pianificazioni di PowerPivot. La migrazione di una pianificazione è un processo in due passaggi. In primo luogo, configurare l'applicazione di servizio PowerPivot per l'utilizzo del database dell'applicazione di servizio sottoposto a migrazione. In secondo luogo, scegliere una delle due opzioni per la migrazione della pianificazione.  
  
 **Configurare l'applicazione di servizio per l'utilizzo del database dell'applicazione di servizio sottoposto a migrazione.**  
  
 In Amministrazione centrale SharePoint configurare l'applicazione di servizio PowerPivot per l'utilizzo del database dell'applicazione di servizio precedente copiato. Tramite il servizio PowerPivot viene aggiornato il database dell'applicazione di servizio in base al nuovo schema.  
  
1.  In Amministrazione centrale SharePoint fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Individuare di PowerPivot servizio dell'applicazione, ad esempio "Default PowerPivot Service Application", fare clic sul nome dell'applicazione del servizio e fare clic su **proprietà** nella barra multifunzione di SharePoint.  
  
3.  Aggiornare l'istanza del nome del server di database e il nome del database nei nomi corretti del database di cui sono stati eseguiti il backup, la copia e il ripristino. Una volta fatto clic su **OK**, il database dell'applicazione di servizio viene aggiornato. Gli errori verranno registrati nel log ULS.  
  
 **Aggiornare le pianificazioni di PowerPivot**  
  
 Configurare l'applicazione di servizio PowerPivot per l'esecuzione della migrazione di pianificazioni di aggiornamenti.  
  
-   **Eseguire la migrazione di pianificazioni option1: Amministratore della farm di SharePoint**  
  
    1.  Durante l'esecuzione di gestione SharePoint 2013 i `Set-PowerPivotServiceApplication` cmdlet con il `-StartMigratingRefreshSchedules` interruttore per abilitare automatica nella migrazione della pianificazione della domanda ![contenuto correlato di PowerShell](../../../reporting-services/media/rs-powershellicon.jpg "contenutocorrelatodiPowerShell"). Nello script di Windows PowerShell seguente si presuppone la presenza di un'unica applicazione di servizio PowerPivot.  
  
        ```  
        $app=Get-PowerPivotServiceApplication  
        Set-PowerPivotServiceApplication $app -StartMigratingRefreshSchedules  
        ```  
  
         Dopo aver eseguito lo script di Windows PowerShell, le pianificazioni sono attive e verranno eseguite al momento appropriato successivo. Tuttavia, lo stato nella pagina di aggiornamento delle pianificazioni non è abilitato. Quando la pianificazione viene eseguita la prima volta, ne verrà eseguita la migrazione e nella pagina di aggiornamento delle pianificazioni verrà attivato lo stato **Abilitata**  .  
  
    2.  Se si desidera controllare il valore corrente della proprietà StartMigratingRefreshSchedules, eseguire lo script PowerShell riportato di seguito. Tramite lo script viene eseguito il ciclo di tutti gli oggetti dell'applicazione di servizio PowerPivot e vengono visualizzati il nome e i valori delle proprietà:  
  
        ```  
        $apps = Get-PowerPivotServiceApplication  
        foreach ($app in $apps){}  
        Get-PowerPivotServiceApplication $appp | format-table -property displayname,id,StartMigratingRefreshSchedules  
        ```  
  
     **Eseguire la migrazione di pianificazioni option2: Utente aggiorna ogni cartella di lavoro**  
  
    1.  Un'altra opzione per eseguire la migrazione delle pianificazioni consiste nell'abilitare l'aggiornamento delle pianificazioni per ogni cartella di lavoro. Passare alla raccolta documenti contenente le cartelle di lavoro.  
  
    2.  Aprire il menu di scelta rapida e fare clic su **Gestisci aggiornamento dati PowerPivot**.  
  
    3.  Nella sezione relativa **all'aggiornamento delle pianificazioni** fare clic su **Abilita**.  
  
    4.  È possibile selezionare **Aggiorna anche appena possibile**. Tramite questa opzione viene aggiunta un'istanza di aggiornamento alla coda non appena si fa clic su OK. La pianificazione dell'aggiornamento regolare viene tuttavia attivata al momento opportuno.  
  
    5.  Scegliere **OK**. La cronologia di aggiornamento è ora visibile nella pagina degli aggiornamenti. La pianificazione verrà attivata al momento previsto.  
  
 **Cartelle di lavoro di SQL Server 2008 R2 PowerPivot**  
  
-   Le cartelle di lavoro di SQL Server 2008 R2 PowerPivot non vengono aggiornate automaticamente se utilizzate in SQL Server 2012 SP1 2013 PowerPivot per SharePoint 2013. Dopo la migrazione di un database del contenuto in cui sono incluse cartelle di lavoro di SQL Server 2008 R2, è possibile utilizzare le cartelle di lavoro ma le pianificazioni non vengono aggiornate.  
  
-   Per altre informazioni, vedere [Aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
##  <a name="bkmk_additional_resources"></a> Risorse aggiuntive  
  
> [!NOTE]  
>  Per ulteriori informazioni sull'aggiornamento del collegamento di un database SharePoint e [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , vedere gli argomenti seguenti:  
  
-   [Aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
-   [Panoramica del processo di aggiornamento a SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256688) (https://go.microsoft.com/fwlink/p/?LinkId=256688).  
  
-   [Pulire le preparazioni prima di un aggiornamento a SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256689) (https://go.microsoft.com/fwlink/p/?LinkId=256689).  
  
-   [Aggiornare i database da SharePoint 2010 a SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256690) (https://go.microsoft.com/fwlink/p/?LinkId=256690).  
  
  
