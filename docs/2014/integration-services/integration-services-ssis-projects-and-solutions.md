---
title: In Integration Services (SSIS) progetti | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- projects [Integration Services], creating
- folders [Integration Services], projects
- files [Integration Services], projects
- folders [Integration Services]
- projects [Integration Services], about projects
ms.assetid: 28ea8120-0a79-4029-93f0-07d521b32bee
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 26ab429a5f2abeda9a811e85dc5113121380e999
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62892492"
---
# <a name="integration-services-ssis-projects"></a>Progetti di Integration Services (SSIS)
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornisce [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per lo sviluppo di pacchetti [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 Quando si distribuiscono i pacchetti in un database [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o nell'archivio pacchetti [!INCLUDE[ssIS](../includes/ssis-md.md)], usare il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] per gestire i pacchetti. Il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] è disponibile solo in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Per altre informazioni sul servizio, vedere [Servizio Integration Services &#40;servizio SSIS&#41;](service/integration-services-service-ssis-service.md). Per altre informazioni sulla distribuzione dei pacchetti, vedere [pacchetto di distribuzione &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md).  
  
 Quando si distribuiscono progetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] nel server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], per gestire i progetti si utilizzano le viste e le stored procedure Transact-SQL in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Per altre informazioni sulla distribuzione dei progetti, vedere [Distribuzione di progetti e pacchetti](packages/deploy-integration-services-ssis-projects-and-packages.md). Per altre informazioni sul server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], vedere [Integration Services &#40;SSIS&#41; Server](catalog/integration-services-ssis-server-and-catalog.md).  
  
 Per una panoramica di [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], vedere [Integration Services &#40;SSIS&#41; e ambienti Studio](integration-services-ssis-development-and-management-tools.md).  
  
## <a name="understanding-integration-services-projects"></a>Informazioni sui progetti di Integration Services  
 Un progetto è un contenitore in cui si sviluppano pacchetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 In un progetto di [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] vengono archiviati e raggruppati i file correlati al pacchetto. Ad esempio, in un progetto sono inclusi i file necessari per creare una specifica soluzione di estrazione, trasferimento e caricamento specifica (ETL).  
  
 Prima di creare un progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , è necessario acquisire dimestichezza con il contenuto di base di questo tipo di progetto. Una volta compreso il contenuto, è possibile cominciare a creare e utilizzare un progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
### <a name="folders-in-integration-services-projects"></a>Cartelle dei progetti di Integration Services  
 Nel diagramma seguente vengono illustrate le cartelle di un progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 ![Cartelle di un progetto di Integration Services](media/solutionexplorer.gif "Cartelle di un progetto di Integration Services")  
  
 Nella tabella seguente si descrivono le cartelle incluse in un progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
|Cartella|Descrizione|  
|------------|-----------------|  
|[!INCLUDE[ssIS](../includes/ssis-md.md)] Pacchetti|Contiene i pacchetti. Per altre informazioni, vedere [Pacchetti di Integration Services &#40;SSIS&#41;](../../2014/integration-services/integration-services-ssis-packages.md).|  
|Varie|Sono contenuti file diversi dai file di pacchetto.|  
  
### <a name="files-in-integration-services-projects"></a>File dei progetti di Integration Services  
 Quando si aggiunge un progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] nuovo o esistente a una soluzione, tramite [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] vengono creati file di progetto con estensione dtproj, dtproj.user e database.  
  
-   Nel file con estensione dtproj sono contenute informazioni sulle configurazioni del progetto e su elementi quali i pacchetti.  
  
-   Il file con estensione dtproj.user contiene informazioni relative alle preferenze dell'utente per l'utilizzo del progetto.  
  
-   Nel file con estensione database sono contenute le informazioni necessarie a [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
## <a name="understanding-solutions"></a>Informazioni sulle soluzioni  
 Una soluzione è un contenitore tramite cui vengono raggruppati e gestiti i progetti utilizzati durante lo sviluppo di soluzioni aziendali end-to-end. Una soluzione consente di gestire più progetti come una singola unità e raggruppa uno o più progetti correlati che concorrono a formare una soluzione aziendale.  
  
 Nelle soluzioni possono essere inclusi diversi tipi di progetto. Per creare un pacchetto di [!INCLUDE[ssIS](../includes/ssis-md.md)] mediante Progettazione [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , sarà necessario utilizzare un progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in una soluzione fornita da [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 Quando si crea una nuova soluzione, [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] aggiunge una cartella specifica della soluzione a Esplora soluzioni e crea file con estensioni sln e suo:  
  
-   Il file con estensione sln contiene informazioni sulla configurazione della soluzione e un elenco dei progetti della soluzione.  
  
-   Il file con estensione suo contiene informazioni sulle preferenze dell'utente relative alla soluzione.  
  
 Quando si crea un nuovo progetto in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], viene automaticamente creata una soluzione, ma è anche possibile creare una soluzione vuota a cui aggiungere progetti in un secondo tempo.  
  
> [!NOTE]  
>  Per impostazione predefinita, quando si crea un nuovo progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], la soluzione non viene visualizzata nel riquadro **Esplora progetti**. Per modificare questo comportamento predefinito, scegliere **Opzioni** dal menu **Strumenti**. Nella finestra di dialogo **Opzioni** espandere **Progetti e soluzioni**e quindi fare clic su **Generale**. Nella pagina **Generale** selezionare **Mostra sempre soluzione**.  
  
## <a name="related-tasks"></a>Attività correlate  
 [Aggiunta o rimozione di un progetto di Integration Services da una soluzione](../../2014/integration-services/add-or-remove-an-integration-services-project-in-a-solution.md)  
  
 [Creazione di un nuovo progetto di Integration Services](../../2014/integration-services/create-a-new-integration-services-project.md)  
  
 [Aggiunta di un elemento a un progetto di Integration Services](../../2014/integration-services/add-an-item-to-an-integration-services-project.md)  
  
 [Copia di elementi di progetto](../../2014/integration-services/copy-project-items.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 [Sviluppo di un progetto di Integration Services](../../2014/integration-services/development-of-an-integration-services-project.md)  
  
  
