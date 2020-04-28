---
title: Confrontare le funzionalità di business intelligence in diversi ambienti Microsoft | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 12/15/2019
ms.openlocfilehash: a5f9e9b52186a2d4569ac30a591ae95acfa36101
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "75656588"
---
# <a name="compare-business-intelligence-capabilities-in-different-microsoft-environments"></a>Confrontare le funzionalità di Business Intelligence in diversi ambienti Microsoft

Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Business Intelligence può essere distribuito in numerosi ambienti diversi, tra cui [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con SharePoint Server, SharePoint Online e Power BI per Office 365. In questo argomento vengono confrontati i componenti e le funzionalità supportati in ogni ambiente.  
  
Per altre informazioni sul confronto tra SharePoint Server e SharePoint Online, vedere [Confrontare piani e opzioni di SharePoint](https://products.office.com/SharePoint/compare-sharepoint-plans).  
  
## <a name="author-and-manage-bi-reports-and-dashboards"></a>Creare e gestire report e dashboard di Business Intelligence  
  
||SQL Server 2014 & SharePoint Server 2013|SharePoint Online Piano 2|Power BI per Office 365|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|Siti di Business Intelligence|Raccolta [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]|No|Sito di Power BI|  
|Amministrazione dei dati e gestione e condivisione delle query|No|No|Sì ** <sup>1</sup>**|  
|Integrazione con Master Data Services (MDS) e Data Quality Services (DQS)|Sì|No|No|  
|Pianificazione dell'aggiornamento dati|Sì, ma non sono supportate le cartelle di lavoro che contengono dati di Power Query|No|Sì|  
|Query in linguaggio naturale (Q&A)|No|No|Sì ** <sup>2</sup>**|  
|Previsione predittiva|No|No|Sì ** <sup>3</sup>**|  
|Integrazione di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Sì|No|No|  
|Integrazione di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] (multidimensionale e tabulare)|Sì|No|No|  
|Esportazione di dashboard interattivi di Power View nelle presentazioni di PowerPoint|Sì|No|No|  
|Creazione di dashboard basati su browser|Sì|No|No|  
|Monitoraggio dell'utilizzo|Sì|No|Sì|  
|Utilizzo della sicurezza a livello di riga dei cubi di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|Sì|No|No|  
|||||

 **<sup>1</sup>**  [Informazioni sul ruolo degli amministratori dei dati nella gestione dei dati](https://support.office.com/Article/Understanding-the-Role-of-Data-Stewards-in-Data-Management-ae3352f3-4389-45e8-a682-7fd6edb92524?ui=en-US&rs=en-US&ad=US) e [Video: Gestione delle informazioni e amministrazione dei dati di Power BI](https://www.youtube.com/watch?v=8dHOj68ts7c).  
  
 **<sup>2</sup>**  [Power bi Q&a: ottimizzare una cartella di lavoro di Power BI (modellazione cloud)](https://powerbi.microsoft.com/nl-nl/blog/new-in-power-bi-cloud-modeling-for-q-and-a/).  
  
 **<sup>3</sup>**  [Introduzione alle nuove funzionalità di previsione in Power View per Office 365](https://blogs.msdn.com/b/powerbi/archive/2014/05/08/introducing-new-forecasting-capabilities-in-power-view-for-office-365.aspx).  
  
## <a name="view-and-browse-bi-data-reports-and-dashboards"></a>Visualizzare ed esplorare dati, report e dashboard di Business Intelligence  
  
||SQL Server 2014 & SharePoint Server 2013|SharePoint Online Piano 2|Power BI per Office 365|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|Visualizzazione delle cartelle di lavoro di Microsoft Excel in un browser|Sì, se le dimensioni della cartella di lavoro sono inferiori a 2 GB|Sì, se le dimensioni della cartella di lavoro sono inferiori a 10 MB|Sì, se le dimensioni della cartella di lavoro sono inferiori a 250 MB|  
|Esplorazione dei dati basati su browser in HTML5|No|No|Sì|  
|App di Business Intelligence per dispositivi mobili per accedere a report e dashboard in remoto|No|No|Sì ** <sup>1</sup>**|  
|Cartella di lavoro di Excel con [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] come origine dati **<sup>2</sup>**|Sì|No|No|  
|Possibilità di usare le funzionalità in versioni e browser diversi|Sì, per le visualizzazioni non relative a Power View **<sup>3</sup>**|Sì, per cartelle di lavoro di dimensioni inferiori a 10 MB **<sup>3</sup>**|Sì ** <sup>3</sup>**|  
|||||

 **<sup>1</sup>**  [Microsoft Power BI](https://apps.microsoft.com/windows/app/microsoft-power-bi/b7e7c94d-2ea3-4fa6-a277-9d19a1f697ba).  
  
 **<sup>2</sup>**  [Cartelle di lavoro di PowerPivot come origine dati](https://support.office.com/article/Power-Pivot-Powerful-data-analysis-and-data-modeling-in-Excel-A9C2C6E2-CC49-4976-A7D7-40896795D045)  
  
 **<sup>3</sup>**  [Supporto mobile tra strumenti di Business Intelligence (BI)](https://msdn.microsoft.com/library/dn151146\(v=sql.110\).aspx) e [Pianificazione per il supporto del browser per Reporting Services e Power View (Reporting Services 2014)](https://msdn.microsoft.com/library/ms156511.aspx).  
  
## <a name="more-information"></a>Ulteriori informazioni  
  
- [Funzionalità di business intelligence in Excel e Office 365](https://support.office.com/article/BI-capabilities-in-Excel-and-Office-365-26c0548e-124c-4fd3-aab3-5f64568cb743).  
  
- Per informazioni sui requisiti per l'uso dei sinonimi, vedere [ottimizzazione di Power bi domande e risposte&a con sinonimi &](https://blog.pragmaticworks.com/optimizing-power-bi-qa-with-synonyms-phrasing-using-cloud-modeling) formulazione in pragmaticworks.com.  
  
- [Office Online - Scegliere un social network aziendale: Yammer o Newsfeed?](https://support.office.com/article/Pick-your-enterprise-social-network-Yammer-or-Newsfeed-21954c85-4384-47d4-96c2-dfa1c9d56e66?ui=en-US&rs=en-US&ad=US).  
  
- [Power BI per Office 365](https://www.microsoft.com/powerbi/default.aspx)  
  
- [Prezzi Power bi](https://www.microsoft.com/powerBI/pricing.aspx).  
  
- [Analisi dei dati e creazione di report con gli strumenti di business intelligence (BI) di Microsoft](../reporting-services/choosing-microsoft-business-intelligence-bi-tools-for-analysis-and-reporting.md)  
  
## <a name="community-content"></a>Contenuto della community

