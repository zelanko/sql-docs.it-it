---
title: Installare le funzionalità di business intelligence di SQL Server con SharePoint (PowerPivot e Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3166107c-30c2-468e-bb1b-bb42b79b37c3
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 954f60e49f5bc94881fcdf66b7a381385fb40416
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890147"
---
# <a name="install-sql-server-bi-features-with-sharepoint-powerpivot-and-reporting-services"></a>Installare le funzionalità di Business Intelligence di SQL Server con SharePoint (PowerPivot e Reporting Services)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] possono essere integrati con una farm di Microsoft SharePoint per abilitare le funzionalità di Business Intelligence (BI) in SharePoint. Tra le funzionalità sono inclusi [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]viene utilizzato per [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] l'accesso ai dati in una farm di SharePoint. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] è il motore dati per le cartelle di lavoro create in [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per Excel a cui si accede da una raccolta di SharePoint. Una volta salvata una cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in SharePoint, è possibile utilizzarla come origine dati per i report [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] .  
  
 Alcuni dei passaggi di installazione e configurazione necessari per SharePoint 2010 sono diversi dai passaggi necessari per SharePoint 2013. Alcuni argomenti di questa sezione si applicano a entrambe le versioni di SharePoint.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|  
  
 ![Nota](../../../2014/reporting-services/media/rs-fyinote.png "Nota") Per le note sulla versione correnti, vedere le [Note sulla versione di SQL server 2014](https://go.microsoft.com/fwlink/?LinkID=296445).  
  
##  <a name="bkmk_top"></a> Contenuto dell'argomento  
  
-   [Scenari di SQL Server BI e SharePoint 2013](#bkmk_bi_scenarios)  
  
-   [Panoramica dell'installazione](#bkmk_install_sharepoint2013_overview)  
  
## <a name="in-this-section"></a>In questa sezione  
 Oltre alle informazioni di questo argomento, in questa sezione del contenuto sono presenti i seguenti argomenti correlati.  
  
 [Topologie di distribuzione per funzionalità di Business Intelligence di SQL Server in SharePoint](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)  
  
 [Guida per l'utilizzo delle funzionalità di Business Intelligence di SQL Server in una farm di SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
 [Elenchi di controllo per l'installazione delle funzionalità di Business Intelligence con SharePoint](../../../2014/sql-server/install/checklists-for-installing-bi-features-with-sharepoint.md)  
  
 [Installazione &#40;in modalità sharepoint di Reporting Services SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)  
  
 [Installazione di PowerPivot per SharePoint 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)  
  
 [Installazione di PowerPivot per SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
##  <a name="bkmk_bi_scenarios"></a>Scenari di SQL Server BI e SharePoint 2013  
 In questa sezione vengono riepilogati i diversi livelli di funzionalità di Business Intelligence che è possibile scegliere di installare e configurare.  
  
 In Excel Services in SharePoint 2013 è inclusa la funzionalità del modello di dati per abilitare l'interazione con una cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nel browser. Per la funzionalità del modello di dati di base non è necessario distribuire il componente aggiuntivo [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 nella farm. È sufficiente installare un server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità SharePoint e registrarlo nelle impostazioni **Modello di dati** di Excel Services.  
  
 Tramite la distribuzione del componente aggiuntivo [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 vengono abilitate le funzionalità aggiuntive nella farm SharePoint in uso. Tra le funzionalità aggiuntive sono incluse la raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , la pianificazione dell'aggiornamento dati e il dashboard di gestione di PowerPivot. Per ulteriori informazioni, vedere la tabella.  
  
||Level|Funzionalità|Installazione o configurazione|  
|-|-----------|--------------|--------------------------|  
|1|Solo SharePoint|Funzionalità native di Excel Services|Excel Services e altri servizi inclusi in SharePoint Server 2013.|  
|**2**|SharePoint con Analysis Services in modalità SharePoint|Cartelle di lavoro interattive di PowerPivot nel browser|Installare [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità SharePoint.<br /><br /> Registrare il server Analysis Services in Excel Services.|  
|**3**|SharePoint con Reporting Services in modalità SharePoint|Power View|Installare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint.<br /><br /> Installare il componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **(rsSharePoint.msi)** per SharePoint. Per ulteriori informazioni, vedere [installare o disinstallare il componente aggiuntivo Reporting Services per SharePoint &#40;SharePoint 2010 e SharePoint 2013&#41; ](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)|  
|**4**|Tutte le funzionalità di PowerPivot|Accedere alle cartelle di lavoro come origine dati dall'esterno della farm.<br /><br /> Pianificare l'aggiornamento dati.<br /><br /> Raccolta PowerPivot.<br /><br /> Dashboard di gestione.<br /><br /> Tipo di contenuto del file di collegamento BISM.|Distribuire il componente aggiuntivo PowerPivot per SharePoint 2013 **(spPowerPivot.msi)** . Per ulteriori informazioni, vedere quanto segue:<br /><br /> [Installare o disinstallare il componente aggiuntivo PowerPivot per SharePoint &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)<br /><br /> Per informazioni su come scaricare **spPowerPivot.msi**, vedere [Scaricare SQL Server 2014 PowerPivot per SharePoint](https://go.microsoft.com/fwlink/?LinkID=296473).|  
  
 Per ulteriori informazioni sull'abilitazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] delle funzionalità, vedere la pagina relativa a [SQL Server BI Light-up Story per SharePoint 2013](https://blogs.msdn.com/b/analysisservices/archive/2012/07/27/introducing-the-bi-light-up-story-for-sharepoint-2013.aspx) (. https://blogs.msdn.com/b/analysisservices/archive/2012/07/27/introducing-the-bi-light-up-story-for-sharepoint-2013.aspx)  
  
##  <a name="bkmk_install_sharepoint2013_overview"></a>Panoramica dell'installazione  
 Se si desidera utilizzare [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], eseguire due volte l'Installazione guidata di SQL Server. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] sono opzioni separate nella pagina **impostazione ruolo** dell'installazione guidata di SQL Server.  
  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] supporta sia SharePoint 2010 sia SharePoint 2013; tuttavia si utilizza un'architettura e un processo di installazione differenti a seconda della versione di SharePoint.  
  
 Di seguito viene riportato un riepilogo dei passaggi di installazione per distribuire le funzionalità di Business Intelligence per [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] in un unico server:  
  
 **[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013**  
  
 Per **SharePoint 2013**, l'installazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] può essere eseguita in un server in cui non è installato un prodotto SharePoint. L'architettura di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] utilizzata per SharePoint 2013 viene eseguita **all'esterno** della farm SharePoint e può essere installata in un server contenente anche un'installazione di SharePoint. In alternativa, può essere installata in un server in cui NON è contenuta un'installazione di SharePoint.  
  
1.  Installare SharePoint Server 2013 e abilitare Excel Services.  
  
2.  Installare [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità SharePoint e concedere agli account dei servizi e della farm di SharePoint i diritti di amministratore di server in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
     Per entrambe le versioni di SharePoint, il processo di installazione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] inizia con la selezione del ruolo di impostazione di **SQL Server PowerPivot per SharePoint** nell'installazione guidata di SQL Server. In alternativa, utilizzare un'installazione dal prompt dei comandi di SQL Server.  
  
     ![Impostazione del ruolo](../../../2014/sql-server/install/media/gmni-setupui-featurerole-sql2012sp1.gif "Impostazione del ruolo")  
  
3.  Per SharePoint 2013, è possibile estendere le funzionalità e l'esperienza di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Scaricare ed eseguire **spPowerPivot.msi** per aggiungere il supporto di gestione, collaborazione ed elaborazione dell'aggiornamento dati lato server per la cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Per ulteriori informazioni, vedere [Microsoft SQL Server 2014 PowerPivot per Microsoft SharePoint](https://go.microsoft.com/fwlink/?LinkID=324854).  
  
     Eseguire il pacchetto di installazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013, **spPowerPivot.msi** , in ogni server nella farm SharePoint per garantire la versione corretta dei provider di dati installati.  
  
4.  Per configurare [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint 2013, utilizzare lo strumento **Configurazione di PowerPivot per SharePoint 2013** .  
  
     Con l'Installazione guidata di SQL Server vengono installati due strumenti di configurazione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Uno degli strumenti di configurazione supporta SharePoint 2013 e l'altro supporta SharePoint 2010.  
  
     ![Due strumenti di configurazione PowerPivot](https://docs.microsoft.com/analysis-services/analysis-services/media/as-powerpivot-configtools-bothicons.gif "Due strumenti di configurazione PowerPivot")  
  
5.  Configurare Excel Services in SharePoint Server 2013 l'utilizzo dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Per ulteriori informazioni, vedere la sezione "configurare l'integrazione di base Analysis Services SharePoint" nell' [installazione di PowerPivot per SharePoint 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode). e [gestire le impostazioni del modello di dati di Excel Services (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780.aspx) (https://technet.microsoft.com/library/jj219780.aspx).  
  
6.  Per ulteriori informazioni, vedere [PowerPivot for SharePoint 2013 Installation](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode).  
  
 **[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010**  
  
 Per SharePoint 2010, è necessario che l'installazione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint venga eseguita in un server in cui è già installato o verrà installato SharePoint 2010. L'architettura di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint 2010 viene eseguita **all'interno** della farm e richiede la presenza di SharePoint nel server in cui è installato [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint.  
  
1.  Installare [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità SharePoint e concedere agli account dei servizi e della farm di SharePoint i diritti di amministratore di server in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
     Una distribuzione di SharePoint 2010 non supporta spPowerPivot.msi e il file con estensione msi **non** è richiesto con SharePoint 2010.  
  
     Per entrambe le versioni di SharePoint, il processo di installazione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] inizia con la selezione del ruolo di impostazione di **SQL Server PowerPivot per SharePoint** nell'installazione guidata di SQL Server. In alternativa, utilizzare un'installazione dal prompt dei comandi di SQL Server.  
  
2.  Con l'Installazione guidata di SQL Server vengono installati due strumenti di configurazione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Uno degli strumenti di configurazione supporta SharePoint 2013 e l'altro supporta SharePoint 2010.  
  
     Per configurare [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint 2010, usare lo **strumento di configurazione PowerPivot** .  
  
3.  Per ulteriori informazioni, vedere [PowerPivot for SharePoint 2010 Installation](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md).  
  
 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**  per SharePoint 2010 e 2013  
  
1.  L'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint rimane invariata dalla versione precedente.  
  
     I passaggi di installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per SharePoint 2010 e SharePoint 2013 sono molto simili. Le note importanti relativamente alle versioni di SharePoint sono:  
  
    -   Vedere le combinazioni supportate dei prodotti seguenti:  
  
        -   Versione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
        -   Componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per prodotti SharePoint.  
  
        -   Versione del prodotto SharePoint.  
  
         [Combinazioni supportate di SharePoint e Reporting Services server e del componente aggiuntivo &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
    -   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] su SharePoint 2010 richiede SharePoint 2010 Service Pack 2 (SP2).  
  
    1.  Installare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint. [Reporting Services l' &#40;installazione in modalità SharePoint di SharePoint 2010&#41; e SharePoint 2013](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md) e [installare Reporting Services modalità SharePoint per SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md).  
  
    2.  Installare il componente aggiuntivo di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per i prodotti SharePoint (rsSharePoint.msi). Vedere [installare o disinstallare il componente aggiuntivo Reporting Services per SharePoint &#40;SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md). Per la versione corrente del [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] componente aggiuntivo per SharePoint, vedere [dove trovare il componente aggiuntivo Reporting Services per prodotti SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
    3.  Configurare il servizio SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e almeno un'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per ulteriori informazioni, vedere la sezione "creare un'applicazione di servizio Reporting Services" in [installare Reporting Services modalità SharePoint per sharepoint 2013](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md).  
  
##  <a name="bkm_database_attach"></a>Panoramica dell'aggiornamento del montaggio del database e di SharePoint 2013  
 SharePoint 2013 non supporta l'aggiornamento sul posto. Tuttavia, l' **aggiornamento del collegamento di un database è supportato**.  
  
 Se si dispone di un'installazione di PowerPivot esistente integrata con SharePoint 2010, non è possibile eseguire l'aggiornamento sul posto del server SharePoint.  Tuttavia, è possibile completare i passaggi seguenti come parte dell'aggiornamento del collegamento di un database di SharePoint:  
  
1.  Installare una nuova farm di SharePoint Server 2013.  
  
2.  Eseguire un aggiornamento del collegamento di un database di SharePoint e la migrazione dei database del contenuto correlati a PowerPivot nella farm di SharePoint 2013.  
  
3.  Installare un'istanza di SQL Server Analysis Services in modalità SharePoint e concedere agli account dei servizi e della farm di SharePoint i diritti di amministratore di server in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
4.  Installare il pacchetto di installazione di PowerPivot per SharePoint 2013 **spPowerPivot.msi** in ogni server nella farm di SharePoint.  
  
5.  In Amministrazione centrale SharePoint 2013 configurare Excel Services per l'utilizzo del server Analysis Services in esecuzione in modalità SharePoint creato nel passaggio 3.  
  
     Per eseguire la migrazione delle pianificazioni di aggiornamento, configurare l'applicazione di servizio PowerPivot.  
  
> [!NOTE]  
>  Per ulteriori informazioni sull'aggiornamento del collegamento di un database di PowerPivot e SharePoint, vedere gli argomenti seguenti:  
  
-   [Eseguire la migrazione di PowerPivot a SharePoint 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013)  
  
-   [Panoramica del processo di aggiornamento a SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256688).  
  
-   [Pulire le preparazioni prima di un aggiornamento a SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256689).  
  
-   [Aggiornare i database da SharePoint 2010 a SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256690).  
  
## <a name="see-also"></a>Vedere anche  
 [Posizione in cui trovare il componente aggiuntivo Reporting Services per prodotti SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [Combinazioni supportate di SharePoint e Reporting Services server e del componente aggiuntivo &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)   
 [Installare o disinstallare il componente aggiuntivo Reporting Services per SharePoint &#40;SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
