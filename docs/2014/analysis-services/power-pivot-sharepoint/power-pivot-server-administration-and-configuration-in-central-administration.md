---
title: Amministrazione e configurazione del server PowerPivot in Amministrazione centrale | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2cdbfdc5-45a9-4000-a03d-318cc7ac8fe9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: de72001ced1b7e2690f90b2de4c59bb35aca6ce4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66071109"
---
# <a name="powerpivot-server-administration-and-configuration-in-central-administration"></a>Amministrazione e configurazione del server PowerPivot in Amministrazione centrale
  L'amministrazione e la configurazione del server PowerPivot vengono eseguite dagli amministratori dell'applicazione del servizio SharePoint, tramite Amministrazione centrale SharePoint.  
  
 Prima di poter usare PowerPivot per SharePoint, è necessario configurarlo. Dopo aver installato PowerPivot per SharePoint usando il programma di installazione di SQL Server, è possibile configurarlo mediante uno degli approcci seguenti:  
  
-   Strumento di configurazione di PowerPivot o di PowerPivot per SharePoint 2013  
  
-   Amministrazione centrale SharePoint  
  
-   Cmdlet PowerShell  
  
 Tutti e tre gli approcci consentono di ottenere un server configurato completamente.  
  
 In questa sezione sono descritte le attività per la configurazione del software usando Amministrazione centrale. È necessario eseguire almeno tutte e tre le attività di configurazione obbligatorie indicate nell'elenco di seguito.  
  
> [!IMPORTANT]  
>  Per SharePoint 2010, prima di poter configurare PowerPivot per SharePoint o una farm di SharePoint in cui viene usato un server di database [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] è necessario che sia installato SharePoint 2010 Service Pack 1 (SP1). Se non è stato ancora installato un Service Pack, eseguire adesso questa operazione prima di iniziare a configurare il server.  
  
## <a name="benefits-of-configuring-powerpivot-for-sharepoint-using-central-administration"></a>Vantaggi della configurazione di PowerPivot per SharePoint usando Amministrazione centrale  
 Amministrazione centrale SharePoint è l'applicazione amministrativa di una farm SharePoint. Un amministratore di farm potrebbe preferire l'utilizzo di uno strumento noto per l'aggiunta di un'istanza di PowerPivot per SharePoint alla farm.  
  
 A differenza degli strumenti di configurazione di PowerPivot o dei cmdlet di PowerShell, in Amministrazione centrale sono disponibili pagine in cui sono specificate in modo completo tutte le opzioni che è possibile impostare per la configurazione di un'applicazione o di un server. Gli altri approcci condensano il flusso di lavoro di configurazione in un numero inferiore di passaggi o richiedono la conoscenza preventiva della modalità di configurazione di un server SharePoint mediante PowerShell.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Configurazione di PowerPivot tramite Windows PowerShell](power-pivot-configuration-using-windows-powershell.md)  
  
 [PowerPivot Configuration Tools](power-pivot-configuration-tools.md)  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Collegamento|Type|Descrizione dell'attività|  
