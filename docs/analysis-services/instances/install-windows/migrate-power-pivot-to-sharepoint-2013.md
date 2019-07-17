---
title: Eseguire la migrazione di Power Pivot per SharePoint 2013 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8df7cc04ea0682212f5a046ca4c614e83ebe9c86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68231877"
---
# <a name="migrate-power-pivot-to-sharepoint-2013"></a>Eseguire la migrazione di PowerPivot a SharePoint 2013
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  
  
 SharePoint 2013 non supporta l'aggiornamento sul posto. Tuttavia, la procedura di **aggiornamento del collegamento di un database è supportata**. Il comportamento è diverso dall'aggiornamento a SharePoint 2010, in cui un cliente può scegliere tra i due approcci di aggiornamento di base: l'aggiornamento sul posto e l'aggiornamento del collegamento di un database.  
  
 Se si dispone di un'installazione di [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] integrata con SharePoint 2010, non è possibile eseguire l'aggiornamento sul posto del server SharePoint. È tuttavia possibile eseguire la migrazione dei database del contenuto e di quelli dell'applicazione di servizio dalla farm di SharePoint 2010 a una di SharePoint 2013. Questo argomento fornisce una panoramica dei passaggi necessari per completare un aggiornamento del collegamento di un database e una migrazione correlata a [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]:  
  
### <a name="migration-overview"></a>Panoramica della migrazione  
  
