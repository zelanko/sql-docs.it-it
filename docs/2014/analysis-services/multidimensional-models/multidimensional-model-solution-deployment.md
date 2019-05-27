---
title: Distribuzione di soluzioni di modelli multidimensionali | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services deployments, planning
- deploying [Analysis Services]
- deploying [Analysis Services], planning
ms.assetid: 7259c201-ff54-43e8-bda5-a6d51474e0e6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9ec674c1eb64f2e5191df600864fa38aa3da0749
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66073547"
---
# <a name="multidimensional-model-solution-deployment"></a>Distribuzione di soluzioni di modelli multidimensionali
  Dopo aver completato lo sviluppo di un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , è possibile distribuire il database in un server Analysis Services. In Analysis Services sono disponibili sei possibili metodi di distribuzione che possono essere utilizzati per spostare il database in un server di prova o di produzione. I metodi sono elencati di seguito in ordine convenienza: Automazione AMO, XMLA, distribuzione guidata, utilità di distribuzione, eseguire la sincronizzazione guidata, Backup e ripristino.  
  
 In questo argomento sono contenute le sezioni seguenti:  
  
 [Metodi di distribuzione](#bkmk_meth)  
  
 [Considerazioni sulla distribuzione](#bkmk_considerations)  
  
 [Attività correlate](#bkmk_rel)  
  
##  <a name="bkmk_meth"></a> Metodi di distribuzione  
  
|Metodo|Descrizione|Collegamento|  
|------------|-----------------|----------|  
|**Automazione AMO (Analysis Management Objects)**|AMO (Analysis Management Objects) offre un'interfaccia di programmazione per il set di comandi completo per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], inclusi comandi che possono essere utilizzati per la distribuzione della soluzione. Come approccio per la distribuzione della soluzione, l'automazione AMO (Analysis Management Objects) è la più flessibile, ma richiede anche un lavoro di programmazione.  Il vantaggio principale offerto da AMO è che consente di utilizzare SQL Server Agent insieme all'applicazione AMO per eseguire la distribuzione in base a una pianificazione predefinita.|[Sviluppo con Analysis Management Objects &#40;AMO&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)|  
|**XMLA**|Utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per generare uno script XMLA dei metadati di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esistente, quindi eseguire tale script in un altro server per ricreare il database iniziale. Per creare script XMLA in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , è sufficiente definire il processo di distribuzione e quindi codificarlo e memorizzarlo in uno script XMLA. Dopo aver salvato lo script XMLA in un file, è possibile eseguire lo script in base a una pianificazione oppure incorporarlo nello script di un'applicazione che si connette direttamente a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].<br /><br /> È inoltre possibile eseguire script XMLA a intervalli predefiniti tramite SQL Server Agent, ma questo metodo non è caratterizzato dalla stessa flessibilità del metodo basato sull'automazione AMO. Nella libreria AMO è disponibile un'ampia gamma di funzionalità che supportano l'insieme completo di comandi amministrativi.|[Distribuire soluzioni di modelli usando XMLA](deploy-model-solutions-using-xmla.md)|  
|**Distribuzione guidata**|Distribuzione guidata consente di utilizzare i file di output XMLA generati da un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per distribuire i metadati del progetto in un server di destinazione. Grazie alla Distribuzione guidata è possibile eseguire la distribuzione direttamente dal file di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] creato nella directory di output tramite la compilazione del progetto.<br /><br /> Il vantaggio principale rappresentato dall'utilizzo della Distribuzione guidata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è la praticità. È possibile salvare script della Distribuzione guidata nello stesso modo in cui è possibile salvare uno script XMLA per un utilizzo successivo in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. La Distribuzione guidata può essere eseguita sia in modalità interattiva sia dal prompt dei comandi tramite l'utilità di distribuzione.|[Deploy Model Solutions Using the Deployment Wizard](deploy-model-solutions-using-the-deployment-wizard.md)|  
|**Utilità di distribuzione**|L'utilità di distribuzione consente di avviare il motore di distribuzione di Analysis Services da un prompt dei comandi.|[Distribuire soluzioni di modelli con l'utilità di distribuzione](deploy-model-solutions-with-the-deployment-utility.md)|  
|**Sincronizzazione guidata database**|Sincronizzazione guidata database consente di sincronizzare i metadati e i dati tra due database qualsiasi di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .<br /><br /> È possibile utilizzare la Sincronizzazione guidata database per copiare sia dati sia metadati da un server di origine in un server di destinazione. Se nel server di destinazione non è disponibile una copia del database che si desidera distribuire, in tale server viene copiato un nuovo database. Se invece nel database di destinazione è già inclusa una copia dello stesso database, il database nel server di destinazione viene aggiornato per utilizzare i metadati e i dati del database di origine.|[Sincronizzare database di Analysis Services](synchronize-analysis-services-databases.md)|  
|**Backup e ripristino**|Il backup rappresenta il metodo di trasferimento di database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] più semplice. Nella finestra di dialogo **Backup** è possibile definire la configurazione delle opzioni desiderate e quindi eseguire il backup dalla finestra di dialogo stessa. In alternativa, è possibile creare uno script che può essere salvato ed eseguito in base alle specifiche esigenze.<br /><br /> Il metodo Backup e ripristino non viene utilizzato con la stessa frequenza degli altri metodi, anche se consente di completare rapidamente un'operazione di distribuzione con requisiti di infrastrutture minimi.|[Backup e ripristino di database di Analysis Services](backup-and-restore-of-analysis-services-databases.md)|  
  
