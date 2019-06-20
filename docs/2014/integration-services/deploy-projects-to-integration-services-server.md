---
title: Distribuire progetti nel Server Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 6e9402f4-4d50-49ff-820d-65a77829c4a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4e260825532f66205e301628f60d68d93f8e7c04
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059583"
---
# <a name="deploy-projects-to-integration-services-server"></a>Distribuire progetti nel server Integration Services
  Nella versione corrente di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]è possibile distribuire i progetti nel server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Con il server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] è possibile gestire ed eseguire pacchetti, nonché configurare i valori di runtime per i pacchetti tramite ambienti.  
  
 Per altre informazioni sugli ambienti, vedere [Creare ed eseguire il mapping di un ambiente server](../../2014/integration-services/create-and-map-a-server-environment.md).  
  
> [!NOTE]  
>  Come nelle versioni precedenti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], nella versione corrente è possibile distribuire i pacchetti in un'istanza di SQL Server e utilizzare il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] per eseguire e gestire i pacchetti. Viene utilizzato il modello di distribuzione del pacchetto. Per altre informazioni, vedere [pacchetto di distribuzione &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md).  
  
 Per distribuire un progetto nel server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , completare le attività seguenti:  
  
1.  Creare un catalogo SSISDB, se non è stato ancora creato. Per altre informazioni, vedere [Creare il catalogo SSIS](catalog/ssis-catalog.md).  
  
2.  Convertire il progetto nel modello di distribuzione del progetto eseguendo la **Conversione guidata progetto di Integration Services** . Per ulteriori informazioni, vedere le istruzioni riportate di seguito: [Per convertire un progetto nel modello di distribuzione del progetto](#convert)  
  
    -   Se il progetto è stato creato in [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)], per impostazione predefinito il progetto utilizza il modello di distribuzione del progetto.  
  
    -   Se il progetto è stato creato in una versione precedente di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], dopo aver aperto il file di progetto in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], convertirlo nel modello di distribuzione del progetto.  
  
        > [!NOTE]  
        >  Se nel progetto sono incluse una o più origini dati, queste ultime vengono rimosse al completamento della conversione del progetto. Per creare una connessione a un'origine dati che può essere condivisa dai pacchetti nel progetto, aggiungere una gestione connessione a livello del progetto. Per altre informazioni, vedere [aggiungere, eliminare o condividere una gestione connessione in un pacchetto](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md).  
  
         Le diverse attività di conversione eseguite dalla **Conversione guidata progetto di Integration Services** variano a seconda che la procedura guidata venga eseguita da [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] o da [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
        -   Se la procedura guidata viene eseguita da [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], i pacchetti contenuti nel progetto vengono convertiti da [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 2005, 2008 o 2008 R2 al formato utilizzato dalla versione corrente di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Vengono aggiornati il progetto originale, con estensione dtproj, e i file di pacchetto, con estensione dtsx.  
  
        -   Se la procedura guidata viene eseguita da [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], vengono generati un file di distribuzione progetto, con estensione ispac, dai pacchetti e le configurazioni contenute nel progetto. I file di pacchetto, con estensione dtsx, originali non vengono aggiornati.  
  
             È possibile selezionare un file esistente o crearne uno nuovo nella pagina **Seleziona destinazione** della procedura guidata.  
  
             Per aggiornare i file di pacchetto durante la conversione di un progetto, eseguire la **Conversione guidata progetti di Integration Services** da [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Per aggiornare i file di pacchetto separatamente rispetto alla conversione del progetto, eseguire la **Conversione guidata progetto di Integration Services** da [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] , quindi eseguire l' **Aggiornamento guidato pacchetti SSIS**. Se i file di pacchetto vengono aggiornati separatamente, assicurarsi di salvare le modifiche. In caso contrario, quando si converte il progetto nel modello di distribuzione del progetto, eventuali modifiche non salvate apportate al pacchetto non vengono convertite.  
  
     Per altre informazioni sull'aggiornamento di pacchetti, vedere [Aggiornare pacchetti di Integration Services](install-windows/upgrade-integration-services-packages.md) e [Aggiornare i pacchetti di Integration Services mediante l'Aggiornamento guidato pacchetti SSIS](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md).  
  
3.  Distribuire il progetto nel server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Per ulteriori informazioni, vedere le istruzioni riportate di seguito: [Per distribuire un progetto nel server Integration Services](#deploy).  
  
4.  (Facoltativo) Creare un ambiente per il progetto distribuito. Per altre informazioni, vedere [Creare ed eseguire il mapping di un ambiente server](../../2014/integration-services/create-and-map-a-server-environment.md).  
  
##  <a name="convert"></a> Per convertire un progetto nel modello di distribuzione del progetto  
  
1.  Aprire il progetto in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], quindi in Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto e scegliere **Converti nel modello di distribuzione del progetto**.  
  
     oppure  
  
     Da Esplora oggetti di [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]fare clic con il pulsante destro del mouse sul nodo **Progetti** e selezionare **Importa pacchetto**.  
  
2.  Completare la procedura guidata. Per altre informazioni, vedere [Integration Services Project Conversion Wizard](../../2014/integration-services/integration-services-project-conversion-wizard.md).  
  
##  <a name="deploy"></a> Per distribuire un progetto nel server Integration Services  
  
1.  Aprire il progetto in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], quindi scegliere **Distribuisci** dal menu **Progetto** per avviare la **Distribuzione guidata Integration Services**.  
  
     oppure  
  
     In [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] espandere il nodo [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] > **SSISDB** in Esplora oggetti e individuare la cartella Progetti per il progetto da distribuire. Fare clic con il pulsante destro del mouse sulla cartella **Progetti** , quindi scegliere **Distribuzione progetto**.  
  
     oppure  
  
     Al prompt dei comandi eseguire **isdeploymentwizard.exe** da **%ProgramFiles%\Microsoft SQL Server\110\DTS\Binn**. Nei computer a 64 bit è presente anche una versione a 32 bit dello strumento in **%ProgramFiles(x86)%\Microsoft SQL Server\100\DTS\Binn**.  
  
2.  Nella pagina **Seleziona origine** fare clic su **File distribuzione progetto** per selezionare il file di distribuzione per il progetto.  
  
     oppure  
  
     Fare clic su **Catalogo di Integration Services** per selezionare un progetto che è già stato distribuito nel catalogo SSISDB.  
  
3.  Completare la procedura guidata. Per altre informazioni, vedere [Integration Services Deployment Wizard](../../2014/integration-services/integration-services-deployment-wizard.md).  
  
  