|1|2|3|4|  
|-------|-------|-------|-------|  
|Preparare la farm di SharePoint 2013|Eseguire il backup, la copia e il ripristino dei database|Montare i database del contenuto|Eseguire la migrazione delle pianificazioni di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]|  
||[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|\- Amministrazione centrale SharePoint<br /><br /> \- Windows PowerShell|\- Pagine dell'applicazione SharePoint<br /><br /> \- Windows PowerShell|  
  
##  <a name="bkmk_prepare_sharepoint2013"></a>Preparare la Farm di SharePoint 2013  
  
> [!TIP]
>  Controllare il metodo di autenticazione per cui sono configurate le applicazioni Web esistenti. Le applicazioni Web SharePoint 2013 sono impostate in modo predefinito sull'autenticazione basata sulle attestazioni. Per le applicazioni Web SharePoint 2010 configurate per l'autenticazione in modalità classica sono richiesti passaggi aggiuntivi per eseguire la migrazione dei database da SharePoint 2010 a SharePoint 2013. Se le applicazioni Web sono configurate per l'autenticazione in modalità classica, controllare la documentazione di SharePoint 2013.  
  
1.  Installare una nuova farm di SharePoint Server 2013.  
  
2.  Installare un'istanza di un server [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità SharePoint. Per altre informazioni, vedere [Install Analysis Services in Power Pivot Mode](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
3.  Eseguire il pacchetto di installazione di [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] **spPowerPivot.msi** in ogni server nella farm SharePoint. Per altre informazioni, vedere [Installare o disinstallare il componente aggiuntivo PowerPivot per &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).  
  
4.  In Amministrazione centrale SharePoint 2013 configurare l'applicazione di servizio per Excel Services per l'utilizzo del server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità SharePoint creato nel passaggio precedente. Per altre informazioni, vedere la sezione "Configurare Analysis Services SharePoint integrazione di base" del [Install Analysis Services in modalità Power Pivot](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
##  <a name="bkmk_backup_restore"></a>Eseguire il backup, copia, il ripristino dei database  
 Il processo "SharePoint database aggiornamento del collegamento" è una sequenza di passaggi per eseguire il backup, copia e ripristino [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] contenuto correlato e i database dell'applicazione del servizio alla farm di SharePoint 2013.  
  
1.  **Impostare il Database in sola lettura:** Nelle [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], fare doppio clic il nome del database e fare clic su **proprietà**. Nella pagina **Opzioni** impostare la proprietà **Database di sola lettura** su **True**.  
  
2.  **Eseguire il backup:** Eseguire il backup di ogni database del contenuto e database dell'applicazione di servizio che si desidera eseguire la migrazione alla farm di SharePoint 2013. In [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]fare clic con il pulsante destro del mouse sul nome del database, fare clic su **Attività**e scegliere **Backup**.  
  
3.  Copiare i file di backup del database (con estensione bak) nel server di destinazione desiderato.  
  
4.  **Ripristino:** Ripristinare i database nella destinazione [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]. Questo passaggio può essere completato utilizzando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
5.  **Impostare il Database in lettura / scrittura:** Impostare il **Database di sola lettura** al **False**.  
  
##  <a name="bkmk_prepare_mount_databases"></a>Preparare le applicazioni Web e database del contenuto di montaggio  
 Per una spiegazione più dettagliata delle procedure seguenti, vedere [aggiornare i database da SharePoint 2010 a SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256690) (http://go.microsoft.com/fwlink/p/?LinkId=256690).  
  
1.  **Portare i database offline:**  
  
     Portare offline ogni database del contenuto di SharePoint 2013 utilizzando Amministrazione centrale SharePoint. I database del contenuto vengono sostituiti da quelli copiati. Si tenga in considerazione la migliore sequenza per l'ambiente. Valutare l'opportunità di portare offline ogni database e montare il relativo database di sostituzione prima di portare offline il successivo database del contenuto. Un'altra opzione consiste nel portare offline tutti i database del contenuto come gruppo.  
  
    1.  In Amministrazione centrale SharePoint fare clic su **Gestione applicazioni**.  
  
    2.  Fare clic su **Gestisci database del contenuto**.  
  
    3.  Fare clic sul nome del database.  
  
    4.  In **Gestisci impostazioni database del contenuto**impostare **Stato del database** su **Offline**.  
  
    5.  Selezionare **Rimuovi database del contenuto**. Si noti l'avviso indicante che i siti archiviati nel database del contenuto non saranno più accessibili.  
  
-   **Montare i database del contenuto:**  
  
     Utilizzare i cmdlet PowerShell nella shell di gestione di SharePoint 2013 per montare il database del contenuto migrato. È necessario montare solo i database di contenuto, non il database dell'applicazione di servizio: ![Contenuto correlato di PowerShell](../../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Contenuto correlato di PowerShell")  
  
    ```  
    Mount-SPContentDatabase "SharePoint_Content_O14-KJSP1" -DatabaseServer "[server name]\powerpivot" -WebApplication [web application URL]  
    ```  
  
     Per altre informazioni, vedere [collegamento o scollegamento di database del contenuto (SharePoint Server 2010)](http://technet.microsoft.com/library/ff628582.aspx) (http://technet.microsoft.com/library/ff628582.aspx).  
  
     **Stato al completamento del passaggio:**  Una volta completata l'operazione di montaggio, gli utenti possono visualizzare i file disponibili nel database del contenuto precedente. Di conseguenza, essi possono visualizzare e aprire le cartelle di lavoro nella raccolta documenti.  
  
    -   > [!TIP]  
        >  È possibile creare, a questo punto del processo di migrazione, nuove pianificazioni per le cartelle di lavoro migrate. Tuttavia, le pianificazioni vengono create nel nuovo database dell'applicazione di servizio [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e non nel database copiato dalla farm SharePoint precedente. Pertanto, in esso non sarà contenuta alcuna pianificazione precedente. Dopo aver completato i passaggi seguenti per utilizzare il database precedente ed eseguire la migrazione delle pianificazioni precedenti, le nuove pianificazioni non saranno disponibili.  
  
### <a name="troubleshoot-issues-when-you-attempt-to-mount-databases"></a>Risolvere eventuali problemi durante il tentativo di montaggio di database  
 In questa sezione vengono riepilogati i possibili problemi riscontrati durante il montaggio del database.  
  
1.  **Errori di autenticazione:** Se vengono visualizzati errori relativi all'autenticazione, controllare le modalità di autenticazione utilizzano nelle applicazioni web di origine. L'errore potrebbe essere causato da una mancata corrispondenza dell'autenticazione tra l'applicazione Web SharePoint 2013 e l'applicazione Web SharePoint 2010. Per ulteriori informazioni, vedere [1) Preparare la farm di SharePoint 2013](#bkmk_prepare_sharepoint2013) .  
  
2.  **File mancante:** Se vengono visualizzati errori relativi alla mancanza [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] file con estensione dll, il **sppowerpivot. msi** non è stato installato oppure il [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] dello strumento di configurazione non è stato usato per configurare [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)].  
  
##  <a name="bkmk_upgrade_powerpivot_schedules"></a>Aggiornare le pianificazioni di PowerPivot  
 Questa sezione illustra i dettagli e le opzioni per eseguire la migrazione delle pianificazioni di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . La migrazione di una pianificazione è un processo in due passaggi. Configurare l'applicazione del servizio [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per usare il database dell'applicazione del servizio migrato. In secondo luogo, scegliere una delle due opzioni per la migrazione della pianificazione.  
  
 **Configurare l'applicazione di servizio per l'utilizzo del database dell'applicazione di servizio sottoposto a migrazione.**  
  
 In Amministrazione centrale SharePoint configurare l'applicazione del servizio [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per usare il database dell'applicazione del servizio precedente sostituito dalla copia. Il servizio [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] aggiorna il database dell'applicazione di servizio al nuovo schema.  
  
1.  In Amministrazione centrale SharePoint fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Trovare il [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] applicazioni di servizio, ad esempio "Default [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] applicazione di servizio", fare clic sul nome dell'applicazione del servizio e fare clic su **proprietà** nella barra multifunzione di SharePoint.  
  
3.  Aggiornare l'istanza del nome del server di database e il nome del database nei nomi corretti del database di cui sono stati eseguiti il backup, la copia e il ripristino. Una volta fatto clic su **OK**, il database dell'applicazione di servizio viene aggiornato. Gli errori verranno registrati nel log ULS.  
  
 **Aggiornare le pianificazioni di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]**  
  
 Configurare l'applicazione del servizio [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per l'esecuzione della migrazione di pianificazioni di aggiornamenti.  
  
-   **Eseguire la migrazione di pianificazioni option1: Amministratore della farm di SharePoint**  
  
    1.  Durante l'esecuzione di gestione SharePoint 2013 i `Set-PowerPivotServiceApplication` cmdlet con il `-StartMigratingRefreshSchedules` interruttore per abilitare automatica nella migrazione della pianificazione della domanda ![contenuto correlato di PowerShell](../../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "contenutocorrelatodiPowerShell"). Lo script di Windows PowerShell seguente presuppone la presenza di un'unica applicazione del servizio [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
        ```  
        $app=Get-PowerPivotServiceApplication  
        Set-PowerPivotServiceApplication $app -StartMigratingRefreshSchedules  
        ```  
  
         Dopo aver eseguito lo script di Windows PowerShell, le pianificazioni sono attive e verranno eseguite al momento appropriato successivo. Tuttavia, lo stato nella pagina di aggiornamento delle pianificazioni non è abilitato. Quando la pianificazione viene eseguita la prima volta, ne verrà eseguita la migrazione e nella pagina di aggiornamento delle pianificazioni verrà attivato lo stato **Abilitata**  .  
  
    2.  Se si desidera controllare il valore corrente della proprietà StartMigratingRefreshSchedules, eseguire lo script PowerShell riportato di seguito. Con script esegue un ciclo di tutti gli oggetti dell'applicazione del servizio [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e visualizza il nome e i valori delle proprietà:  
  
        ```  
        $apps = Get-PowerPivotServiceApplication  
        foreach ($app in $apps){}  
        Get-PowerPivotServiceApplication $appp | format-table -property displayname,id,StartMigratingRefreshSchedules  
        ```  
  
     **Eseguire la migrazione di pianificazioni option2: Utente aggiorna ogni cartella di lavoro**  
  
    1.  Un'altra opzione per eseguire la migrazione delle pianificazioni consiste nell'abilitare l'aggiornamento delle pianificazioni per ogni cartella di lavoro. Passare alla raccolta documenti contenente le cartelle di lavoro.  
  
    2.  Aprire il menu di scelta rapida e fare clic su **Gestisci [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]aggiornamento dati**.  
  
    3.  Nella sezione relativa **all'aggiornamento delle pianificazioni** fare clic su **Abilita**.  
  
    4.  È possibile selezionare **Aggiorna anche appena possibile**. Tramite questa opzione viene aggiunta un'istanza di aggiornamento alla coda non appena si fa clic su OK. La pianificazione dell'aggiornamento regolare viene tuttavia attivata al momento opportuno.  
  
    5.  Fare clic su **OK**. La cronologia di aggiornamento è ora visibile nella pagina degli aggiornamenti. La pianificazione verrà attivata al momento previsto.  
  
 **Cartelle di lavoro di SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]**  
  
-   Cartelle di lavoro di SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] non vengono aggiornate automaticamente se usate in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)][!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2013. Dopo la migrazione di un database del contenuto in cui sono incluse cartelle di lavoro di SQL Server 2008 R2, è possibile utilizzare le cartelle di lavoro ma le pianificazioni non vengono aggiornate.  
  
-   Per altre informazioni, vedere [Aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
##  <a name="bkmk_additional_resources"></a> Risorse aggiuntive  
  
> [!NOTE]  
>  Per ulteriori informazioni sull'aggiornamento del collegamento di un database SharePoint e [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , vedere gli argomenti seguenti:  
  
-   [Aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
-   [Panoramica del processo di aggiornamento a SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256688) (http://go.microsoft.com/fwlink/p/?LinkId=256688).  
  
-   [Pulire le preparazioni prima di un aggiornamento a SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256689) (http://go.microsoft.com/fwlink/p/?LinkId=256689).  
  
-   [Aggiornare i database da SharePoint 2010 a SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256690) (http://go.microsoft.com/fwlink/p/?LinkId=256690).  
  
  
