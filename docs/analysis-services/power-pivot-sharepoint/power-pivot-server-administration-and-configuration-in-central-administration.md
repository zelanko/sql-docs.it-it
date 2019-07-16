---
title: Power Pivot Server amministrazione e configurazione in Amministrazione centrale | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 87e2903607b476b04c44ac81ba337ea38e68a58b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208072"
---
# <a name="power-pivot-server-administration-and-configuration-in-central-administration"></a>Amministrazione e configurazione del server PowerPivot in Amministrazione centrale
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] vengono eseguite dagli amministratori dell'applicazione del servizio SharePoint usando Amministrazione centrale SharePoint.  
  
 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] per SharePoint, è necessario configurarlo. Dopo aver installato [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] per SharePoint con il programma di installazione di SQL Server, è possibile configurarlo usando uno degli approcci seguenti:  
  
-   [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] o di [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] per SharePoint 2013  
  
-   Amministrazione centrale SharePoint  
  
-   PowerShell - cmdlet  
  
 Tutti e tre gli approcci consentono di ottenere un server configurato completamente.  
  
 In questa sezione sono descritte le attività per la configurazione del software usando Amministrazione centrale. È necessario eseguire almeno tutte e tre le attività di configurazione obbligatorie indicate nell'elenco di seguito.  
  
> [!IMPORTANT]  
>  Per SharePoint 2010, prima di poter configurare [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] per SharePoint o una farm di SharePoint in cui viene usato un server di database [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] è necessario che sia installato SharePoint 2010 Service Pack 1 (SP1). Se non è stato ancora installato un Service Pack, eseguire adesso questa operazione prima di iniziare a configurare il server.  
  
## <a name="benefits-of-configuring-power-pivot-for-sharepoint-using-central-administration"></a>Vantaggi della configurazione di PowerPivot per SharePoint usando Amministrazione centrale  
 Amministrazione centrale SharePoint è l'applicazione amministrativa di una farm SharePoint. Un amministratore di farm potrebbe preferire l'utilizzo di uno strumento noto per l'aggiunta di un'istanza di [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] per SharePoint alla farm.  
  
 A differenza degli strumenti di configurazione di [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] o dei cmdlet di PowerShell, in Amministrazione centrale sono disponibili pagine in cui sono specificate in modo completo tutte le opzioni che è possibile impostare per la configurazione di un'applicazione o di un server. Gli altri approcci condensano il flusso di lavoro di configurazione in un numero inferiore di passaggi o richiedono la conoscenza preventiva della modalità di configurazione di un server SharePoint mediante PowerShell.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Configurazione di Power Pivot con Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
 [Strumenti di configurazione di Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Collegamento|type|Descrizione dell'attività|  
|----------|----------|----------------------|  
|[Distribuire soluzioni PowerPivot in SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)|Obbligatoria|Tramite questo passaggio vengono installati i file della soluzione che aggiungono file di programma e pagine di applicazione alla farm e alle raccolte siti.|  
|[Creare e configurare un'applicazione del servizio Power Pivot in Amministrazione centrale](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)|Obbligatoria|Questo passaggio esegue il provisioning del servizio di sistema [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] .|  
|[Attivare l'integrazione delle funzionalità di Power Pivot per le raccolte siti in Amministrazione centrale](../../analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca.md)|Obbligatoria|Questo passaggio attiva le funzionalità di [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] a livello di raccolta siti.|  
|[Aggiungere MSOLAP.5 come provider di dati attendibile in Excel Services](../../analysis-services/power-pivot-sharepoint/add-msolap-5-as-a-trusted-data-provider-in-excel-services.md)|Obbligatoria|Tramite questo passaggio viene aggiunto il provider OLE DB per Analysis Services come provider attendibile in Excel Services.|  
|[Aggiornamento dati PowerPivot con SharePoint 2010](http://msdn.microsoft.com/01b54e6f-66e5-485c-acaa-3f9aa53119c9)|Consigliato|L'aggiornamento dei dati è facoltativo, ma consigliato. Consente all'utente di pianificare aggiornamenti automatici dei dati [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] nelle cartelle di lavoro di Excel pubblicate.|  
|[Configurare l'account di aggiornamento dati automatico PowerPivot (PowerPivot per SharePoint)](http://msdn.microsoft.com/81401eac-c619-4fad-ad3e-599e7a6f8493)|Consigliato|Tramite questo passaggio viene eseguito il provisioning di un account a scopo speciale che può essere usato per eseguire processi di aggiornamento dati nel server.|  
|[Configurare la raccolta dati di utilizzo per PowerPivot per SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)|Facoltativo|La raccolta dei dati di utilizzo è configurata per impostazione predefinita. È possibile usare questi passaggi per modificare le impostazioni predefinite.|  
|[Configurare l'aggiornamento dati o l'elaborazione di sole query dedicato (PowerPivot per SharePoint)](http://msdn.microsoft.com/5e027605-1086-4941-bb01-f315df8f829b)|Facoltativo|Un'istanza di [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] può essere dedicata solo ai processi di aggiornamento dati o alle query. Inoltre, è possibile modificare le impostazioni predefinite per i processi di aggiornamento dati paralleli.|  
|[Configurare gli account del servizio PowerPivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)|Facoltativo|Si illustra come aggiornare le password o modificare gli account di servizio.|  
|[Connettere un'applicazione del servizio PowerPivot a un'applicazione Web SharePoint in Amministrazione centrale](../../analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md)|Facoltativo|Si illustra come modificare le associazioni di servizio.|  
|[Creare un percorso attendibile per i siti Power Pivot in Amministrazione centrale](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)|Facoltativo|Spiega come aggiungere la raccolta [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] come percorso attendibile.|  
|[Configurare e visualizzare i file di log di SharePoint e la registrazione diagnostica &#40;Power Pivot per SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md)|Facoltativo|La registrazione eventi è configurata per impostazione predefinita. È possibile usare questi passaggi per modificare le impostazioni predefinite.|  
|[Configurare le regole di integrità di Power Pivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-health-rules.md)|Facoltativo|Le regole di integrità del server sono configurate per impostazione predefinita. È possibile usare questi passaggi per modificare alcune delle impostazioni predefinite.|  
|[Creare e personalizzare la Raccolta Power Pivot](../../analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery.md)|Facoltativo|Per le installazioni configurate manualmente, questa procedura illustra come creare una libreria di raccolte [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] in cui sono mostrate le anteprime delle immagini delle cartelle di lavoro di [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] contenute.|  
|[Aggiungere un tipo di contenuto Connessione BISM (BI Semantic Model) a una raccolta &#40;Power Pivot per SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/add-bi-semantic-model-connection-content-type-to-library.md)|Facoltativo|Si illustra come estendere una raccolta documenti per supportare la creazione di file di connessione BISM.|  
  
## <a name="see-also"></a>Vedere anche  
 [Installazione di Power Pivot per SharePoint 2010](http://msdn.microsoft.com/8d47dde7-c941-4280-a934-e2fe3f9a938f)   
 [Riferimento all'impostazione della configurazione &#40;Power Pivot per SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [Ripristino di emergenza per PowerPivot per SharePoint](http://go.microsoft.com/fwlink/p/?LinkId=389570)  
  
  
