---
title: Distribuzione guidata Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.deploymentwizard.f1
ms.assetid: f3d93e13-2d85-47ff-a913-cda4046491c4
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 727eb2b745a732049d6eb4a5e2f1808f076167d0
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968311"
---
# <a name="integration-services-deployment-wizard"></a>Distribuzione guidata Integration Services
  Con la Distribuzione guidata [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] è possibile distribuire progetti nel catalogo SSISDB in un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilizzando il modello di distribuzione del progetto.  
  
 Per avviare la [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] distribuzione guidata da un progetto aperto in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] , selezionare **Distribuisci** dal menu **progetto** . Per avviare la procedura guidata [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] in, espandere il nodo SSISDB **cataloghi Integration Services**  >  **SSISDB** in Esplora oggetti, fare clic con il pulsante destro del mouse sulla cartella **progetti** , quindi scegliere **Distribuisci progetto**.  
  
 La procedura guidata prevede inoltre i quattro passaggi seguenti. Fare clic su **Avanti** per passare al passaggio successivo o **indietro** per tornare al passaggio precedente.  
  
1.  **Selezionare l'origine** : selezionare il [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] progetto che si desidera distribuire.  
  
2.  **Selezionare destinazione** : selezionare la destinazione del progetto.  
  
3.  **Verifica** : consente di visualizzare le selezioni effettuate.  
  
4.  **Deploy/results** : distribuisce il progetto e Visualizza i risultati.  
  
## <a name="select-source"></a>Selezionare l'origine  
 Per distribuire un file di distribuzione del progetto creato, selezionare **file distribuzione progetto** e immettere il percorso del file con estensione ispac oppure fare clic su **Sfoglia** per trovarlo nella [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] cartella del progetto. Per distribuire un progetto che si trova nel catalogo di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , selezionare **Catalogo di Integration Services**, quindi immettere il nome del server e il percorso del progetto nel catalogo.  
  
 Se si inizia la procedura guidata in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], per impostazione predefinita tramite la procedura guidata viene selezionato il progetto aperto come origine e questo passaggio viene ignorato. Per tornare a questo passaggio e selezionare un'altra origine, fare clic su **indietro** o su **Seleziona origine** nel riquadro sinistro.  
  
## <a name="select-destination"></a>Seleziona destinazione  
 Per selezionare la cartella di destinazione per il progetto nel catalogo di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , immettere l'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o fare clic su **Sfoglia** per effettuare una selezione da un elenco di server. Immettere il percorso del progetto in SSISDB o fare clic su **Sfoglia** per selezionarlo.  
  
 Se si inizia la procedura guidata in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], per impostazione predefinita tramite la procedura guidata viene selezionata l'istanza del server connessa e viene immesso il percorso al progetto selezionato. È possibile modificare questi valori per distribuire il progetto in un percorso diverso.  
  
## <a name="review"></a>Verifica  
 Con la procedura guidata è possibile verificare le impostazioni selezionate prima di distribuire il progetto. È possibile modificare le selezioni facendo clic su **Indietro**o selezionando un qualsiasi passaggio nel riquadro sinistro.  
  
## <a name="deployresults"></a>Distribuisci/Risultati  
 Quando si fa clic su **Distribuisci** nella pagina **Verifica** , il progetto viene distribuito e nella pagina **risultati** viene visualizzato l'esito positivo o negativo di ogni azione. Se l'azione non viene completata correttamente, fare clic su **Non riuscito** nella colonna **Risultato** per visualizzare una spiegazione dell'errore. Fare clic su **Salva report...** per salvare i risultati in un file XML.  
  
 Fare clic su **Chiudi** per uscire dalla procedura guidata.  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuire progetti nel server Integration Services](../../2014/integration-services/deploy-projects-to-integration-services-server.md)   
 [Distribuzione di progetti e pacchetti](packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
  
