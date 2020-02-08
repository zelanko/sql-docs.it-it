---
title: Guida all'installazione di SQL Server
ms.description: 'An index of content that helps you install SQL Server and associated components through various options such as the installation wizard, command prompt, or sysprep. '
ms.custom: ''
ms.date: 11/14/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- AdventureWorks sample database
- installing SQL Server, preparing to install
- installation [SQL Server]
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 30155a37f57391edeee916cd2b6629d63a1dcaaa
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "75688248"
---
# <a name="sql-server-installation-guide"></a>Guida all'installazione di SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo è un indice dei contenuti che forniscono indicazioni per l'installazione di SQL Server in Windows.

Per altri scenari di distribuzione, vedere:

- [Linux](../../linux/sql-server-linux-setup.md)
- [Contenitori Docker](../../linux/sql-server-linux-configure-docker.md)
- [Kubernetes - Cluster Big Data](../../big-data-cluster/deploy-get-started.md)

A partire da [!INCLUDE[sssql15](../../includes/sssql15-md.md)], [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] è disponibile solo come applicazione a 64 bit. Di seguito sono riportati importanti dettagli su come ottenere SQL Server e su come eseguire l'installazione.

## <a name="getting-started"></a>Introduzione
  
* **Edizioni e funzionalità**: Esaminare le funzionalità supportate per le diverse edizioni e versioni di SQL Server per determinare la soluzione più adatta alle proprie esigenze aziendali. 
    - [[!INCLUDE[ss2019](../../includes/sssqlv15-md.md)]](~/sql-server/editions-and-components-of-sql-server-version-15.md).  
    - [[!INCLUDE[ss2017](../../includes/sssqlv14-md.md)]](~/sql-server/editions-and-components-of-sql-server-2017.md).  
    - [[!INCLUDE[ss2016](../../includes/sssql15-md.md)]](~/sql-server/editions-and-components-of-sql-server-2016.md).  
    - [[!INCLUDE[ss2014](../../includes/sssql14-md.md)]](https://technet.microsoft.com/library/cc645993(v=sql.120).aspx)

*  **Requisiti**: Rivedere i requisiti di installazione, i controlli di configurazione del sistema e le considerazioni sulla sicurezza in [Pianificazione di un'installazione di SQL Server](../../sql-server/install/planning-a-sql-server-installation.md) 
  
* **Esempi di database e di codice**: 
    * Non sono installati come parte predefinita dell'installazione di SQL Server, ma possono essere reperiti 
    * Per installarli per edizioni non Express di SQL Server, vedere [dove si trovano gli esempi](../../samples/sql-samples-where-are.md)
    

## <a name="installation-media"></a>Supporto di installazione

La posizione per il download di [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] dipende dall'edizione:

* **SQL Server Enterprise Edition, Standard Edition ed Express Edition** sono concessi in licenza per l'uso in ambienti di produzione. Per l'Enterprise Edition e la Standard Edition, richiedere il supporto di installazione al fornitore software di fiducia. È possibile trovare informazioni sull'acquisto e una directory per i partner Microsoft nella [pagina Microsoft delle licenze](https://www.microsoft.com/licensing/product-licensing/sql-server).
* [Versione gratuita - più recente](https://www.microsoft.com/sql-server/sql-server-downloads)
* [Versione gratuita - altre](https://www.microsoft.com/evalcenter/evaluate-sql-server)


Altri componenti SQL Server sono disponibili qui: 

* [Tutti gli aggiornamenti cumulativi](https://sqlserverbuilds.blogspot.com/)
* [SQL Server Reporting Services](https://www.microsoft.com/download/details.aspx?id=100122). 
* [SQL Server Management Studio](https://aka.ms/ssmsfullsetup)
* [Azure Data Studio](https://go.microsoft.com/fwlink/?linkid=2109256)


## <a name="sql-server-installation"></a>Installazione di SQL Server
 
|Articolo|Descrizione|  
|-----------|-----------------|  
|[Installazione guidata](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)|Installare SQL Server tramite l'interfaccia utente dell'installazione guidata avviata dal supporto di installazione Setup.exe. |  
|[Prompt dei comandi](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)|Sintassi e parametri di installazione di esempio per l'esecuzione di un'installazione di SQL Server dal prompt dei comandi. | 
|[Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md)|Installare [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] in Windows Server Core.|  
|[Parametri di controllo di Controllo configurazione sistema](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)|Descrive la funzione di controllo configurazione sistema (SCC).|   
|[File di configurazione](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)|Sintassi di esempio e parametri di installazione per l'esecuzione del programma di installazione tramite un file di configurazione.|  
|[SysPrep](../../database-engine/install-windows/install-sql-server-using-sysprep.md)|Sintassi di esempio e parametri di installazione per l'esecuzione del programma di installazione tramite SysPrep.|
|[Aggiungere funzionalità a un'istanza](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)|Aggiornare i componenti di un'istanza esistente di [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].|  
|[Installazione del cluster di failover di SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)| Aggiornare un'istanza del cluster di failover di SQL Server.  | 
|[Ripristinare un'installazione non riuscita di [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)|Ripristinare un'installazione di [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] danneggiata.|  
|[Rinominare un computer con SQL Server](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)|Aggiornare i metadati di sistema archiviati in sys.servers dopo la modifica del nome host di un computer che ospita un'istanza autonoma di SQL Server. |  
|[Installare gli aggiornamenti di manutenzione per [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/install-sql-server-servicing-updates.md)|Installare gli aggiornamenti per [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].|  
|[File di log del programma di installazione](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)| Visualizzare e leggere gli errori nei file di log del programma di installazione di SQL Server. |  
|[Convalidare un'installazione](../../database-engine/install-windows/validate-a-sql-server-installation.md)|Esaminare l'utilizzo del report SQL Discovery per verificare la versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installate nel computer.|  
  
  
## <a name="individual-component-installation"></a>Installazione di singoli componenti 
  
|Articolo|Descrizione|  
|-----------|-----------------|  
|[Motore di database di SQL Server](../../database-engine/install-windows/install-sql-server-database-engine.md)|Installare e configurare il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
|[Replica di SQL Server](../../database-engine/install-windows/install-sql-server-replication.md)|Installare e configurare la replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Riesecuzione distribuita](../../tools/distributed-replay/install-distributed-replay-overview.md)|Elenca gli articoli sull'installazione della funzionalità Riesecuzione distribuita.|  
|[Strumenti di gestione di SQL Server con SSMS](https://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381)|Installare e configurare gli strumenti di gestione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[SQL Server PowerShell](../../database-engine/install-windows/install-sql-server-powershell.md)|Considerazioni per l'installazione dei componenti di PowerShell per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  

## <a name="sql-server-configuration"></a>Configurazione di SQL Server 
  
|Articolo|Descrizione|  
|-----------|-----------------|  
|[Configurare Windows Firewall (SQL Server)](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|Panoramica della configurazione dei firewall e di come configurare Windows Firewall per consentire l'accesso a SQL Server.|  
|[Configurare Windows Firewall (SSAS)](https://docs.microsoft.com/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access)|Consentono di configurare le impostazioni delle porte e del firewall necessarie per accedere ad [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint.|  
|[Configurare un computer multihomed](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|Configurare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Windows Firewall con sicurezza avanzata per fornire le connessioni di rete a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un ambiente multihomed.|  

 
## <a name="see-also"></a>Vedere anche  

[Aggiornare [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/upgrade-sql-server.md)   
[Disinstallare [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../sql-server/install/uninstall-sql-server.md)   
[Installare SQL Server Reporting Services (SSRS)](../../reporting-services/install-windows/install-reporting-services.md)
[Installare SQL Server Analysis Services (SSAS)](/analysis-services/instances/install-windows/install-analysis-services)
[Installare le funzionalità di Business Intelligence di [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../sql-server/install/install-sql-server-business-intelligence-features.md)   
[Soluzioni a disponibilità elevata &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
