---
title: PowerPivot per SharePoint (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c4c393d3-4856-47ac-ab5f-15da2f240d1d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 486db389b3cca8936a5350da61880637406a1387
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66071135"
---
# <a name="powerpivot-for-sharepoint-ssas"></a>PowerPivot per SharePoint (SSAS)
  PowerPivot per SharePoint è un server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eseguito in modalità SharePoint. PowerPivot per SharePoint offre l'hosting nel server dei dati PowerPivot in una farm di SharePoint 2010. I dati PowerPivot sono un modello di dati analitici che viene compilato con uno degli elementi seguenti:  
  
-   Componente aggiuntivo PowerPivot per Excel  
  
-   Excel 2013  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 | [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010  
  
 L'hosting nel server di tali dati richiede SharePoint, Excel Services e un'installazione di PowerPivot per SharePoint. I dati vengono caricati nelle istanze di PowerPivot per SharePoint, dove è possibile effettuare aggiornamenti a intervalli programmati tramite la funzionalità di aggiornamento dati di PowerPivot fornita dal server per le cartelle di lavoro di Excel 2010 o da SharePoint 2013 Excel Services per le cartelle di lavoro di Excel 2013.  
  
## <a name="powerpivot-for-sharepoint-2013"></a>PowerPivot per SharePoint 2013  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] supporta l'utilizzo delle cartelle di lavoro di Excel di [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint 2013 Excel Services contenenti modelli di dati e report Power View di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 In Excel Services in SharePoint 2013 è inclusa la funzionalità del modello di dati per consentire l'interazione con una cartella di lavoro di PowerPivot nel browser. Non è necessario distribuire il componente aggiuntivo PowerPivot per SharePoint 2013 nella farm. È sufficiente installare un server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità SharePoint e registrarlo nelle impostazioni **Modello di dati** di Excel Services.  
  
 Tramite la distribuzione del componente aggiuntivo PowerPivot per SharePoint 2013 vengono abilitate le funzionalità aggiuntive nella farm di SharePoint in uso. Tra le funzionalità aggiuntive sono incluse la raccolta PowerPivot, la pianificazione dell'aggiornamento dati e il dashboard di gestione di PowerPivot.  
  
 ![Distribuzione di Server PowerPivot in modalità 2 SSAS](../media/as-powerpivot-mode-2server-deployment.gif "distribuzione di Server SSAS PowerPivot modalità 2")  
  
## <a name="powerpivot-for-sharepoint-2010"></a>PowerPivot per SharePoint 2010  
 PowerPivot per SharePoint 2010 offre l'hosting nel server dei dati PowerPivot in una farm di SharePoint 2010. I dati PowerPivot sono un modello di dati analitici compilato in Excel usando il componente aggiuntivo PowerPivot per Excel. L'hosting nel server di tali dati richiede SharePoint 2010, Excel Services e un'installazione di PowerPivot per SharePoint. I dati vengono caricati nelle istanze di PowerPivot per SharePoint nella farm, dove è possibile effettuare aggiornamenti a intervalli programmati usando la funzionalità di aggiornamento dati di PowerPivot fornita dal server.  
  
### <a name="components-of-powerpivot-for-sharepoint-2010"></a>Componenti di PowerPivot per SharePoint 2010  
 PowerPivot per SharePoint viene implementato come servizio condiviso, pertanto le caratteristiche predefinite e l'infrastruttura possono essere usate per amministrare, proteggere e usare un'applicazione del servizio PowerPivot. Le operazioni di individuazione, reindirizzamento e gestione della connessione di server e database sono interamente gestite a livello della farm. Amministrazione centrale fornisce l'interfaccia amministrativa ai servizi usati per gestire identità del server, stato del server e proprietà di configurazione.  
  
 Una distribuzione completa di PowerPivot per SharePoint include componenti client e server che si integrano con Excel ed Excel Services in una farm di SharePoint. I dati PowerPivot all'interno di una cartella di lavoro di Excel sono costituiti da un database di Analysis Services che richiede un motore di analisi in memoria xVelocity (VertiPaq) di Analysis Services per caricare i dati ed eseguire query su di essi. In una workstation client, il motore xVelocity viene eseguito in-process all'interno di Excel. In una farm di SharePoint, Analysis Services viene eseguito in un server applicazioni in cui viene abbinato a servizi correlati che gestiscono le richieste per i dati PowerPivot. Nel diagramma seguente vengono illustrati i componenti dei client e dei server PowerPivot:  
  
 ![GMNI_GeminiArch2](../media/gmni-geminiarch2.gif "GMNI_GeminiArch2")  
  
 Il servizio Web di PowerPivot viene eseguito in un server applicazioni Web. Reindirizza le richieste dall'applicazione Web a un'istanza del servizio di sistema PowerPivot nella farm.  
  
 Il servizio di sistema PowerPivot genera richieste di carico al server Analysis Services e gestisce le connessioni in corso ai dati già caricati in memoria, memorizzando nella cache o scaricando dati se non vengono più usati o in caso di contesa per le risorse di sistema. Tiene inoltre traccia dell'attività dell'utente. I dati relativi allo stato di integrità del server e di altro tipo vengono raccolti e presentati in report per fornire informazioni sulla qualità dell'esecuzione del sistema.  
  
 Un'istanza del server Analysis Services in modalità integrata SharePoint completa la distribuzione. Carica, esegue query e scarica i dati. Elabora inoltre i dati se la cartella di lavoro viene configurata per l'aggiornamento dati PowerPivot.  Ogni istanza è strettamente associata al servizio di sistema PowerPivot locale che fa parte della stessa installazione.  
  
##  <a name="bkmk_RelatedContent"></a> Contenuto della sezione  
 [Amministrazione e configurazione del server PowerPivot in Amministrazione centrale](power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
 [Configurazione di PowerPivot tramite Windows PowerShell](power-pivot-configuration-using-windows-powershell.md)  
  
 [Strumenti di configurazione PowerPivot](power-pivot-configuration-tools.md)  
  
 [Autenticazione e autorizzazione di PowerPivot](power-pivot-authentication-and-authorization.md)  
  
 [Configurare regole di integrità di PowerPivot:](configure-power-pivot-health-rules.md)  
  
 [Dati di utilizzo e dashboard di gestione PowerPivot](power-pivot-management-dashboard-and-usage-data.md)  
  
 [Raccolta PowerPivot](../../2014-toc/books-online-for-sql-server-2014.md)  
  
 [Accesso ai dati PowerPivot](power-pivot-data-access.md)  
  
 [Aggiornamento dei dati PowerPivot](power-pivot-data-refresh.md)  
  
 [Feed di dati PowerPivot](power-pivot-data-feeds.md)  
  
 [Connessione BI Semantic Model di PowerPivot &#40;con estensione bism&#41;](power-pivot-bi-semantic-model-connection-bism.md)  
  
 **Nelle altre sezioni**  
  
## <a name="additional-topics"></a>Argomenti aggiuntivi  
 [Aggiornare PowerPivot per SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)  
  
 [Installazione di PowerPivot per SharePoint 2013](../instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
 [Informazioni di riferimento di PowerShell per PowerPivot per SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
  
 [Esempi di topologie di licenza e costi per SQL Server 2014 Self-Service di Business Intelligence](../../sql-server/install/example-license-topologies-costs-self-service-business-intelligence.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Pianificazione di PowerPivot e la distribuzione](https://go.microsoft.com/fwlink/?linkID=220972)   
 [Ripristino di emergenza per PowerPivot per SharePoint](https://go.microsoft.com/fwlink/p/?LinkId=389570)  
  
  
