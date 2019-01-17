---
title: Funzionalità di Reporting Services supportate dalle edizioni di SQL Server
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.date: 11/01/2018
ms.openlocfilehash: 37dec44c539db86f8f0d239fffe0ca28699f2799
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645330"
---
# <a name="reporting-services-features-supported-by-the-editions-of-sql-server"></a>Funzionalità di Reporting Services supportate dalle edizioni di SQL Server

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Questo argomento illustra i dettagli delle funzionalità di Reporting Services supportate dalle diverse edizioni di SQL Server. SQL Server Evaluation Edition è disponibile per un periodo di valutazione di 180 giorni.  
  
 Per le note sulla versione più recenti di SQL Server, vedere [Note sulla versione di SQL Server 2017](../sql-server/sql-server-2017-release-notes.md). Per le ultime informazioni sulle novità, vedere [Novità di Reporting Services (SSRS)](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md).

 **Per provare SQL Server 2017**    

> [![Scaricare SQL Server 2017](../analysis-services/media/download.png)](https://go.microsoft.com/fwlink/?LinkID=829477) **[Scaricare SQL Server 2017 da Evaluation Center](https://go.microsoft.com/fwlink/?LinkID=829477)**    
>
> ![Macchina virtuale di Azure piccola](../analysis-services/media/azure-virtual-machine-small.png) **[Attivare una macchina virtuale con SQL Server 2017 già installato](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)**    

Per le funzionalità supportate dalle edizioni Evaluation e Developer, vedere la colonna SQL Server Enterprise Edition.

##  <a name="SSRS"></a> Reporting Services  
  
|Nome funzionalità|Enterprise|Standard|Web|Express with Advanced Services|Developer|  
|------------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Report e KPI per dispositivi mobili|Sì||||Sì|  
|Edizione supportata di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per il database del catalogo|Standard o versione successiva|Standard o versione successiva|Web|Express|Standard o versione successiva|  
|Edizione supportata di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per le origini dati|Tutte le edizioni di   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Tutte le edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Web|Express|Tutte le edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|  
|Server di report|Sì|Sì|Sì|Sì|Sì|  
|Progettazione report|Sì|Sì|Sì|Sì|Sì|  
|Portale Web di Progettazione report|Sì|Sì|Sì|Sì|Sì|  
|Sicurezza basata sui ruoli|Sì|Sì|Sì|Sì|Sì|  
|Esportazione in Excel, PowerPoint, Word, PDF e immagini|Sì|Sì|Sì|Sì|Sì|  
|Misuratori e grafici migliorati|Sì|Sì|Sì|Sì|Sì|  
|Aggiungere elementi di un report a dashboard di [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]|Sì|Sì|Sì|Sì|Sì|  
|Autenticazione personalizzata|Sì|Sì|Sì||Sì|  
|Dati del report come feed di dati|Sì|Sì|Sì|Sì|Sì|  
|Supporto modelli|Sì|Sì|Sì||Sì|  
|Creare ruoli personalizzati per la sicurezza basata sui ruoli|Sì|Sì|||Sì|  
|Sicurezza elemento modello|Sì|Sì|||Sì|  
|Click-through illimitato|Sì|Sì|||Sì|  
|Libreria componenti condivisa|Sì|Sì|||Sì|  
|Sottoscrizioni e pianificazione posta elettronica e condivisione file|Sì|Sì|||Sì|  
|Cronologia report, esecuzione snapshot e memorizzazione nella cache|Sì|Sì|||Sì|  
|Integrazione con SharePoint|Sì|Sì|||Sì|  
|Supporto origini dati remote e non SQL<sup>1</sup>|Sì|Sì|||Sì|  
|Estensibilità RDCE per il rendering, il recapito e le origini dati|Sì|Sì|||Sì|  
|Personalizzazione|Sì||||Sì|  
|Sottoscrizione di report guidate dai dati|Sì||||Sì|  
|Distribuzione con scalabilità orizzontale (Web farm)|Sì||||Sì|  
|Avvisi<sup>2</sup> (SSRS 2016) |Sì||||Sì|  
| Power View<sup>2</sup> (SSRS 2016) |Sì||||Sì| 
|Commenti<sup>3</sup> |Sì|Sì|Sì|Sì|Sì|  

 <sup>1</sup> Per altre informazioni sulle origini dati supportate in SQL Server Reporting Services (SSRS), vedere [Origini dei dati supportate da Reporting Services &#40;SSRS&#41;](../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
 <sup>2</sup> Richiede Reporting Services 2016 in modalità SharePoint. Per altre informazioni, vedere [Installare la modalità SharePoint di Reporting Services](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md). A partire da Reporting Services 2017, l'integrazione di Reporting Services con SharePoint non è più disponibile. 

<sup>3</sup> Solo nel server di report di Power BI e in Reporting Services 2017 e versioni successive.

> [!NOTE]
> SQL Server Express e SQL Server Express with Tools non supportano SQL Server Reporting Services.
  
## <a name="report-server-database-server-edition-requirements"></a>Requisiti dell'edizione server del database del server di report
 Quando si crea un database del server di report, non tutte le edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] possono essere usate per ospitare il database. Nella tabella seguente sono illustrate le edizioni del [!INCLUDE[ssDE](../includes/ssde-md.md)] che è possibile usare per le edizioni specifiche di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
|Per questa edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services|Edizione dell'istanza del Motore di database da usare per ospitare il database|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Edizioni Enterprise o Standard (locali o remote)|  
|Standard|Edizioni Enterprise o Standard (locali o remote)|  
|Web|Web Edition (solo locale)|  
|Express with Advanced Services|Express with Advanced Services (solo locale).|  
|Copia di valutazione|Copia di valutazione|  
  
##  <a name="BIC"></a> Client di Business Intelligence  
 Le seguenti applicazioni client del software sono disponibili nell'Area download Microsoft e sono disponibili come supporto per la creazione di documenti di Business Intelligence eseguiti in un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Quando questi documenti vengono ospitati in un ambiente server, usare un'edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] supportata per tale tipo di documento. Nella tabella seguente viene indicata l'edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contenente le funzionalità del server richieste per ospitare i documenti creati in queste applicazioni client.  
  
