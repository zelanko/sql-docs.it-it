---
title: Linee guida per l'uso di SQL Server funzionalità di business intelligence in una farm di SharePoint 2010 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 5f9a94c4-854b-4577-a8b1-7142f19904e3
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 02aaab5056d5e2b095d9440f696edcc77475323e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78172560"
---
# <a name="guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm"></a>Guida per l'utilizzo delle funzionalità di Business Intelligence di SQL Server in una farm di SharePoint 2010
  In questo argomento viene riepilogata la disponibilità delle funzionalità in base alle versioni e alle edizioni del software in uso. Vengono inoltre illustrati i requisiti di installazione di SharePoint 2010 per l'utilizzo di funzionalità SQL Server specifiche. Per informazioni correlate a SharePoint 2013, vedere [topologie di distribuzione per SQL Server le funzionalità di business intelligence in SharePoint](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md).

 In questo argomento

-   [Requisiti generali di SharePoint 2010](#bkmk_generalsharepoint)

-   [SharePoint 2010 Service Pack 1 (SP1)](#bkmk_sp1)

-   [Edizioni di SharePoint Edizioni e supporto per la funzionalità BI](#bkmk_vers)

-   [Utilità preparazione prodotti SharePoint 2010](#bkmk_prereq)

-   [Requisiti e suggerimenti per l'esecuzione dell'installazione di SharePoint](#bkmk_install)

##  <a name="general-sharepoint-2010-requirements"></a><a name="bkmk_generalsharepoint"></a>Requisiti generali di SharePoint 2010

-   I prodotti SharePoint 2010 sono solo a 64 bit. Se si dispone di un'installazione a 32 bit di una versione precedente di SharePoint e di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installato in modalità integrata SharePoint, non è possibile effettuare l'aggiornamento a SharePoint 2010. Per ulteriori informazioni, esaminare la documentazione relativa a SharePoint.

-   Reporting Services include un componente aggiuntivo per prodotti SharePoint. Le configurazioni supportate per il componente aggiuntivo e il server di report sono disponibili con un livello di granularità superiore rispetto a quello indicato qui. Per ulteriori informazioni, vedere [combinazioni supportate di SharePoint e Reporting Services server e del componente aggiuntivo &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md).

-   Gli strumenti di sviluppo di SharePoint supportano solo una configurazione autonoma di SharePoint.  Per ulteriori informazioni, vedere la documentazione di SharePoint: [requisiti per lo sviluppo di soluzioni SharePoint](https://msdn.microsoft.com/library/ee231582.aspx).

##  <a name="sharepoint-editions-and-bi-feature-support"></a><a name="bkmk_vers"></a>Edizioni di SharePoint e supporto delle funzionalità di Business Intelligence
 Alcune funzionalità di Business Intelligence di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] sono supportate solo in edizioni specifiche di prodotti SharePoint.

|Funzionalità supportate|Prodotto SharePoint|
|------------------------|------------------------|
|[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], una funzionalità del [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] componente aggiuntivo per [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition.<br /><br /> Avvisi dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].|[!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition.|
|Visualizzazione generale di report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e integrazione della funzionalità con SharePoint.|[!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Standard ed Enterprise Edition.<br /><br /> [!INCLUDE[SPF2010](../../includes/spf2010-md.md)].|

 Per ulteriori informazioni, vedere [funzionalità supportate dalle edizioni di SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473).

##  <a name="sharepoint-2010-service-pack-1-sp1"></a><a name="bkmk_sp1"></a>SharePoint 2010 Service Pack 1 (SP1)
 È consigliabile effettuare l'aggiornamento dell'installazione di SharePoint 2010 a SharePoint 2010 Service Pack 1 (SP1). SharePoint SP1 è obbligatorio nei casi seguenti:

-   Si desidera utilizzare la versione [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] del motore di database per i database del contenuto di SharePoint o i database del catalogo di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

-   Si desidera utilizzare [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].

 Uno dei motivi principali per cui è necessario SP1 per le installazioni di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SharePoint in cui viene eseguito con è la funzionalità del motore di database **sp_dboption**, che è stata deprecata in una [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] versione precedente, non è più disponibile nella versione. Per ulteriori informazioni, vedere la pagina relativa [alla funzionalità discontinued motore di database SQL Server 2014](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)

### <a name="sharepoint-2010-sp1-installation-guidance"></a>Guida all'installazione di SharePoint 2010 SP1
 [Scaricare SharePoint Server 2010 SP1](https://go.microsoft.com/fwlink/?LinkID=219697) e applicarlo a tutti i server della farm.

> [!NOTE]
>  In una farm esistente è necessario eseguire uno dei passaggi **aggiuntivi** seguenti per completare l'aggiornamento di SharePoint SP1. Per ulteriori informazioni, vedere [problemi noti durante l'installazione di Office 2010 SP1 e sharepoint 2010 SP1](https://support.microsoft.com/kb/2532126) e [Descrizione di SharePoint Server 2010 SP1](https://support.microsoft.com/kb/2460045):

-   **Configurazione guidata Prodotti SharePoint:** Eseguire la procedura guidata per completare l'aggiornamento e la configurazione di SP1.

-   **Completare l'aggiornamento con psconfig:** Eseguire il comando `psconfig -upgrade` per completare l'aggiornamento di SP1

 Per ulteriori informazioni, vedere la sezione "aggiornamento" di [(SharePoint Server 2010)](https://technet.microsoft.com/library/cc263093.aspx) e [Resource Center: aggiornamenti per prodotti SharePoint 2010](https://technet.microsoft.com/sharepoint/ff800847.aspx)

## <a name="sharepoint-installation-with-sql-server-bi-features"></a>Installazione di SharePoint con le funzionalità di Business Intelligence di SQL Server

###  <a name="sharepoint-2010-products-preparation-tool"></a><a name="bkmk_prereq"></a>Strumento di preparazione prodotti SharePoint 2010
 L'Utilità preparazione prodotti SharePoint consente di abilitare i ruoli del server nel sistema operativo e di installare altro software necessario richiesto da un'installazione SharePoint. Nella tabella seguente vengono identificati i passaggi aggiuntivi per configurare il server per [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].

|Componente|Azione|
|---------------|------------|
|Componente aggiuntivo Reporting Services|L'Utilità preparazione prodotti SharePoint 2010 consente di installare la versione [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] del componente aggiuntivo Reporting Services. In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] è inclusa una versione più recente di questo componente aggiuntivo richiesta per le funzionalità di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Il componente aggiuntivo può essere installato utilizzando l'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure può essere scaricato da MSDN. Per ulteriori informazioni su dove ottenere la versione corrente del componente aggiuntivo e su come installarlo, vedere [dove trovare il componente aggiuntivo Reporting Services per prodotti SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md) e [installare o disinstallare il componente aggiuntivo Reporting Services per sharepoint &#40;SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).|
|Provider OLE DB per Analysis Services (MSOLAP)|Mediante SharePoint 2010 viene installata la versione SQL Server 2008 del provider OLE DB come parte di una distribuzione di Excel Services. Questa versione non supporta l'accesso ai dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. È necessario installare versioni successive del provider su server SharePoint che supportano connessioni dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Per ulteriori informazioni, vedere [Install the provider OLE DB Analysis Services on SharePoint Servers](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)|
|Servizi Web ADO.NET|I servizi ADO.NET sono presenti nell'elenco dei prerequisiti in SharePoint 2010, ma non vengono tuttavia installati dal programma di installazione dei prerequisiti. Per aggiungere servizi ADO.NET, è necessario installarli manualmente. L'installazione di servizi ADO.NET è necessaria se si desidera utilizzare gli elenchi SharePoint come feed di dati per cartelle di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o report di Reporting Services. Per istruzioni, vedere [installare ADO.NET Data Services per supportare esportazioni di feed di dati di elenchi SharePoint](../../../2014/sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md).|

###  <a name="requirements-and-suggestions-for-running-the-sharepoint-installation"></a><a name="bkmk_install"></a>Requisiti e suggerimenti per l'esecuzione dell'installazione di SharePoint
 Le funzionalità di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] installate e l'ordine di installazione di tali funzionalità determina i livelli di integrazione possibili con SharePoint. Ad esempio, sebbene alcuni livelli di integrazione delle funzionalità siano disponibili tramite Reporting Services su un server SharePoint che utilizza un database predefinito, la maggior parte degli scenari di integrazione delle funzionalità richiede un'installazione della farm SharePoint, poiché solo questa fornisce l'infrastruttura richiesta per alcune funzionalità di Business Intelligence.

 Una farm SharePoint può essere costituita da uno o più server. Ciò che distingue una farm da un'installazione autonoma è la presenza di infrastrutture aggiuntive, ad esempio Attestazioni per il servizio token Windows.

 Una farm viene abilitata quando si sceglie l'opzione **server farm** nel programma di installazione di SharePoint. Se si desidera utilizzare [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], è necessario disporre dell'installazione di una farm. L'installazione autonoma di SharePoint è supportata ed è comune per gli ambienti di sviluppo di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Un'installazione di una farm di SharePoint è tuttavia consigliata per un ambiente di produzione.

 ![GMNI_SetupUI_SharePoint2010InstallType](../../../2014/sql-server/install/media/gmni-setupui-sharepoint2010installtype.gif "GMNI_SetupUI_SharePoint2010InstallType")

 Un'installazione server completa è inoltre richiesta per [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint o per il servizio condiviso di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

 ![GMNI_SetupUI_SharePoint2010ServerType](../../../2014/sql-server/install/media/gmni-setupui-sharepoint2010servertype.gif "GMNI_SetupUI_SharePoint2010ServerType")

 Nell'ultima pagina dell'Installazione guidata viene richiesto di configurare la farm, nonché, facoltativamente, un'applicazione Web predefinita e una raccolta siti radice. Questo percorso di installazione è seguito dalla maggior parte degli utenti. Se per qualsiasi motivo la farm non viene configurata, è possibile utilizzare l'opzione di configurazione della farm nello strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per configurarla.

 Nelle versioni precedenti viene consigliato di lasciare la farm non configurata per l'installazione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], perché riduce i passaggi successivi necessari se si utilizzano le opzioni di installazione di SQL Server per installare [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint in uno stato pronto per l'utilizzo. Questo non è più importante nella versione corrente. È possibile utilizzare lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per ottimizzare una farm esistente in modo che utilizzi le impostazioni consigliate per un'installazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint.

 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] può essere installato in una farm di SharePoint esistente. È possibile installare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o SharePoint in qualsiasi ordine, ma la configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] varia a seconda dell'ordine. Per ulteriori informazioni, vedere [aggiungere un ulteriore server di report a una Farm &#40;la scalabilità orizzontale di SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md) e [installare Reporting Services modalità sharepoint per SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)

 ![GMNI_SetupUI_DoNotConfigureMOSS](../../../2014/sql-server/install/media/gmni-setupui-donotconfiguremoss.gif "GMNI_SetupUI_DoNotConfigureMOSS")

## <a name="see-also"></a>Vedere anche
 [Installazione e distribuzione per SharePoint server 2010](https://technet.microsoft.com/sharepoint/ee518643.aspx) [più server per una farm a tre livelli (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?linkID=219834)


