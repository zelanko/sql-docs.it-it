---
title: Confrontare le funzionalità di Business Intelligence In diversi ambienti Microsoft | Microsoft Docs
ms.prod: sql-server-2014
ms.technology:
- reporting-services-native
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 03/06/2017
ms.openlocfilehash: 60ea737f20ba48c6ba8d441d389a124e90444a76
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582505"
---
# <a name="compare-business-intelligence-capabilities-in-different-microsoft-environments"></a>Confrontare le funzionalità di Business Intelligence in diversi ambienti Microsoft

Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Business Intelligence può essere distribuito in numerosi ambienti diversi, tra cui [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con SharePoint Server, SharePoint Online e Power BI per Office 365. In questo argomento vengono confrontati i componenti e le funzionalità supportati in ogni ambiente.  
  
Per altre informazioni sul confronto tra SharePoint Server e SharePoint Online, vedere [Confrontare piani e opzioni di SharePoint](http://products.office.com/SharePoint/compare-sharepoint-plans).  
  
## <a name="author-and-manage-bi-reports-and-dashboards"></a>Creare e gestire report e dashboard di Business Intelligence  
  
||SQL Server 2014 & SharePoint Server 2013|SharePoint Online Piano 2|Power BI per Office 365|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|Siti di Business Intelligence|Raccolta [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]|No|Sito di Power BI|  
|Amministrazione dei dati e gestione e condivisione delle query|No|No|Sì **<sup>1</sup>**|  
|Integrazione con Master Data Services (MDS) e Data Quality Services (DQS)|Yes|No|No|  
|Pianificazione dell'aggiornamento dati|Sì, ma non sono supportate le cartelle di lavoro che contengono dati di Power Query|No|Yes|  
|Query in linguaggio naturale (domande e risposte)|no|No|Sì **<sup>2</sup>**|  
|Previsione predittiva|No|No|Sì **<sup>3</sup>**|  
|Integrazione di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Yes|No|no|  
|Integrazione di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] (multidimensionale e tabulare)|Yes|no|No|  
|Esportazione di dashboard interattivi di Power View nelle presentazioni di PowerPoint|Yes|No|no|  
|Creazione di dashboard basati su browser|Yes|No|No|  
|Monitoraggio dell'utilizzo|Yes|No|Yes|  
|Utilizzo della sicurezza a livello di riga dei cubi di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|Yes|No|No|  
  
 **<sup>1</sup>**[informazioni sul ruolo degli amministratori dei dati nella gestione dei dati](https://support.office.com/Article/Understanding-the-Role-of-Data-Stewards-in-Data-Management-ae3352f3-4389-45e8-a682-7fd6edb92524?ui=en-US&rs=en-US&ad=US) e [Video: Gestione delle informazioni di BI e amministrazione dei dati di Power](https://www.youtube.com/watch?v=8dHOj68ts7c).  
  
 **<sup>2</sup>**[di power BI domande e risposte: Ottimizzare una cartella di lavoro di Power BI (modellazione cloud)](https://powerbi.microsoft.com/nl-nl/blog/new-in-power-bi-cloud-modeling-for-q-and-a/).  
  
 **<sup>3</sup>**  [Introduzione alle nuove funzionalità di previsione in Power View per Office 365](https://blogs.msdn.com/b/powerbi/archive/2014/05/08/introducing-new-forecasting-capabilities-in-power-view-for-office-365.aspx).  
  
## <a name="view-and-browse-bi-data-reports-and-dashboards"></a>Visualizzare ed esplorare dati, report e dashboard di Business Intelligence  
  
||SQL Server 2014 & SharePoint Server 2013|SharePoint Online Piano 2|Power BI per Office 365|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|Visualizzazione delle cartelle di lavoro di Microsoft Excel in un browser|Sì, se le dimensioni della cartella di lavoro sono inferiori a 2 GB|Sì, se le dimensioni della cartella di lavoro sono inferiori a 10 MB|Sì, se le dimensioni della cartella di lavoro sono inferiori a 250 MB|  
|Esplorazione dei dati basati su browser in HTML5|No|no|Yes|  
|App di Business Intelligence per dispositivi mobili per accedere a report e dashboard in remoto|No|No|Sì **<sup>1</sup>**|  
|Cartella di lavoro di Excel con [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] come origine dati **<sup>2</sup>**|Yes|no|No|  
|Possibilità di usare le funzionalità in versioni e browser diversi|Sì, per le visualizzazioni non relative a Power View **<sup>3</sup>**|Sì, per cartelle di lavoro di dimensioni inferiori a 10 MB **<sup>3</sup>**|Sì **<sup>3</sup>**|  
  
 **<sup>1</sup>**  [Microsoft Power BI](http://apps.microsoft.com/windows/app/microsoft-power-bi/b7e7c94d-2ea3-4fa6-a277-9d19a1f697ba).  
  
 **<sup>2</sup>**  [Cartelle di lavoro di PowerPivot come origine dati](http://blogs.technet.com/b/excel_services__powerpivot_for_sharepoint_support_blog/archive/2013/02/15/powerpivot-workbook-as-a-data-source.aspx)  
  
 **<sup>3</sup>**  [Supporto mobile tra strumenti di Business Intelligence (BI)](https://msdn.microsoft.com/library/dn151146\(v=sql.110\).aspx) e [Pianificazione per il supporto del browser per Reporting Services e Power View (Reporting Services 2014)](https://msdn.microsoft.com/library/ms156511.aspx).  
  
## <a name="more-information"></a>Ulteriori informazioni  
  
- [Funzionalità di Business Intelligence in Excel e Office 365](https://support.office.com/article/BI-capabilities-in-Excel-and-Office-365-26c0548e-124c-4fd3-aab3-5f64568cb743).  
  
- Per informazioni sui requisiti per l'uso dei sinonimi, vedere [ottimizzazione di Power BI domande e risposte con sinonimi & formulazione](https://blog.pragmaticworks.com/optimizing-power-bi-qa-with-synonyms-phrasing-using-cloud-modeling) al sito Web pragmaticworks.com.  
  
- [Office Online-scegliere un social network aziendale: Yammer o Newsfeed? ](https://support.office.com/article/Pick-your-enterprise-social-network-Yammer-or-Newsfeed-21954c85-4384-47d4-96c2-dfa1c9d56e66?ui=en-US&rs=en-US&ad=US).  
  
- [Power BI per Office 365](https://www.microsoft.com/powerbi/default.aspx)  
  
- [Prezzi di Power BI](https://www.microsoft.com/powerBI/pricing.aspx)  
  
- [Analisi e creazione di report con strumenti Microsoft business intelligence (BI)](../reporting-services/choosing-microsoft-business-intelligence-bi-tools-for-analysis-and-reporting.md)  
  
## <a name="community-content"></a>Contenuto della community

[Microsoft BI in modalità self-service in locale e nel cloud](http://businessintelligist.com/2014/02/07/microsoft-self-service-bi-on-premise-vs-could/)