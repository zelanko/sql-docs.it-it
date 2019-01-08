---
title: Distribuzione guidata di Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.deploymentwizard.f1
ms.assetid: f3d93e13-2d85-47ff-a913-cda4046491c4
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8f90613d3c8e0204e2861008a5f7be0846eca64a
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535900"
---
# <a name="integration-services-deployment-wizard"></a>Distribuzione guidata Integration Services
  Con la Distribuzione guidata [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] è possibile distribuire progetti nel catalogo SSISDB in un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilizzando il modello di distribuzione del progetto.  
  
 Per avviare il [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] distribuzione guidata da un progetto aperto in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], selezionare **Distribuisci** dal **progetto** menu. Per avviare la procedura guidata in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], espandere il **cataloghi di Integration Services** > **SSISDB** fare clic sul nodo in Esplora oggetti il **progetti** cartella e quindi fare clic su **Distribuisci progetto**.  
  
 La procedura guidata prevede inoltre i quattro passaggi seguenti. Fare clic su **successivo** per procedere al passaggio successivo, o **Previous** per tornare al passaggio precedente.  
  
1.  **Seleziona origine** : selezionare il [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] progetto che si desidera distribuire.  
  
2.  **Seleziona destinazione** -selezionare la destinazione del progetto.  
  
3.  **Revisione** -consente di visualizzare le opzioni selezionate.  
  
4.  **Distribuisci/risultati** : distribuisce il progetto e visualizza i risultati.  
  
## <a name="select-source"></a>Seleziona origine  
 Per distribuire un file di progetto di distribuzione che è stato creato, selezionare **file distribuzione progetto** e immettere il percorso del file con estensione ispac o fare clic su **Sfoglia** per individuarlo nella [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] cartella del progetto. Per distribuire un progetto che si trova nel catalogo di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , selezionare **Catalogo di Integration Services**, quindi immettere il nome del server e il percorso del progetto nel catalogo.  
  
 Se si inizia la procedura guidata in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], per impostazione predefinita tramite la procedura guidata viene selezionato il progetto aperto come origine e questo passaggio viene ignorato. Per tornare a questo passaggio e selezionare un'origine diversa, fare clic su **Previous** oppure fare clic su **Seleziona origine** nel riquadro sinistro.  
  
## <a name="select-destination"></a>Seleziona destinazione  
 Per selezionare la cartella di destinazione per il progetto nel catalogo di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , immettere l'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o fare clic su **Sfoglia** per effettuare una selezione da un elenco di server. Immettere il percorso del progetto in SSISDB o fare clic su **Sfoglia** per selezionarlo.  
  
 Se si inizia la procedura guidata in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], per impostazione predefinita tramite la procedura guidata viene selezionata l'istanza del server connessa e viene immesso il percorso al progetto selezionato. È possibile modificare questi valori per distribuire il progetto in un percorso diverso.  
  
## <a name="review"></a>Verifica  
 Con la procedura guidata è possibile verificare le impostazioni selezionate prima di distribuire il progetto. È possibile modificare le selezioni facendo clic su **Indietro**o selezionando un qualsiasi passaggio nel riquadro sinistro.  
  
## <a name="deployresults"></a>Distribuisci/Risultati  
 Quando fa clic su **Deploy** dal **revisione** pagina, il progetto viene distribuito e il **risultati** pagina viene visualizzato l'esito positivo o negativo di ogni azione. Se l'azione non viene completata correttamente, fare clic su **Non riuscito** nella colonna **Risultato** per visualizzare una spiegazione dell'errore. Fare clic su **Salva Report...**  per salvare i risultati in un file XML.  
  
 Per uscire dalla procedura guidata, fare clic su **Chiudi**.  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuire progetti nel server Integration Services](../../2014/integration-services/deploy-projects-to-integration-services-server.md)   
 [Distribuzione di progetti e pacchetti](packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
  
