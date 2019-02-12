---
title: Aggiungere un ulteriore server di report a una farm (con scalabilità orizzontale SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: c1a6b683-15cf-44ae-ac60-ceee63a60aaf
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 03928e651b742061e726b9c92683d9d4e9aebd08
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56014832"
---
# <a name="add-an-additional-report-server-to-a-farm-ssrs-scale-out"></a>Aggiungere un ulteriore server di report a una farm (con scalabilità orizzontale SSRS)
  L'aggiunta di un secondo o altri server di report in modalità SharePoint alla farm di SharePoint può migliorare le prestazioni e il tempo di risposta dell'elaborazione del server di report. Se le prestazioni risultano rallentate dopo aver aggiunto altri utenti, report e applicazioni al server di report, l'aggiunta di ulteriori server di report può migliorare le prestazioni. È inoltre consigliabile aggiungere un secondo server di report per aumentare la disponibilità dei server di report in caso di problemi hardware o di manutenzione generale di singoli server di report nell'ambiente. A partire dalla versione [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , la procedura per la scalabilità orizzontale dell'ambiente [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint segue la distribuzione standard della farm di SharePoint e sfrutta le funzionalità di bilanciamento del carico di SharePoint.  
  
> [!IMPORTANT]  
>  La distribuzione con scalabilità orizzontale di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non è supportata in tutte le edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere la [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sezione del [funzionalità supportate dalle edizioni di SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
> [!TIP]  
>  A partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] non viene utilizzato Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per aggiungere server e per la scalabilità orizzontale dei server di report. Con i prodotti SharePoint è possibile gestire la distribuzione con scalabilità orizzontale di Reporting Services in quanto i server SharePoint con il servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] vengono aggiunti alla farm.  
  
 Per altre informazioni sul ridimensionamento dei server di report in modalità nativa, vedere [Configurare una distribuzione con scalabilità orizzontale di un server di report in modalità nativa &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md).  
  
-   [Bilanciamento del carico](#bkmk_loadbalancing)  
  
-   [Prerequisiti](#bkmk_prerequisites)  
  
-   [Passaggi](#bkmk_steps)  
  
-   [Configurazione aggiuntiva](#bkmk_additional)  
  
##  <a name="bkmk_loadbalancing"></a> Bilanciamento del carico  
 Il bilanciamento del carico di applicazioni del servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene gestito automaticamente da SharePoint, a meno che nell'ambiente sia presente una soluzione di bilanciamento del carico personalizzata o di terze parti. Secondo il comportamento predefinito del bilanciamento del carico di SharePoint, ogni applicazione del servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene bilanciata tra tutti i server applicazioni in cui è stato avviato il servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per verificare se il servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è installato e avviato, fare clic su **Gestisci servizi nel server** in Amministrazione centrale SharePoint.  
  
##  <a name="bkmk_prerequisites"></a> Prerequisiti  
  
-   Per eseguire il programma di installazione di SQL Server, è necessario essere un amministratore locale.  
  
-   Il computer deve fare parte di un dominio.  
  
-   È inoltre necessario conoscere il nome del server di database esistente che ospita i database di configurazione e del contenuto di SharePoint.  
  
-   Il server di database deve essere configurato in modo da consentire le connessioni ai database remoti.  In caso contrario, non sarà possibile creare un join del nuovo server alla farm, in quanto il nuovo server non sarà in grado di stabilire una connessione ai database di configurazione di SharePoint.  
  
-   Nel nuovo server dovrà essere installata la stessa versione di SharePoint in esecuzione sui server della farm correnti. Se nella farm è già installato, ad esempio, SharePoint 2010 Service Pack 1 (SP1), sarà necessario installare SP1 anche nel nuovo server prima di poterne creare un join alla farm.  
  
-   Esaminare gli argomenti aggiuntivi seguenti per comprendere i requisiti relativi al sistema e alla versione:  
  
     [Guida per l'utilizzo delle funzionalità di Business Intelligence di SQL Server in una farm di SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
##  <a name="bkmk_steps"></a> Passaggi  
 Nei passaggi di questo argomento si presuppone che l'installazione e la configurazione del server vengano eseguite da un amministratore della farm di SharePoint. Nel diagramma è illustrato un tipico ambiente a tre livelli e gli elementi numerati nel diagramma sono descritti nell'elenco seguente:  
  
-   (1) Più server front-end Web (WFE). I server front-end Web richiedono il componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per SharePoint 2010.  
  
-   (2) Un singolo server applicazioni che esegue [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e siti Web, ad esempio Amministrazione centrale. Nei passaggi seguenti viene aggiunto un secondo server applicazioni a questo livello.  
  
-   (3) Due server di database SQL Server.  
  
-   (4) Rappresenta una soluzione software o hardware di bilanciamento del carico di rete.  
  
 ![Aggiunta di un server applicazioni di Reporting Services](../../../2014/sql-server/install/media/rs-sharepointscale.gif "Aggiunta di un server applicazioni di Reporting Services")  
  
 Nei seguenti passaggi si presuppone che l'installazione e la configurazione del server vengano eseguite da un amministratore. Il server verrà configurato come nuovo server applicazioni nella farm e non verrà utilizzato come un front-end Web.  
  
|Passaggio|Descrizione e collegamento|  
|----------|--------------------------|  
|Eseguire l'Utilità preparazione prodotti SharePoint 2010.|È necessario disporre dei supporti di installazione di SharePoint 2010. L'utilità di preparazione corrisponde al file **PrerequisiteInstaller.exe** disponibile nei supporti di installazione.|  
|Installare un prodotto SharePoint 2010.|1) selezionare il **Server Farm** tipo di installazione.<br /><br /> 2) selezionare **completa** per il tipo di server.<br /><br /> 3) Una volta completata l'installazione, non eseguire la Configurazione guidata Prodotti SharePoint se nella farm di SharePoint esistente è installato SharePoint 2010 SP1. È necessario installare SharePoint SP1 prima di eseguire la Configurazione guidata Prodotti SharePoint.|  
|Installare SharePoint Server 2010 SP1.|Se nella farm di SharePoint esistente è installato SharePoint 2010 SP1 scaricare e installare SharePoint 2010 SP1 da:[https://support.microsoft.com/kb/2460045](https://go.microsoft.com/fwlink/p/?linkID=219697).<br /><br /> Per ulteriori informazioni su SharePoint 2010 SP1, vedere [Problemi noti durante l'installazione di Office 2010 SP1 e SharePoint 2010 SP1](https://support.microsoft.com/kb/2532126):|  
|Eseguire la Configurazione guidata Prodotti SharePoint per aggiungere il server alla farm.|1) nella **prodotti Microsoft SharePoint 2010** gruppo di programmi, fare clic su **configurazione guidata prodotti di Microsoft SharePoint 2010**.<br /><br /> 2) nella **Connetti a una Server Farm** pagina Scegli **Connetti a una Farm esistente** e fare clic su **Next**.<br /><br /> 3) nella **specifica impostazioni Database di configurazione** , digitare il nome del server di database utilizzato per la farm esistente e il nome del database di configurazione. Scegliere **Avanti**.<br />**\*\* Importanti \* \***  se viene visualizzato un messaggio di errore simile al seguente ed è stata verificata la disponibilità delle autorizzazioni, quindi verificare che i protocolli sono abilitati per la configurazione di rete SQL Server in **Sql Server Configuration Manager**: "Impossibile connettersi al server di database. Verificare che il database esista, sia un Sql Server e di disporre delle autorizzazioni appropriate per accedere al server."<br />**\*\* Importanti \* \***  se viene visualizzata la pagina **stato di Patch e prodotti nella Server Farm**, sarà necessario esaminare le informazioni nella pagina e aggiornare il server con i file necessari prima di continuare con aggiunge il server alla farm.<br /><br /> 4) nella **specifica impostazioni sicurezza Farm** digitare la passphrase della farm e fare clic su **successivo**. Scegliere **Avanti** nella pagina di configurazione per eseguire la procedura guidata.<br /><br /> 5) fare clic su **successivo** per eseguire il **configurazione guidata Farm**.|  
|Verificare che il server sia stato aggiunto alla farm di SharePoint.|1) Nel gruppo **Impostazioni di sistema** di Amministrazione centrale SharePoint fare clic su **Gestisci server della farm** .<br /><br /> 2) Verificare che il nuovo server sia stato aggiunto e che lo stato sia corretto.<br /><br /> 3) Nota Il servizio non viene visualizzata **servizio SQL Server Reporting Services** in esecuzione. Verrà installato nel passaggio successivo.<br /><br /> 4) per rimuovere questo server dal ruolo WFE, fare clic su **Gestisci servizi nel server** e arrestare il servizio **applicazione Web di Microsoft SharePoint Foundation**.|  
|Installare e configurare la modalità SharePoint di Reporting Services|Eseguire il programma di installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Per altre informazioni sull'installazione del [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modalità SharePoint, vedere [installare Reporting Services SharePoint Mode for SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md) se il server verrà utilizzato solo come un server applicazioni e il server verrà usati non come un server WFE, è necessario selezionare **componente aggiuntivo di Reporting Services per prodotti SharePoint** in:<br /><br /> il **ruolo di installazione** pagina, selezionare **installazione funzionalità SQL Server**<br /><br /> il **selezione delle caratteristiche** pagina, selezionare **Reporting Services - SharePoint**<br /><br /> oppure<br /><br /> il **configurazione di Reporting Services** verifica pagina le **solo installazione** sia selezionata l'opzione **Reporting Services SharePoint Mode**.|  
|Verificare che Reporting Services sia operativo.|1) Nel gruppo **Impostazioni di sistema** di Amministrazione centrale SharePoint fare clic su **Gestisci server della farm** .<br /><br /> 2) Verificare il **Servizio SQL Server Reporting Services**.<br /><br /> Per altre informazioni, vedere [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)|  
  