|----------|----------|----------------------|  
|[Distribuire soluzioni PowerPivot in SharePoint](deploy-power-pivot-solutions-to-sharepoint.md)|Obbligatoria|Tramite questo passaggio vengono installati i file della soluzione che aggiungono file di programma e pagine di applicazione alla farm e alle raccolte siti.|  
|[Creare e configurare un'applicazione del servizio PowerPivot in Amministrazione centrale](create-and-configure-power-pivot-service-application-in-ca.md)|Obbligatoria|Tramite questo passaggio viene eseguito il provisioning del servizio di sistema PowerPivot.|  
|[Attivare l'integrazione delle funzionalità di PowerPivot per le raccolte siti in Amministrazione centrale](activate-power-pivot-integration-for-site-collections-in-ca.md)|Obbligatoria|Tramite questo passaggio vengono abilitate le funzionalità di PowerPivot a livello di raccolta siti.|  
|[Aggiungere MSOLAP.5 come provider di dati attendibile in Excel Services](add-msolap-5-as-a-trusted-data-provider-in-excel-services.md)|Obbligatoria|Tramite questo passaggio viene aggiunto il provider OLE DB per Analysis Services come provider attendibile in Excel Services.|  
|[Aggiornamento di dati PowerPivot con SharePoint 2010](../powerpivot-data-refresh-with-sharepoint-2010.md)|Consigliato|L'aggiornamento dei dati è facoltativo, ma consigliato. Consente all'utente di pianificare aggiornamenti automatici dei dati PowerPivot nelle cartelle di lavoro di Excel pubblicate.|  
|[Configurare l'account di aggiornamento dati automatico PowerPivot &#40;PowerPivot per SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)|Consigliato|Tramite questo passaggio viene eseguito il provisioning di un account a scopo speciale che può essere usato per eseguire processi di aggiornamento dati nel server.|  
|[Configurare la raccolta dati di utilizzo per &#40;PowerPivot per SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)|Facoltativo|La raccolta dei dati di utilizzo è configurata per impostazione predefinita. È possibile usare questi passaggi per modificare le impostazioni predefinite.|  
|[Configurare l'aggiornamento dati dedicato o l'elaborazione solo query &#40;PowerPivot per SharePoint&#41;](../configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)|Facoltativo|Un'istanza di PowerPivot può essere dedicata solo ai processi di aggiornamento dati o alle query. Inoltre, è possibile modificare le impostazioni predefinite per i processi di aggiornamento dati paralleli.|  
|[Configurare gli account del servizio PowerPivot](configure-power-pivot-service-accounts.md)|Facoltativo|Si illustra come aggiornare le password o modificare gli account di servizio.|  
|[Connettere un'applicazione del servizio PowerPivot a un'applicazione Web SharePoint in Amministrazione centrale](connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md)|Facoltativo|Si illustra come modificare le associazioni di servizio.|  
|[Creare un percorso attendibile per i siti PowerPivot in Amministrazione centrale](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)|Facoltativo|Si illustra come aggiungere la raccolta PowerPivot come percorso attendibile|  
|[Configurare e visualizzare i file di log di SharePoint e la registrazione diagnostica &#40;PowerPivot per SharePoint&#41;](configure-and-view-sharepoint-and-diagnostic-logging.md)|Facoltativo|La registrazione eventi è configurata per impostazione predefinita. È possibile usare questi passaggi per modificare le impostazioni predefinite.|  
|[Regole di integrità di PowerPivot: configurazione](configure-power-pivot-health-rules.md)|Facoltativo|Le regole di integrità del server sono configurate per impostazione predefinita. È possibile usare questi passaggi per modificare alcune delle impostazioni predefinite.|  
|[Creare e personalizzare la raccolta PowerPivot](create-and-customize-power-pivot-gallery.md)|Facoltativo|Per le installazioni configurate manualmente, in questa procedura si illustra come creare una libreria della raccolta PowerPivot in cui sono mostrate anteprime delle immagini delle cartelle di lavoro di PowerPivot che contiene.|  
|[Aggiungere un tipo di contenuto connessione BI Semantic Model a una raccolta &#40;PowerPivot per SharePoint&#41;](add-bi-semantic-model-connection-content-type-to-library.md)|Facoltativo|Si illustra come estendere una raccolta documenti per supportare la creazione di file di connessione BISM.|  
  
## <a name="see-also"></a>Vedi anche  
 [Installazione di PowerPivot per SharePoint 2010](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [Informazioni di riferimento sulle impostazioni di configurazione &#40;PowerPivot per SharePoint&#41;](configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [Ripristino di emergenza per PowerPivot per SharePoint](https://go.microsoft.com/fwlink/p/?LinkId=389570)  
  
  
