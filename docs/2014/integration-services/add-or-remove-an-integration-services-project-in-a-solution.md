---
title: Aggiungere o rimuovere un progetto di Integration Services in una soluzione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- adding projects
- Integration Services projects, adding
- SQL Server Integration Services projects, adding
- SSIS projects, adding
- projects [Integration Services], adding
ms.assetid: f01f6475-b63c-41dc-82ac-b62162b3adf7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2581aaffaeeba033e92cff305f0e9904cfb9a970
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62837068"
---
# <a name="add-or-remove-an-integration-services-project-in-a-solution"></a>Aggiunta o rimozione di un progetto di Integration Services da una soluzione
  Nelle procedure seguenti viene descritto come aggiungere o rimuovere un progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] da una soluzione.  
  
 È possibile aggiungere o rimuovere un progetto da una soluzione solo se la soluzione è visibile in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Se è stata selezionata l'opzione **Mostra sempre soluzione** di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] visualizzerà una soluzione anche se questa contiene un unico progetto. In caso contrario, [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] visualizzerà una soluzione solo se questa contiene più di un progetto. I progetti aggiuntivi possono essere progetti di [!INCLUDE[ssIS](../includes/ssis-md.md)] o di altri tipi.  
  
## <a name="adding-an-integration-services-project"></a>Aggiunta di un progetto di Integration Services  
 È possibile aggiungere un nuovo progetto vuoto tramite [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] oppure aggiungere un progetto già creato per una soluzione diversa. È possibile aggiungere un progetto in una soluzione esistente solo se la soluzione è visibile in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
#### <a name="to-add-a-new-integration-services-project-to-a-solution"></a>Per aggiungere un nuovo progetto di Integration Services a una soluzione  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] aprire la soluzione a cui si vuole aggiungere un nuovo progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ed eseguire una delle operazioni seguenti:  
  
    -   Fare clic con il pulsante destro del mouse sulla soluzione, scegliere **Aggiungi** e quindi fare clic su **Nuovo progetto**.  
  
    -   Scegliere **Aggiungi** dal menu **File** e quindi fare clic su **Nuovo progetto**.  
  
2.  Nella finestra di dialogo **Aggiungi nuovo progetto** fare clic su **Progetto di Integration Services** nel riquadro **Modelli**.  
  
3.  È inoltre possibile modificare il nome e il percorso del progetto.  
  
4.  Fare clic su **OK**.  
  
#### <a name="to-add-an-existing-integration-services-project-to-a-solution"></a>Per aggiungere un progetto di Integration Services esistente a una soluzione  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] aprire la soluzione a cui si desidera aggiungere un progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] esistente ed eseguire una delle operazioni seguenti:  
  
    -   Fare clic con il pulsante destro del mouse sulla soluzione, scegliere **Aggiungi** e quindi fare clic su **Progetto esistente**.  
  
    -   Scegliere **Aggiungi** dal menu **File** e quindi fare clic su **Progetto esistente**.  
  
2.  Nella finestra di dialogo **Aggiungi progetto esistente** usare il pulsante Sfoglia per individuare il progetto da aggiungere e quindi fare clic su **Apri**.  
  
3.  Il progetto verrà aggiunto alla cartella della soluzione in **Esplora soluzioni**.  
  
## <a name="removing-an-integration-services-project"></a>Rimozione di un progetto di Integration Services  
 È possibile rimuovere un progetto da una soluzione solo se la soluzione è visibile in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Quando la soluzione è visibile, è possibile rimuovere tutti i progetti tranne uno. Se rimane un solo progetto, la cartella della soluzione non verrà più visualizzata in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e non sarà possibile rimuovere l'ultimo progetto.  
  
#### <a name="to-remove-an-integration-services-project-from-a-solution"></a>Per rimuovere un progetto di Integration Services da una soluzione  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] aprire la soluzione da cui si vuole rimuovere un progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
2.  In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto e quindi scegliere **Scarica progetto**.  
  
3.  Fare clic su **OK** per confermare la rimozione.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services &#40;SSIS&#41; i progetti](integration-services-ssis-projects-and-solutions.md)   
 [Creazione di un nuovo progetto di Integration Services](../../2014/integration-services/create-a-new-integration-services-project.md)  
  
  
