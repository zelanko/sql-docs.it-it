---
title: Installare o disinstallare il componente aggiuntivo PowerPivot per SharePoint (SharePoint 2013) | Microsoft Docs
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
ms.openlocfilehash: f7a5abbb831d6630ebb7846534c7a9a96c83e861
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "72797372"
---
# <a name="install-or-uninstall-the-powerpivot-for-sharepoint-add-in-sharepoint-2013"></a>Installare o disinstallare il componente aggiuntivo PowerPivot per SharePoint (SharePoint 2013)
  
  [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] è una raccolta di servizi back-end e componenti del server applicazioni che forniscono l'accesso a dati [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in una farm di [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)] . Il componente aggiuntivo [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint (**spPowerpivot.msi**) è un pacchetto di installazione utilizzato per installare i componenti del server applicazioni.  
  
-   Il componente aggiuntivo non è necessario per le distribuzioni di SharePoint 2010.  
  
-   Il componente aggiuntivo non è necessario in una distribuzione a server singolo che prevede SharePoint 2013 e [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità SharePoint. I componenti installati con il componente aggiuntivo vengono inclusi quando si installa un server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità SharePoint. Per i diagrammi di distribuzioni di esempio con il componente aggiuntivo, vedere [topologie di distribuzione per SQL Server le funzionalità di business intelligence in SharePoint](../../../sql-server/install/deployment-topologies-for-sql-server-bi-features-in-sharepoint.md).  
  
 **Nota:** Questo argomento descrive l'installazione [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] dei file di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] soluzione e dello strumento di configurazione per SharePoint 2013. Al termine dell'installazione, vedere l'argomento seguente per informazioni sullo strumento di configurazione e sulle funzionalità aggiuntive, [configurare PowerPivot e distribuire soluzioni &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013).  
  
 Per informazioni su come scaricare **spPowerPivot.msi**, vedere la pagina relativa a [Microsoft® SQL Server® 2014 PowerPivot® per Microsoft SharePoint®](https://go.microsoft.com/fwlink/?LinkID=324854).  
  
 **In questo argomento**  
  
-   [Background](#bkmk_background)  
  
-   [Dove installare spPowerPivot. msi?](#bkmk_where_to_install)  
  
-   [Requisiti e prerequisiti](#bkmk_prereq)  
  
-   [Per installare PowerPivot per SharePoint](#bkmk_install)  
  
-   [Distribuire i file di soluzione di SharePoint con lo strumento di configurazione di PowerPivot per SharePoint 2013](#bkmk_deploy_solution)  
  
-   [Disinstallare o ripristinare il componente aggiuntivo](#bkmk_remove_addin)  
  
##  <a name="bkmk_background"></a> Background  
  
-   **Server applicazioni:** [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] la funzionalità di SharePoint 2013 include l'uso di cartelle di lavoro come origine dati, l'aggiornamento dati [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] pianificato e il dashboard di gestione.  
  
     [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)]è un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] pacchetto di Windows Installer (**spspPowerpivot. msi**) che distribuisce Analysis Services librerie client [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] e copia i file di installazione nel computer. Tramite il programma di installazione non vengono distribuite né configurate le funzionalità di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in SharePoint. I componenti seguenti vengono installati per impostazione predefinita:  
  
    -   
  [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013. In questo componente sono inclusi script di PowerShell (file con estensione ps1), pacchetti della soluzione SharePoint (con estensione wsp) e lo strumento di configurazione di [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013 per distribuire [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in una farm di SharePoint 2013.  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)]Provider di OLE DB per Analysis Services (MSOLAP).  
  
    -   Provider di dati ADOMD.NET.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Analysis Management Objects.  
  
-   **Servizi back-end:** Se si utilizza [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per Excel per creare cartelle di lavoro che contengono dati analitici, è necessario che Excel Services sia configurato con un server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] bi in esecuzione in modalità SharePoint per accedere a tali dati in un ambiente server. Il programma di installazione di SQL Server può essere eseguito in un computer in cui è installato SharePoint Server 2013 o in uno diverso in cui non è disponibile il software SharePoint. In Analysis Services non è presente alcuna dipendenza da SharePoint.  
  
     Per ulteriori informazioni sull'installazione, sulla disinstallazione e sulla configurazione di servizi back-end, vedere l'argomento seguente:  
  
    -   [PowerPivot for SharePoint 2013 Installation](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)  
  
    -   [Disinstallare PowerPivot per SharePoint](../../../sql-server/install/uninstall-power-pivot-for-sharepoint.md)  
  
##  <a name="bkmk_where_to_install"></a>Dove installare spPowerPivot. msi?  
 Una procedura consigliata consiste nell'installare il file **spPowerPivot.msi** in tutti i server nella farm di SharePoint per coerenza di configurazione, inclusi i server applicazioni e quelli front-end Web. Nel pacchetto di installazione sono inclusi i provider di dati di Analysis Services, nonché lo strumento di configurazione di [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] . Quando si installa il file **spPowerPivot.msi** è possibile personalizzare l'installazione escludendo singoli componenti.  
  
 **Provider di dati:** Diverse tecnologie SharePoint e SQL Server utilizzano i provider di dati Analysis Services, tra cui Excel Services, PerformancePoint Services e Power View. Installando il file **spPowerPivot.msi** in tutti i server SharePoint si garantiscono la disponibilità in modo coerente del set completo di provider di dati di Analysis Services e la connettività di PowerPivot nella farm.  
  
> [!NOTE]  
>  È necessario installare i provider di dati di Analysis Services in un server SharePoint 2013 tramite **spPowerPivot.msi**. Gli altri pacchetti di installazione disponibili in [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Feature Pack non sono supportati in quanto in essi non sono inclusi i file di supporto di SharePoint 2013 richiesti dai provider di dati in questo ambiente.  
  
 **Strumento di configurazione:** Lo strumento di configurazione PowerPivot per SharePoint 2013 è obbligatorio in uno solo dei server SharePoint. Tuttavia, una procedura consigliata nelle farm con più server consiste nell'installare lo strumento di configurazione in almeno due server in modo da poter disporre dell'accesso allo strumento qualora uno dei due server sia offline.  
  
##  <a name="bkmk_prereq"></a>Requisiti e prerequisiti  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)]SharePoint Server 2013.  
  
-   **spPowerPivot. msi** è solo a 64 bit, in base ai requisiti di prodotti e tecnologie SharePoint.  
  
-   Un server [!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)] in modalità PowerPivot. In Excel Services verrà utilizzata l'istanza di SQL Server Analysis Services come server di PowerPivot. Analysis Services può essere eseguito nel computer locale o in uno remoto.  
  
-   **Autorizzazioni:** Per installare [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)], è necessario che l'utente corrente sia un amministratore del computer e un gruppo di amministratori della farm di SharePoint.  
  
-   Per ulteriori informazioni sui [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] requisiti e i prerequisiti, vedere la pagina relativa ai [requisiti hardware e software per Analysis Services server in modalità SharePoint &#40;SQL Server 2014&#41;](../../../sql-server/install/hardware-software-requirements-analysis-services-server-sharepoint-mode.md).  
  
##  <a name="bkmk_install"></a>Per installare PowerPivot per SharePoint  
 Il pacchetto di installazione **spPowerpivot.msi** supporta sia la modalità interfaccia utente grafica sia quella da riga di comando. Per entrambi i metodi di installazione è richiesta l'esecuzione del file con estensione msi con privilegi di amministratore. Al termine dell'installazione, vedere l'argomento seguente per informazioni sullo strumento di configurazione e sulle funzionalità aggiuntive, [configurare PowerPivot e distribuire soluzioni &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013).  
  
### <a name="user-interface-installation"></a>Installazione tramite l'interfaccia utente  
 Per installare [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] con l'interfaccia utente grafica, completare i passaggi seguenti:  
  
1.  Eseguire il file **SpPowerPivot.msi**.  
  
2.  Nella pagina iniziale fare clic su **Avanti**.  
  
3.  Leggere e accettare il Contratto di Licenza, quindi scegliere **Avanti**.  
  
4.  Nella pagina **Selezione funzionalità** tutte le funzionalità sono selezionate per impostazione predefinita.  
  
5.  Fare clic su **Avanti**.  
  
6.  Fare clic su **Installa** per completare l'installazione.  
  
### <a name="command-line-installation"></a>Installazione dalla riga di comando  
 Per un'installazione dalla riga di comando, aprire un prompt dei comandi con autorizzazioni amministrative, quindi eseguire il file **spPowerPivot.msi**. Ad esempio:  
  
 `Msiexec.exe /i SpPowerPivot.msi`.  
  
 Per creare un log dell'installazione, utilizzare le opzioni di registrazione standard MsiExec. Nell'esempio seguente viene creato il file di log "Install_Log. txt" tramite l'opzione di registrazione dettagliata "v".  
  
```cmd
Msiexec.exe /i SpPowerPivot.msi /L v c:\test\Install_Log.txt  
```  
  
### <a name="quiet-command-line-installation-for-scripting"></a>Installazione dalla riga di comando non interattiva per lo scripting  
 È possibile usare le opzioni **/q** o **/quiet** per un'installazione non interattiva durante la quale non verranno visualizzati avvisi o finestre di dialogo. L'installazione non interattiva è utile se si desidera creare uno script dell'installazione del componente aggiuntivo.  
  
> [!IMPORTANT]  
>  Se si usa l'opzione **/q** per un'installazione da riga di comando invisibile all'utente, il contratto di licenza con l'utente finale non viene visualizzato. Indipendentemente dal metodo di installazione, l'utilizzo di questo software è governato da un contratto di licenza e l'utente è tenuto a rispettarlo.  
  
#### <a name="to-perform-a-quiet-installation"></a>Per eseguire un'installazione non interattiva
  
1.  Aprire un prompt dei comandi **con autorizzazioni di amministratore**.  
  
2.  Eseguire il comando seguente:  
  
    ```cmd
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
  
##  <a name="bkmk_deploy_solution"></a>Distribuire i file della soluzione di SharePoint con lo strumento di configurazione PowerPivot per SharePoint 2013  
 Tre dei file copiati nel disco rigido tramite spPowerPivot.msi sono file di soluzione di SharePoint. L'ambito di un file della soluzione è il livello applicazione Web mentre quello degli altri file è il livello farm. I file sono i seguenti:  
  
-   `PowerPivotFarmSolution.wsp`  
  
-   `PowerPivotFarm14Solution.wsp`  
  
-   `PowerPivotWebApplicationSolution.wsp`  
  
 I file della soluzione vengono copiati nella cartella seguente:  
  
 `C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\SPAddinConfiguration\Resources`  
  
 Dopo l'installazione del file con estensione msi, eseguire lo strumento di configurazione di [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] per configurare e distribuire le soluzioni nella farm di SharePoint.  
  
### <a name="to-start-the-configuration-tool"></a>Per avviare lo strumento di configurazione 
  
 Dalla schermata iniziale di Windows digitare "Power" e nei risultati di ricerca per le app fare clic su **configurazione di PowerPivot per SharePoint 2013**. I risultati della ricerca possono includere due collegamenti perché con l'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono installati separatamente gli strumenti di configurazione di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2010 e SharePoint 2013. Assicurarsi di avviare [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per lo strumento di configurazione di SharePoint 2013.  
  
 ![due strumenti di configurazione PowerPivot](https://docs.microsoft.com/analysis-services/analysis-services/media/as-powerpivot-configtools-bothicons.gif "due strumenti di configurazione PowerPivot")  
  
 **O**  
  
1.  Andare a **Start**, **Tutti i programmi**.  
  
2.  Fare clic su **Microsoft SQL Server 2014**.  
  
3.  Fare clic su **Strumenti di configurazione**.  
  
4.  Scegliere **Configurazione di PowerPivot per SharePoint 2013**.  
  
 Per ulteriori informazioni sullo strumento di configurazione, vedere [PowerPivot Configuration Tools](../../power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
##  <a name="bkmk_remove_addin"></a>Disinstallare o ripristinare il componente aggiuntivo  
  
> [!CAUTION]  
>  Se si disinstalla **spPowerPivot.msi** , i provider di dati e lo strumento di configurazione vengono disinstallati. Disinstallando i provider di dati, non sarà più possibile connettere il server a PowerPivot.  
  
 È possibile disinstallare o ripristinare [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] tramite uno dei metodi seguenti:  
  
1.  **Pannello di controllo di Windows:** Selezionare **Microsoft SQL Server 2012 PowerPivot per SharePoint 2013**. Fare clic su **Disinstalla** o **Ripristina**.  
  
2.  Eseguire spPowerPivot.msi e selezionare l'opzione **Rimuovi** o **Ripristina** .  
  
 **Riga di comando:** Per ripristinare o disinstallare PowerPivot per SharePoint 2013 usando la riga di comando, aprire un prompt dei comandi **con autorizzazioni di amministratore** ed eseguire uno dei comandi seguenti:  
  
-   Per effettuare il ripristino, eseguire il comando riportato di seguito:  
  
    ```cmd
    msiexec.exe /f spPowerPivot.msi  
    ```  
  
 o  
  
-   Per effettuare la disinstallazione, eseguire il comando riportato di seguito:  
  
    ```cmd
    msiexec.exe /uninstall spPowerPivot.msi  
    ```
