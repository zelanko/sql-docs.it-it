---
title: Attività di installazione per Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 03/24/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: bb7aa3e7-8807-42c8-884f-0e41d7a20837
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: be150cce4e4dcdec19f2369e058a9283d8d137a1
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65488481"
---
# <a name="installation-tasks-for-master-data-services"></a>Attività di installazione per Master Data Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In questo articolo viene offerta una panoramica delle attività di installazione, con collegamenti alle istruzioni. Per una procedura dettagliata di installazione e configurazione di Master Data Services, vedere [Installazione e configurazione di Master Data Services](../../master-data-services/master-data-services-installation-and-configuration.md) 
  
-   [Attività di preinstallazione](#preinstall): Verificare i requisiti di sistema prima di installare [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
-   [Operazioni di installazione](#install): Installare [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il programma di installazione o il prompt dei comandi.  
  
-   [Attività di post-installazione](#postinstall): Apri [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] per completare le operazioni di post-installazione. Creare e configurare il database [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , l'applicazione Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] e i servizi Web e distribuire un modello di esempio.  
  
##  <a name="preinstall"></a> Attività di preinstallazione  
  
|Azione|Dettagli|Argomenti correlati|  
|------------|-------------|--------------------|  
|Verificare i requisiti di installazione|Nel computer in cui viene eseguito il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devono essere soddisfatti i requisiti minimi per:<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Programma di installazione.<br /><br /> Applicazione Web e servizi Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .<br /><br /> Il database [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , se si ospita il database nello stesso computer dell'applicazione Web.<br /><br /> <br /><br /> È possibile separare il computer del server Web e il computer del server di database eseguendo il programma di installazione solo sul computer del server Web e creando il database [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] in un computer remoto in cui vengono eseguite una versione e un'edizione supportate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[Funzionalità supportate dalle edizioni di SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)<br /><br /> [Requisiti hardware e software per l'installazione di SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)<br /><br /> [Requisiti dell'applicazione Web &#40;Master Data Services&#41;](../../master-data-services/install-windows/web-application-requirements-master-data-services.md)<br /><br /> [Requisiti del database &#40;Master Data Services&#41;](../../master-data-services/install-windows/database-requirements-master-data-services.md)|  
|Configurare i necessari ruoli, servizi ruolo e funzionalità|Prima di eseguire il programma di installazione, configurare il computer con i ruoli, i servizi ruolo e le funzionalità di Windows necessari.<br /><br /> Nota: Benché sia possibile eseguire questo passaggio in un secondo momento nel flusso di lavoro, è utile per questa configurazione prima di eseguire il programma di installazione in modo che sia possibile eseguire le attività di configurazione web subito dopo l'installazione.|[Requisiti dell'applicazione Web &#40;Master Data Services&#41;](../../master-data-services/install-windows/web-application-requirements-master-data-services.md)|  
|Esaminare le considerazioni sul supporto per la lingua|Determinare la lingua con cui si desidera installare ed eseguire [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|[Distribuzioni multilingue e globali &#40;Master Data Services&#41;](../../master-data-services/install-windows/multi-lingual-and-global-deployments-master-data-services.md)|  
  
##  <a name="install"></a> Operazioni di installazione  
  
|Azione|Dettagli|Argomenti correlati|  
|------------|-------------|--------------------|  
|Eseguire il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Nel computer in cui sarà ospitata l'applicazione Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] e i servizi Web [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] usare il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un prompt dei comandi per installare [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Se si usa il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] è disponibile nella pagina **Selezione funzionalità** di **Funzionalità condivise**. Se si utilizza un prompt dei comandi, [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] è disponibile come parametro della funzionalità. Si noti che tramite il processo di installazione dalla riga di comando [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]viene installato ma non configurato. È necessario configurarlo mediante Gestione configurazione Master Data Services.<br /><br /> Processo di installazione:<br /><br /> Vengono installate le cartelle e i file di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] nel percorso specificato per le funzionalità condivise e vengono assegnate le autorizzazioni a questi oggetti.<br /><br /> Vengono registrati gli assembly di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] nella Global Assembly Cache (GAC).<br /><br /> Viene installato [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].|[Installare SQL Server 2016 dall'Installazione guidata &#40;programma di installazione&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)<br /><br /> [Autorizzazioni per file e cartelle &#40;Master Data Services&#41;](../../master-data-services/folder-and-file-permissions-master-data-services.md)|  
  
##  <a name="postinstall"></a> Attività di post-installazione  
  
|Azione|Dettagli|Argomenti correlati|  
|------------|-------------|--------------------|  
|Aprire [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] per completare le operazioni di post-installazione|Dopo il completamento dell'installazione, aprire [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]. [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] esegue le operazioni di post-installazione seguenti nel computer locale:<br /><br /> Crea un gruppo di Windows, **MDS_ServiceAccounts**, che conterrà gli account di servizio di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] per i pool di applicazioni.<br /><br /> Crea la cartella MDSTempDir nel percorso di installazione di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e assegna le autorizzazioni per **MDS_ServiceAccounts**. In questa cartella vengono compilati i file di compilazione temporanei per l' [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] applicazione Web.<br /><br /> Nel file Web.config di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] configura l'attributo **tempDirectory** dell'elemento **\<compilation>** con il percorso alla cartella MDSTempDir.|[Autorizzazioni per file e cartelle &#40;Master Data Services&#41;](../../master-data-services/folder-and-file-permissions-master-data-services.md)<br /><br /> [Guida di riferimento alla configurazione Web &#40;Master Data Services&#41;](../../master-data-services/web-configuration-reference-master-data-services.md)|  
|Creare un database [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|Utilizzare [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] per creare un database [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] per i dati master.|[Creare un database Master Data Services](../../master-data-services/install-windows/create-a-master-data-services-database.md)|  
|Creare un'applicazione Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]|Utilizzare [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] per creare e configurare un'applicazione Web per ospitare [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].|[Creare un'applicazione Web Gestione dati master &#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)|  
|Associare un database [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] a un'applicazione Web|Usare [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] per associare l'applicazione Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] al database [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|[Associare un'applicazione Web e un database Master Data Services](../../master-data-services/install-windows/associate-a-master-data-services-database-and-web-application.md)|  
|Configurare Sicurezza avanzata di Internet Explorer|Quando si installa [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] in un computer Windows Server 2012, può essere necessario configurare Sicurezza avanzata di Internet Explorer per consentire lo scripting per il sito dell'applicazione [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] . In caso contrario, il passaggio al sito dell'applicazione [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] nel computer server avrà esito negativo.|[Internet Explorer: Configurazione sicurezza avanzata](https://go.microsoft.com/fwlink/p/?LinkId=223869)|  
|Installare [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|Utenti che opereranno con i dati master possono installare [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)].|[https://go.microsoft.com/fwlink/?LinkID=398159](https://go.microsoft.com/fwlink/?LinkID=398159)|  
|Abilitare l'integrazione con Data Quality Services (DQS)|Per gli utenti di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], abilitare l'integrazione con la funzionalità DQS che può essere usata per la corrispondenza di dati simili.|[Abilitare l'integrazione di Data Quality Services con Master Data Services](../../master-data-services/install-windows/enable-data-quality-services-integration-with-master-data-services.md)|  
|Distribuire un modello di esempio|I pacchetti del modello di esempio sono installati con Master Data Services e possono essere distribuiti tramite MDSModelDeploy.exe.|[Distribuzione di esempi MDS in SQL Server](~/master-data-services/sql-server-samples-model-deployment-packages-mds.md)|
  
 Se si riscontrano problemi durante il processo di installazione o la configurazione iniziale, vedere la pagina relativa alla [risoluzione dei problemi di installazione e di configurazione](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-installation-and-configuration-issues-master-data-services.aspx) nella pagina Wiki di TechNet.  
  
 Se non è più necessario utilizzare [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] su un computer, è possibile disinstallare [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e determinare se rimuovere elementi non interessati dal processo di disinstallazione. Per altre informazioni, vedere [Disinstallare e rimuovere Master Data Services](../../sql-server/install/uninstall-and-remove-master-data-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Installare SQL Server 2016](../../database-engine/install-windows/install-sql-server.md)  
  
  
