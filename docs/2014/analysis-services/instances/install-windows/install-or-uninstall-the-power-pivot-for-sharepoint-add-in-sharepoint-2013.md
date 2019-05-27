---
title: Installare o disinstallare PowerPivot per componente aggiuntivo per SharePoint (SharePoint 2013) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: fe13ce8b-9369-4126-928a-9426f9119424
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b1fb1e718f8b2ab0257651ff47674d293a9e6a95
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079878"
---
# <a name="install-or-uninstall-the-powerpivot-for-sharepoint-add-in-sharepoint-2013"></a>Installare o disinstallare il componente aggiuntivo PowerPivot per SharePoint (SharePoint 2013)
  [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] è una raccolta di servizi back-end e componenti del server applicazioni che forniscono l'accesso a dati [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in una farm di [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)] . Il componente aggiuntivo [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint (**spPowerpivot.msi**) è un pacchetto di installazione utilizzato per installare i componenti del server applicazioni.  
  
-   Il componente aggiuntivo non è necessario per le distribuzioni di SharePoint 2010.  
  
-   Il componente aggiuntivo non è necessario in una distribuzione a server singolo che prevede SharePoint 2013 e [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità SharePoint. I componenti installati con il componente aggiuntivo vengono inclusi quando si installa un server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità SharePoint. Per i diagrammi delle distribuzioni di esempio con il componente aggiuntivo, vedere [topologie di distribuzione per le funzionalità di SQL Server BI in SharePoint](../../../sql-server/install/deployment-topologies-for-sql-server-bi-features-in-sharepoint.md).  
  
 **Nota:** In questo argomento viene descritto come installare il [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] file di soluzione e [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per lo strumento di configurazione di SharePoint 2013. Dopo l'installazione, vedere l'argomento seguente per informazioni su strumento di configurazione e sulle funzionalità aggiuntive [configurare PowerPivot e distribuire soluzioni &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md).  
  
 Per informazioni su come scaricare **spPowerPivot.msi**, vedere la pagina relativa a [Microsoft® SQL Server® 2014 PowerPivot® per Microsoft SharePoint®](https://go.microsoft.com/fwlink/?LinkID=324854).  
  
 **Contenuto dell'argomento:**  
  
-   [Background](#bkmk_background)  
  
-   [Percorso in cui installare il file spPowerPivot.msi](#bkmk_where_to_install)  
  
-   [Requisiti e prerequisiti](#bkmk_prereq)  
  
-   [Per installare PowerPivot per SharePoint](#bkmk_install)  
  
-   [Distribuire i file di soluzione SharePoint con PowerPivot per SharePoint 2013 Configuration Tool](#bkmk_deploy_solution)  
  
-   [Disinstallare o ripristinare il componente aggiuntivo](#bkmk_remove_addin)  
  
##  <a name="bkmk_background"></a> Background  
  
-   **Server applicazioni:** [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in SharePoint 2013 sono inclusi l'uso delle cartelle di lavoro come origine dati, l'aggiornamento dati pianificato e il dashboard di gestione [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
     [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] è un pacchetto di Windows Installer [!INCLUDE[msCoName](../../../includes/msconame-md.md)] (**spPowerpivot.msi**) tramite il quale vengono distribuite le librerie client di Analysis Services e vengono copiati i file di installazione di [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] nel computer. Tramite il programma di installazione non vengono distribuite né configurate le funzionalità di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in SharePoint. I componenti seguenti vengono installati per impostazione predefinita:  
  
    -   [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013. In questo componente sono inclusi script di PowerShell (file con estensione ps1), pacchetti della soluzione SharePoint (con estensione wsp) e lo strumento di configurazione di [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013 per distribuire [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in una farm di SharePoint 2013.  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Provider OLE DB per Analysis Services (MSOLAP).  
  
    -   Provider di dati ADOMD.NET.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Analysis Management Objects.  
  
-   **Servizi back-end:** Se si usa [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per Excel creare le cartelle di lavoro contenenti dati analitici, è necessario configurare Excel Services con un server BI che esegue [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità SharePoint per accedere ai dati in un ambiente server. Il programma di installazione di SQL Server può essere eseguito in un computer in cui è installato SharePoint Server 2013 o in uno diverso in cui non è disponibile il software SharePoint. In Analysis Services non è presente alcuna dipendenza da SharePoint.  
  
     Per ulteriori informazioni sull'installazione, sulla disinstallazione e sulla configurazione di servizi back-end, vedere l'argomento seguente:  
  
    -   [Installazione di PowerPivot per SharePoint 2013](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
    -   [Disinstallare PowerPivot per SharePoint](../../../sql-server/install/uninstall-power-pivot-for-sharepoint.md)  
  
##  <a name="bkmk_where_to_install"></a> Percorso in cui installare il file spPowerPivot.msi  
 Una procedura consigliata consiste nell'installare il file **spPowerPivot.msi** in tutti i server nella farm di SharePoint per coerenza di configurazione, inclusi i server applicazioni e quelli front-end Web. Nel pacchetto di installazione sono inclusi i provider di dati di Analysis Services, nonché lo strumento di configurazione di [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] . Quando si installa il file **spPowerPivot.msi** è possibile personalizzare l'installazione escludendo singoli componenti.  
  
 **Provider di dati:** Diverse tecnologie SharePoint e SQL Server usano il provider di dati di Analysis Services tra cui Excel Services, PerformancePoint Services e Power View. Installando il file **spPowerPivot.msi** in tutti i server SharePoint si garantiscono la disponibilità in modo coerente del set completo di provider di dati di Analysis Services e la connettività di PowerPivot nella farm.  
  
> [!NOTE]  
>  È necessario installare i provider di dati di Analysis Services in un server SharePoint 2013 tramite **spPowerPivot.msi**. Gli altri pacchetti di installazione disponibili in [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Feature Pack non sono supportati in quanto in essi non sono inclusi i file di supporto di SharePoint 2013 richiesti dai provider di dati in questo ambiente.  
  
 **Strumento di configurazione:** PowerPivot per SharePoint 2013 lo strumento di configurazione è obbligatorio in uno solo dei server SharePoint. Tuttavia, una procedura consigliata nelle farm con più server consiste nell'installare lo strumento di configurazione in almeno due server in modo da poter disporre dell'accesso allo strumento qualora uno dei due server sia offline.  
  
##  <a name="bkmk_prereq"></a> Requisiti e prerequisiti  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SharePoint Server 2013.  
  
-   Il file**spPowerPivot.msi** è solo a 64 bit, in base ai requisiti di prodotti e tecnologie SharePoint.  
  
-   Un server [!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)] in modalità PowerPivot. In Excel Services verrà utilizzata l'istanza di SQL Server Analysis Services come server di PowerPivot. Analysis Services può essere eseguito nel computer locale o in uno remoto.  
  
-   **Autorizzazioni:** Per installare [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)], è necessario che l'utente corrente sia un amministratore del computer e un gruppo di amministratori Farm di SharePoint.  
  
-   Per ulteriori informazioni sul [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] requisiti e prerequisiti, passare a [requisiti Hardware e Software per Server di Analysis Services in modalità SharePoint &#40;SQL Server 2014&#41;](../../../sql-server/install/hardware-software-requirements-analysis-services-server-sharepoint-mode.md).  
  
##  <a name="bkmk_install"></a> Per installare PowerPivot per SharePoint  
 Il pacchetto di installazione **spPowerpivot.msi** supporta sia la modalità interfaccia utente grafica sia quella da riga di comando. Per entrambi i metodi di installazione è richiesta l'esecuzione del file con estensione msi con privilegi di amministratore. Dopo l'installazione, vedere l'argomento seguente per informazioni su strumento di configurazione e sulle funzionalità aggiuntive [configurare PowerPivot e distribuire soluzioni &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md).  
  
### <a name="user-interface-installation"></a>Installazione tramite l'interfaccia utente  
 Per installare [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] con l'interfaccia utente grafica, completare i passaggi seguenti:  
  
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
 Lo strumento di configurazione di [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] non è obbligatorio nei server SharePoint, tuttavia se ne consiglia l'installazione in almeno due server in modo da renderlo disponibile quando necessario.  
  
 Quando si installa spPowerPivot.msi, è possibile utilizzare le opzioni della riga di comando per installare elementi specifici, ad esempio i provider di dati e non lo strumento di configurazione di [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] . La riga di comando seguente è un esempio di installazione di tutti i componenti, eccetto lo strumento di configurazione:  
  
```  
Msiexec /i spPowerPivot.msi AGREETOLICENSE="yes" ADDLOCAL=" SQL_OLAPDM,SQL_ADOMD,SQL_AMO,SQLAS_SP_Common"  
```  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|Analysis_Server_SP_addin|Configurazione di PowerPivot|  
|SQL_OLAPDM|MSOLAP|  
|SQL_ADOMD|Provider ADOMD.net|  
|SQL_AMO|Provider AMO|  
|SQLAS_SP_Common|Componenti comuni di Analysis Services per SharePoint 2013|  
  
##  <a name="bkmk_deploy_solution"></a> Distribuire i file di soluzione SharePoint con PowerPivot per SharePoint 2013 Configuration Tool  
 Tre dei file copiati nel disco rigido tramite spPowerPivot.msi sono file di soluzione di SharePoint. L'ambito di un file della soluzione è il livello applicazione Web mentre quello degli altri file è il livello farm. I file sono i seguenti:  
  
-   `PowerPivotFarmSolution.wsp`  
  
-   `PowerPivotFarm14Solution.wsp`  
  
-   `PowerPivotWebApplicationSolution.wsp`  
  
 I file della soluzione vengono copiati nella cartella seguente:  
  
 `C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\SPAddinConfiguration\Resources`  
  
 Dopo l'installazione del file con estensione msi, eseguire lo strumento di configurazione di [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] per configurare e distribuire le soluzioni nella farm di SharePoint.  
  
 **Per avviare lo strumento di configurazione:**  
  
 Dalla schermata iniziale di Windows digitare "power" e nei risultati della ricerca delle App, fare clic su **PowerPivot per SharePoint 2013**. I risultati della ricerca possono includere due collegamenti perché con l'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono installati separatamente gli strumenti di configurazione di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2010 e SharePoint 2013. Assicurarsi di avviare [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per lo strumento di configurazione di SharePoint 2013.  
  
 ![due strumenti di configurazione di powerpivot](../../../analysis-services/media/as-powerpivot-configtools-bothicons.gif "due strumenti di configurazione powerpivot")  
  
 **Or**  
  
1.  Andare a **Start**, **Tutti i programmi**.  
  
2.  Fare clic su **Microsoft SQL Server 2014**.  
  
3.  Fare clic su **Strumenti di configurazione**.  
  
4.  Scegliere **Configurazione di PowerPivot per SharePoint 2013**.  
  
 Per ulteriori informazioni sullo strumento di configurazione, vedere [PowerPivot Configuration Tools](../../power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
##  <a name="bkmk_remove_addin"></a> Disinstallare o ripristinare il componente aggiuntivo  
  
> [!CAUTION]  
>  Se si disinstalla **spPowerPivot.msi** , i provider di dati e lo strumento di configurazione vengono disinstallati. Disinstallando i provider di dati, non sarà più possibile connettere il server a PowerPivot.  
  
 È possibile disinstallare o ripristinare [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] tramite uno dei metodi seguenti:  
  
1.  **Pannello di controllo di Windows:** Selezionare **Microsoft SQL Server 2012 PowerPivot per SharePoint 2013**. Fare clic su **Disinstalla** o **Ripristina**.  
  
2.  Eseguire spPowerPivot.msi e selezionare l'opzione **Rimuovi** o **Ripristina** .  
  
 **Riga di comando:** Per ripristinare o disinstallare PowerPivot per SharePoint 2013 tramite la riga di comando, aprire un prompt dei comandi **con autorizzazioni di amministratore** ed eseguire uno dei seguenti comandi:  
  
-   Per effettuare il ripristino, eseguire il comando riportato di seguito:  
  
    ```  
    msiexec.exe /f spPowerPivot.msi  
    ```  
  
 o  
  
-   Per effettuare la disinstallazione, eseguire il comando riportato di seguito:  
  
    ```  
    msiexec.exe /uninstall spPowerPivot.msi  
    ```  
  
  
