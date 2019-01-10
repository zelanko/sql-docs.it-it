---
title: Installare o disinstallare Power Pivot per componente aggiuntivo per SharePoint (SharePoint 2013) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1fdc41aaaad19317db3b3795cc63d137b19600c2
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52418512"
---
# <a name="install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013"></a>Installare o disinstallare il componente aggiuntivo Power Pivot per SharePoint (SharePoint 2013)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] è una raccolta di servizi back-end e componenti del server applicazioni che forniscono l'accesso a dati [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in una farm di [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)] . Il componente aggiuntivo [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint (**spPowerpivot.msi**) è un pacchetto di installazione utilizzato per installare i componenti del server applicazioni.  
  
-   Il componente aggiuntivo non è necessario per le distribuzioni di SharePoint 2010.  
  
-   Il componente aggiuntivo non è necessario in una distribuzione a server singolo che prevede SharePoint 2013 e [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità SharePoint. I componenti installati con il componente aggiuntivo vengono inclusi quando si installa un server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità SharePoint. Per esempi di distribuzione più complessi, vedere [Topologie di distribuzione per funzionalità di Business Intelligence di SQL Server in SharePoint](http://msdn.microsoft.com/library/39f76bc7-94e6-4dbc-bfa5-d56f4430bb26)  
  
 **Nota:** questo argomento fornisce informazioni sull'installazione dei file di soluzione [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e dello strumento di configurazione di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2013. Al termine dell'installazione, per informazioni sullo strumento di configurazione e sulle funzionalità aggiuntive, vedere [Configurare Power Pivot e distribuire soluzioni &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md).  
  
 Per informazioni su come scaricare **spPowerPivot.msi**, vedere la pagina relativa a [Microsoft® SQL Server® 2014 Power Pivot® per Microsoft SharePoint®](http://go.microsoft.com/fwlink/?LinkID=324854).  
  
##  <a name="bkmk_background"></a> Background  
  
-   **Server applicazioni:** [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in SharePoint 2013 sono inclusi l'uso delle cartelle di lavoro come origine dati, l'aggiornamento dati pianificato e il dashboard di gestione [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
     [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] è un pacchetto di Windows Installer [!INCLUDE[msCoName](../../../includes/msconame-md.md)] (**spPowerpivot.msi**) tramite il quale vengono distribuite le librerie client di Analysis Services e vengono copiati i file di installazione di [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] nel computer. Tramite il programma di installazione non vengono distribuite né configurate le funzionalità di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in SharePoint. I componenti seguenti vengono installati per impostazione predefinita:  
  
    -   [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013. In questo componente sono inclusi script di PowerShell (file con estensione ps1), pacchetti della soluzione SharePoint (con estensione wsp) e lo strumento di configurazione di [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013 per distribuire [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in una farm di SharePoint 2013.  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Provider OLE DB per Analysis Services (MSOLAP).  
  
    -   Provider di dati ADOMD.NET.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Analysis Management Objects.  
  
-   **Servizi back-end:** se si utilizza [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per Excel per creare cartelle di lavoro contenenti dati analitici, è necessario configurare Excel Services con un server BI in cui è eseguito [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità SharePoint per accedere a questi dati in un ambiente server. Il programma di installazione di SQL Server può essere eseguito in un computer in cui è installato SharePoint Server 2013 o in uno diverso in cui non è disponibile il software SharePoint. In Analysis Services non è presente alcuna dipendenza da SharePoint.  
  
     Per ulteriori informazioni sull'installazione, sulla disinstallazione e sulla configurazione di servizi back-end, vedere l'argomento seguente:  
  
    -   [Installazione di Analisi Services in modalità Power Pivot](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
    -   [Disinstallare PowerPivot per SharePoint](../../../sql-server/install/uninstall-power-pivot-for-sharepoint.md)  
  
##  <a name="bkmk_where_to_install"></a> Percorso in cui installare il file spPowerPivot.msi  
 Una procedura consigliata consiste nell'installare il file **spPowerPivot.msi** in tutti i server nella farm di SharePoint per coerenza di configurazione, inclusi i server applicazioni e quelli front-end Web. Nel pacchetto di installazione sono inclusi i provider di dati di Analysis Services, nonché lo strumento di configurazione di [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] . Quando si installa il file **spPowerPivot.msi** è possibile personalizzare l'installazione escludendo singoli componenti.  
  
 **Provider di dati:** in diverse tecnologie SharePoint e di SQL Server vengono utilizzati i provider di dati di Analysis Services, tra cui Excel Services, PerformancePoint Services e Power View. Installando il file **spPowerPivot.msi** in tutti i server SharePoint si garantiscono la disponibilità in modo coerente del set completo di provider di dati di Analysis Services e la connettività di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] nella farm.  
  
> [!NOTE]  
>  È necessario installare i provider di dati di Analysis Services in un server SharePoint 2013 tramite **spPowerPivot.msi**. Gli altri pacchetti di installazione disponibili in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Feature Pack non sono supportati in quanto in essi non sono inclusi i file di supporto di SharePoint 2013 richiesti dai provider di dati in questo ambiente.  
  
 **Strumento di configurazione:** Il [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2013 è obbligatorio in uno solo dei server SharePoint. Tuttavia, una procedura consigliata nelle farm con più server consiste nell'installare lo strumento di configurazione in almeno due server in modo da poter disporre dell'accesso allo strumento qualora uno dei due server sia offline.  
  
##  <a name="bkmk_prereq"></a> Requisiti e prerequisiti  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SharePoint Server 2013.  
  
-   Il file**spPowerPivot.msi** è solo a 64 bit, in base ai requisiti di prodotti e tecnologie SharePoint.  
  
-   Un server in [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] modalità. In Excel Services verrà usata l'istanza di SQL Server Analysis Services come server di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Analysis Services può essere eseguito nel computer locale o in uno remoto.  
  
-   **Autorizzazioni:** per installare [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)], è necessario che l'utente corrente sia un amministratore del computer e un membro del gruppo di amministratori farm di SharePoint.  
  
-   Per altre informazioni sui requisiti e prerequisiti di [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] , visitare la pagina relativa ai [Requisiti hardware e software per il server Analysis Services in modalità SharePoint](http://msdn.microsoft.com/library/fb86ca0a-518c-4c61-ae78-7680c57fae1f).  
  
##  <a name="bkmk_install"></a> Per disinstallare Power Pivot per SharePoint  
 Il pacchetto di installazione **spPowerpivot.msi** supporta sia la modalità interfaccia utente grafica sia quella da riga di comando. Per entrambi i metodi di installazione è richiesta l'esecuzione del file con estensione msi con privilegi di amministratore. Al termine dell'installazione, per informazioni sullo strumento di configurazione e sulle funzionalità aggiuntive, vedere [Configurare Power Pivot e distribuire soluzioni &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md).  
  
### <a name="user-interface-installation"></a>Installazione tramite l'interfaccia utente  
 Per installare [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] con l'interfaccia utente grafica, completare i passaggi seguenti:  
  
1.  Eseguire il file **SpPowerPivot.msi**.  
  
2.  Nella pagina introduttiva scegliere **Avanti** .  
  
3.  Leggere e accettare il Contratto di Licenza, quindi scegliere **Avanti**.  
  
4.  Nella pagina **Selezione funzionalità** tutte le funzionalità sono selezionate per impostazione predefinita.  
  
5.  Scegliere **Avanti**.  
  
6.  Fare clic su **Installa** per completare l'installazione.  
  
### <a name="command-line-installation"></a>Installazione dalla riga di comando  
 Per un'installazione dalla riga di comando, aprire un prompt dei comandi con autorizzazioni amministrative, quindi eseguire il file **spPowerPivot.msi**. Ad esempio:  
  
 `Msiexec.exe /i SpPowerPivot.msi`.  
  
 Per creare un log dell'installazione, utilizzare le opzioni di registrazione standard MsiExec. L'esempio seguente crea il file di log "Install_log" tramite l'opzione di registrazione dettagliata "v".  
  
```  
Msiexec.exe /i SpPowerPivot.msi /L v c:\test\Install_Log.txt  
```  
  
### <a name="quiet-command-line-installation-for-scripting"></a>Installazione dalla riga di comando non interattiva per lo scripting  
 È possibile usare le opzioni **/q** o **/quiet** per un'installazione non interattiva durante la quale non verranno visualizzati avvisi o finestre di dialogo. L'installazione non interattiva è utile se si desidera creare uno script dell'installazione del componente aggiuntivo.  
  
> [!IMPORTANT]  
>  Se si usa l'opzione **/q** per un'installazione da riga di comando invisibile all'utente, il contratto di licenza con l'utente finale non viene visualizzato. Indipendentemente dal metodo di installazione, l'utilizzo di questo software è governato da un contratto di licenza e l'utente è tenuto a rispettarlo.  
  
 **Per eseguire un'installazione non interattiva:**  
  
1.  Aprire un prompt dei comandi **con autorizzazioni di amministratore**.  
  
2.  Eseguire il comando seguente:  
  
    ```  
    Msiexec.exe /i spPowerPivot.msi /q  
    ```  
  
### <a name="command-line-installation-to-include-specific-components"></a>Installazione dalla riga di comando per includere componenti specifici  
 Lo strumento di configurazione di [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] non è obbligatorio nei server SharePoint, tuttavia se ne consiglia l'installazione in almeno due server in modo da renderlo disponibile quando necessario.  
  
 Quando si installa spPowerPivot.msi, è possibile utilizzare le opzioni della riga di comando per installare elementi specifici, ad esempio i provider di dati e non lo strumento di configurazione di [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] . La riga di comando seguente è un esempio di installazione di tutti i componenti, eccetto lo strumento di configurazione:  
  
```  
Msiexec /i spPowerPivot.msi AGREETOLICENSE="yes" ADDLOCAL=" SQL_OLAPDM,SQL_ADOMD,SQL_AMO,SQLAS_SP_Common"  
```  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|Analysis_Server_SP_addin|[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Configurazione|  
|SQL_OLAPDM|MSOLAP|  
|SQL_ADOMD|Provider ADOMD.net|  
|SQL_AMO|Provider AMO|  
|SQLAS_SP_Common|Componenti comuni di Analysis Services per SharePoint 2013|  
  
##  <a name="bkmk_deploy_solution"></a> Distribuire i file della soluzione di SharePoint con lo strumento di configurazione di Power Pivot per SharePoint 2013  
 Tre dei file copiati nel disco rigido tramite spPowerPivot.msi sono file di soluzione di SharePoint. L'ambito di un file della soluzione è il livello applicazione Web mentre quello degli altri file è il livello farm. I file sono i seguenti:  
  
-   `PowerPivotFarmSolution.wsp`  
  
-   `PowerPivotFarm14Solution.wsp`  
  
-   `PowerPivotWebApplicationSolution.wsp`  
  
 I file della soluzione vengono copiati nella cartella seguente:  
  
 `ssInstallPathTools\PowerPivotTools\SPAddinConfiguration\Resources`  
  
 Dopo l'installazione del file con estensione msi, eseguire lo strumento di configurazione di [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] per configurare e distribuire le soluzioni nella farm di SharePoint.  
  
 **Per avviare lo strumento di configurazione:**  
  
 Dalla schermata iniziale di Windows digitare "power" e nei risultati della ricerca delle App, fare clic su  **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2013**. I risultati della ricerca possono includere due collegamenti perché con l'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono installati separatamente gli strumenti di configurazione di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2010 e SharePoint 2013. Assicurarsi di avviare [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per lo strumento di configurazione di SharePoint 2013.  
  
 ![Due strumenti di configurazione PowerPivot](../../../analysis-services/instances/install-windows/media/as-powerpivot-configtools-bothicons.gif "Due strumenti di configurazione PowerPivot")  
  
 **Or**  
  
1.  Andare a **Start**, **Tutti i programmi**.  
  
2.  Fare clic su [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)].  
  
3.  Fare clic su **Strumenti di configurazione**.  
  
4.  Fare clic su Configurazione di **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2013**.  
  
 Per altre informazioni sullo strumento di configurazione, vedere [Strumenti di configurazione di Power Pivot](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
##  <a name="bkmk_remove_addin"></a> Disinstallare o ripristinare il componente aggiuntivo  
  
> [!CAUTION]  
>  Se si disinstalla **spPowerPivot.msi** , i provider di dati e lo strumento di configurazione vengono disinstallati. Disinstallando i provider di dati, non sarà più possibile connettere il server a [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)].  
  
 È possibile disinstallare o ripristinare [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] tramite uno dei metodi seguenti:  
  
1.  **Pannello di controllo di Windows:** Selezionare [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]  **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2013**. Fare clic su **Disinstalla** o **Ripristina**.  
  
2.  Eseguire spPowerPivot.msi e selezionare l'opzione **Rimuovi** o **Ripristina** .  
  
 **Riga di comando:** Per ripristinare o disinstallare [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2013 tramite la riga di comando, aprire un prompt dei comandi **con autorizzazioni di amministratore** ed eseguire uno dei seguenti comandi:  
  
-   Per effettuare il ripristino, eseguire il comando riportato di seguito:  
  
    ```  
    msiexec.exe /f spPowerPivot.msi  
    ```  
  
 o  
  
-   Per effettuare la disinstallazione, eseguire il comando riportato di seguito:  
  
    ```  
    msiexec.exe /uninstall spPowerPivot.msi  
    ```  
  
  
