---
title: Installare Analysis Services in modalità multidimensionale e di data mining | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Analysis Services, about installing Analysis Services
- installing Analysis Services
- SSAS, installing
- Analysis Services, installing
- SQL Server Analysis Services, installing
ms.assetid: 8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: 002a4ce66108622ce5efcf33231edaed9cd1c99b
ms.sourcegitcommit: e914effe771a1ee323bb3653626cd4ba83d77308
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/04/2020
ms.locfileid: "78280858"
---
# <a name="install-analysis-services-in-multidimensional-and-data-mining-mode"></a>Installazione di Analysis Services in modalità Multidimensionale e Data Mining
  
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] offre funzionalità di elaborazione analitica in linea (OLAP) e di data mining per applicazioni di Business Intelligence. In questa versione, il supporto per i database OLAP e i modelli di data mining è [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] disponibile quando si installa in *modalità multidimensionale*. La modalità multidimensionale è una delle tre modalità del server in cui viene eseguito [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Si tratta della modalità predefinita. Se si installa [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizzando i valori predefiniti, si ottiene un'istanza che esegue database multidimensionali e modelli di data mining.  
  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è una funzionalità per istanze multiple, ovvero è possibile installare più di un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in un unico computer oppure eseguire una nuova istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] side-by-side con una versione precedente. La modalità del server è specifica di un'istanza. L'utilizzo di altre modalità richiede l'installazione di altre istanze del server.  
  
 È possibile installare [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] da solo o con altri componenti. Se si installa solo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], le seguenti funzionalità vengono installate quando si seleziona **Analysis Services** nella pagina Selezione funzionalità dell' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installazione guidata di:  
  
-   Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per l'esecuzione dei modelli di data mining e dei database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   Provider di dati utilizzati per l'accesso ai dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nei database di origine  
  
-   Gestione configurazione SQL Server  
  
## <a name="choosing-additional-features"></a>Scelta di ulteriori funzionalità  
 Per soluzioni OLAP e di data warehouse di Analysis Services è richiesta l'installazione di componenti aggiuntivi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ai fini dello sviluppo, della distribuzione e dell'amministrazione dei database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Le funzionalità aggiuntive seguenti rappresentano opzioni disponibili per molti scenari utente tipici:  
  
-   
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], utilizzato per creare e visualizzare modelli di data mining e strutture di dati di Analysis Services.  
  
-   Componenti per connettività degli strumenti client, utilizzati per la comunicazione tra client e server, incluse le librerie di rete per DB-Library, ODBC e OLE DB.  
  
-   
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], un set di oggetti grafici e programmabili per lo spostamento, la copia e la trasformazione dei dati.  
  
-   Strumenti di gestione, tra cui Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e Monitoraggio replica.  
  
## <a name="installation-tasks"></a>Attività di installazione  
 Le attività di installazione includono quanto segue:  
  
|Collegamenti|Attività|  
|-----------|-----------|  
|[Requisiti hardware e software per l'installazione di SQL Server 2014 e la](hardware-and-software-requirements-for-installing-sql-server.md) [configurazione di account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).|Prima di eseguire il programma di installazione, controllare i prerequisiti relativi all'installazione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e determinare quale account verrà utilizzato per il provisioning del server.|  
|[Installare SQL Server 2014 dall'installazione guidata &#40;&#41;di installazione ](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).|Eseguire il programma di installazione di SQL Server per installare il software.|  
|[Configurare Windows Firewall per consentire l'accesso ad Analysis Services](https://docs.microsoft.com/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access)|Al termine dell'installazione, è necessario configurare le impostazioni del firewall per consentire le connessioni remote al server.|  
|[Autorizzazione dell'accesso a oggetti e operazioni &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services)|Gli utenti che accedono ai database di Analysis Services devono disporre dell'autorizzazione in lettura per almeno un database nel server.|  
  
## <a name="related-content"></a>Contenuto correlato  
 Ulteriori informazioni sull'installazione sono disponibili negli argomenti seguenti:  
  
 [Installare Analysis Services in modalità Tabella](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services)  
  
 [PowerPivot for SharePoint 2010 Installation](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
 [Determinare la modalità server di un'istanza di Analysis Services](https://docs.microsoft.com/analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance)  
  
 [SQL Server componenti aggiuntivi Data mining](https://www.microsoft.com/download/details.aspx?id=35578)  
  
 Per impostazione predefinita, i database di esempio, il codice di esempio e i componenti aggiuntivi delle applicazioni client non vengono installati come parte dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per installare i database di esempio e il codice di esempio, vedere il sito Web [CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità supportate dalle edizioni di SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473)   
 [Lingue e regole di confronto &#40;Analysis Services&#41;](../../../2014/analysis-services/languages-and-collations-analysis-services.md)   
 [Aggiornare Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)  
  
  
