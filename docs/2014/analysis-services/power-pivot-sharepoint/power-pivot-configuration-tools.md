---
title: Strumenti di configurazione PowerPivot | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: f934c51d-01fe-4e67-971d-cd87d7d7ee51
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 133f5db597dfd56464678c52273e576e3493f172
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210870"
---
# <a name="powerpivot-configuration-tools"></a>PowerPivot Configuration Tools
  Configurare, ripristinare o rimuovere [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] con gli strumenti di configurazione PowerPivot.  
  
 L'Installazione guidata [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] consente di installare lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint 2010 e lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint 2013. In questo argomento viene descritto l'utilizzo generale dei due strumenti e le relative differenze.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 | SharePoint 2010  
  
 **Contenuto dell'argomento**  
  
-   [Requisiti per l'utilizzo degli strumenti di configurazione](#bkmk_requirements)  
  
-   [Due versioni dello strumento di configurazione](#bkmk_twoversions)  
  
-   [Panoramica dell'uso di uno strumento di configurazione PowerPivot](#bkmk_overview)  
  
-   [Avviare uno degli strumenti di configurazione PowerPivot](#bmkm_start_tool)  
  
##  <a name="bkmk_requirements"></a> Requisiti per l'utilizzo degli strumenti di configurazione  
  
-   È necessario essere un amministratore di farm.  
  
-   È necessario essere un amministratore del server nell'istanza di Analysis Services (solo SharePoint 2010).  
  
-   È necessario essere db_owner nel database di configurazione della farm.  
  
-   Non esistono requisiti della porta TCP/IP per l'utilizzo degli strumenti di configurazione, pertanto non dovrebbe essere necessario configurare il firewall per poterli utilizzare. Nello strumento di configurazione è previsto che le applicazioni Web e i servizi condivisi siano disponibili come parte della piattaforma SharePoint. Potrebbe essere necessario configurare il firewall per il server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Per altre informazioni, vedere [Configure the Windows Firewall to Allow Analysis Services Access](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
##  <a name="bkmk_twoversions"></a> Due versioni dello strumento di configurazione  
 Con l'installazione guidata [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] vengono installati lo strumento di configurazione PowerPivot per SharePoint 2010 e quello per SharePoint 2013.  
  
 Gli strumenti possono essere utilizzati solo con un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. Non utilizzarli con installazioni di [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .  
  
|nome|Versione supportata di SharePoint|Configurazione dettagliata|  
|----------|-------------------------------------|----------------------------|  
|configurazione di PowerPivot per SharePoint 2013|SharePoint 2013|[Configurare o ripristinare PowerPivot per SharePoint 2013 &#40;strumento di configurazione PowerPivot&#41;](configure-or-repair-power-pivot-for-sharepoint-2013.md)|  
|Strumento di configurazione PowerPivot|SharePoint 2010 con SharePoint 2010 Service Pack 1 (SP1)|[Configurare o ripristinare PowerPivot per SharePoint 2010 &#40;strumento di configurazione PowerPivot&#41;](../configure-repair-powerpivot-sharepoint-2010.md)|  
  
###  <a name="bkmk_sum_differences_betweentools"></a> Diversità tra i due strumenti di configurazione  
 Le due versioni dello strumento di configurazione sono simili ma esistono differenze nei passaggi di configurazione eseguiti dai due strumenti. Le differenze sono dovute alle modifiche tra SharePoint 2010 e SharePoint 2013 nonché alle differenze di architettura tra la versione SQL Server 2012 SP1 di PowerPivot per SharePoint e le versioni precedenti di PowerPivot per SharePoint.  
  
 Nella tabella seguente vengono descritte le funzionalità nuove e modificate nello strumento **Configurazione di PowerPivot per SharePoint 2013** . Nella tabella vengono descritte inoltre le funzionalità dello **strumento di configurazione PowerPivot** che non sono presenti nello strumento di configurazione di PowerPivot per SharePoint 2013. Le righe della tabella sono nello stesso ordine delle schede negli strumenti di configurazione.  
  
|Configurazione di PowerPivot per SharePoint 2013|Strumento di configurazione PowerPivot|  
|--------------------------------------------------|-----------------------------------|  
|La pagina principale contiene una nuova opzione per **Server PowerPivot per Excel Services**. L'opzione supporta la nuova architettura con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in esecuzione all'esterno della farm di SharePoint. Configurare Excel Services per utilizzare uno o più server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in esecuzione in modalità SharePoint.<br /><br /> ![PowerPivot Server nel nuovo strumento di configurazione](../media/as-powerpivot-configtool-differences-new-mainpage.gif "PowerPivot Server nel nuovo strumento di configurazione")||  
||Lo strumento 2010 include la pagina **registrare SQL Server Analysis Services (PowerPivot) sul Server locale** per configurare un'istanza locale di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Questa pagina non fa parte dello strumento 2013 perché non è presente alcuna istanza locale di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].<br /><br /> ![COME account del servizio nello strumento di configurazione precedente](../media/as-powerpivot-configtool-differences-old-register-as-localserver.gif "come account del servizio nello strumento di configurazione precedente")|  
||La pagina **Creare applicazione del servizio PowerPivot** contiene un'opzione aggiuntiva **Aggiorna le cartelle di lavoro per abilitare l'aggiornamento dati**. Questa opzione non è disponibile nello strumento 2013.<br /><br /> ![aggiornare le cartelle di lavoro nello strumento di configurazione precedente](../media/as-powerpivot-configtool-differences-old-uprgadeworkbooks.gif "aggiornare le cartelle di lavoro nello strumento di configurazione precedente")|  
|Lo strumento 2013 contiene una nuova pagina **Configura server PowerPivot**. Questa pagina supporta la nuova architettura di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in esecuzione all'esterno della farm di SharePoint. Per impostazione predefinita, il nome del server digitato nella pagina principale nella casella di testo **Server PowerPivot per Excel Services**viene elencato anche in **Configura server PowerPivot**.<br /><br /> ![Registrare PowerPivot server nuovo strumento di configurazione](../media/as-powerpivot-configtool-differences-new-powerpivot-servers.gif "PowerPivot registrare server nuovo strumento di configurazione")||  
|Lo strumento 2013 contiene una nuova pagina **Registra componente aggiuntivo di PowerPivot come Analisi utilizzo di Excel Services**. SharePoint 2010 Excel Services non tiene traccia dei dati sull'utilizzo di PowerPivot.||  
||Lo strumento 2010 include la pagina **Aggiungere MSOLAP.5 come provider attendibile** per registrare MSOLAP in modo da consentire a Excel Services in SharePoint 2010 di caricare i modelli PowerPivot. Questa pagina non fa parte dello strumento 2013. SharePoint 2013 Excel Services non utilizza il provider MSOLAP per caricare i modelli.|  
  
##  <a name="bkmk_overview"></a> Panoramica dell'uso di uno strumento di configurazione PowerPivot  
 All'avvio di uno strumento di configurazione PowerPivot, viene effettuata una valutazione dell'installazione esistente per determinare quali operazioni siano applicabili. In una nuova installazione, è disponibile solo l'attività di configurazione. Dopo la configurazione del server, verrà visualizzata l'attività di rimozione. Se si inizia con un'istanza di [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] , l'aggiornamento sarà anche abilitato nell'elenco delle attività disponibili.  
  
 Se non si ha familiarità con Amministrazione centrale o Windows PowerShell, è possibile eseguire lo strumento di configurazione come alternativa per completare un'installazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] .  
  
 Inoltre, lo strumento è in grado di rilevare se la farm è configurata o se alcune funzionalità obbligatorie sono mancanti. Se i file di programma di SharePoint sono installati ma la farm non è configurata, lo strumento rende disponibili azioni per configurare sia la farm, sia l'installazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] .  
  
 Per ulteriori informazioni sulla modalità di configurazione di PowerPivot e SharePoint tramite Windows PowerShell, esaminare la scheda **Script** . Per ulteriori informazioni, vedere quanto segue:  
  
-   [Configurazione di PowerPivot tramite Windows PowerShell](power-pivot-configuration-using-windows-powershell.md)  
  
-   [Informazioni di riferimento di PowerShell per PowerPivot per SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
  
> [!NOTE]
>  Reporting Services non viene configurato tramite lo strumento. Se si aggiunge Reporting Services all'ambiente di SharePoint, è necessario installarlo e configurarlo separatamente. Per ulteriori informazioni, vedere quanto segue:  
> 
>  -   [Installare Reporting Services SharePoint Mode for SharePoint 2013](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md).  
> -   [Installare la modalità SharePoint di Reporting Services per SharePoint 2010](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md).  
  
##  <a name="bmkm_start_tool"></a> Avviare uno degli strumenti di configurazione PowerPivot  
  
1.  Nel **avviare** digitare `powerpivot`  
  
     Nel **avviare** digitare `powerpivot` o scegliere il **Start** dal menu fare clic su **tutti i programmi**, fare clic su [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], fare clic su **gli strumenti di configurazione** , quindi fare clic su uno dei seguenti:  
  
    -   **Strumento di configurazione PowerPivot**.  
  
    -   **OR**  
  
    -   **Configurazione di PowerPivot per SharePoint 2013**.  
  
     ![Due strumenti di configurazione PowerPivot](../media/as-powerpivot-configtools-bothicons.gif "Due strumenti di configurazione PowerPivot")  
  
     **Nota:** Gli strumenti sono disponibili solo se [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] è installato nel server locale.  
  
2.  All'avvio, gli strumenti di configurazione controllano lo stato dell'installazione e rendono disponibili le attività valide per l'installazione.  
  
3.  A seconda dello stato corrente dell'installazione, è possibile eseguire una o più delle attività seguenti:  
  
    1.  Fare clic su **Configura o Ripristina PowerPivot per SharePoint** per completare le attività di post-installazione o ripristinare un'installazione.  
  
    2.  Fare clic su **Rimuovi funzionalità, servizi, applicazioni e soluzioni** per rimuovere funzionalità e soluzioni dalla farm.  
  
    3.  Fare clic su **Aggiorna funzionalità, servizi, applicazioni e soluzioni** per aggiornare funzionalità e soluzioni installate utilizzando una versione precedente di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].  
  
     Ad esempio, nella figura è illustrata la pagina iniziale dello strumento di configurazione PowerPivot per SharePoint 2013.  
  
     ![PowerPivot per SharePoint 2013 Configuration Tool](../media/ssas-powerpivot-configtool-4-sharepoint2013-choosemode.gif "PowerPivot per SharePoint 2013 Configuration Tool")  
  
 Ogni attività è costituita da singole azioni relative ad alcuni aspetti della configurazione del server. Ad esempio, l'attività di configurazione include azioni per la distribuzione delle soluzioni, la creazione di un'applicazione del servizio PowerPivot, l'attivazione delle funzionalità e la configurazione dell'aggiornamento dei dati. L'elenco delle azioni sarà diverso in base allo stato corrente dell'installazione. Se un'azione non è necessaria, viene esclusa dall'elenco attività.  
  
 Quando si fa clic su Esegui, lo strumento elabora tutte le azioni in modalità batch. Benché ogni azione sia visualizzata come elemento separato nell'elenco attività, tutte le azioni sono incluse insieme nel processo dell'attività. Vengono elaborate solo le azioni che superano un controllo di convalida. Potrebbe essere necessario aggiungere o modificare alcuni dei valori di input per superare il controllo di convalida.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Upgrade PowerPivot for SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md) Viene descritto il flusso di lavoro che aggiorna un'installazione esistente già presente in una farm.  
  
 [Uninstall PowerPivot for SharePoint](../../sql-server/install/uninstall-power-pivot-for-sharepoint.md) Viene descritto il flusso di lavoro che rimuove servizi, soluzioni e pagine di applicazioni di PowerPivot per SharePoint da una farm.  
  
 [Configurazione di PowerPivot tramite Windows PowerShell](power-pivot-configuration-using-windows-powershell.md)  
  
 [Amministrazione e configurazione del server PowerPivot in Amministrazione centrale](power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
