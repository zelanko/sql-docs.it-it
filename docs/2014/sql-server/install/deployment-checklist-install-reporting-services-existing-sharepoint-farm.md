---
title: 'Elenco di controllo per la distribuzione: installare Reporting Services in una farm di SharePoint esistente | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 436b4c3d-3f2f-464a-be7e-5c051d9ffb8f
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: e7a66be0d4e002643ffe1c72ce8c44aa50f61c0e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952618"
---
# <a name="deployment-checklist-install-reporting-services-into-an-existing-sharepoint-farm"></a>Elenco di controllo per la distribuzione: installare Reporting Services in una farm di SharePoint esistente
  È possibile installare i server di report di SharePoint per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in una farm SharePoint nuova o esistente. In questo argomento vengono descritti i possibili scenari e le procedure consigliate per installare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in una farm SharePoint esistente.  
  
## <a name="prerequisites"></a>Prerequisites  
 Prima di eseguire il programma di installazione, esaminare le informazioni seguenti:  
  
|Passaggio|Collegamento|  
|----------|----------|  
|Creare o identificare gli account utilizzati nella distribuzione di un server di report. È necessario disporre di un account del servizio server di report e di credenziali per la connessione al database del server di report||  
|Definire un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ospiterà il database del server di report. È possibile utilizzare un'istanza locale o remota di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È consigliabile scegliere un'istanza che si trovi in un computer dotato di sufficiente capacità di archiviazione per i report.||  
|Facoltativo. Se si desidera utilizzare la funzionalità di posta elettronica del server di report per le sottoscrizioni, individuare il nome del server o del gateway SMTP utilizzato per il servizio di posta elettronica nell'organizzazione|[Configurare un server di report per il recapito tramite posta elettronica &#40;Configuration Manager SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)|  
|Nota: se si esegue l'aggiornamento di un computer da una versione [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] CTP precedente e sono state apportate modifiche personalizzate ai file di configurazione, sarà necessario apportare le stesse modifiche ai file di configurazione, dopo l' [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]aggiornamento a. I file interessati sono **web.config** e **client.config**.||  
  
## <a name="installation-scenarios"></a>Scenari di installazione  
 Nella tabella seguente vengono descritti i possibili scenari che si possono presentare durante l'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in una farm SharePoint esistente. la modalità locale consente l'esecuzione del rendering locale dei report dalla raccolta documenti di SharePoint, senza l'integrazione con un server di report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . A differenza del server di report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , il componente aggiuntivo di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per i prodotti SharePoint è obbligatorio. Per ulteriori informazioni sulla modalità locale, vedere [report in modalità locale e con connessione nel Visualizzatore di report &#40;Reporting Services in modalità SharePoint&#41;](../../../2014/reporting-services/local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md) e [dove trovare il componente aggiuntivo Reporting Services per prodotti SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
|Avvio configurazione|Flusso di lavoro|Fine della configurazione|Commenti|  
|----------------------------|--------------|--------------------------|--------------|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]in modalità locale|Installazione|Modalità con connessione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].||  
|Modalità con connessione [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|Aggiornamento sul posto|Modalità con connessione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].||  
|Modalità con connessione [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|Migrazione|Modalità con connessione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].||  
  
## <a name="installation-and-in-place-upgrade-checklist"></a>Elenco di controllo installazione e aggiornamento sul posto  
 Nella tabella seguente sono riepilogati i passaggi, gli strumenti e le informazioni che occorre verificare e utilizzare per l'installazione.  
  
|Passaggio|Collegamento|  
|----------|----------|  
|**Installazione e configurazione iniziale**||  
|Installare il componente aggiuntivo SharePoint in tutti i computer front-end Web.|[Aggiungere un ulteriore front-end Web di Reporting Services a una farm](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|Installare SQL Server [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Reporting Services e il motore di database.|[Installare la modalità SharePoint di Reporting Services per SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|Creare almeno un'applicazione di servizio SSRS e configurare l'associazione applicazione di servizio.|Vedere la sezione "applicazione di servizio" in [Install Reporting Services modalità SharePoint per sharepoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|**Configurazione aggiuntiva**||  
|Aggiungere i tipi di contenuto SSRS alla raccolta documenti.|[Aggiungere tipi di contenuto del server di report a una raccolta &#40;Reporting Services in modalità integrata SharePoint&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md)|  
|Effettuare il provisioning di SQL Server Agent|[Provisioning di sottoscrizioni e avvisi per le applicazioni di servizio SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)|  
|Configurare le impostazioni di posta elettronica per l'applicazione di servizio|[Configurare la posta elettronica per un'applicazione di servizio Reporting Services &#40;SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)|  
|Configurare Claims to Windows Token Service (C2WTS)|[Attestazioni per il servizio token Windows &#40;C2WTS&#41; e Reporting Services](../../../2014/sql-server/install/claims-to-windows-token-service-c2wts-and-reporting-services.md)|  
  
## <a name="migration-checklist"></a>Elenco di controllo per la migrazione  
 Di seguito viene fornito un elenco dei passaggi di base per la migrazione da un'installazione esistente a una nuova installazione.  
  
|Passaggio|Collegamento|  
|----------|----------|  
|Installare e configurare il nuovo server. Sono inclusi gli elementi seguenti:<br /><br /> Utilità preparazione prodotti SharePoint<br /><br /> Prodotti SharePoint 2010<br /><br /> SharePoint 2010 SP1<br /><br /> 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint<br /><br /> Componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per i prodotti SharePoint 2010|[Installare la modalità SharePoint di Reporting Services per SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|Creare almeno un'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Eseguire il backup dei database di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Eseguire il backup delle chiavi di crittografia di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Ripristinare il database e le chiavi di crittografia di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Eseguire il mapping di tutte le applicazioni Web alle nuove applicazioni di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|La nuova installazione **è ora funzionante**|  
|Rimuovere l'URL di integrazione nel vecchio server.|Nella pagina **Impostazioni generali dell'applicazione** di Amministrazione centrale SharePoint fare clic su **Integrazione Reporting Services**.|  
|Se richiesto, disinstallare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dalla vecchia installazione.||  
  
## <a name="next-steps"></a>Passaggi successivi  
  
## <a name="see-also"></a>Vedere anche  
 [Reporting Services installazione in modalità SharePoint &#40;SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)   
 [Linee guida per l'uso di SQL Server funzionalità di business intelligence in una farm di SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)   
 [Combinazioni supportate di SharePoint e Reporting Services server e componenti aggiuntivi &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
  
