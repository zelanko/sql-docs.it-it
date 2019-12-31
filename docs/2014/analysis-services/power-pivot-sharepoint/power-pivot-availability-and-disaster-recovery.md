---
title: Disponibilità e ripristino di emergenza di PowerPivot (SQL Server 2014) | Microsoft Docs
ms.custom: ''
ms.date: 03/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4aaf008c-3bcb-4dbf-862c-65747d1a668c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 731550d385d073c7b2f2e2758d4fcaf2353db746
ms.sourcegitcommit: 9b8b11961b33e66fc9f433d094fc5c0f9b473772
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/07/2019
ms.locfileid: "74908989"
---
# <a name="powerpivot-availability-and-disaster-recovery-sql-server-2014"></a>Ripristino di emergenza e disponibilità di PowerPivot (SQL Server 2014)
  I piani di ripristino di emergenza e disponibilità per [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] dipendono principalmente dalla struttura della farm di SharePoint, dalla quantità di inattività accettabile per i diversi componenti e dagli strumenti e dalle procedure consigliate che si implementano per la disponibilità di SharePoint. In questo argomento vengono riepilogate le tecnologie e inclusi i diagrammi di topologia di esempio da tenere [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] in considerazione durante la pianificazione della disponibilità e del ripristino di emergenza  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|  
  
 **In questo argomento**  
  
