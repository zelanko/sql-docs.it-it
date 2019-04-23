---
title: Analisi dei dati e creazione di report con gli strumenti di business intelligence (BI) di Microsoft
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: reporting-services-2014, sql-server-2014
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 8ef547b99b7e51fa1f642fa11442e9eea466c6dd
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59947617"
---
# <a name="analysis-and-reporting-with-microsoft-business-intelligence-bi-tools"></a>Analisi dei dati e creazione di report con gli strumenti di business intelligence (BI) di Microsoft

  Nella tabella seguente viene indicato il mapping dei carichi di lavoro per l'analisi dei dati e gli strumenti di Business Intelligence di Microsoft più appropriati per i carichi di lavoro.  
  
 Lo scopo consiste nel consentire la scelta dello strumento che meglio soddisfa le esigenze. Per ulteriori informazioni su un prodotto, fare clic sul relativo collegamento nella tabella.  
  
 Per una breve panoramica di questi strumenti che permetta di definire quelli più appropriati, vedere la pagina sull'[introduzione agli strumenti di Microsoft Business Intelligence (BI)](https://www.digitalvidya.com/blog/introduction-to-microsoft-power-bi/).  
  
|Carichi di lavoro|Utente|||Strumenti di Business Intelligence|||  
|---------------|----------|-|-|--------------|-|-|  
|||**Excel**|**SharePoint**|**SharePoint Online**|**Power BI**|**SQL Server**|  
|**Business Intelligence in modalità self-service**|Analisti/utenti finali||||||  
|Individuare facilmente e accedere ai dati pubblici e aziendali||[Power Query](https://go.microsoft.com/fwlink/p/?LinkId=391845)||[Azure Data Catalog](https://azure.microsoft.com/services/data-catalog/)<br /><br />||  
|Creare modelli di dati potenti||[Power Pivot](https://support.office.com/article/power-pivot-overview-and-learning-f9001958-7901-4caa-ad80-028a6d2432ed?ui=en-US&rs=en-US&ad=US)|||[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)||  
|Eseguire analisi predittive self-service||||||[Dati di componenti aggiuntivi Data Mining per Excel](../analysis-services/data-mining-client-for-excel-sql-server-data-mining-add-ins.md)|  
|Visualizzare ed esplorare i dati||[Power View](https://go.microsoft.com/fwlink/p/?LinkId=391847)<br /><br /> [Power Map](https://go.microsoft.com/fwlink/p/?LinkId=391848)|||||  
|Porre domande tramite query in linguaggio naturale|||||[DOMANDE E RISPOSTE](https://docs.microsoft.com/power-bi/consumer/end-user-q-and-a)||  
|Accedere ai report tramite i dispositivi mobili||||[HTML 5 (supporta la visualizzazione di file <10 MB)](https://go.microsoft.com/fwlink/p/?LinkId=391853)|[HTML 5 (supporta la visualizzazione di file <250 MB)](https://go.microsoft.com/fwlink/p/?LinkId=391854)<br /><br /> [App Power BI per dispositivi mobili su dispositivi iOS](https://docs.microsoft.com/power-bi/consumer/mobile/mobile-iphone-app-get-started)<br /><br /> [App Power BI per dispositivi mobili su dispositivi Android](https://docs.microsoft.com/power-bi/consumer/mobile/mobile-android-app-get-started) <br /><br />[App Power BI per dispositivi mobili per Windows 10](https://docs.microsoft.com/power-bi/consumer/mobile/mobile-windows-10-phone-app-get-started)||  
|Collaborare e condividere|||[Siti di SharePoint](https://go.microsoft.com/fwlink/p/?LinkId=391849)|[Siti del team SharePoint](https://go.microsoft.com/fwlink/p/?LinkId=391850)|[Siti di Power BI](https://docs.microsoft.com/power-bi/service-how-to-collaborate-distribute-dashboards-reports)||  
|**Business Intelligence aziendale**|Professionisti IT||||||  
|Creare modelli aziendali multidimensionali e tabulari||||||[Analysis Services](../analysis-services/analysis-services.md)|  
|Creare visualizzazioni di dati ad hoc|||[Power View per SharePoint](https://go.microsoft.com/fwlink/p/?LinkId=391858)||||  
|Creare dashboard|||[Dashboard di SharePoint](https://go.microsoft.com/fwlink/p/?LinkId=391859)<br /><br /> [PerformancePoint Services](https://technet.microsoft.com/library/ee424392.aspx)||||  
|Creare report operativi||||||<sup>1</sup> [Reporting Services](create-deploy-and-manage-mobile-and-paginated-reports.md)|  
|Creare report personalizzati e incorporati||||||<sup>1</sup> [Reporting Services](create-deploy-and-manage-mobile-and-paginated-reports.md)|  
|**Analisi avanzata**|Data Scientist||||||  
|Eseguire analisi predittive self-service||||||[Dati di componenti aggiuntivi Data Mining per Excel](https://msdn.microsoft.com/library/dn282385\(v=sql.120\).aspx)|  
|Utilizzare algoritmi di data mining||||||[Data mining in Analysis Services](https://technet.microsoft.com/library/bb510516\(v=sql.120\).aspx)|  
  
 <sup>1</sup> reporting Services include numerose funzionalità che supportano il recapito di report operativi e report personalizzati, quali sottoscrizioni e avvisi dati.