##  <a name="bkmk_additional"></a> Configurazione aggiuntiva  
 È possibile ottimizzare singoli server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in una distribuzione con scalabilità orizzontale solo per eseguire l'elaborazione in background, in modo da non condividere le risorse con esecuzione interattiva del report. Nell'elaborazione in background sono incluse pianificazioni, sottoscrizioni e avvisi dati.  
  
 Per modificare il comportamento di server di report singoli, impostare **\<IsWebServiceEnable>** su false nel file di configurazione **RSreportServer.config**.  
  
 Per impostazione predefinita, i server di report vengono configurati con \<IsWebServiceEnable> impostato su TRUE. Quando tutti i server sono configurati per TRUE, l'elaborazione interattiva e in background sarà con carico bilanciato in tutti i nodi nella farm.  
  
 Se si configurano tutti i server di report con \<IsWebServiceEnable> impostato su False, verrà visualizzato un messaggio di errore simile al seguente quando si tenterà di usare le funzionalità di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
 Il servizio Web Reporting Services non è abilitato. Configurare almeno un'istanza di servizio Reporting Services SharePoint avere \<IsWebServiceEnable > impostato su true. Per altre informazioni, vedere [Modificare un file di configurazione di Reporting Services&#40;RSreportserver.config&#41;](../report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere server web o applicazione server alle farm in SharePoint 2013](https://technet.microsoft.com/library/cc261752.aspx)   
 [Configurare i servizi (SharePoint Server 2010)](https://technet.microsoft.com/library/ee794878.aspx)  
  
  