-   [Topologia di esempio SharePoint 2013 per la disponibilità elevata di PowerPivot](#bkmk_sharepoint2013)  
  
-   [Topologia di esempio SharePoint 2010 per la disponibilità elevata di PowerPivot](#bkmk_sharepoint2010)  
  
-   [Database dell'applicazione del servizio PowerPivot e tecnologie di disponibilità e ripristino SQL Server](#bkmk_sql_server_technologies)  
  
-   [Collegamenti a ulteriori informazioni](#bkmk_more_resources)  
  
##  <a name="bkmk_sharepoint2013"></a>Topologia di esempio di SharePoint 2013 per la disponibilità elevata di PowerPivot  
 In una distribuzione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 è disponibile una maggiore flessibilità nella progettazione della disponibilità di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . In SharePoint 2013, l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] distribuita in modalità SharePoint, anche denominata come server di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , viene eseguita all'esterno della farm di SharePoint e può essere installata in server separati. Ogni istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità SharePoint viene registrata con Excel Services. Un'applicazione del servizio e del servizio condiviso di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] viene eseguita nei server applicazioni SharePoint.  
  
 Nel diagramma seguente viene illustrato un esempio di distribuzione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013. In questo esempio viene supportata una buona disponibilità dei servizi di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] e si presuppone il backup dei database su base regolare.  
  
 ![disponibilità di powerpivot in 2013](../media/ssas-powerpivot-services-2013.png "disponibilità di powerpivot in 2013")  
  
-   **(1)** server front-end Web. Usare il componente aggiuntivo di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 per installare i provider di dati in ogni server. Per ulteriori informazioni, vedere [installare o disinstallare il componente aggiuntivo PowerPivot per SharePoint &#40;SharePoint 2013&#41;](../instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).  
  
-   **(2)** il [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] servizio condiviso viene eseguito **in ogni** server applicazioni e consente **l'esecuzione dell'** applicazione del servizio su tutti i server applicazioni. Pertanto se un singolo server applicazioni è offline, l'applicazione [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] sarà comunque disponibile.  
  
-   **(3)** servizi di calcolo Excel viene eseguito in ciascun server applicazioni e consente l'esecuzione dell'applicazione del servizio su tutti i server applicazioni. Pertanto se un singolo server applicazioni è offline, Servizi di calcolo Excel sarà comunque disponibile.  
  
-   **(4)** e **(6)** le istanze [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] di in modalità SharePoint vengono eseguite nei server all'esterno della farm di sharepoint, incluso il servizio Windows **SQL Server Analysis Services (PowerPivot)**. Ognuna di queste istanze viene registrata con Excel Services **(3)**. Excel Services gestisce il bilanciamento del carico delle richieste ai server [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] . L'architettura [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 consente di disporre di più server per [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] in modo da poter facilmente aggiungere più istanze in base alle esigenze. Per altre informazioni, vedere [Gestire le impostazioni del modello di dati di Excel Services (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780\(v=office.15\).aspx).  
  
-   **(5)** database SQL Server utilizzati per i database di contenuto, configurazione e applicazione. È incluso il database dell'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Il piano DR deve includere il livello di database. In questa progettazione i database vengono eseguiti nello stesso server come **(4)** una delle istanze di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] . **(4)** e **(5)** possono trovarsi anche in server diversi.  
  
-   **(7)** una forma di SQL Server backup o ridondanza del database.  
  
##  <a name="bkmk_sharepoint2010"></a>Topologia di esempio di SharePoint 2010 per la disponibilità elevata di PowerPivot  
 L'architettura di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 richiede che tutti i componenti di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] vengono eseguiti negli stessi server applicazioni di SharePoint. Ciò include l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] distribuita in modalità SharePoint e due servizi condivisi rispetto a una sola in una distribuzione di SharePoint 2013.  
  
 Nel diagramma seguente viene illustrato un esempio di distribuzione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010. In questo esempio viene supportata una buona disponibilità dei servizi di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] e si presuppone il backup dei database su base regolare.  
  
 ![disponibilità di powerpivot in sharepoint 2010](../media/ssas-powerpivot-services-2010.png "disponibilità di powerpivot in sharepoint 2010")  
  
-   **(1)** server front-end Web. Installare i provider di dati in ogni server. Per altre informazioni, vedere [Installazione del provider OLE DB di Analysis Services nei server di SharePoint](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md).  
  
-   **(2)** i due [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] servizi condivisi e **(4)** il servizio Windows **SQL Server Analysis Services (PowerPivot)** viene installato nei server applicazioni di SharePoint.  
  
     Il servizio di sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] viene eseguito in **ciascun** server applicazioni e consente l'esecuzione dell'applicazione del servizio **nei** server applicazioni. Se un singolo server applicazioni è offline, l'applicazione del servizio [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] sarà comunque disponibile.  
  
     Per aumentare la capacità di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in SharePoint 2010, distribuire più server applicazioni di SharePoint in cui vengono eseguiti il servizio di sistema di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
-   **(3)** servizi di calcolo Excel viene eseguito in ogni server applicazioni e consente l'esecuzione dell'applicazione del servizio su tutti i server applicazioni. Pertanto se un singolo server applicazioni è offline, Servizi di calcolo Excel sarà comunque disponibile.  
  
-   **(5)** database SQL Server utilizzati per i database di contenuto, configurazione e applicazione. È incluso il database dell'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Il piano DR deve includere il livello di database.  
  
-   **(6)** una forma di SQL Server backup o ridondanza del database.  
  
##  <a name="bkmk_sql_server_technologies"></a>Database dell'applicazione del servizio PowerPivot e tecnologie di disponibilità e ripristino SQL Server  
 Includere il database dell'applicazione del servizio di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] nella pianificazione della disponibilità elevata di SharePoint. Il nome predefinito per il database è `DefaultPowerPivotServiceApplicationDB-<GUID>`. Di seguito viene riportato un riepilogo delle tecnologie per la disponibilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e delle raccomandazioni da usare con il database di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] . Per altre informazioni, vedere [Opzioni supportate di disponibilità elevata e ripristino di emergenza per i database di SharePoint (SharePoint 2013)](https://technet.microsoft.com/library/jj841106.aspx).  
  
||Commenti|  
|-|--------------|  
|
  [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] e [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] in una farm per la disponibilità.|Supportato ma non consigliato. Si consiglia di usare AlwaysOn in modalità con commit sincrono.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)] in modalità con commit sincrono|Supportato e consigliato.|  
|
  [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] mirroring asincrono o log shipping a un'altra farm per il ripristino di emergenza.|Supportato.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)] con commit asincrono per il ripristino di emergenza|Supportato|  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Log shipping  
  
 Per ulteriori informazioni su come pianificare uno scenario di cold standby con [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], vedere [Ripristino di emergenza per PowerPivot](https://social.technet.microsoft.com/wiki/contents/articles/22137.sharepoint-powerpivot-disaster-recovery.aspx).  
  
## <a name="verification"></a>Verifica  
 Per istruzioni e script che consentono di verificare una [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] distribuzione prima e dopo un ciclo di ripristino di emergenza, vedere [elenco di controllo: usare PowerShell per verificare PowerPivot per SharePoint](../instances/install-windows/checklist-use-powershell-to-verify-power-pivot-for-sharepoint.md).  
  
##  <a name="bkmk_more_resources"></a>Collegamenti a ulteriori informazioni  
  
-   [Opzioni di disponibilità elevata e ripristino di emergenza supportate per i database di SharePoint (SharePoint 2013)](https://technet.microsoft.com/library/jj841106.aspx)  
  
-   [Pianificare il ripristino di emergenza (SharePoint Server 2010)](https://technet.microsoft.com/library/ff628971\(v=office.14\).aspx)  
  

  
  