##  <a name="bkmk_considerations"></a> Considerazioni sulla distribuzione  
 Prima di distribuire un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , si considerino quali di queste domande riguardano la soluzione in uso, quindi controllare il collegamento correlato per apprendere come risolvere il problema:  
  
|Considerazione|Collegamento a ulteriori informazioni|  
|-------------------|------------------------------|  
|Quali risorse hardware e software sono richieste per questa soluzione?|[Requisiti e considerazioni per la distribuzione di Analysis Services](requirements-and-considerations-for-analysis-services-deployment.md)|  
|Come verranno distribuiti gli oggetti correlati che non rientrano nell'ambito del progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , quali pacchetti, report o schemi del database relazionale di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ?||  
|Come sono stati caricati e aggiornati i dati nel database [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] distribuito?<br /><br /> Come verranno aggiornati i metadati (ad esempio calcoli) nel database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] distribuito?|[Metodi di distribuzione](#bkmk_meth) in questo argomento.|  
|Si desidera concedere agli utenti l'accesso ai dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tramite Internet?|[Configurare l'accesso HTTP ad Analysis Services in Internet Information Services &#40;IIS&#41; 8.0](../instances/configure-http-access-to-analysis-services-on-iis-8-0.md)|  
|Si desidera fornire accesso continuo ai dati [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per query?|[Requisiti e considerazioni per la distribuzione di Analysis Services](requirements-and-considerations-for-analysis-services-deployment.md)|  
|Si desidera distribuire oggetti in un ambiente distribuito utilizzando oggetti collegati o partizioni remote?|[Creare e gestire una partizione locale &#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md), [Creare e gestire una partizione remota &#40;Analysis Services&#41;](create-and-manage-a-remote-partition-analysis-services.md) e [Gruppi di misure collegati](linked-measure-groups.md).|  
|Come verranno protetti i dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ?|[Autorizzazione dell'accesso a oggetti e operazioni &#40;Analysis Services&#41;](authorizing-access-to-objects-and-operations-analysis-services.md)|  
  
##  <a name="bkmk_rel"></a> Attività correlate  
 [Requisiti e considerazioni per la distribuzione di Analysis Services](requirements-and-considerations-for-analysis-services-deployment.md)  
  
 [Distribuire soluzioni di modelli usando XMLA](deploy-model-solutions-using-xmla.md)  
  
 [Distribuire soluzioni di modelli tramite la Distribuzione guidata](deploy-model-solutions-using-the-deployment-wizard.md)  
  
 [Distribuire soluzioni di modelli con l'utilità di distribuzione](deploy-model-solutions-with-the-deployment-utility.md)  
  
  
