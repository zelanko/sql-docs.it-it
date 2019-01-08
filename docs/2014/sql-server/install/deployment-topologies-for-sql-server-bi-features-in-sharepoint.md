---
title: Topologie di distribuzione per le funzionalità SQL Server BI in SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 39f76bc7-94e6-4dbc-bfa5-d56f4430bb26
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 2bcb706eda464730d978d0098281c2ebcd2336ed
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53365763"
---
# <a name="deployment-topologies-for-sql-server-bi-features-in-sharepoint"></a>Topologie di distribuzione per funzionalità di Business Intelligence di SQL Server in SharePoint
  In questo argomento vengono descritte le topologie comuni per l'installazione delle funzionalità [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] di SQL Server Business Intelligence negli ambienti SharePoint 2010 e SharePoint 2013. Ad esempio installazioni a server singolo e a tre livelli.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|  
  
 **Contenuto dell'argomento:**  
  
-   [Topologie di distribuzione di esempio di SharePoint 2013](#bkmk_example_deployments_2013)  
  
    -   [Distribuzione a tre Server di PowerPivot per SharePoint 2013 e Reporting Services](#bkmk_bi_Sharepoint2013_3tier)  
  
    -   [PowerPivot per SharePoint 2013 distribuzione a Server singolo](#bkmk_powerpivot_sharepoint2013_1server)  
  
    -   [PowerPivot per SharePoint 2013 due Server di distribuzione](#bkmk_powerpivot_sharepoint2013_2server)  
  
    -   [PowerPivot per SharePoint 2013 tre Server di distribuzione](#bkmk_powerpivot_sharepoint2013_3server)  
  
    -   [PowerPivot per SharePoint 2013 e Reporting Services distribuzione a Server singolo](#bkmk_powerpivot_ssrs_sharepoint2013_1server)  
  
    -   [Distribuzione a due Server di PowerPivot per SharePoint 2013 e Reporting Services](#bkmk_powerpivot_ssrs_sharepoint2013_2server)  
  
-   [Topologie di distribuzione di esempio di SharePoint 2010](#bkmk_example_deployments_2010)  
  
    -   [Distribuzioni a Server singolo](#bkmk_sharepoint2010_1server)  
  
    -   [Distribuzione a due livelli](#bkmk_sharepoint2010_2server)  
  
    -   [Distribuzione a tre livelli](#bkmk_sharepoint2010_3server)  
  
    -   [Distribuzione con scalabilità orizzontale a tre livelli](#bkmk_sharepoint2010_scaleserver)  
  
##  <a name="bkmk_example_deployments_2013"></a> Topologie di distribuzione di esempio di SharePoint 2013  
 L'opzione di installazione di SQL Server **PowerPivot per SharePoint** è priva di dipendenze da SharePoint. In essa non vengono utilizzati il modello a oggetti o le interfacce di SharePoint per supportare l'integrazione. Pertanto, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] può essere installato in tutti i computer con Windows Server 2008 R2 o versione successiva. Può trattarsi, senza obbligo, di un server applicazioni in una farm di SharePoint. Uno dei passaggi di configurazione consiste nel puntare Excel Services al server in cui viene eseguito [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per il bilanciamento del carico e la tolleranza di errore, si consiglia di installare e registrare più server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in esecuzione in modalità SharePoint.  
  
 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modalità SharePoint** richiede SharePoint server 2013 e viene utilizzata l'architettura di applicazione di servizio SharePoint.  
  
 Nelle sezioni seguenti vengono illustrate topologie di distribuzione tipiche:  
  
###  <a name="bkmk_bi_Sharepoint2013_3tier"></a> Distribuzione a tre Server di PowerPivot per SharePoint 2013 e Reporting Services  
 Nella distribuzione a tre server il motore di database di SQL Server, il server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in esecuzione in modalità SharePoint e SharePoint vengono eseguiti ognuno in un server diverso. Il pacchetto di installazione di [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] 2013 (**spPowerPivot.msi**) deve essere eseguito nel server SharePoint.  
  
 ![Modalità SharePoint per SSRS e SSAS 3 Server di distribuzione](../../../2014/sql-server/install/media/as-and-rs-3server-deployment.gif "in modalità SharePoint per SSRS e SSAS 3 Server di distribuzione")  
  
|||  
|-|-|  
|**(1)**|Applicazione Excel Services. L'applicazione di servizio viene creata durante l'installazione di SharePoint.|  
|**(2)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Applicazione di servizio. Il nome predefinito è **Applicazione di servizio PowerPivot predefinita**.|  
|**(3)**|Applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|**(4)**|Installare il componente aggiuntivo Reporting Services per SharePoint dai supporti di installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o dal feature pack di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .|  
|**(5)**|Eseguire **spPowerPivot.msi** per installare i provider di dati, lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , Raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e pianificare l'aggiornamento dati.|  
|**(6)**|Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità SharePoint. Configurare **Impostazioni modello di dati** dell'applicazione Excel services per l'utilizzo di questo server.|  
|**(7)**|Database dell'applicazione di servizio, di configurazione e del contenuto di SharePoint.|  
  
 ![Impostazioni di SharePoint](../../../2014/analysis-services/media/as-sharepoint2013-settings-gear.gif "impostazioni SharePoint") [Invia commenti e suggerimenti e informazioni di contatto tramite Microsoft SQL Server Connect](https://connect.microsoft.com/SQLServer/Feedback) (https://connect.microsoft.com/SQLServer/Feedback).  
  
###  <a name="bkmk_powerpivot_sharepoint2013_1server"></a> PowerPivot per SharePoint 2013 distribuzione a Server singolo  
 La distribuzione a server singolo è utile ai fini del test, ma non è consigliata per distribuzioni di produzione.  
  
 Nel diagramma seguente sono illustrati i componenti che fanno parte di una distribuzione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a server singolo.  
  
 ![PowerPivot per la distribuzione a Server singolo di SharePoint](../../../2014/sql-server/install/media/as-powerpivot-mode-1server-deployment.gif "PowerPivot per la distribuzione a Server singolo di SharePoint")  
  
|||  
|-|-|  
|**(1)**|Applicazione Excel Services. L'applicazione di servizio viene creata durante l'installazione di SharePoint.|  
|**(2)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Applicazione di servizio. Il nome predefinito è **Applicazione di servizio PowerPivot predefinita**.|  
|**(3)**|Database dell'applicazione di servizio, di configurazione e del contenuto di SharePoint.|  
|**(4)**|Un server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità SharePoint. Configurare **Impostazioni modello di dati** dell'applicazione Excel services per l'utilizzo di questo server.|  
  
###  <a name="bkmk_powerpivot_sharepoint2013_2server"></a> PowerPivot per SharePoint 2013 due Server di distribuzione  
 Nella distribuzione a due server seguente, il motore di database di SQL Server e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità SharePoint vengono eseguiti in un server diverso da SharePoint. Per SharePoint 2013 il pacchetto di installazione di [!INCLUDE[ssGeminiLongvnext](../../includes/ssgeminilongvnext-md.md)] (**spPowerPivot.msi**) è installato nel server SharePoint.  
  
 [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] estende SharePoint Server 2013 per aggiungere l'elaborazione, dell'aggiornamento dati lato server, i provider di dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] della raccolta e il supporto di gestione per [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] cartelle di lavoro e le cartelle di lavoro di Excel con modelli di dati avanzati.  
  
 Il pacchetto di installazione è disponibile come parte del Feature Pack di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] . Il feature pack può essere scaricato dal [!INCLUDE[msCoName](../../includes/msconame-md.md)] area download all'indirizzo [PowerPivot® Microsoft® SQL Server® 2014 per Microsoft® SharePoint®](https://go.microsoft.com/fwlink/?LinkID=296473) (HYPERLINK "<https://go.microsoft.com/fwlink/?LinkID=296473>" \t blank" <https://go.microsoft.com/fwlink/?LinkID=296473>).  
  
 ![Distribuzione di Server PowerPivot in modalità 2 SSAS](../../../2014/analysis-services/media/as-powerpivot-mode-2server-deployment.gif "distribuzione di Server SSAS PowerPivot modalità 2")  
  
|||  
|-|-|  
|**(1)**|Applicazione Excel Services. L'applicazione di servizio viene creata durante l'installazione di SharePoint.|  
|**(2)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Applicazione di servizio. Il nome predefinito è **Applicazione di servizio PowerPivot predefinita**.|  
|**(3)**|ESEGUIRE **spPowerPivot.msi** per installare i provider di dati, lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , Raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e pianificare l'aggiornamento dati.|  
|**(4)**|Un server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità SharePoint. Configurare **Impostazioni modello di dati** dell'applicazione Excel services per l'utilizzo di questo server.|  
|**(5)**|Database dell'applicazione di servizio, di configurazione e del contenuto di SharePoint.|  
  
###  <a name="bkmk_powerpivot_sharepoint2013_3server"></a> PowerPivot per SharePoint 2013 tre Server di distribuzione  
 Nella distribuzione a tre server il motore di database di SQL Server, il server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in esecuzione in modalità SharePoint e SharePoint vengono eseguiti ognuno in un server diverso. Il pacchetto di installazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 (spPowerPivot.msi) deve essere installato nel server SharePoint.  
  
 ![DISTRIBUZIONE di Server PowerPivot Mode3](../../../2014/sql-server/install/media/as-powerpivot-mode-3server-deployment.gif "come distribuzione di Server PowerPivot Mode3")  
  
|||  
|-|-|  
|**(1)**|Applicazione Excel Services. L'applicazione di servizio viene creata durante l'installazione di SharePoint.|  
|**(2)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Applicazione di servizio. Il nome predefinito è **Applicazione di servizio PowerPivot predefinita**.|  
|**(3)**|ESEGUIRE spPowerPivot.msi per installare i provider di dati, lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , Raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e pianificare l'aggiornamento dati.|  
|**(4)**|Un server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità SharePoint. Configurare **Impostazioni modello di dati** dell'applicazione Excel services per l'utilizzo di questo server.|  
|**(5)**|Database dell'applicazione di servizio, di configurazione e del contenuto di SharePoint.|  
  
###  <a name="bkmk_powerpivot_ssrs_sharepoint2013_1server"></a> PowerPivot per SharePoint 2013 e Reporting Services distribuzione a Server singolo  
 La distribuzione a server singolo è utile ai fini del test, ma non è consigliata per distribuzioni di produzione.  
  
 ![Modalità SharePoint per SSRS e SSAS 1 Server di distribuzione](../../../2014/sql-server/install/media/as-and-rs-1server-deployment.gif "in modalità SharePoint per SSRS e SSAS 1 Server di distribuzione")  
  
|||  
|-|-|  
|**(1)**|Applicazione Excel Services. L'applicazione di servizio viene creata durante l'installazione di SharePoint.|  
|**(2)**|Applicazione di servizio PowerPivot. Il nome predefinito è **Applicazione di servizio PowerPivot predefinita**.|  
|**(3)**|Applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|**(4)**|Installare il componente aggiuntivo Reporting Services per SharePoint dai supporti di installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o dal feature pack di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .|  
|**(5)**|Database dell'applicazione di servizio, di configurazione e del contenuto di SharePoint.|  
|**(6)**|Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità SharePoint. Configurare **Impostazioni modello di dati** dell'applicazione Excel services per l'utilizzo di questo server.|  
  
###  <a name="bkmk_powerpivot_ssrs_sharepoint2013_2server"></a> Distribuzione a due Server di PowerPivot per SharePoint 2013 e Reporting Services  
 Nella distribuzione a due server seguente il motore di database di SQL Server e il server Analysis Services in esecuzione in modalità SharePoint vengono eseguiti in un server diverso da SharePoint. Il pacchetto di installazione di PowerPivot per SharePoint 2013 **(spPowerPivot.msi)** deve essere eseguito nel server SharePoint.  
  
 ![Distribuzione a Server in modalità SharePoint 2 SSRS e SSAS](../../../2014/sql-server/install/media/as-and-rs-2server-deployment.gif "distribuzione Server modalità SharePoint 2 per SSRS e SSAS")  
  
|||  
|-|-|  
|**(1)**|Applicazione Excel Services. L'applicazione di servizio viene creata durante l'installazione di SharePoint.|  
|**(2)**|Applicazione di servizio PowerPivot. Il nome predefinito è **Applicazione di servizio PowerPivot predefinita**.|  
|**(3)**|Applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|**(4)**|Installare il componente aggiuntivo Reporting Services per SharePoint dai supporti di installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o dal feature pack di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .|  
|**(5)**|ESEGUIRE **spPowerPivot.msi** per installare i provider di dati, lo strumento di configurazione PowerPivot, Raccolta PowerPivot e pianificare l'aggiornamento dati.|  
|**(6)**|Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità SharePoint. Configurare **Impostazioni modello di dati** dell'applicazione Excel services per l'utilizzo di questo server.|  
|**(7)**|Database dell'applicazione di servizio, di configurazione e del contenuto di SharePoint.|  
  
##  <a name="bkmk_example_deployments_2010"></a> Topologie di distribuzione di esempio di SharePoint 2010  
 Nel diagramma seguente vengono mostrati i servizi e i provider eseguiti in ogni livello. Si noti che il diagramma include diversi servizi predefiniti, richiesti per alcuni scenari di Business Intelligence di SQL Server. Excel Services, servizio di archiviazione sicura e Claims to Windows Token Service sono richiesti o consigliati per una distribuzione di PowerPivot per SharePoint o di Reporting Services in SharePoint. Inoltre, i provider MSOLAP OLE DB e i servizi ADO.NET sono richiesti per alcuni scenari di accesso ai dati PowerPivot. Facoltativamente, è possibile installare Analysis Services nel livello dati se si desidera compilare report [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] basati su database modello tabulari ospitati all'esterno di SharePoint.  
  
 ![Diagramma dell'architettura logica](../../../2014/sql-server/install/media/sql11bisetup.gif "diagramma dell'architettura logica")  
  
##  <a name="bkmk_sharepoint2010_1server"></a> Distribuzioni a Server singolo  
 È possibile installare tutti i componenti server, compreso il livello dati, in un unico computer. Questa configurazione di distribuzione è utile per la valutazione del software o lo sviluppo di applicazioni personalizzate che includono Reporting Services in modalità SharePoint. Questa distribuzione è la più semplice da configurare. Poiché tutti i componenti sono installati nello stesso computer, viene anche utilizzata la quantità minima di licenze. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] e il [!INCLUDE[ssDE](../../includes/ssde-md.md)] vengono installati come una singola copia con licenza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Per installare tutte le caratteristiche in un server unico, installare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] in sequenza nello stesso server fisico. Per istruzioni sulla configurazione server autonoma, vedere [elenco di controllo distribuzione: Reporting Services, Power View e PowerPivot per SharePoint](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md).  
  
##  <a name="bkmk_sharepoint2010_2server"></a> Distribuzione a due livelli  
 Una distribuzione a due livelli prevede in genere SharePoint Server 2010 in un computer e il motore di database di SQL Server nel secondo computer. Lo spostamento del livello dati in un server dedicato è la configurazione più comune per una farm a 2 computer. In una farm a due livelli, installare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] nel server SharePoint. Tutti i servizi Web sul front-end e i servizi condivisi nel livello applicazione vengono eseguiti sullo stesso server fisico. I passaggi di installazione per una distribuzione a due livelli sono molto simili a una distribuzione autonoma, in quanto [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] vengono installati in modo sequenziale nello stesso server fisico.  
  
##  <a name="bkmk_sharepoint2010_3server"></a> Distribuzione a tre livelli  
 In una distribuzione a tre livelli vengono in genere separati i servizi front-end Web dall'elaborazione o dalle applicazioni che utilizzano una quantità elevata di memoria. In questa topologia, installare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] solo nel server applicazioni. I servizi Web in esecuzione sul front-end Web vengono installati tramite soluzioni distribuite in applicazioni nella farm, durante la configurazione server, come un'attività successiva all'installazione. Nel diagramma seguente viene illustrata una distribuzione a tre livelli.  
  
 ![topologia server 3](../../../2014/sql-server/install/media/sql11bisetup-3server.gif "topologia server 3")  
  
##  <a name="bkmk_sharepoint2010_scaleserver"></a> Distribuzione con scalabilità orizzontale a tre livelli  
 Questa topologia illustra una distribuzione con scalabilità orizzontale che esegue lo stesso servizio condiviso su più server, in grado di soddisfare un volume più grande di richieste e di fornire una maggiore potenza di elaborazione per dati PowerPivot o report di Reporting Services. Nel diagramma sottostante, sono presenti tre cluster di server applicazioni, ognuno dei quali esegue una combinazione diversa di servizi condivisi. In un ambiente SharePoint, l'individuazione e la disponibilità del servizio sono incorporate nella farm. Il bilanciamento del carico tra più server fisici che eseguono la stessa applicazione di servizio condivisa è parte dell'architettura di servizi condivisi.  
  
 Quando si distribuisce una farm multiserver, assicurarsi di seguire le istruzioni riportate in questo articolo relativo a SharePoint: [Più server per una farm a tre livelli (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?linkID=219834).  
  
 ![5 server topologia](../../../2014/sql-server/install/media/sql11bisetup-5server.gif "topologia 5 server")  
  
## <a name="see-also"></a>Vedere anche  
 [Installazione in modalità SharePoint di Reporting Services &#40;SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)   
 [PowerPivot per SharePoint 2013 Installation](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)   
 [Installazione di PowerPivot per SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