|Nome dello strumento|Enterprise|Standard|Web|Express with Advanced Services|Developer|  
|---------------|----------------|--------------|------------------------|-------------|---------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)] (rdl e rds)|Sì|Sì|Sì|Sì|Sì|  
|[!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] (rsmobile)|Sì||||Sì|  
|App di Power BI per dispositivi mobili (iOS, Windows 10, Android) (rsmobile)|Sì||||Sì|  
  
> [!NOTE]  
> 1. La tabella sopra riportata identifica le edizioni [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] richieste per abilitare gli strumenti client; le funzionalità possono tuttavia accedere ai dati ospitati in ogni edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
> 2. [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] è il punto singolo per la creazione di report per dispositivi mobili. Connettersi a un server di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per accedere alle origini dati e creare report. Pubblicare quindi i report nel server di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per consentire l'accesso ad altri utenti dell'organizzazione, nel server o nei dispositivi mobili. È anche possibile usare [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] autonomo con origini dati locali  
> 3. Se si usa  [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] in locale, [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] nel cloud o entrambi come soluzione di recapito dei report, è necessaria una sola app per dispositivi mobili per accedere a dashboard e report sui dispositivi mobili. Le app di [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] sono disponibili per il download dall'App Store di Windows, iOS o Android.  

## <a name="next-steps"></a>Passaggi successivi

[Funzionalità supportate dalle edizioni di SQL Server 2017](~/sql-server/editions-and-components-of-sql-server-2017.md)  
[Pianificazione di un'installazione di SQL Server](../sql-server/install/planning-a-sql-server-installation.md) 

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
